```hcl
# =============================================================================
# VARIABLES DEL LABORATORIO
# =============================================================================


variable "primary_region" {
	description = "Región AWS primaria para el laboratorio"
	type = string
	default = "us-east-1"
	
	validation {
		condition = can(regex("^[a-z]{2}-[a-z]+-[0-9]$", var.primary_region))
		error_message = "La región debe tener formato válido (ej: us-east-1)."
	}
}


variable "secondary_region" {
	description = "Región AWS secundaria para el laboratorio"
	type = string
	default = "us-west-2"
	
	validation {
		condition = can(regex("^[a-z]{2}-[a-z]+-[0-9]$", var.secondary_region))
		error_message = "La región debe tener formato válido (ej: us-west-2)."
	}
}


variable "environment" {

description = "Ambiente del laboratorio"

type = string

default = "lab"

  

validation {

condition = contains(["lab", "dev", "staging", "prod"], var.environment)

error_message = "El ambiente debe ser: lab, dev, staging o prod."

}

}

  

variable "project_name" {

description = "Nombre del proyecto"

type = string

default = "aws-saa-certification"

}

  

variable "lab_number" {

description = "Numero del laboratorio"

type = string

default = "01"

}

  

variable "lab_name" {

description = "Nombre descriptivo del laboratorio"

type = string

default = "regions-azs-exploration"

}

  

variable "owner" {

description = "Propietario del laboratorio"

type = string

default = "aws-student"

}
```