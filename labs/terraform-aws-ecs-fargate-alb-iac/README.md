# AWS ECS Fargate + Terraform: Infraestrutura como Código (IaC)

Este repositório contém a automação completa para o deploy de aplicações containerizadas na AWS, utilizando **Terraform** para orquestrar uma arquitetura escalável, segura e resiliente.

## Arquitetura da Solução

O projeto provisiona uma infraestrutura moderna baseada em containers (Serverless Compute), composta por:

- **Networking:** VPC customizada com Subnets Públicas e Privadas, Route Tables e Internet Gateway.
- **Segurança:** Security Groups granulares para isolamento de tráfego entre Load Balancer e Containers.
- **Orquestração:** Cluster ECS com AWS Fargate (Serverless).
- **Edge & Traffic:** Application Load Balancer (ALB) para distribuição de carga e Health Checks.
- **Observabilidade:** CloudWatch Logs integrado para monitoramento das tasks.

> **[ILUSTRAÇÃO DO FLUXO  ]**
> '![Fluxo de Infraestrutura](./labs/terraform-aws-ecs-fargate-alb-iac/diagrams/terraform-aws-flow-excalidraw.png)'

---

## Como Executar

### Opção A: Ambiente Isolado (Docker)
Para garantir que o ambiente de execução seja idêntico, você pode utilizar o Dockerfile incluso para subir um container de deploy com Terraform e AWS CLI pré-instalados.

1. **Build da imagem de deploy:**

   docker build -t terraform-iac-engine:v1.0 .

   Execução do container (mapeando o volume de código):
    docker run -dit --name iac-deploy-container -v ${PWD}:/iac terraform-iac-engine:v1.0 /bin/bash

Opção B: Execução Local
Navegue até a pasta da infraestrutura: cd labs/terraform-aws-ecs-fargate-alb-iac/infra
Configure suas credenciais AWS localmente (aws configure).
Crie seu arquivo de variáveis real: cp terraform.tfvars.example terraform.tfvars

Inicialize e aplique:
terraform init
terraform plan
terraform apply

Segurança e Boas Práticas
Zero Secrets: Nenhuma credencial AWS ou ID de conta real é armazenado no repositório.
Variáveis Sensíveis: O uso de sensitive = true no Terraform garante que dados críticos não apareçam nos logs de console.
Modularização: Estrutura preparada para evolução em módulos reutilizáveis.

Autor: Gabriel Pacheco
Analytics Engineer em formação.
