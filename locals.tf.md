```hcl
# =============================================================================
# VARIABLES LOCALES
# =============================================================================
  

locals {
	
	common_tags = {
		# Tags comunes para todos los recursos
		Project = var.project_name
		Environment = var.environment
		Lab = "Lab-${var.lab_number}-${var.lab_name}"
		Owner = var.owner
		CreatedBy = "Terraform"
		Phase = "Phase-1-Fundamentals"
		Purpose = "AWS-SAA-Certification-Study"
		CreatedDate = formatdate("YYYY-MM-DD", timestamp())
	}
  

	# Configuraciones derivadas
	resource_prefix = "${var.project_name}-${var.environment}-lab${var.lab_number}"
	
	regions_info = {
		primary = {
			name = var.primary_region
			description = "Región primaria para el laboratorio"
		}
  

secondary = {

name = var.secondary_region

description = "Región secundaria para el laboratorio"

}

}

}
```