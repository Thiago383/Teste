# 📘 Documentação Técnica

— Instalação e Configuração: 
- MongoDB (Docker)
- Mongo Compass 
- Apache Airflow
Este repositório descreve os procedimentos técnicos para instalação e configuração dos seguintes componentes:

MongoDB via Docker

Mongo Compass (interface gráfica)

Apache Airflow com integração ao MongoDB

✅ Pré-requisitos
Docker instalado no sistema operacional
👉 Documentação Oficial do Docker

Acesso à linha de comando (terminal, shell ou prompt de comando)

🚀 Passo a Passo
1. Instalação do Docker
Siga as instruções disponíveis no site oficial:

🔗 Instalar Docker

2. Instalação do Mongo Compass
Acesse: Download Mongo Compass

Faça o download da versão adequada ao seu sistema.

Execute o instalador e siga as instruções.

3. Preparação dos Arquivos de Configuração
Você deve receber um arquivo .zip com os arquivos necessários (ex: docker-compose.yml, Dockerfile, etc).

Descompacte esse arquivo em um diretório à sua escolha.

4. Inicialização do Ambiente Docker
Abra o terminal.

Navegue até o diretório onde os arquivos foram descompactados:

bash
Copiar
Editar
cd <caminho_para_a_pasta_descompactada>
Inicialize os serviços do Airflow:

bash
Copiar
Editar
docker compose up airflow-init
Após isso, execute:

bash
Copiar
Editar
docker compose up -d
A interface do Airflow estará disponível em http://localhost:<porta>.

🔑 Credenciais Padrão do Airflow:

makefile
Copiar
Editar
Username: airflow
Password: airflow
5. Configuração da Conexão MongoDB no Airflow
Acesse a interface web do Airflow.

Vá em Admin > Connections.

Clique em + Create e preencha:

Campo	Valor
Conn Id	mongodb_default
Conn Type	Mongo
Host	mongodb
Schema	admin
Login	root
Password	example









