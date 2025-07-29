# analisesentmlops

Este projeto realiza análise de sentimentos de comentários do YouTube, utilizando Python, DVC, AWS, Docker e GitHub Actions para orquestração de um pipeline completo de MLOps.


Configuração do Ambiente
bashconda create -n youtube python=3.11 -y
conda activate youtube
pip install -r requirements.txt
DVC (Data Version Control)
bashdvc init
dvc repro
dvc dag
AWS
bashaws configure
Teste da API
Dados JSON de demonstração no Postman:
URL: http://localhost:5000/predict

{
    "comments": ["Este vídeo é incrível! Eu adorei muito", "Explicação muito ruim. vídeo péssimo"]
}
Extensões do Chrome
chrome://extensions
Como Obter a Chave da API do YouTube pelo GCP:
https://www.youtube.com/watch?v=i_FdiQMwKiw
Deploy AWS-CICD com GitHub Actions
1. Fazer Login no Console AWS
2. Criar Usuário IAM para Deploy
# Com acesso específico

1. Acesso EC2: É uma máquina virtual

2. ECR: Elastic Container Registry para salvar sua imagem docker na AWS

# Descrição: Sobre o deploy

1. Construir imagem docker do código fonte

2. Enviar sua imagem docker para o ECR

3. Iniciar sua EC2

4. Baixar sua imagem do ECR na EC2

5. Executar sua imagem docker na EC2

# Políticas:

1. AmazonEC2ContainerRegistryFullAccess

2. AmazonEC2FullAccess
3. Criar Repositório ECR para Armazenar/Salvar Imagem Docker
- Salvar a URI: 315865595366.dkr.ecr.us-east-1.amazonaws.com/youtube
4. Criar Máquina EC2 (Ubuntu)
5. Abrir EC2 e Instalar Docker na Máquina EC2:
bash# opcional
sudo apt-get update -y
sudo apt-get upgrade -y

# obrigatório
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ubuntu
newgrp docker
6. Configurar EC2 como Runner Auto-hospedado:
settings > actions > runner > new self hosted runner > escolher OS > então executar comandos um por um
7. Configurar Secrets do GitHub:
AWS_ACCESS_KEY_ID=

AWS_SECRET_ACCESS_KEY=

AWS_REGION = us-east-1

AWS_ECR_LOGIN_URI = exemplo >> 566373416292.dkr.ecr.ap-south-1.amazonaws.com

ECR_REPOSITORY_NAME = simple-app