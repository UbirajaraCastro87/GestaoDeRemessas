# 🚀 Data Lake - Gestão de Remessas e Reparos

## 📌 Visão Geral

Este projeto implementa uma arquitetura de **Data Lake moderna** para acompanhamento completo do ciclo de remessas e ordens de serviço, desde o envio pelo cliente até o retorno após o reparo.

O objetivo é fornecer **visibilidade ponta a ponta**, com foco em:

* SLA (tempo de atendimento)
* Eficiência operacional
* Custos de reparo
* Experiência do cliente

---

## 🧠 Arquitetura

A arquitetura segue o padrão de Data Lake em três camadas:

```
RAW (Bronze) → TRUSTED (Silver) → REFINED (Gold)
```

### 🔹 Fluxo de Dados

1. Sistemas operacionais (ERP / Remessas)
2. Ingestão (API, CDC, Batch)
3. Data Lake (armazenamento)
4. Processamento de dados
5. Consumo via BI

---

## 🏗️ Estrutura do Projeto

```
data-lake/
│
├── ingestion/          # Scripts de ingestão (API, CDC, Batch)
├── raw/                # Dados brutos (JSON, CSV)
├── trusted/            # Dados tratados
├── refined/            # Dados prontos para BI
├── models/             # Modelagem dimensional (fatos e dimensões)
├── pipelines/          # Jobs ETL / ELT
├── dashboards/         # Arquivos de BI (Power BI, Metabase)
└── docs/               # Documentação e diagramas
```

---

## 🌊 Camadas do Data Lake

### 🟤 RAW (Bronze)

* Dados brutos, sem transformação
* Fonte única da verdade
* Exemplo:

  * `remessa_raw`
  * `os_raw`
  * `eventos_raw`

---

### 🟡 TRUSTED (Silver)

* Dados limpos e estruturados
* Tipagem correta
* Remoção de duplicidades

Exemplo:

* `remessa`
* `ordem_servico`
* `eventos_status`

---

### 🟢 REFINED (Gold)

* Dados analíticos
* KPIs e métricas calculadas

Exemplo:

* `fato_ordem_servico`
* `dim_cliente`
* `dim_tempo`
* `fato_material`

---

## 🔄 Modelo baseado em eventos (Event Driven)

O sistema utiliza uma abordagem baseada em eventos para rastrear todas as etapas do processo.

### 📌 Tabela: `eventos_status`

| id_remessa | status     | data_hora |
| ---------- | ---------- | --------- |
| 1          | ENVIADO    | ...       |
| 1          | RECEBIDO   | ...       |
| 1          | EM_REPARO  | ...       |
| 1          | FINALIZADO | ...       |

---

### 🎯 Benefícios

* Cálculo preciso de SLA
* Reconstrução de timeline
* Auditoria completa
* Base para Machine Learning

---

## 📊 KPIs Monitorados

* ⏱️ Tempo total da remessa
* 🚚 Tempo de transporte
* 🔧 Tempo de reparo
* ⏳ Tempo de aprovação do cliente
* 💰 Custo por ordem de serviço
* 📉 Taxa de atraso
* 📊 SLA cumprido (%)

---

## 🧰 Stack Tecnológica

### 🔹 Armazenamento

* Data Lake (S3, MinIO, HDFS)
* Formato: Parquet

### 🔹 Processamento

* Apache Spark
* Databricks (opcional)

### 🔹 Ingestão

* Airbyte
* Apache Kafka
* API REST

### 🔹 Orquestração

* Apache Airflow

### 🔹 BI / Visualização

* Power BI
* Metabase
* Apache Superset

---

## ⚙️ Pipeline de Dados

1. Ingestão dos dados do sistema transacional
2. Armazenamento na camada RAW
3. Processamento e limpeza (TRUSTED)
4. Enriquecimento e modelagem (REFINED)
5. Consumo via dashboards

---

## 📈 Casos de Uso

* Monitoramento de SLA
* Identificação de gargalos operacionais
* Análise de custos de manutenção
* Performance de técnicos
* Tempo de resposta ao cliente

---

## 🔮 Evolução Futura

* Previsão de tempo de reparo (Machine Learning)
* Detecção automática de atrasos
* Score de clientes
* Otimização logística

---

## 🚀 Como Executar (Exemplo Local)

```bash
# Subir ambiente com Docker
docker-compose up -d

# Executar pipeline
python pipelines/run_pipeline.py
```

---

## 📌 Boas Práticas

* Sempre registrar eventos com timestamp
* Nunca sobrescrever dados da camada RAW
* Utilizar versionamento de dados (Delta/Parquet)
* Garantir idempotência nos pipelines

---

## 👨‍💻 Autor

Projeto desenvolvido para gestão inteligente de remessas e serviços técnicos.

---

## 📄 Licença

Este projeto pode ser utilizado para fins educacionais e comerciais.
