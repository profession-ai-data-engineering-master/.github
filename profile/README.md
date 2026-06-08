# Data Engineering — Portfolio dei progetti

Questa organizzazione raccoglie i progetti sviluppati lungo il percorso di
**Data Engineering**: dall'ingegneria del software (Clean Architecture, testing,
CI/CD) all'analisi dati, dai database SQL/NoSQL all'elaborazione distribuita,
fino alle pipeline cloud end-to-end.

I progetti vengono **sistemati e documentati in modo incrementale**. Questo
indice viene aggiornato man mano: ogni progetto passa da 🚧 *in lavorazione* a
✅ *pronto* una volta completato il refactoring e la documentazione.

---

## Progetti pronti

### ✅ Progetto 1 — Household Expense Manager

> [`profession_ai_data_engineering_progetto1`](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto1)

Applicazione **da riga di comando in Python** per tracciare le spese personali,
produrre un report mensile ed evidenziare le spese più significative, con
persistenza su file CSV.

Nato come esercizio di portfolio, va oltre i requisiti funzionali: è strutturato
secondo i principi di **Clean Architecture** e **Domain-Driven Design**, con
copertura dei test, type checking statico e CI.

**Funzionalità**
- Aggiunta di una spesa (data, descrizione, importo) salvata su CSV.
- Report mensile aggregato per anno/mese.
- Top 10 delle spese per importo.
- Motore di reporting **intercambiabile** a runtime: in-memory (Python, default)
  oppure SQL (DuckDB, extra `analytics`).

**Qualità & ingegneria**
- 🏛️ Architettura a 4 layer concentrici (domain · application · infrastructure · interfaces) con *Dependency Inversion*.
- 🧩 Pattern **Command** per le operazioni della CLI; *composition root* per il wiring delle dipendenze.
- ✅ Test con **pytest** (coverage ~96%), type checking **strict** con **mypy**, lint/format con **ruff**.
- ⚙️ **CI GitHub Actions** multi-versione (Python 3.10 / 3.11 / 3.12) + report di coverage.
- 📚 Documentazione API generata con **Sphinx** e pubblicata online.

**Stack:** Python · Clean Architecture · DDD · SOLID · pytest · mypy · ruff · GitHub Actions · Sphinx · DuckDB

📖 [Documentazione online](https://profession-ai-data-engineering-master.github.io/profession_ai_data_engineering_progetto1/)

---

## In lavorazione

I progetti seguenti sono in fase di sistemazione/refactoring e verranno censiti
qui in dettaglio man mano che vengono completati.

| # | Progetto | Tema | Stato |
|---|----------|------|-------|
| 2  | `profession_ai_data_engineering_progetto2` | Analisi indici azionari (S&P 500 ed EURO STOXX 50) con pandas | 🚧 In lavorazione |
| 3  | `profession_ai_data_engineering_progetto3` | Feature engineering clienti bancari — tabella denormalizzata SQL | 🚧 In lavorazione |
| 4  | `profession_ai_data_engineering_progetto4` | Rubrica contatti con MongoDB (document store, query e update) | 🚧 In lavorazione |
| 5  | `profession_ai_data_engineering_progetto5` | *(da definire)* | 🚧 In lavorazione |
| 6  | `profession_ai_data_engineering_progetto6` | *(da definire)* | 🚧 In lavorazione |
| 7  | `profession_ai_data_engineering_progetto7` | *(da definire)* | 🚧 In lavorazione |
| 8  | `profession_ai_data_engineering_progetto8_databricks` · `…_zeppelin` | Elaborazione distribuita con Spark (Databricks / Zeppelin) | 🚧 In lavorazione |
| 9  | `profession_ai_data_engineering_progetto9` | CryptoData Insights — pipeline E2E su AWS (S3 · Glue · Redshift · Step Functions) | 🚧 In lavorazione |
| 10 | `profession_ai_data_engineering_progetto10` | Pipeline di orchestrazione dati film con Azure Data Factory | 🚧 In lavorazione |
| 11 | `profession_ai_data_engineering_progetto11` | Gestione dati pazienti con Snowflake (data warehouse, RBAC, GDPR) | 🚧 In lavorazione |
| —  | `creazione_dataset_cassandra_movielens` | Creazione dataset MovieLens su Apache Cassandra | 🚧 In lavorazione |

---

<sub>Indice mantenuto manualmente. Ultimo aggiornamento: progetto 1 censito; restanti progetti in sistemazione.</sub>
