```hcl
terraform {
	required_version = ">= 1.0"
	
	required_providers {
		aws = {
			source = "hashicorp/aws"
			version = "~> 5.0"
		}
	}
}

  
# Provider principal - Región principal
provider "aws" {
	alias = "primary"
	region = var.primary_region
	
	default_tags {
		tags = local.common_tags
	}
}

  
# Provider secundario - Región secundario para comparación
provider "aws" {
	alias = "secondary"
	region = var.secondary_region
	
	default_tags {
		tags = local.common_tags
	}
}
```