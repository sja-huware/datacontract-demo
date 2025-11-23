# Data Contract Demo

[![Data Contract Specification v1.2.1](https://img.shields.io/badge/Data%20Contract-v1.2.1-blue)](https://datacontract.com)

Questo progetto implementa un Data Contract per la gestione dei dati relativi ai personaggi delle serie animate Futurama e I Simpson. Il contratto definisce la struttura, i vincoli e le specifiche dei dati attraverso un'interfaccia PostgreSQL.

## 🎯 Caratteristiche Principali

- Definizione strutturata dei dati dei personaggi
- Implementazione basata su PostgreSQL
- Containerizzazione tramite Docker
- Script di inizializzazione automatica del database

## 🏗️ Struttura del Progetto

```
.
├── datacontract.yaml     # Definizione del data contract
├── docker-compose.yaml   # Configurazione Docker
├── init-scripts/
│   ├── create-tables.sql # Script creazione tabelle
│   └── insert-data.sql   # Script inserimento dati
└── README.md
```

## 📋 Prerequisiti

- [Docker](https://docs.docker.com/get-started/introduction/get-docker-desktop/) e Docker Compose

## 🚀 Installazione e Avvio

1. Clona il repository:
   ```bash
   git clone https://github.com/sja-huware/data-contract-l2.git
   cd data-contract-l2
   ```

2. Avvia il container Docker:
   ```bash
   docker-compose up -d
   ```

3. Verifica che il container sia in esecuzione:
   ```bash
   docker-compose ps
   ```

## 🗄️ Struttura del Database

### Tabella `futurama`

| Campo             | Tipo    | Descrizione                    | Vincoli           |
|------------------|---------|-------------------------------|-------------------|
| character_id     | integer | ID univoco del personaggio    | Primary Key      |
| name             | varchar | Nome completo                 | Not Null         |
| species          | varchar | Specie del personaggio        | Not Null         |
| occupation       | varchar | Occupazione/professione       | -                |
| age              | integer | Età (min: 0)                 | -                |
| planet_of_origin | varchar | Pianeta di origine           | -                |

## 🛠️ Sviluppo

### Modificare i Dati
Per modificare o aggiungere nuovi dati, aggiorna gli script nella cartella `init-scripts/`:
1. `create-tables.sql` per modificare la struttura delle tabelle
2. `insert-data.sql` per modificare i dati di esempio

### Ricostruire il Container
Dopo modifiche agli script:
```bash
docker-compose down -v
docker-compose up -d
```

## Demo

Eseguire i seguenti comandi di esempio per provare le funzionalità del progetto.

### 1. Inizializzare un Data Contract base:

```bash
uv run datacontract init base.yaml
```

### 2. Creare un Data Contract da un file SQL:

```bash
uv run datacontract import --format sql --source ./init-scripts/create-tables.sql > datacontract_import.yaml
```

### 3. Linting del contratto:

```bash
uv run datacontract lint
```

### 4. Esportare schemi e modelli:

```bash
uv run datacontract export --format jsonschema --model futurama >> futurama_schema.json
uv run datacontract export --format pydantic-model
uv run datacontract export --format dbt
uv run datacontract export --format html
```

### 5. Testare il Data Contract:

```bash
uv run datacontract test
```

---

Sviluppato con ❤️ da Jacopo Sardellini
