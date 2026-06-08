# Master Professionale in Data Engineering — Portfolio

Questa organizzazione raccoglie i progetti realizzati lungo il **Master
Professionale in Data Engineering** di [ProfessionAI](https://www.profession.ai/corsi/master-data-engineering/):
**11 corsi professionalizzanti** e **11 progetti pratici** (~400 ore) che
coprono l'intero spettro del mestiere — dall'ingegneria del software
all'analisi dati, dai database SQL/NoSQL ai Big Data, fino alle pipeline cloud
end-to-end. Percorso completato e **certificato**.

Ogni progetto nasce da un caso di business reale del corrispondente corso. I
repository vengono **sistemati e documentati in modo incrementale**: questo
indice viene aggiornato man mano, e ogni progetto passa da 🚧 *in lavorazione* a
✅ *pronto* una volta completati refactoring e documentazione.

**Stack del percorso:** Python · NumPy/Pandas · SQL (MySQL/MariaDB) · NoSQL
(MongoDB, Cassandra, DynamoDB, Neo4j) · BeautifulSoup/Selenium · scikit-learn ·
Apache Spark (Databricks, Zeppelin, EMR) · AWS (S3, Glue, Kinesis, Redshift,
Step Functions) · Azure Data Factory · Snowflake.

---

## Progetti pronti

### ✅ Corso 1 · Programmazione con Python — Household Expense Manager

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

Progetti in fase di sistemazione/refactoring. Il tema e lo stack riportati
seguono il programma ufficiale del master; verranno censiti qui in dettaglio
man mano che vengono completati.

| Corso | Progetto · Repository | Tema | Stack | Stato |
|:-----:|-----------------------|------|-------|:-----:|
| 2  | Analisi indici azionari `…progetto2` | Analisi dell'andamento di S&P 500 ed EURO STOXX 50 (rendimenti, volatilità, volumi) | NumPy · Pandas · Matplotlib | 🚧 |
| 3  | Clienti banca `…progetto3` | Feature engineering: tabella denormalizzata di indicatori comportamentali da dati transazionali | SQL · MySQL/MariaDB | 🚧 |
| 4  | Rubrica contatti `…progetto4` | Gestione e interrogazione di una rubrica document-oriented | MongoDB · NoSQL | 🚧 |
| 4  | Dataset MovieLens `creazione_dataset_cassandra_movielens` | Creazione di un dataset MovieLens su database colonna-famiglia | Apache Cassandra · NoSQL | 🚧 |
| 5  | Web scraping `…progetto5` | Scraping dei titoli di una libreria online (pagine statiche e dinamiche) | Python · BeautifulSoup · Selenium | 🚧 |
| 6  | Preprocessing & Feature Eng. `…progetto6` | Pre-processing di un dataset di rilevazione del tumore al seno | scikit-learn · PCA · SMOTE | 🚧 |
| 7  | Fondamenti ML `…progetto7` | Previsione della progressione del diabete in pazienti a rischio | scikit-learn · regressione · classificazione · clustering | 🚧 |
| 8  | Big Data su Wikipedia `…progetto8_databricks` · `…_zeppelin` | Processing e analisi dell'intero dump di Wikipedia | Apache Spark · Spark SQL · Databricks · Zeppelin · AWS EMR | 🚧 |
| 9  | CryptoData Insights `…progetto9` | Pipeline E2E in cloud per analizzare Bitcoin e Monero | AWS S3 · Glue · Kinesis · Redshift · Step Functions | 🚧 |
| 10 | Dataset film `…progetto10` | Orchestrazione di una pipeline di trasformazione su un dataset di film | Azure Data Factory · Blob Storage · Stream Analytics | 🚧 |
| 11 | Dati pazienti `…progetto11` | Data management & security dei dati clinici di un ospedale (RBAC, GDPR) | Snowflake · Data Warehouse | 🚧 |

> I nomi repository sono abbreviati con il prefisso comune `profession_ai_data_engineering_`.

---

<sub>Indice mantenuto manualmente. Ultimo aggiornamento: progetto 1 censito in dettaglio; restanti progetti mappati al programma ufficiale e in fase di sistemazione.</sub>
