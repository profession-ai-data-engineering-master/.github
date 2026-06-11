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

### ✅ Corso 2 · Python Data Toolkit: NumPy, Pandas, Pyplot — Analisi indici azionari S&P 500 ed EURO STOXX 50

> [`profession_ai_data_engineering_progetto2`](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto2)

Analisi esplorativa a **10 anni** di due indici azionari globali — **S&P 500**
(USA) ed **EURO STOXX 50** (Europa) — per ricavare insight utili alle decisioni
di investimento: rendimenti percentuali, volatilità e volumi di scambio.

Più che un semplice script di calcolo, il progetto è impostato su un **framework
metodologico riconosciuto**: il flusso segue le 5 fasi di **OSEMN** (Obtain ·
Scrub · Explore · Model · iNterpret), scelto motivatamente rispetto a CRISP-DM,
così da garantire un processo strutturato e ripetibile.

**Analisi svolte**
- **Q1 — Rendimenti percentuali** giornaliero/mensile/annuale, con **performance
  cumulata** a confronto tra i due indici.
- **Q2 — Rendimento medio per giorno della settimana**, interpretato alla luce di
  fenomeni documentati (*reverse weekend effect*, composizione settoriale USA/Europa).
- **Q3 — Giornate di rendimento estremo** trattate come **outlier detection** con
  il **metodo IQR** (preferito allo Z-score perché non assume normalità), e
  ricondotte a eventi reali di mercato.
- **Q4 — Volume medio giornaliero** di scambi a confronto tra i due indici.

**Qualità & metodo**
- 🧭 Processo guidato dal framework **OSEMN**, con scelte progettuali esplicitate.
- 📒 **Data Dictionary** formale (tipi, business rules, semantica del volume) come presidio di qualità sui dati.
- 🧹 Scrub mirato ai dati di mercato: uniformazione fusi orari in UTC, allineamento sul **calendario di trading comune**, rimozione di volumi nulli.
- 📈 Visualizzazioni **Matplotlib** e interpretazione orientata all'investitore (diversificazione *core-satellite*, timing, liquidità/slippage).

**Stack:** Python · Pandas · Matplotlib · OSEMN · Jupyter Notebook

---

### ✅ Corso 3 · SQL — Analisi dei clienti di una banca

> [`profession_ai_data_engineering_progetto3`](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto3)

Costruzione di una **tabella denormalizzata di feature comportamentali** (una riga per
cliente) per alimentare modelli di *machine learning* supervisionato, a partire da un
database bancario **MySQL 8**. Il caso di business: **Banking Intelligence** vuole prevedere
abbandono, rischio e frodi dei clienti partendo dai dati transazionali e dal possesso di prodotti.

Il cuore è la vista **`DATI_DENORMALIZZATI_BANCA`** — **27 colonne** (`id_cliente` + 26
feature) ottenute con `LEFT JOIN` `cliente → conto → transazioni` e aggregazioni condizionali
(`CASE`) su segno della transazione e tipologia di conto: numero e importo di entrate/uscite,
in totale e per ciascuna delle 4 tipologie di conto.

Più che la sola query, il progetto cura **riproducibilità, qualità e leggibilità** fino a
livello di vetrina: chiunque può alzare l'ambiente e interrogare i dati in un comando.

**Cosa contiene**
- 🧱 **Vista di feature engineering**: una-riga-per-cliente, 26 indicatori comportamentali documentati uno a uno.
- 🧭 **Tour guidato** dentro Adminer: viste `tour_*` che traducono le feature in 5 domande di business (churn, rischio, valore, segmentazione, anomalie/frodi).
- ⚡ **Ottimizzazione dello schema** dimostrata e misurata: da **~1,55 s a ~120 ms** con chiavi e indice *covering*, con ripristino dello schema originale.

**Qualità & ingegneria**
- 🐳 **Ambiente Docker monocomando** (`run.sh`/`run.ps1`): MySQL + Adminer, dump scaricato in fase di build, healthcheck, vista e tour caricati automaticamente.
- 🔎 **Adminer** (web UI) con utente di **sola lettura** dedicato: si esplora il DB senza credenziali amministrative.
- ✅ **Asserzioni di validazione** in SQL (`SIGNAL`): una-riga-per-cliente, coerenza tra totali e somme per tipologia, range di età, assenza di `NULL` inattesi.
- 🧹 **Lint SQL** con **SQLFluff** (dialect MySQL) e **CI GitHub Actions** che a ogni push/PR avvia il DB, crea vista e tour, ed esegue asserzioni e lint.
- 📚 **Documentazione**: data dictionary delle 26 feature + diagramma **ER** (Mermaid).

**Stack:** SQL · MySQL 8 · Docker · Adminer · SQLFluff · GitHub Actions

---

### ✅ Corso 4 · Database NoSQL — Rubrica di contatti document-oriented su MongoDB

> [`profession_ai_data_engineering_progetto4`](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto4)

Gestione e interrogazione di una **rubrica di contatti** su **MongoDB**: 6 query
e 2 update su un dataset volutamente **eterogeneo** (campi opzionali, telefoni
talvolta stringa e talvolta lista) — il terreno tipico del document model. Il
caso di business: **DigitalConnect** vuole una rubrica flessibile per contatti
con informazioni disomogenee.

Su 11 documenti il valore non è la scala: è il **giudizio di modellazione**,
con i compromessi dichiarati apertamente nel README — incluso quando una
tecnica di scala *non* serve.

**Cosa contiene**
- 🔎 Le 6 query + 2 update della consegna come **package Python tipizzato**
  (`contacts/`: connessione, query, runner — entrypoint `python -m contacts`):
  aggregation pipeline con `$expr`/`$cond`/`$isArray`, `$unwind`, `$group`/`$avg`.
- 🧩 Gestione del campo telefono string|array **in un punto solo**: la stessa
  normalizzazione `$isArray`/`$cond` serve query e append (`$concatArrays`);
  niente upsert sull'update di un contatto esistente, così un refuso nel nome
  non crea documenti fantasma.
- 🧭 **Scelte di modellazione** esplicite: chiave naturale dichiarata
  imperfetta, indice univoco come **vincolo di integrità** (non
  ottimizzazione), embedding vs referencing, valori mancanti non mascherati
  da default.

**Qualità & ingegneria**
- 🐳 **Ambiente Docker monocomando**: `docker compose up` → MongoDB 7
  standalone + seed automatico (healthcheck anti-race, indice univoco creato
  *prima* dell'import come gate di integrità sul dataset).
- ✅ **13 test pytest** con oracoli calcolati dal dataset e regressioni mirate
  (append che resta piatto, `$exists` su path annidato, `DuplicateKeyError`
  sul duplicato), su un DB di test isolato e riseminato a ogni test.
- 🧹 Lint/format con **ruff** e **CI GitHub Actions** con MongoDB come service
  container; dipendenze **pinnate** (stesse versioni in locale e in CI).

**Stack:** Python · MongoDB · pymongo · Docker · pytest · ruff · GitHub Actions

---

### ✅ Corso 5 · Web Scraping — Scraping di un catalogo di libri online

> [`profession_ai_data_engineering_progetto5`](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto5)

Estrazione di dati strutturati — titolo, valutazione, prezzo, disponibilità —
dal catalogo di una **libreria online** ([books.toscrape.com](https://books.toscrape.com)),
salvati in CSV per l'analisi di mercato. Il caso di business: **BookSmart
Solutions** vuole monitorare l'offerta della concorrenza (prezzi, rating,
disponibilità) per orientare pricing e assortimento.

Più che lo script richiesto, il progetto cura il **giudizio tecnico** e la
robustezza: riconosciuto che il sito è **statico**, abbandona Selenium per
**requests** (più semplice e veloce, senza browser) e struttura il codice come
**pipeline modulare** anziché script monolitico.

**Cosa contiene**
- 🧱 **Package `bookscraper/`** in moduli a responsabilità singola: navigazione e
  paginazione (`scraper`), parsing HTML (`parsing`), strutturazione/salvataggio
  CSV (`storage`), orchestrazione (`pipeline`) — eseguibile con `python -m bookscraper`.
- 🧭 **Estrazione resiliente per-campo**: l'assenza di un campo non azzera il
  record (resta `None`); solo i `product_pod` privi di titolo vengono scartati.
- 🛡️ **Robustezza di rete** come da consegna: **retry** con backoff esponenziale
  (`tenacity`), **rate limiting** (`ratelimit`) ed encoding UTF-8 forzato.

**Qualità & ingegneria**
- ✅ **28 test pytest** (coverage **90%**) senza rete: parsing su HTML fixture,
  `requests` mockato per scraper e pipeline, CSV su file temporanei.
- 📋 **Logging** console-first leggibile, con output JSON rotante opt-in
  (`LOG_TO_FILE=1`, compatibile ELK/Kibana).
- 🧹 **Type hints**, lint/format con **ruff** e **CI GitHub Actions** (ruff +
  pytest) a ogni push/PR, con **branch protection** su `main`.

**Stack:** Python · requests · BeautifulSoup · pandas · tenacity · pytest · ruff · GitHub Actions

---

## In lavorazione

Progetti in fase di sistemazione/refactoring. Il tema e lo stack riportati
seguono il programma ufficiale del master; verranno censiti qui in dettaglio
man mano che vengono completati.

| Corso | Progetto · Repository | Tema | Stack | Stato |
|:-----:|-----------------------|------|-------|:-----:|
| 6  | Preprocessing & Feature Eng. `…progetto6` | Pre-processing di un dataset di rilevazione del tumore al seno | scikit-learn · PCA · SMOTE | 🚧 |
| 7  | Fondamenti ML `…progetto7` | Previsione della progressione del diabete in pazienti a rischio | scikit-learn · regressione · classificazione · clustering | 🚧 |
| 8  | Big Data su Wikipedia `…progetto8_databricks` · `…_zeppelin` | Processing e analisi dell'intero dump di Wikipedia | Apache Spark · Spark SQL · Databricks · Zeppelin · AWS EMR | 🚧 |
| 9  | CryptoData Insights `…progetto9` | Pipeline E2E in cloud per analizzare Bitcoin e Monero | AWS S3 · Glue · Kinesis · Redshift · Step Functions | 🚧 |
| 10 | Dataset film `…progetto10` | Orchestrazione di una pipeline di trasformazione su un dataset di film | Azure Data Factory · Blob Storage · Stream Analytics | 🚧 |
| 11 | Dati pazienti `…progetto11` | Data management & security dei dati clinici di un ospedale (RBAC, GDPR) | Snowflake · Data Warehouse | 🚧 |

> I nomi repository sono abbreviati con il prefisso comune `profession_ai_data_engineering_`.

---

<sub>Indice mantenuto manualmente. Ultimo aggiornamento: progetti 1, 2, 3, 4 e 5 censiti in dettaglio; restanti progetti mappati al programma ufficiale e in fase di sistemazione.</sub>
