# Master in Data Engineering — Portfolio

This organisation collects the projects built during the **Master in Data Engineering** at
[ProfessionAI](https://www.profession.ai/corsi/master-data-engineering/): **11 professional
courses** and **11 hands-on projects** (~400 hours) spanning the whole craft — from software
engineering to data analysis, from SQL/NoSQL databases to Big Data, up to end-to-end cloud
pipelines. Course completed and [**certified**](https://certify.profession.ai/69f88359c63b283adf882aca).

Built by [**Federico Vita**](https://github.com/fedevita) — Data Engineer, 7+ years on
enterprise data systems. [LinkedIn](https://www.linkedin.com/in/federicovita/) ·
[federico.vita1997@gmail.com](mailto:federico.vita1997@gmail.com)

Each project starts from a real business case taken from its course. The repositories were
then **cleaned up and documented** to a uniform quality standard — curated README, code and
documentation, with tests and CI wherever the nature of the project allows it: **all 11
projects are ready** ✅.

**Stack across the programme:** Python · NumPy/Pandas · SQL (MySQL/MariaDB) · NoSQL
(MongoDB, Cassandra, DynamoDB, Neo4j) · BeautifulSoup/Selenium · scikit-learn · Apache Spark
(Databricks, Zeppelin, EMR) · AWS (S3, Glue, Kinesis, Redshift, Step Functions) · Azure Data
Factory · Snowflake.

🇮🇹 [Versione italiana](README.it.md)

---

## Projects

### ✅ Course 1 · Programming with Python — Household Expense Manager

> [`profession_ai_data_engineering_progetto1`](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto1)

A **command-line Python application** for tracking personal expenses, producing a monthly
report and surfacing the largest spends, with CSV persistence.

Born as a portfolio exercise, it goes beyond the functional requirements: it is structured
along **Clean Architecture** and **Domain-Driven Design** principles, with test coverage,
static type checking and CI.

**Features**
- Add an expense (date, description, amount), stored in CSV.
- Monthly report aggregated by year/month.
- Top 10 expenses by amount.
- **Swappable** reporting engine at runtime: in-memory (Python, default) or SQL (DuckDB,
  `analytics` extra).

**Quality & engineering**
- 🏛️ Four concentric layers (domain · application · infrastructure · interfaces) with *Dependency Inversion*.
- 🧩 **Command** pattern for CLI operations; *composition root* for dependency wiring.
- ✅ Tests with **pytest** (~96% coverage), **strict** type checking with **mypy**, lint/format with **ruff**.
- ⚙️ **GitHub Actions CI** across versions (Python 3.10 / 3.11 / 3.12) plus a coverage report.
- 📚 API documentation generated with **Sphinx** and published online.

**Stack:** Python · Clean Architecture · DDD · SOLID · pytest · mypy · ruff · GitHub Actions · Sphinx · DuckDB

📖 [Online documentation](https://profession-ai-data-engineering-master.github.io/profession_ai_data_engineering_progetto1/)

---

### ✅ Course 2 · Python Data Toolkit: NumPy, Pandas, Pyplot — S&P 500 and EURO STOXX 50 index analysis

> [`profession_ai_data_engineering_progetto2`](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto2)

A **ten-year** exploratory analysis of two global stock indices — **S&P 500** (US) and
**EURO STOXX 50** (Europe) — to derive insights useful to investment decisions: percentage
returns, volatility and trading volumes.

Rather than a plain calculation script, the project rests on a **recognised methodological
framework**: the flow follows the five **OSEMN** phases (Obtain · Scrub · Explore · Model ·
iNterpret), chosen over CRISP-DM with the reasoning stated, so the process is structured and
repeatable.

**Analyses performed**
- **Q1 — Percentage returns** daily/monthly/yearly, with **cumulative performance** compared
  across the two indices.
- **Q2 — Average return by day of the week**, read against documented phenomena (*reverse
  weekend effect*, US/Europe sector composition).
- **Q3 — Extreme-return days** treated as **outlier detection** with the **IQR method**
  (preferred to Z-score because it assumes no normality), traced back to real market events.
- **Q4 — Average daily trading volume** compared across the two indices.

**Quality & method**
- 🧭 Process driven by the **OSEMN** framework, with design choices made explicit.
- 📒 A formal **Data Dictionary** (types, business rules, volume semantics) as a data-quality control.
- 🧹 Scrubbing targeted at market data: time zones unified to UTC, alignment on the **common trading calendar**, removal of null volumes.
- 📈 **Matplotlib** visualisations and investor-oriented interpretation (*core-satellite* diversification, timing, liquidity/slippage).

**Stack:** Python · Pandas · Matplotlib · OSEMN · Jupyter Notebook

---

### ✅ Course 3 · SQL — Bank customer analysis

> [`profession_ai_data_engineering_progetto3`](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto3)

Construction of a **denormalised table of behavioural features** (one row per customer) to
feed supervised *machine learning* models, starting from a **MySQL 8** banking database. The
business case: **Banking Intelligence** wants to predict customer churn, risk and fraud from
transactional data and product holdings.

At its core is the **`DATI_DENORMALIZZATI_BANCA`** view — **27 columns** (`id_cliente` plus
26 features) obtained with `LEFT JOIN` across `customer → account → transactions` and
conditional aggregations (`CASE`) on transaction sign and account type: count and amount of
inflows/outflows, in total and for each of the four account types.

Beyond the query itself, the project invests in **reproducibility, quality and readability**
all the way to a showcase standard: anyone can bring the environment up and query the data
with one command.

**What it contains**
- 🧱 **Feature engineering view**: one row per customer, 26 behavioural indicators documented one by one.
- 🧭 **Guided tour** inside Adminer: `tour_*` views translating the features into five business questions (churn, risk, value, segmentation, anomalies/fraud).
- ⚡ **Schema optimisation** demonstrated and measured: from **~1.55 s to ~120 ms** with keys and a *covering* index, with the original schema restored afterwards.

**Quality & engineering**
- 🐳 **One-command Docker environment** (`run.sh`/`run.ps1`): MySQL + Adminer, dump downloaded at build time, healthcheck, view and tour loaded automatically.
- 🔎 **Adminer** (web UI) with a dedicated **read-only** user: the database can be explored without administrative credentials.
- ✅ **Validation assertions** in SQL (`SIGNAL`): one row per customer, consistency between totals and per-type sums, age ranges, absence of unexpected `NULL`s.
- 🧹 **SQL linting** with **SQLFluff** (MySQL dialect) and **GitHub Actions CI** that on every push/PR starts the database, creates view and tour, and runs assertions and lint.
- 📚 **Documentation**: data dictionary of the 26 features plus an **ER** diagram (Mermaid).

**Stack:** SQL · MySQL 8 · Docker · Adminer · SQLFluff · GitHub Actions

---

### ✅ Course 4 · NoSQL Databases — Document-oriented contact book on MongoDB

> [`profession_ai_data_engineering_progetto4`](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto4)

Managing and querying a **contact book** on **MongoDB**: 6 queries and 2 updates over a
deliberately **heterogeneous** dataset (optional fields, phone numbers sometimes a string and
sometimes a list) — the natural terrain of the document model. The business case:
**DigitalConnect** wants a flexible contact book for contacts with inconsistent information.

Across 11 documents the value is not scale: it is **modelling judgement**, with the
trade-offs stated openly in the README — including when a scaling technique is *not* needed.

**What it contains**
- 🔎 The 6 queries and 2 updates as a **typed Python package** (`contacts/`: connection,
  queries, runner — entrypoint `python -m contacts`): aggregation pipelines with
  `$expr`/`$cond`/`$isArray`, `$unwind`, `$group`/`$avg`.
- 🧩 The string-or-array phone field handled **in exactly one place**: the same
  `$isArray`/`$cond` normalisation serves both queries and appends (`$concatArrays`); no
  upsert when updating an existing contact, so a typo in a name cannot create phantom documents.
- 🧭 Explicit **modelling choices**: the natural key declared imperfect, a unique index as an
  **integrity constraint** (not an optimisation), embedding vs referencing, missing values not
  masked by defaults.

**Quality & engineering**
- 🐳 **One-command Docker environment**: `docker compose up` → standalone MongoDB 7 plus
  automatic seeding (race-proof healthcheck, unique index created *before* the import as an
  integrity gate on the dataset).
- ✅ **13 pytest tests** with oracles computed from the dataset and targeted regressions
  (appends staying flat, `$exists` on a nested path, `DuplicateKeyError` on a duplicate),
  against an isolated test database reseeded for every test.
- 🧹 Lint/format with **ruff** and **GitHub Actions CI** with MongoDB as a service container;
  dependencies **pinned** (same versions locally and in CI).

**Stack:** Python · MongoDB · pymongo · Docker · pytest · ruff · GitHub Actions

---

### ✅ Course 5 · Web Scraping — Scraping an online book catalogue

> [`profession_ai_data_engineering_progetto5`](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto5)

Extraction of structured data — title, rating, price, availability — from an **online
bookshop** catalogue ([books.toscrape.com](https://books.toscrape.com)), saved to CSV for
market analysis. The business case: **BookSmart Solutions** wants to monitor competitor
offerings (prices, ratings, availability) to steer pricing and assortment.

Beyond the required script, the project invests in **technical judgement** and robustness:
having established that the site is **static**, it drops Selenium for **requests** (simpler
and faster, no browser) and structures the code as a **modular pipeline** rather than a
monolithic script.

**What it contains**
- 🧱 **`bookscraper/` package** in single-responsibility modules: navigation and pagination
  (`scraper`), HTML parsing (`parsing`), structuring and CSV storage (`storage`),
  orchestration (`pipeline`) — runnable with `python -m bookscraper`.
- 🧭 **Resilient per-field extraction**: a missing field does not void the record (it stays
  `None`); only `product_pod` entries without a title are discarded.
- 🛡️ **Network robustness** as required: **retry** with exponential backoff (`tenacity`),
  **rate limiting** (`ratelimit`) and forced UTF-8 encoding.

**Quality & engineering**
- ✅ **28 pytest tests** (**90%** coverage) with no network access: parsing against HTML
  fixtures, `requests` mocked for scraper and pipeline, CSV written to temporary files.
- 📋 Readable console-first **logging**, with opt-in rotating JSON output (`LOG_TO_FILE=1`,
  ELK/Kibana compatible).
- 🧹 **Type hints**, lint/format with **ruff** and **GitHub Actions CI** (ruff + pytest) on
  every push/PR, with **branch protection** on `main`.

**Stack:** Python · requests · BeautifulSoup · pandas · tenacity · pytest · ruff · GitHub Actions

---

### ✅ Course 6 · Preprocessing & Feature Engineering — Preprocessing pipeline on clinical data

> [`profession_ai_data_engineering_progetto6`](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto6)

Construction of a **single reusable preprocessing object** that turns a raw clinical dataset
— **Breast Cancer Wisconsin** (569 records, numerical and categorical features, widespread
missing values) — into a *feature-ready* dataset for machine learning. The business case:
quality healthcare data for robust diagnostic models.

Beyond simply completing the exercise, the project brings the two **custom scikit-learn
transformers** up to the standard of a tested, typed **library**, fixing the fragilities of
the original implementation instead of merely packaging it.

**What it contains**
- 🧱 **`preprocessing/` package**: two custom transformers (`PipelineWithRowFilter`,
  `SelectiveTransformerBySkewness`) plus factories assembling the **three pipelines** of the
  assignment into the *max-feature* dataset (`FeatureUnion`) — runnable with
  `python -m preprocessing`.
- 🧭 **Three complementary pipelines**: selective imputation by symmetry, Yeo-Johnson
  symmetrisation, one-hot/ordinal encoding, discretisation, **PCA**, selection of the most
  informative features (ANOVA F), standardisation/normalisation.
- 🩺 **Extensions to the sklearn API** where the primitives fall short: training a pipeline on
  a subset of records only, applying a transformer only to skewed columns.

**Quality & engineering**
- 🧠 **Explicit modelling choices**: Pipeline 1 *learns* its parameters from positive records
  only (no leakage) but transforms every row → a dataset with no structural NaNs and the
  invariant `fit_transform == fit().transform()`.
- 🛡️ **Robustness to degenerate cases**: constant or near-empty columns always imputed (PCA
  does not blow up), unseen categories handled at inference, feature names unique end to end.
- ✅ **24 pytest tests** (oracles plus **property-based** testing with Hypothesis on the
  transformers), **97%** coverage.
- 🧹 Complete **type hints**, lint/format with **ruff**, type checking with **mypy**,
  **GitHub Actions CI** (ruff + mypy + pytest) on every push/PR.

**Stack:** Python · scikit-learn · pandas · Hypothesis · pytest · mypy · ruff · GitHub Actions

---

### ✅ Course 7 · Machine Learning Fundamentals — Predicting diabetes progression

> [`profession_ai_data_engineering_progetto7`](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto7)

A **regression** model estimating one-year diabetes progression from a patient's clinical
data — scikit-learn's **Diabetes** dataset (442 patients), loaded raw so that preprocessing
is done from scratch. The business case: **MedPredict** wants a decision-support tool for
personalising treatment plans.

Rather than a monolithic notebook, the project **separates narrative from logic**: the
notebook remains the story guided by **OSEMN**, while all the logic lives in a package that
is tested, type-checked and **99%** covered — showcase readability and engineering robustness
at once.

**What it contains**
- 🧱 **`diabetes/` package**: data loading, feature engineering transformers, pipeline and
  model factories, cross-validated evaluation, plotting utilities — the notebook imports and
  orchestrates.
- 🧭 **Preprocessing entirely inside scikit-learn pipelines**: imputation, one-hot encoding,
  **six clinically grounded derived features** (age×BMI interaction, HDL ratio, and so on),
  Yeo-Johnson transformation and RobustScaler — fitting happens inside each CV fold, so
  **no data leakage**.
- 📊 **Baseline vs advanced**: `SelectKBest` + `LinearRegression` compared with
  **`ElasticNetCV`** (internal tuning via nested CV); the chosen model improves
  **R² 0.444 → 0.476** (−5.6% MSE), honest results for an intrinsically noisy dataset.

**Quality & engineering**
- 🧠 **Robust feature engineering**: the ColumnTransformers keep the base column names
  (`verbose_feature_names_out=False`) → derived features do not depend on pipeline step names.
- 🛡️ **Correctness**: de-duplication moved outside the pipeline (no rows dropped inside a
  transformer, which would misalign X and y), corrected metric standard deviations, final
  interpretation derived from the actual results.
- ✅ **21 pytest tests** (**99%** coverage): end-to-end fit/predict, no-leakage check,
  per-seed reproducibility, plots rendered on a headless backend.
- 🧹 **Type hints**, lint/format with **ruff**, type checking with **mypy**, **GitHub Actions
  CI** (ruff + mypy + pytest with a coverage threshold) on every push/PR.

**Stack:** Python · scikit-learn · pandas · Matplotlib · seaborn · pytest · mypy · ruff · GitHub Actions

---

### ✅ Course 8 · Big Data with Apache Spark — Analysing and classifying Wikipedia articles

> [`profession_ai_data_engineering_progetto8`](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto8)

Exploratory analysis and **automatic classification** of ~153,000 Wikipedia articles into 15
thematic categories, with **Apache Spark**. The business case: **Wikidata Insights** wants to
understand how content is distributed and to have a classifier that categorises new articles
from their text.

Beyond simply completing the assignment, the project **rescues an exercise born cloud-bound**:
the original ran on **Zeppelin/Databricks**, constrained by free-tier limits (capped
downloads, `spark.ml` unavailable). Here it is **ported to local Spark** — explicit
`SparkSession`, no Zeppelin magics, zero paid cloud dependencies — so **anyone can reproduce
it for free**, while being engineered to the same library standard as the earlier projects.

**What it contains**
- 🧱 **`wikianalysis/` package** (`data` · `eda` · `model` · `plots`) holding the testable
  logic; the **notebook** remains the **OSEMN** narrative that imports and orchestrates.
- 🧭 **EDA on Spark**: counts and lengths per category, **word cloud** of the most frequent
  tokens. It emerges that after cleaning the dataset **halves** (153,232 → 75,523 rows: half
  are duplicates) and is **heavily imbalanced** (`medicine` ~8,300 articles vs `politics` ~240).
- 🤖 **Spark ML classifier**: `StringIndexer → Tokenizer → StopWordsRemover → CountVectorizer
  → StandardScaler → LogisticRegression` pipeline, **accuracy ~0.845** as an interpretable
  baseline, with a confusion matrix and the most influential tokens per category.

**Quality & engineering**
- ☁️➡️💻 **Zeppelin/Databricks → local Spark port**: reproducible `SparkSession`, idempotent
  data download and a **versioned sample** for tests/CI, so the whole project runs without a
  paid cluster.
- 🐛 **Pipeline bug fixed**: the `StopWordsRemover` now actually feeds the `CountVectorizer`
  (the `filtered` column), a step previously ignored — a semantically correct pipeline, with a
  regression test covering it.
- ✅ **30 pytest tests** against a **local** `SparkSession` run on the versioned sample
  (**87%** coverage), including the bug regression and seed reproducibility.
- 🧹 **Type hints**, lint/format with **ruff**, type checking with **mypy** and **GitHub
  Actions CI with Java + Spark** (ruff + mypy + pytest) on every push/PR.

**Stack:** Python · Apache Spark / PySpark · Spark ML · pandas · Matplotlib · seaborn · pytest · mypy · ruff · GitHub Actions

---

### ✅ Course 9 · Cloud Data Engineering with AWS — End-to-end cryptocurrency analysis pipeline

> [`profession_ai_data_engineering_progetto9`](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto9)

An **end-to-end AWS** data engineering pipeline that ingests, cleans and enriches market data
for **Bitcoin (BTC)** and **Monero (XMR)**, correlating the daily price with weekly
**Google Trends** search interest and making the results queryable on a data warehouse and
dashboards. The business case: **CryptoData Insights** wants to turn raw market data into
actionable insight in a volatile context.

Unlike the other projects — tested code libraries running locally — this is an
**infrastructure** project, built entirely on AWS managed services. The deliverable is
therefore a **technical report** documenting the architecture, the implementation choices and
the real console runs, with the code produced (PySpark, Amazon States Language, SQL) included
in full.

> 📄 **[Full project report (PDF)](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto9/blob/main/Report_Progetto9.pdf)**

**What it contains**
- 🗄️ **Layered (Medallion) storage** on Amazon S3 — Bronze (raw CSV) → Silver (cleaned
  Parquet) → Gold (analytical dataset) — as the central *source of truth*.
- ⚙️ **Parametric Glue ETL job (PySpark)** (`--coin BTC|XMR`): a single codebase for both
  currencies, with price cleaning (date parsing, *forward-fill* of `-1` sentinels), a
  **10-day moving average** and a **robust temporal join** price↔trend on the containing week
  (`date_trunc`), with missing trends kept as `NULL`.
- 🔀 **Orchestration with Step Functions**: a *Parallel* state running the BTC and XMR
  pipelines simultaneously, with error handling (`Catch` → `Fail`).
- 📊 **Serverless warehouse & BI**: loading into **Redshift Serverless** (`COPY` from S3) and
  **QuickSight** dashboards fed through **Athena** over the Gold layer.

**Architecture & cloud engineering**
- 🔐 **Least-privilege IAM**: a dedicated policy/role per service (Glue, Step Functions,
  Redshift), with permissions scoped strictly to the project buckets.
- 🧩 **Parametric design**: one reusable Glue job instead of duplicated scripts, with currency
  parameters injected by the orchestrator.
- 🏛️ **Lakehouse pattern**: separation between the compute layer (Redshift) and the
  presentation layer (QuickSight → Athena → S3), with no physical duplication of the data.
- 🧱 **ETL script versioning** on S3 (`v1`/`v2`/`latest`) to decouple the code lifecycle from
  the job definition.
- 📝 **Reproducible report** in **Typst** (compilable from source) with an architecture
  diagram and screenshots of successful runs.

**Stack:** AWS S3 · AWS Glue (PySpark) · AWS Step Functions · Amazon Redshift Serverless · Amazon Athena · Amazon QuickSight · IAM · Typst

---

### ✅ Course 10 · Data Engineering on Azure — ETL pipeline for a film dataset

> [`profession_ai_data_engineering_progetto10`](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto10)

A data orchestration pipeline on **Azure Data Factory** that ingests a film catalogue from
**Azure Blob Storage**, cleans and transforms it with a **Mapping Data Flow** and writes a
filtered, standardised dataset to an output container. The business case: **CineData
Solutions** wants to automate the preparation of heterogeneous film data for distribution
platforms.

Like project 9, this is an **infrastructure** project built on Azure managed services: the
deliverable is a **technical report** documenting resource creation in the portal, the Data
Flow logic and the real runs — all of it **without application code**, the transformation
being entirely declarative.

> 📄 **[Full project report (PDF)](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto10/blob/main/Report_Progetto10.pdf)**

**What it contains**
- 🗂️ **Ingestion from Blob Storage**: separate `input`/`output` containers for raw and
  processed data, with Linked Service and DelimitedText Dataset configured in ADF.
- 🔧 **Mapping Data Flow** (`Source → Derived Column → Filter → Derived Column → Select →
  Sink`): **safe** conversion of the textual rating into a number (`regexMatch` validation,
  dirty values → `null`), a **quality filter** (`Valutazione > 7`), **title normalisation**
  into catalogue format (`Kid, The` → `The Kid`) and schema renaming into Italian.
- 🎬 **Clean output**: a single `movies_filtered.csv` file with columns `Id`, `Film`,
  `Genere`, `Valutazione`, written in *single partition*.

**Architecture & cloud engineering**
- 🧭 **Declarative transformation**: all the logic lives in the `df_movies_transform` Data
  Flow, orchestrated by the `pl_movies_transform` pipeline — no scripts to maintain.
- 🛡️ **Robustness on real data**: handling of anomalous CSV headers, titles containing commas
  and quotes, and non-numeric ratings, with defensive conversion before the filter.
- 📝 **Reproducible report** in **Typst** (compilable from source) with a flow diagram, JSON
  snippets of pipeline and data flow, and screenshots of *Succeeded* runs.

**Stack:** Azure Data Factory · Mapping Data Flow · Azure Blob Storage · Linked Services / Datasets · Typst

---

### ✅ Course 11 · Data Warehousing with Snowflake — Clinical data warehouse with RBAC and GDPR

> [`profession_ai_data_engineering_progetto11`](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto11)

A data warehouse for a hospital's clinical data on **Snowflake**: ingestion from an S3 data
lake, a layered **RAW → CURATED → ANALYTICS** model, a **star schema** for BI, an
**idempotent ELT** pipeline orchestrated by a task chain, and a **security-by-design** setup
(RBAC + dynamic data masking) for **GDPR** compliance. The business case: **HealthDataPro**
must centralise fragmented clinical data securely, at scale and in compliance.

The assignment asked only for the data schema; the project goes further, delivering an
**end-to-end and verifiable** data warehouse. It is an **infrastructure** project: the
deliverable is a **technical report** with architecture, full DDL and real runs on Snowflake.

> 📄 **[Full project report (PDF)](https://github.com/profession-ai-data-engineering-master/profession_ai_data_engineering_progetto11/blob/main/Report_Progetto11.pdf)**

**What it contains**
- 🗄️ **Layered warehouse** (`RAW` mirror → `CURATED` standardisation → `ANALYTICS`
  consumption) plus a technical `PIPELINE` schema, with three virtual warehouses sized per
  workload.
- ⭐ **Star schema** (`DIM_PAZIENTE/REPARTO/DISPOSITIVO`, `FACT_RICOVERI/MISURAZIONI`,
  diagnosis bridge).
- 🔄 **Idempotent ELT**: a task chain invoking three stored procedures — fail-fast `COPY INTO`,
  `MERGE` on business keys with deterministic de-duplication, and **quarantine** of orphan
  records.
- ☁️ **S3 → Snowflake ingestion** via **Storage Integration** (cross-account IAM role, *least
  privilege*, no static credentials).

**Architecture & cloud engineering**
- 🔐 **Security by design**: native RBAC with three roles and a hierarchy
  (engineer/analyst/compliance), writes reserved to technical roles, analyst access confined
  to the consumption layer.
- 🕶️ **GDPR dynamic data masking**: the residual PII in `DIM_PAZIENTE` (city, date of birth)
  is masked at runtime according to role; direct identifiers excluded by design.
- 🧪 **Synthetic data** (SDV library) for developing and testing with no privacy risk.
- 📝 **Reproducible report** in **Typst** with diagram, DDL and screenshots of the runs.

**Stack:** Snowflake · SQL · Snowflake Tasks & Stored Procedures · Storage Integration · AWS S3 / IAM · Dynamic Data Masking · RBAC · Typst
