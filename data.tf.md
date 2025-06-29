```hcl
# =============================================================================
# DATA SOURCES - EXPLORACIÓN DE REGIONES Y AZs
# =============================================================================


# Información de la región primaria
data "aws_region" "primary" {
	provider = aws.primary
}

# Información de la región secundaria
data "aws_region" "secondary" {
	provider = aws.secondary
}
  

# Zonas en disponibilidad de la región primaria
data "aws_availability_zones" "primary_azs" {
	provider = aws
	state = "available"
}
  

# Zonas de disponibilidad de la región secundaria
data "aws_availability_zones" "secondary_azs" {
	provider = aws.secondary
	state = "available"
}

  

# Información de la cuenta AWS actual

data "aws_caller_identity" "current" {}

  

# Información de la partición AWS (aws, aws-cn, aws-us-gov)

data "aws_partition" "current" {}

  

# AMIs disponibles en la región primaria (para referencia)

data "aws_ami" "amazon_linux_primary" {

provider = aws

most_recent = true

owners = ["amazon"]

  

filter {

name = "name"

values = ["amzn2-ami-hvm-*-x86_64-gp2"]

}

  

filter {

name = "virtualization-type"

values = ["hvm"]

}

}

  

# AMIs disponibles en la región secundaria (para comparación)

data "aws_ami" "amazon_linux_secondary" {

provider = aws.secondary

most_recent = true

owners = ["amazon"]

  

filter {

name = "name"

values = ["amzn2-ami-hvm-*-x86_64-gp2"]

}

  

filter {

name = "virtualization-type"

values = ["hvm"]

}

}

  

# Servicios disponibles en cada región

data "aws_service" "ec2_primary" {

provider = aws

service_id = "ec2"

region = var.primary_region

}

  

data "aws_service" "ec2_secondary" {

provider = aws.secondary

service_id = "ec2"

region = var.secondary_region

}
```