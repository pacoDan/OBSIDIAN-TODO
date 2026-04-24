**MinIO es una excelente alternativa open-source a AWS S3 que soporta pre-signed URLs y es completamente compatible con Terraform.** Otras alternativas gratuitas incluyen DigitalOcean Spaces, Backblaze B2, Cloudflare R2 y Supabase Storage.

**Alternativas S3 gratuitas compatibles con Terraform:**

- **MinIO**: Solución self-hosted completamente gratuita, API S3-compatible, soporte nativo para pre-signed URLs y excelente integración con Terraform
- **Supabase Storage**: Tier gratuito generoso, recientemente añadió compatibilidad S3, ideal para aplicaciones modernas
- **Backblaze B2**: Pricing muy competitivo, compatible con S3 API, 10GB gratuitos mensualmente
- **Cloudflare R2**: Sin costos de egress, compatible con S3, tier gratuito de 10GB
- **DigitalOcean Spaces**: $5/mes por 250GB, pero con trial credits frecuentemente disponibles

**Ventajas de MinIO para desarrollo:**

- **Deployment flexible**: Kubernetes, Docker, bare metal o cloud
- **Performance superior**: Optimizado para high-throughput workloads
- **Desarrollo local**: Perfecto para testing sin costos de cloud
- **Multi-tenant**: Soporte nativo para buckets y políticas granulares
- **Terraform provider**: Configuración declarativa completa de buckets, políticas y usuarios

**Configuración típica con Terraform:**

MinIO se integra perfectamente usando el provider AWS de Terraform cambiando solo el endpoint. Las pre-signed URLs funcionan idénticamente a S3, permitiendo uploads/downloads directos desde frontend sin exponer credenciales. Para producción, muchos equipos combinan MinIO on-premise para datos sensibles y Cloudflare R2 para assets públicos, maximizando cost-efficiency.

**MinIO con URLs pre-firmadas como alternativa a S3**

**Implementación de pre-signed URLs en MinIO**

- **Compatibilidad total**: MinIO implementa la misma API de pre-signed URLs que AWS S3, permitiendo generar URLs temporales para upload/download directo
- **Configuración simple**: Usa las mismas librerías SDK (boto3, aws-sdk-js) cambiando únicamente el endpoint
- **Seguridad granular**: Permite definir tiempo de expiración, permisos específicos (GET/PUT/DELETE) y restricciones por IP
- **Performance optimizada**: Al ser self-hosted, eliminas latencia de red hacia AWS y tienes control total sobre la infraestructura

**Ejemplo de configuración con Terraform**
```hcl
resource "minio_s3_bucket" "uploads" {
  bucket = "user-uploads"
  acl    = "private"
}

resource "minio_s3_bucket_policy" "uploads_policy" {
  bucket = minio_s3_bucket.uploads.bucket
  policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Effect = "Allow"
        Principal = "*"
        Action = ["s3:GetObject"]
        Resource = "${minio_s3_bucket.uploads.arn}/*"
        Condition = {
          StringEquals = {
            "s3:ExistingObjectTag/public" = "true"
          }
        }
      }
    ]
  })
}
```
**Alternativas gratuitas a S3 compatibles con Terraform**

**Opciones self-hosted**

- **MinIO**: Completamente gratuito, deployment en Docker/Kubernetes, soporte enterprise opcional
- **SeaweedFS**: Alternative distribuida con API S3, excelente para high-volume scenarios
- **Garage**: Rust-based, lightweight, ideal para edge computing y IoT deployments

**Servicios cloud con tiers gratuitos**

- **Cloudflare R2**: 10GB storage + 1M operaciones gratis mensualmente, zero egress fees
- **Backblaze B2**: 10GB gratuitos, pricing muy competitivo después del tier gratuito
- **Wasabi**: Primer mes gratuito, después $5.99/TB sin fees adicionales
- **Oracle Cloud**: Always Free tier con 20GB Object Storage

**Configuración Terraform multi-provider**
```hcl
# MinIO local/self-hosted
provider "aws" {
  alias                       = "minio"
  access_key                 = var.minio_access_key
  secret_key                 = var.minio_secret_key
  region                     = "us-east-1"
  s3_use_path_style          = true
  skip_credentials_validation = true
  skip_metadata_api_check    = true
  skip_region_validation     = true
  endpoints {
    s3 = "http://localhost:9000"
  }
}

# Cloudflare R2
provider "aws" {
  alias      = "r2"
  access_key = var.r2_access_key
  secret_key = var.r2_secret_key
  region     = "auto"
  endpoints {
    s3 = "https://${var.account_id}.r2.cloudflarestorage.com"
  }
}
```
**Estrategia híbrida recomendada**

- **MinIO para desarrollo**: Environment local idéntico a producción, testing sin costos
- **Cloudflare R2 para assets públicos**: CDN integrado, zero egress costs, global distribution
- **Backblaze B2 para backups**: Pricing competitivo para long-term storage
- **Supabase Storage para aplicaciones modernas**: Integración nativa con auth, real-time subscriptions

Esta combinación te permite optimizar costos mientras mantienes flexibilidad y performance según el use case específico.