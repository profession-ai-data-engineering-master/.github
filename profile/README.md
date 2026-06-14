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

### ✅ Corso 6 · Preprocessing & Feature Engineering — Pipeline di pre-processing su dati clinici

> [`profession_ai_data_engineering_progetto6`](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto6)

Costruzione di un **unico oggetto di preprocessing riutilizzabile** che trasforma un
dataset clinico grezzo — **Breast Cancer Wisconsin** (569 record, feature numeriche e
categoriche, valori mancanti diffusi) — in un dataset *feature-ready* per il machine
learning. Il caso di business: dati sanitari di qualità per modelli diagnostici robusti.

Più che il semplice svolgimento dell'esercizio, il progetto porta i due **transformer
scikit-learn custom** allo standard di una **libreria** testata e tipizzata, correggendo le
fragilità dell'implementazione originale invece di limitarsi a impacchettarla.

**Cosa contiene**
- 🧱 **Package `preprocessing/`**: due transformer custom (`PipelineWithRowFilter`,
  `SelectiveTransformerBySkewness`) + factory che assemblano le **3 pipeline** della consegna
  nel dataset *max-feature* (`FeatureUnion`) — eseguibile con `python -m preprocessing`.
- 🧭 **Tre pipeline complementari**: imputazione selettiva per simmetria, simmetrizzazione
  Yeo-Johnson, one-hot/ordinal encoding, discretizzazione, **PCA**, selezione delle feature più
  informative (ANOVA F), standardizzazione/normalizzazione.
- 🩺 **Estensioni dell'API sklearn** dove le primitive non bastano: addestrare una pipeline solo
  su un sottoinsieme di record, applicare un transformer solo alle colonne asimmetriche.

**Qualità & ingegneria**
- 🧠 **Scelte di modellazione esplicite**: la Pipeline 1 *apprende* i parametri solo dai record
  positivi (no leakage) ma trasforma tutte le righe → dataset senza NaN strutturali e invariante
  `fit_transform == fit().transform()`.
- 🛡️ **Robustezza ai casi degeneri**: colonne costanti o quasi-vuote sempre imputate (la PCA non
  esplode), categorie mai viste gestite in inferenza, nomi feature unici end-to-end.
- ✅ **24 test pytest** (oracoli + **property-based** con Hypothesis sui transformer), coverage **97%**.
- 🧹 **Type hints** completi, lint/format con **ruff**, type checking con **mypy**, **CI GitHub
  Actions** (ruff + mypy + pytest) a ogni push/PR.

**Stack:** Python · scikit-learn · pandas · Hypothesis · pytest · mypy · ruff · GitHub Actions

---

### ✅ Corso 7 · Fondamenti di Machine Learning — Previsione della progressione del diabete

> [`profession_ai_data_engineering_progetto7`](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto7)

Modello di **regressione** che stima la progressione del diabete a un anno dai
dati clinici di un paziente — dataset **Diabetes** di scikit-learn (442 pazienti),
caricato grezzo per svolgere da zero il preprocessing. Il caso di business:
**MedPredict** vuole uno strumento di supporto decisionale per personalizzare i
piani terapeutici.

Più che un notebook monolitico, il progetto **separa la narrazione dalla logica**:
il notebook resta il racconto guidato da **OSEMN**, mentre tutta la logica vive in
un package testato, type-checkato e coperto al **99%** — leggibilità della showcase
e robustezza ingegneristica insieme.

**Cosa contiene**
- 🧱 **Package `diabetes/`**: caricamento dati, transformer di feature engineering, factory delle pipeline e dei modelli, valutazione in cross-validation, utility di plotting — il notebook importa e orchestra.
- 🧭 **Preprocessing tutto in pipeline scikit-learn**: imputazione, encoding one-hot, **6 feature derivate a base clinica** (interazione età×BMI, rapporto HDL, ecc.), trasformazione Yeo-Johnson e RobustScaler — il fit avviene dentro ogni fold della CV, **nessun data leakage**.
- 📊 **Base vs avanzato**: `SelectKBest` + `LinearRegression` confrontato con **`ElasticNetCV`** (tuning interno via CV annidata); il modello scelto migliora **R² 0.444 → 0.476** (−5.6% MSE), risultati onesti per un dataset intrinsecamente rumoroso.

**Qualità & ingegneria**
- 🧠 **Feature engineering robusta**: i ColumnTransformer mantengono i nomi base delle colonne (`verbose_feature_names_out=False`) → le feature derivate non dipendono dai nomi degli step della pipeline.
- 🛡️ **Correttezza**: de-duplicazione spostata fuori dalla pipeline (niente righe rimosse dentro un transformer, che disallineerebbe X e y), deviazioni standard delle metriche corrette, interpretazione finale derivata dai risultati reali.
- ✅ **21 test pytest** (coverage **99%**): fit/predict end-to-end, controllo no-leakage, riproducibilità per seed, grafici in backend headless.
- 🧹 **Type hints**, lint/format con **ruff**, type checking con **mypy**, **CI GitHub Actions** (ruff + mypy + pytest con soglia di coverage) a ogni push/PR.

**Stack:** Python · scikit-learn · pandas · Matplotlib · seaborn · pytest · mypy · ruff · GitHub Actions

---

### ✅ Corso 8 · Big Data con Apache Spark — Analisi e classificazione di articoli di Wikipedia

> [`profession_ai_data_engineering_progetto8`](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto8)

Analisi esplorativa e **classificazione automatica** di ~153.000 articoli di
Wikipedia in 15 categorie tematiche, con **Apache Spark**. Il caso di business:
**Wikidata Insights** vuole capire la distribuzione dei contenuti e disporre di
un classificatore che categorizzi i nuovi articoli a partire dal testo.

Più che il semplice svolgimento, il progetto **riscatta un esercizio nato
cloud-bound**: l'originale girava su **Zeppelin/Databricks**, vincolato dai
limiti del piano gratuito (download capato, `spark.ml` non disponibile). Qui è
**portato a Spark in locale** — `SparkSession` esplicita, nessun magic Zeppelin,
zero dipendenze cloud a pagamento — così **chiunque può riprodurlo gratis**, e
allo stesso tempo è ingegnerizzato allo standard libreria come i progetti
precedenti.

**Cosa contiene**
- 🧱 **Package `wikianalysis/`** (`data` · `eda` · `model` · `plots`) con la
  logica testabile; il **notebook** resta la narrazione **OSEMN** che importa e
  orchestra.
- 🧭 **EDA su Spark**: conteggi e lunghezze per categoria, **word cloud** dei
  token più frequenti. Emerge che dopo la pulizia il dataset **si dimezza**
  (153.232 → 75.523 righe: metà sono duplicati) ed è **fortemente sbilanciato**
  (`medicine` ~8.300 articoli vs `politics` ~240).
- 🤖 **Classificatore Spark ML**: pipeline `StringIndexer → Tokenizer →
  StopWordsRemover → CountVectorizer → StandardScaler → LogisticRegression`,
  **accuracy ~0.845** come baseline interpretabile, con confusion matrix e token
  più influenti per categoria.

**Qualità & ingegneria**
- ☁️➡️💻 **Port Zeppelin/Databricks → Spark locale**: `SparkSession`
  riproducibile, download dati idempotente e **campione versionato** per
  test/CI, così l'intero progetto gira senza cluster a pagamento.
- 🐛 **Bug di pipeline corretto**: lo `StopWordsRemover` ora alimenta davvero il
  `CountVectorizer` (colonna `filtered`), step prima ignorato — pipeline
  semanticamente corretta, con regressione a copertura.
- ✅ **30 test pytest** con una `SparkSession` **locale** eseguiti sul campione
  versionato (coverage **87%**), inclusa la regressione del bug e la
  riproducibilità del seed.
- 🧹 **Type hints**, lint/format con **ruff**, type checking con **mypy** e **CI
  GitHub Actions con Java + Spark** (ruff + mypy + pytest) a ogni push/PR.

**Stack:** Python · Apache Spark / PySpark · Spark ML · pandas · Matplotlib · seaborn · pytest · mypy · ruff · GitHub Actions

---

### ✅ Corso 9 · Cloud Data Engineering con AWS — Pipeline E2E per l'analisi di criptovalute

> [`profession_ai_data_engineering_progetto9`](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto9)

Pipeline di Data Engineering **End-to-End su AWS** che ingerisce, pulisce e
arricchisce i dati di mercato di **Bitcoin (BTC)** e **Monero (XMR)**, correlando
il prezzo giornaliero con l'interesse di ricerca settimanale di **Google Trends** e
rendendo i risultati interrogabili su data warehouse e dashboard. Il caso di
business: **CryptoData Insights** vuole trasformare dati grezzi di mercato in
insight azionabili in un contesto volatile.

A differenza degli altri progetti — librerie di codice testate in locale — questo
è un progetto **infrastrutturale**, costruito interamente sui servizi gestiti AWS.
Il deliverable è quindi un **report tecnico** che documenta l'architettura, le
scelte implementative e le esecuzioni reali sulla console, con il codice prodotto
(PySpark, Amazon States Language, SQL) integralmente riportato.

> 📄 **[Report completo del progetto (PDF)](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto9/blob/main/Report_Progetto9.pdf)**

**Cosa contiene**
- 🗄️ **Storage a livelli (Medallion)** su Amazon S3 — Bronze (CSV grezzi) → Silver
  (Parquet puliti) → Gold (dataset analitico) — come *source of truth* centrale.
- ⚙️ **Job ETL Glue (PySpark) parametrico** (`--coin BTC|XMR`): un'unica codebase per
  entrambe le valute, con pulizia prezzi (parsing date, *forward-fill* dei sentinel
  `-1`), **media mobile a 10 giorni** e **join temporale robusto** prezzo↔trend sulla
  settimana di appartenenza (`date_trunc`), con i trend mancanti mantenuti `NULL`.
- 🔀 **Orchestrazione con Step Functions**: stato *Parallel* che esegue le pipeline
  BTC e XMR simultaneamente, con gestione degli errori (`Catch` → `Fail`).
- 📊 **Warehouse & BI serverless**: caricamento su **Redshift Serverless** (`COPY` da
  S3) e dashboard **QuickSight** alimentate via **Athena** sul Gold layer.

**Architettura & ingegneria cloud**
- 🔐 **IAM a privilegio minimo**: una policy/ruolo dedicato per servizio (Glue,
  Step Functions, Redshift), con permessi limitati esclusivamente ai bucket del progetto.
- 🧩 **Design parametrico**: un solo Glue Job riutilizzabile invece di script
  duplicati, con i parametri valuta iniettati dall'orchestratore.
- 🏛️ **Pattern Lakehouse**: separazione fra layer di calcolo (Redshift) e di
  visualizzazione (QuickSight → Athena → S3), senza duplicazione fisica del dato.
- 🧱 **Versioning degli script ETL** su S3 (`v1`/`v2`/`latest`) per disaccoppiare il
  ciclo di vita del codice dalla definizione del job.
- 📝 **Report riproducibile** in **Typst** (compilabile da sorgente) con diagramma
  architetturale e screenshot delle esecuzioni andate a buon fine.

**Stack:** AWS S3 · AWS Glue (PySpark) · AWS Step Functions · Amazon Redshift Serverless · Amazon Athena · Amazon QuickSight · IAM · Typst

---

### ✅ Corso 10 · Data Engineering su Azure — Pipeline ETL per un dataset di film

> [`profession_ai_data_engineering_progetto10`](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto10)

Pipeline di orchestrazione dati su **Azure Data Factory** che ingerisce un catalogo
di film da **Azure Blob Storage**, lo pulisce e trasforma con un **Mapping Data Flow** e
scrive un dataset filtrato e standardizzato su un container di output. Il caso di
business: **CineData Solutions** vuole automatizzare la preparazione di dati
cinematografici eterogenei per le piattaforme di distribuzione.

Come il progetto 9, è un progetto **infrastrutturale** costruito sui servizi gestiti
Azure: il deliverable è un **report tecnico** che documenta la creazione delle risorse
nel portale, la logica del Data Flow e le esecuzioni reali — il tutto **senza codice
applicativo**, con la trasformazione interamente dichiarativa.

> 📄 **[Report completo del progetto (PDF)](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto10/blob/main/Report_Progetto10.pdf)**

**Cosa contiene**
- 🗂️ **Ingestione da Blob Storage**: container `input`/`output` separati per dati grezzi
  ed elaborati, con Linked Service e Dataset DelimitedText configurati in ADF.
- 🔧 **Mapping Data Flow** (`Source → Derived Column → Filter → Derived Column → Select → Sink`):
  conversione **sicura** del rating testuale in numero (validazione `regexMatch`, valori
  sporchi → `null`), **filtro di qualità** (`Valutazione > 7`), **normalizzazione dei titoli**
  in formato catalogo (`Kid, The` → `The Kid`) e rinomina dello schema in italiano.
- 🎬 **Output pulito**: file singolo `movies_filtered.csv` con colonne `Id`, `Film`,
  `Genere`, `Valutazione`, scritto in *single partition*.

**Architettura & ingegneria cloud**
- 🧭 **Trasformazione dichiarativa**: tutta la logica vive nel Data Flow `df_movies_transform`,
  orchestrato dalla pipeline `pl_movies_transform` — nessuno script da mantenere.
- 🛡️ **Robustezza sui dati reali**: gestione di header anomali nel CSV, titoli con
  virgole/virgolette e rating non numerici, con conversione difensiva prima del filtro.
- 📝 **Report riproducibile** in **Typst** (compilabile da sorgente) con diagramma del
  flusso, snippet JSON di pipeline e data flow, e screenshot delle esecuzioni *Succeeded*.

**Stack:** Azure Data Factory · Mapping Data Flow · Azure Blob Storage · Linked Services / Datasets · Typst

---

## In lavorazione

Progetti in fase di sistemazione/refactoring. Il tema e lo stack riportati
seguono il programma ufficiale del master; verranno censiti qui in dettaglio
man mano che vengono completati.

| Corso | Progetto · Repository | Tema | Stack | Stato |
|:-----:|-----------------------|------|-------|:-----:|
| 11 | Dati pazienti `…progetto11` | Data management & security dei dati clinici di un ospedale (RBAC, GDPR) | Snowflake · Data Warehouse | 🚧 |

> I nomi repository sono abbreviati con il prefisso comune `profession_ai_data_engineering_`.

---

<sub>Indice mantenuto manualmente. Ultimo aggiornamento: progetti da 1 a 10 censiti in dettaglio; restanti progetti mappati al programma ufficiale e in fase di sistemazione.</sub>
