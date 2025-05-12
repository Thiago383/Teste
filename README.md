# 📊 Categorização de Empresas por CNAE com Airflow e RabbitMQ

> Projeto desenvolvido para automatizar a classificação de empresas com base no CNAE, integrando Apache Airflow, MongoDB e RabbitMQ.

---

## 👤 Autor

**Seu Nome Aqui**

## 🏫 Instituição

Escola DNC

## 📅 Data

2025

---

## 📌 Sumário

- [1. Business Understanding](#1-business-understanding)
- [2. Data Understanding](#2-data-understanding)
- [3. Data Preparation](#3-data-preparation)
- [4. Modeling](#4-modeling)
- [5. Evaluation](#5-evaluation)
- [6. Deployment](#6-deployment)
- [7. Notas Técnicas](#7--notas-técnicas)

---

## 1. Business Understanding

### 1.1 Objetivo do Negócio

O objetivo deste projeto é automatizar a **classificação de empresas por CNAE** (Classificação Nacional de Atividades Econômicas), a partir de bases atualizadas periodicamente. Sempre que uma **nova empresa** for detectada nos dados, uma **notificação** será enviada e a empresa será incluída na **fila de processamento**, categorizada por seu setor (com base no CNAE).

A automação do processo será realizada com o uso de **Airflow** para orquestração e **RabbitMQ** para gerenciar as filas por categoria.

- 📅 Dados atualizados periodicamente
- 🔔 Notificações de novas empresas
- 🧵 Fila de processamento segmentada por setor


### 1.2 Avaliação da Situação

- **Stakeholders:** Equipes de dados, ETL, risco e gestão.
- **Tecnologias utilizadas:**
    - Apache Airflow  (orquestração)
    - Mongo DB via Docker (Infraestrutura de Banco de Dados)
    - Mongo Compass (Interface Gráfica)
    - RabbitMQ (mensageria)
    - Python (desenvolvimento)
    - Pandas & NumPy (manipulação dos dados)
- **Benefícios esperados:**
  - 🚀 Eficiência no fluxo de dados
  - 🔄 Atualização automática
  - 📦 Categorias bem definidas
- **Restrições:** As bases de dados podem conter registros inconsistentes ou desatualizados, exigindo verificação contínua de qualidade.

### 1.3 Metas

- Identificar e categorizar automaticamente empresas novas por CNAE
- Monitorar a chegada de novos registros periodicamente
- Enviar os dados organizados em filas temáticas via RabbitMQ

### 1.4 Plano do Projeto

1. 📥 Coletar e validar dados de entrada
2. 🔎 Identificar registros novos
3. 🏷️ Categorizar por CNAE
4. 📨 Enviar dados organizados para filas específicas no RabbitMQ
5. 🛠️ Automatizar via Airflow (com DAG diária)
6. 🧩 Monitorar logs e filas para garantir robustez

---

## 2. Data Understanding

### 2.1 Coleta Inicial dos Dados
As bases de dados são arquivos CSV fornecidos por um sistema externo ou API que contém o CNPJ, Nome, CNAE principal e secundário, entre outros campos.

Arquivos CSV com:

- CNPJ
- Nome
- CNAE principal e secundário
- UF

### 2.2 Campos Relevantes

| Campo           | Tipo   | Descrição                             |
|----------------|--------|----------------------------------------|
| CNPJ           | String | Identificador único da empresa         |
| Nome           | String | Nome fantasia ou razão social          |
| CNAE_Principal | String | Atividade principal                    |
| CNAE_Secundario| Lista  | Atividades complementares              |
| UF             | String | Estado                                 |

### 2.3 Exploração dos Dados

- 📊 Frequência dos CNAEs
- 🗺️ Distribuição por UF
- 🆕 Empresas detectadas em cada lote

### 2.4 Qualidade dos Dados

- ❌ Ausência de CNAEs
- 🔁 CNPJs duplicados
- ✅ Limpeza e padronização aplicadas

---

## 3. Data Preparation

### 3.1 Seleção de Dados

Utilizados: CNPJ, Nome, CNAE_Principal

### 3.2 Limpeza

- Remoção de duplicatas
- Preenchimento de CNAEs ausentes com `"Não informado"`
- Conversão de tipos

### 3.3 Feature Engineering

- Criação do campo `categoria` com base no mapeamento CNAE → setor

### 3.4 Integração

- Comparação com base anterior para encontrar empresas novas

### 3.5 Formatação

- Dados formatados em JSON para envio ao RabbitMQ

---

## 4. Modeling

### 4.1 Abordagem

🔧 Mapeamento determinístico (sem aprendizado de máquina)

### 4.2 Testes

- Simulações para garantir:
  - 📍 Identificação de novas empresas
  - 📤 Envio correto por categoria

### 4.3 Pipeline

- Scripts Python categorizando empresas
- Publicação em filas por setor:
  - `comercio`
  - `industria`
  - `servicos`
  - `outros`

### 4.4 Resultados

- ✅ 100% de identificação
- 📦 99,8% de envio correto para a fila

---

## 5. Evaluation

### 5.1 Resultados

- Automatização eficiente
- Resultados consistentes com os objetivos

### 5.2 Revisão

- 🧪 Validação contínua
- 🔄 Integração com pipeline em produção

### 5.3 Próximos Passos

- 🌍 Escalar para outros estados
- 🤖 Explorar classificação inteligente com IA

---

## 6. Deployment

### 6.1 Pipeline via Airflow

- DAG diária executa:
  - Leitura dos dados
  - Comparação
  - Categorização
  - Publicação nas filas

### 6.2 Monitoramento

- Logs do Airflow
- Dashboards do RabbitMQ
- Verificação e reprocessamento de filas mortas

### 6.3 Resumo

| Item        | Resultado                         |
|-------------|-----------------------------------|
| ✅ Objetivo | Detecção de novas empresas        |
| ⚙️ Ferramentas | Airflow, Python, MongoDB, RabbitMQ |
| 💰 Custo     | Baixo (open-source)              |
| 📈 Status    | Em produção                      |

### 6.4 Revisão

| ✅ Funcionou bem                  | ⚠️ Melhorias sugeridas                   |
|-------------------------------|---------------------------------------|
| DAG diária automatizada       | Considerar CNAEs secundários          |
| Categorização precisa         | Adicionar modelo preditivo futuramente|

---

## ✅ Notas Técnicas

### 📦 Tecnologias

- Apache Airflow
- RabbitMQ
- MongoDB + Mongo Compass
- Docker + Docker Compose
- Python (Pandas, NumPy)

### ⚙️ Setup Rápido

> Pré-requisitos: Docker, Docker Compose, Mongo Compass

```bash
# Inicializar Airflow e MongoDB
docker compose up airflow-init
docker compose up -d

# Acessar Airflow
http://localhost:<porta>
Usuário: airflow
Senha: airflow
