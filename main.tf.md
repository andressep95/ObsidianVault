```hcl
# =============================================================================
# LAB 01 - EXPLORING AWS REGIONS AND AVAILABILITY ZONES
# =============================================================================


# Recurso para demostrar creación en región primaria
# (Usamos un bucket S3 como ejemplo, ya que es global pero region-specific)
resource "aws_s3_bucket" "lab_primary_region" {
	provider = aws
	bucket = "${local.resource_prefix}-primary-${random_id.bucket_suffix.hex}"
  
	tags = merge(local.common_tags, {
		Name = "Lab01-Primary-Region-Bucket"
		Region = var.primary_region
		Description = "Bucket creado en region primaria para exploración"
	})
}

  
# Recurso para demostrar creación en región secundaria
resource "aws_s3_bucket" "lab_secondary_region" {
	provider = aws.secondary
	bucket = "${local.resource_prefix}-secondary-${random_id.bucket_suffix.hex}"
  
	tags = merge(local.common_tags, {
		Name = "Lab01-secondary-Region-Bucket"
		Region = var.secondary_region
		Description = "Bucket creado en region secundaria para exploración"
	})
}

  

# ID aleatorio para nombres únicos de buckets

resource "random_id" "bucket_suffix" {

byte_length = 4

}

  

# Configuración de versionado para buckets (buena práctica)

resource "aws_s3_bucket_versioning" "lab_primary_versioning" {

provider = aws

bucket = aws_s3_bucket.lab_primary_region.id

versioning_configuration {

status = "Enabled"

}

}

  

resource "aws_s3_bucket_versioning" "lab_secondary_versioning" {

provider = aws.secondary

bucket = aws_s3_bucket.lab_secondary_region.id

versioning_configuration {

status = "Enabled"

}

}

  

# Server-side encryption para buckets

resource "aws_s3_bucket_server_side_encryption_configuration" "lab_primary_encrypt" {

provider = aws

bucket = aws_s3_bucket.lab_primary_region.id

  

rule {

apply_server_side_encryption_by_default {

sse_algorithm = "AES256"

}

}

}

  

resource "aws_s3_bucket_server_side_encryption_configuration" "lab_secondary_encrypt" {

provider = aws.secondary

bucket = aws_s3_bucket.lab_secondary_region.id

  

rule {

apply_server_side_encryption_by_default {

sse_algorithm = "AES256"

}

}

}

  

# Bloquear acceso público (seguridad)

resource "aws_s3_bucket_public_access_block" "lab_primary_pab" {

provider = aws

bucket = aws_s3_bucket.lab_primary_region.id

  

block_public_acls = true

block_public_policy = true

ignore_public_acls = true

restrict_public_buckets = true

}

  

resource "aws_s3_bucket_public_access_block" "lab_secondary_pab" {

provider = aws.secondary

bucket = aws_s3_bucket.lab_secondary_region.id

  

block_public_acls = true

block_public_policy = true

ignore_public_acls = true

restrict_public_buckets = true

}
```

