# AWS ECS Fargate + Terraform: Infraestrutura como Código (IaC)

Este repositório contém a automação completa para o deploy de aplicações containerizadas na AWS, utilizando **Terraform** para orquestrar uma arquitetura escalável, segura e resiliente.

---

## Arquitetura da Solução

A solução provisiona uma infraestrutura baseada em containers (Serverless Compute), garantindo alta disponibilidade e isolamento de rede:

- **Networking:** VPC customizada com Subnets Públicas e Privadas, Route Tables e Internet Gateway.
- **Segurança:** Security Groups granulares para isolamento de tráfego entre Load Balancer e Containers.
- **Orquestração:** Cluster ECS utilizando **AWS Fargate** (Serverless).
- **Edge & Traffic:** Application Load Balancer (ALB) para distribuição de carga e monitoramento de Health Checks.
- **Observabilidade:** Integração nativa com CloudWatch Logs.

> **Diagrama de Arquitetura:**
> ![Fluxo de Infraestrutura](./diagrams/IlustracaoFluxo_TerraformAWS.jpg)

---

## Como Executar

### Opção A: Ambiente Isolado (Docker)

Para garantir que o ambiente de execução seja idêntico, utilize o `Dockerfile` incluso para subir um container de deploy.

1. **Build da imagem de deploy:**
```bash
docker build -t terraform-iac-engine:v1.0 .
Execução do container (mapeando o volume de código):
bash
Copy
docker run -dit --name iac-deploy-container -v ${PWD}:/iac terraform-iac-engine:v1.0 /bin/bash
Acessar o ambiente:
bash
Copy
docker exec -it iac-deploy-container /bin/bash
cd /iac/labs/terraform-aws-ecs-fargate-alb-iac/infra
Opção B: Execução Local
Navegue até a pasta da infraestrutura:
bash
Copy
cd labs/terraform-aws-ecs-fargate-alb-iac/infra
Configure suas credenciais AWS:
bash
Copy
aws configure
Prepare as variáveis de ambiente:
bash
Copy
cp terraform.tfvars.example terraform.tfvars
Provisionamento:
bash
Copy
terraform init
terraform plan
terraform apply


Segurança e Boas Práticas
Zero Secrets: Nenhuma credencial AWS ou ID de conta real é armazenado no repositório.
Variáveis Sensíveis: Uso de sensitive = true no Terraform para proteger dados críticos.
Infra Imutável: Toda alteração é feita via código, garantindo rastreabilidade.
Modularização: Estrutura preparada para evolução em módulos reutilizáveis.


Autor
Gabriel Pacheco
Analytics Engineer em formação 


