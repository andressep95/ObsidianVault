```hcl
# =============================================================================
# OUTPUTS - INFORMACIÓN DE REGIONES Y ZONAS DE DISPONIBILIDAD
# =============================================================================
  

# Información de la cuenta AWS
output "account_info" {
	description = "Información de la cuenta AWS"
	
	value = {
		account_id = data.aws_caller_identity.current.account_id
		user_id = data.aws_caller_identity.current.user_id
		arn = data.aws_caller_identity.current.arn
		partition = data.aws_partition.current.partition
	}
}

  
# Información de la región primaria
output "primary_region_info" {
	description = "Información detallada de la región primaria"
	
	value = {
		name = data.aws_region.primary.name
		description = data.aws_region.primary.description
		endpoint = data.aws_region.primary.endpoint
	
		availability_zones = {
			count = length(data.aws_availability_zones.primary_azs.names)
			names = data.aws_availability_zones.primary_azs.names
			zone_ids = data.aws_availability_zones.primary_azs.zone_ids
		}
	
		latest_ami = {
			id = data.aws_ami.amazon_linux_primary.id
			name = data.aws_ami.amazon_linux_primary.name
			description = data.aws_ami.amazon_linux_primary.description
			creation_date = data.aws_ami.amazon_linux_primary.creation_date
		}
		
		created_resources = {
			s3_bucket = aws_s3_bucket.lab_primary_region.id
			bucket_arn = aws_s3_bucket.lab_primary_region.arn	
		}
	}
}
  

# Información de la región secundaria
output "secondary_region_info" {	
	description = "Información detallada de la región secundaria"

	value = {
		name = data.aws_region.secondary.name
		description = data.aws_region.secondary.description
		endpoint = data.aws_region.secondary.endpoint

		availability_zones = {
			count = length(data.aws_availability_zones.secondary_azs.names)
			names = data.aws_availability_zones.secondary_azs.names
			zone_ids = data.aws_availability_zones.secondary_azs.zone_ids
		}

		latest_ami = {
			id = data.aws_ami.amazon_linux_secondary.id
			name = data.aws_ami.amazon_linux_secondary.name
			description = data.aws_ami.amazon_linux_secondary.description
			creation_date = data.aws_ami.amazon_linux_secondary.creation_date
		}

		created_resources = {
			s3_bucket = aws_s3_bucket.lab_secondary_region.id
			bucket_arn = aws_s3_bucket.lab_secondary_region.arn
		}
	}
}
  

# Comparación entre regiones
output "regions_comparison" {
description = "Comparación entre las dos regiones"
	value = {
		primary_region = {
			name = var.primary_region
			az_count = length(data.aws_availability_zones.primary_azs.names)
			azs = data.aws_availability_zones.primary_azs.names
		}

		secondary_region = {
			name = var.secondary_region
			az_count = length(data.aws_availability_zones.secondary_azs.names)
			azs = data.aws_availability_zones.secondary_azs.names
		}

		summary = {
			total_azs_explored = length(data.aws_availability_zones.primary_azs.names) + length(data.aws_availability_zones.secondary_azs.names)
		
		regions_compared = 2

}

}

}

  

# Información de laboratorio

output "lab_summary" {

description = "Resumen del laboratorio completado"

value = {

lab_name = "Lab 01 - Exploring AWS Regions and AZs"

objective = "Understand AWS global infrastructure"

  

learned_concepts = [

"AWS Regions and Availability Zones",

"Data sources in Terraform",

"Multi-provider configuration",

"Resource tagging strategies",

"S3 bucket security best practices"

]

  

resources_created = {

s3_buckets = 2

regions_used = 2

providers_configured = 2

}

  

cleanup_command = "terraform destroy"

estimated_cost = "~$0.00 (Free Tier S3 usage)"

}

}
```