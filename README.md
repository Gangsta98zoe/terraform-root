# terraform-root — Módulo Raíz

Repositorio principal que orquesta los módulos de Terraform para desplegar
la infraestructura completa en AWS.

## Estructura de módulos

```
terraform-root/
├── main.tf            # Llama a los 3 módulos externos
├── variables.tf       # Variables globales del stack
├── outputs.tf         # Outputs del stack completo
├── terraform.tfvars   # Valores por defecto (sin credenciales)
├── .gitignore
└── .github/workflows/ # CI/CD (fmt, validate, tflint, checkov)

Módulos externos:
├── terraform-module-networking  → VPC, subredes, IGW, rutas
├── terraform-module-compute     → EC2, Security Group
└── terraform-module-storage     → S3 con versionado
```

## ¿Qué hace cada módulo?

| Módulo | Descripción |
|---|---|
| networking | VPC, subredes pública/privada, IGW, tabla de rutas |
| compute | EC2 con Apache + Security Group |
| storage | S3 con versionado y acceso público bloqueado |

## Historial de versiones (SemVer)

| Versión | Tipo | Descripción |
|---|---|---|
| v0.1.0 | Inicial | Código monolítico (Prueba 1) |
| v0.2.0 | MINOR | Agrega módulo networking con variables y outputs |
| v0.2.1 | PATCH | Fix: corrección de bug en nombre del security group |
| v1.0.0 | MAJOR | Arquitectura modular completa |

## Justificación del número de versión

El salto a **v1.0.0** es MAJOR porque cambia la arquitectura completa:
de código monolítico a 3 módulos independientes y reutilizables.

## Uso

```bash
export AWS_ACCESS_KEY_ID=<key>
export AWS_SECRET_ACCESS_KEY=<secret>
export AWS_SESSION_TOKEN=<token>
terraform init
terraform plan
terraform apply
terraform output
terraform destroy
```

## CI/CD

GitHub Actions valida en cada PR a `main`: fmt, validate, tflint y checkov.
