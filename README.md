# 🚀 Innovatech Chile - Plataforma DevOps con Amazon EKS y CI/CD

![AWS](https://img.shields.io/badge/AWS-EKS-orange?style=for-the-badge\&logo=amazonaws)
![Kubernetes](https://img.shields.io/badge/Kubernetes-1.35-326CE5?style=for-the-badge\&logo=kubernetes)
![Docker](https://img.shields.io/badge/Docker-Containers-2496ED?style=for-the-badge\&logo=docker)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-CI/CD-2088FF?style=for-the-badge\&logo=githubactions)
![Amazon ECR](https://img.shields.io/badge/Amazon-ECR-FF9900?style=for-the-badge\&logo=amazonaws)

Proyecto semestral desarrollado para la asignatura **ISY1101 - Introducción a Herramientas DevOps** de la **Escuela de Informática y Telecomunicaciones - Duoc UC**.

El proyecto implementa una arquitectura moderna basada en microservicios, desplegada sobre **Amazon Elastic Kubernetes Service (EKS)** y automatizada mediante un pipeline de **Integración Continua y Entrega Continua (CI/CD)** utilizando **GitHub Actions**.

La solución fue diseñada siguiendo principios de alta disponibilidad, automatización, seguridad Zero Trust y optimización de costos en la nube.

---

# 📌 Objetivos

* Implementar una infraestructura cloud en AWS.
* Orquestar aplicaciones mediante Kubernetes (Amazon EKS).
* Automatizar compilación y despliegue con GitHub Actions.
* Aplicar buenas prácticas DevOps.
* Implementar monitoreo y escalabilidad automática.

---

# 🏗️ Arquitectura

La solución está compuesta por una arquitectura de microservicios desplegada sobre AWS.

## Infraestructura

* Amazon VPC
* Amazon EKS
* Amazon ECR
* Elastic Load Balancer
* Amazon CloudWatch
* Metrics Server
* GitHub Actions
* Docker

### Red Virtual (VPC)

| Configuración    | Valor               |
| ---------------- | ------------------- |
| CIDR             | `10.0.0.0/16`       |
| Arquitectura     | Multi-AZ            |
| Subredes         | Públicas y Privadas |
| NAT Gateway      | Sí                  |
| Internet Gateway | Sí                  |

La infraestructura fue segmentada en distintas capas para garantizar aislamiento entre los servicios públicos y privados.

---

# 🔒 Seguridad

El proyecto sigue un enfoque **Zero Trust**, donde:

* No se utilizan llaves `.pem`
* El puerto SSH (22) permanece cerrado
* Administración mediante **AWS Systems Manager Session Manager**
* Backend completamente aislado mediante servicios `ClusterIP`

---

# ☸️ Kubernetes (Amazon EKS)

| Configuración | Valor                     |
| ------------- | ------------------------- |
| Cluster       | innovatech-eks-cluster    |
| Kubernetes    | v1.35                     |
| Auto Mode     | Habilitado                |
| Node Type     | T3.LARGE (Spot Instances) |

## Microservicios

### Frontend

* Servicio tipo `LoadBalancer`
* Acceso público mediante Elastic Load Balancer

### Backend

* Servicio tipo `ClusterIP`
* Acceso únicamente desde la red interna del clúster

---

# ⚙️ Pipeline CI/CD

Todo el ciclo de vida del software se encuentra automatizado mediante **GitHub Actions**.

El flujo de trabajo incluye:

1. Checkout del repositorio.
2. Autenticación con AWS STS.
3. Construcción de imágenes Docker mediante Multi-Stage Build.
4. Publicación de imágenes en Amazon ECR.
5. Versionado automático utilizando:

```text
eks-${{ github.run_number }}
```

6. Despliegue automático en Kubernetes.
7. Rolling Update sin tiempos de inactividad.

---

# 📈 Escalabilidad

Se implementó **Horizontal Pod Autoscaler (HPA)**.

Configuración:

* Escalado automático al superar el **50% de CPU**
* Incremento automático de réplicas
* Optimización de recursos del clúster

---

# 📊 Observabilidad

Se implementaron herramientas de monitoreo para supervisar el estado del sistema.

## Metrics Server

Permite visualizar el consumo de recursos mediante:

```bash
kubectl top pods -n tienda
```

## Amazon CloudWatch

Registros habilitados para:

* API Server
* Auditoría
* Autenticación
* Eventos del clúster

---

# 🛠️ Tecnologías utilizadas

* AWS
* Amazon EKS
* Amazon ECR
* Docker
* Kubernetes
* GitHub Actions
* CloudWatch
* Metrics Server
* kubectl

---

# 📂 Estructura del proyecto

```text
.
├── backend/
├── frontend/
├── kubernetes/
├── .github/
│   └── workflows/
├── Dockerfiles
└── README.md
```

---

# 🚀 Validación del despliegue

Verificar los Pods:

```bash
kubectl get pods -n tienda
```

Obtener la URL pública:

```bash
kubectl get svc frontend-service -n tienda
```

Ver consumo de recursos:

```bash
kubectl top pods -n tienda
```

---

# 🎯 Características implementadas

* Arquitectura de microservicios
* Dockerización completa
* Kubernetes administrado con Amazon EKS
* Pipeline CI/CD
* Rolling Updates
* Escalabilidad automática (HPA)
* Arquitectura Multi-AZ
* Seguridad Zero Trust
* Monitoreo mediante CloudWatch
* Optimización de costos utilizando Spot Instances

---

# 👨‍💻 Proyecto Académico

**Institución:** Duoc UC

**Escuela:** Informática y Telecomunicaciones

**Asignatura:** ISY1101 - Introducción a Herramientas DevOps

---

# 📄 Licencia

Proyecto desarrollado exclusivamente con fines académicos.
