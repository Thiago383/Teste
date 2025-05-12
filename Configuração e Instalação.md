# 📘 Documentação Técnica

## 📌 Sumário



Este repositório descreve os procedimentos técnicos para instalação e configuração dos seguintes componentes:

MongoDB via Docker

Mongo Compass (interface gráfica)

Apache Airflow com integração ao MongoDB

## ✅ Pré-requisitos
Docker instalado no sistema operacional
👉 Documentação Oficial do Docker

Acesso à linha de comando (terminal, shell ou prompt de comando)

## 🚀 Passo a Passo
### 1. Instalação do Docker
Siga as instruções disponíveis no site oficial:

🔗 Instalar Docker

### 2. Instalação do Mongo Compass
Acesse: Download Mongo Compass

Faça o download da versão adequada ao seu sistema.

Execute o instalador e siga as instruções.

### 3. Preparação dos Arquivos de Configuração
Você deve receber um arquivo .zip com os arquivos necessários (ex: docker-compose.yml, Dockerfile, etc).

Descompacte esse arquivo em um diretório à sua escolha.

### 4. Inicialização do Ambiente Docker
* Abra o terminal.

* Navegue até o diretório onde os arquivos foram descompactados:
```
cd: bash
cd <caminho_para_a_pasta_descompactada>
```

* Inicialize os serviços do Airflow:
```
docker compose up airflow-init
```

* Após isso, para iniciar os serviços do Airflow em modo detached (em segundo plano), execute:
``` 
docker compose up -d
```

* O ambiente Docker com Airflow e MongoDB estará agora em execução. Para acessar a interface web do Airflow, localize a porta mapeada para o serviço web no Docker Desktop ou através da inspeção dos containers. A URL será similar a http://localhost:<porta>.

* Credenciais Padrão do Airflow:
- Username: airflow
- Password: airflow
  
### 5. Configuração da Conexão MongoDB no Airflow
Acesse a interface web do Airflow.

Vá em Admin > Connections.

Clique em + Create e preencha para adicionar uma nova conexão:

Conn Id: 	mongodb_default
Conn Type: 	Mongo
Host:	mongodb, este é o nome do serviço MongoDB definido no arquivo docker-compose.yml
Schema:	admin
Login:	root
Password:	example









