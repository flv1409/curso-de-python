Excelente! 👏
Adicionar scripts Bash ao repositório vai deixar seu projeto muito mais completo e prático — mostrando domínio real da AWS CLI.

Aqui está o README atualizado com uma nova seção /scripts, incluindo exemplos prontos de criação, inicialização, parada e encerramento de instâncias EC2 — tudo automatizado.
Você só precisa copiar os arquivos .sh e ajustar o ID da instância conforme o seu ambiente.


---

💻 Gerenciamento de Instâncias EC2 na AWS

📘 Sobre o Projeto

Este repositório foi desenvolvido como parte do desafio da Digital Innovation One (DIO), com o objetivo de consolidar o aprendizado sobre gerenciamento de instâncias EC2 na Amazon Web Services (AWS).

A proposta é aplicar na prática os conceitos vistos nas aulas, documentando o processo de criação, configuração e gerenciamento de uma instância EC2 — tanto via Console AWS quanto via AWS CLI e scripts automatizados.


---

🎯 Objetivos de Aprendizagem

Aplicar na prática os conceitos aprendidos sobre EC2;

Automatizar tarefas com AWS CLI e scripts Bash;

Documentar processos técnicos de forma clara e organizada;

Utilizar o GitHub como ferramenta de portfólio técnico.



---

☁️ Estrutura do Projeto

aws-ec2-gerenciamento/
│
├── README.md               # Documentação principal
├── /images                 # Prints do laboratório
└── /scripts                # Scripts Bash para automação AWS CLI


---

☁️ Tópicos Abordados

Criação e configuração de uma instância EC2;

Geração e uso de chaves SSH;

Acesso remoto via terminal;

Gerenciamento de Security Groups;

Associação de Elastic IP;

Encerramento seguro da instância;

Automação via scripts AWS CLI.



---

🛠️ Passo a Passo Realizado

1. Criação da Instância

1. Acesse o Console AWS → EC2 → Launch Instance


2. Configurações utilizadas:

Nome: DIO-EC2-Lab

AMI: Amazon Linux 2

Tipo: t2.micro

Par de chaves: dio-key.pem

Security Group: portas 22 (SSH) e 80 (HTTP) liberadas





---

2. Conectando via SSH

chmod 400 dio-key.pem
ssh -i "dio-key.pem" ec2-user@<IP_DA_INSTANCIA>


---

3. Configurando o Ambiente

Atualização do sistema e instalação de ferramentas básicas:

sudo yum update -y
sudo yum install git -y


---

💻 Automação com AWS CLI e Scripts Bash

Abaixo estão os scripts prontos que podem ser salvos na pasta /scripts/.


---

🔹 01-create-instance.sh

Cria uma nova instância EC2 e salva o ID em um arquivo local.

#!/bin/bash

echo "🚀 Criando nova instância EC2..."

aws ec2 run-instances \
  --image-id ami-0c55b159cbfafe1f0 \
  --instance-type t2.micro \
  --key-name dio-key \
  --security-group-ids sg-xxxxxxxxxxxxx \
  --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=DIO-EC2-Lab}]' \
  --query 'Instances[0].InstanceId' \
  --output text > instance-id.txt

echo "✅ Instância criada com ID: $(cat instance-id.txt)"


---

🔹 02-start-instance.sh

Inicia a instância criada.

#!/bin/bash

INSTANCE_ID=$(cat instance-id.txt)

echo "▶️ Iniciando instância $INSTANCE_ID..."
aws ec2 start-instances --instance-ids $INSTANCE_ID
echo "✅ Instância iniciada!"


---

🔹 03-stop-instance.sh

Para a instância em execução.

#!/bin/bash

INSTANCE_ID=$(cat instance-id.txt)

echo "⏸ Parando instância $INSTANCE_ID..."
aws ec2 stop-instances --instance-ids $INSTANCE_ID
echo "✅ Instância parada!"


---

🔹 04-terminate-instance.sh

Encerra (deleta) a instância definitivamente.

#!/bin/bash

INSTANCE_ID=$(cat instance-id.txt)

echo "🗑 Encerrando instância $INSTANCE_ID..."
aws ec2 terminate-instances --instance-ids $INSTANCE_ID
echo "✅ Instância encerrada e removida!"


---

🔹 05-describe-instance.sh

Exibe informações detalhadas sobre a instância.

#!/bin/bash

INSTANCE_ID=$(cat instance-id.txt)

echo "🔍 Consultando status da instância $INSTANCE_ID..."
aws ec2 describe-instances --instance-ids $INSTANCE_ID \
  --query 'Reservations[*].Instances[*].[InstanceId,State.Name,PublicIpAddress]' \
  --output table


---

⚙️ Como Usar os Scripts

1. Certifique-se de que a AWS CLI esteja instalada e configurada:

aws configure


2. Acesse a pasta /scripts e torne os scripts executáveis:

chmod +x *.sh


3. Execute conforme a necessidade:

./01-create-instance.sh
./02-start-instance.sh
./05-describe-instance.sh
./03-stop-instance.sh
./04-terminate-instance.sh




---

📸 Evidências

As capturas de tela estão na pasta /images, contendo:

instancia-criada.png

conexao-ssh.png

instancia-finalizada.png


Use a sintaxe Markdown para incluir as imagens no README:

![Instância criada](./images/instancia-criada.png)


---

📚 Recursos Consultados

Documentação oficial da AWS EC2

Documentação da AWS CLI

Guia GitHub Markdown

DIO - Formação AWS Cloud Practitioner



---

🧑‍💻 Autor

flv1409
🔗 GitHub Profile


---

💬 Dica Final

Esses scripts tornam o gerenciamento de instâncias totalmente automatizado — ideal para quem deseja dominar infraestrutura como código e se preparar para certificações AWS.
Você pode evoluir o projeto adicionando:

Variáveis de ambiente para diferentes ambientes (dev, test, prod);

Scripts Python usando boto3;

Integração com pipelines CI/CD.



---

Quer que eu gere também os arquivos .sh prontos (com cabeçalhos, comentários e formatação de código para copiar e colar direto)?
Posso montar os cinco scripts completos e formatados.
