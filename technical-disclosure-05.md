**DEFENSIVE TECHNICAL DISCLOSURE**

**Systems and Methods for Semantic Schema Mapping in Heterogeneous Data Sources 
via Large Language Model Synthesis of Transformation Logic**

**Publication Date:** 2026-08-20
**Disclosure Number:** CB-2026-0005

---

### FIELD OF THE DISCLOSURE

This disclosure relates generally to data integration and schema 
reconciliation. More specifically, it relates to systems and methods for 
dynamically identifying semantic correspondences between columns, fields, or 
attributes of heterogeneous data sources—including relational database 
management systems, comma-separated value files, tab-separated value files, 
fixed-width text files, JSON documents, XML documents, Parquet files, Avro 
records, API response schemas, and any other structured or semi-structured data 
format—by means of natural-language semantic annotation and large language 
model synthesis of executable transformation logic.

### BACKGROUND

Data integration is a pervasive requirement across enterprise software, 
analytics pipelines, data migration projects, ETL/ELT workflows, and 
application interoperability. In practice, data originating from independently 
authored systems rarely shares a common schema. Two databases may represent the 
same conceptual attribute using different column names (`cust_name` versus 
`customer_full_name`), different data types (`VARCHAR(50)` versus `TEXT`), 
different granularities (a single `full_name` column in one system versus 
separate `first_name` and `last_name` columns in another), or different 
encoding conventions (ISO 8601 timestamps versus Unix epoch integers).

Conventional schema mapping approaches rely on one or more of the following: 
manual authoring of mapping specifications by data engineers; syntactic 
matching algorithms that compare column names using string similarity metrics 
(Levenshtein distance, Jaccard similarity, token overlap); schema ontology 
matching using predefined taxonomies; or rule-based inference over data type 
compatibility matrices. Each of these approaches exhibits well-known 
limitations. Manual mapping does not scale to large schemas or frequent schema 
changes. Syntactic matching fails when column names diverge (`ln` versus 
`last_name` versus `surname` versus `family_name`) and produces false positives 
when names collide (`name` may refer to a person, a product, or a file). 
Ontology-based matching requires pre-existing taxonomies that are expensive to 
maintain and often absent in practice. Rule-based type matching cannot resolve 
semantic ambiguity.

There remains a need for automated semantic schema mapping that identifies 
conceptual correspondences between data source attributes regardless of naming 
conventions, type system differences, or structural granularity mismatches, and 
that produces executable transformation logic without requiring human-authored 
integration code.

### SUMMARY

Disclosed are systems, methods, and computer-readable media that identify 
semantic correspondences between attributes of heterogeneous data sources and 
synthesize executable transformation logic by means of a large language model 
or equivalent generative model. Each data source is annotated with a semantic 
schema that describes its columns or fields in natural language, optionally 
supplemented by sample data, type metadata, and statistical profiles. A 
generative model identifies semantic overlaps between attributes across sources 
and emits transformation logic in a programming language, declarative format, 
domain-specific language, or any combination thereof. A validation engine 
verifies type compatibility, cardinality constraints, and transformation 
correctness before the mapping is applied.

Any of the described steps or components may be combined, omitted, reordered, 
or replaced by functional equivalents.

### DETAILED DESCRIPTION

#### General System

A computing system comprises one or more processors and one or more 
non-transitory computer-readable media storing instructions that, when 
executed, realize the following non-limiting components (which may be present 
in any subset or combination):

- a data ingestion interface capable of reading schema metadata and optionally 
sample data from one or more heterogeneous data sources;
- a semantic annotation layer that produces or receives natural-language 
semantic schemas for each data source;
- a semantic mapping layer that employs a large language model or other 
generative model to identify correspondences between attributes across sources 
and synthesize transformation logic;
- a validation engine that verifies synthesized logic;
- a transformation execution engine that applies validated logic to migrate, 
translate, or reconcile data between sources.

The system may operate at pipeline initialization, upon addition or removal of 
a data source, upon detection of a schema change in a source system, upon user 
request, upon detection of a data drift condition, or continuously during data 
ingestion.

#### Semantic Schemas for Data Sources

Each data source—whether a relational database table, a CSV file, a JSON 
document collection, an API response schema, a Parquet file, or any other 
structured or semi-structured data artifact—may be accompanied by a 
machine-readable semantic schema (for example JSON, YAML, XML, or any other 
structured format). The schema annotates each column, field, or attribute using:

- a natural-language description of the attribute's real-world meaning (for 
example "the customer's legal family name as recorded at account creation");
- optional type metadata (declared type, observed type, nullable status);
- optional range or domain constraints (minimum, maximum, allowed values, regex 
pattern);
- optional statistical profile (sampled value distribution, cardinality 
estimate, null ratio, top-K frequent values);
- optional sample data rows (a finite subset of actual data values drawn from 
the source);
- optional relational metadata (foreign key indicators, uniqueness constraints, 
primary key status).

Schemas may be authored manually by data engineers or domain experts, may be 
partially or fully derived from source code analysis, database catalog 
introspection, data dictionary parsing, automated type inference, statistical 
profiling of sample data, or any combination thereof.

**Data dictionaries and accompanying documentation.** Many data sources ship 
with accompanying documentation that describes the meaning, format, and 
intended use of each column or field. This documentation may take the form of a 
data dictionary, codebook, data manual, schema specification document, PDF 
report, README file, separate metadata file (such as a JSON or CSV file 
describing column meanings), or any other human-readable or machine-readable 
documentation provided alongside the data source. Such accompanying 
documentation may be used directly as the semantic schema, may be ingested and 
converted into a structured semantic schema format by the semantic annotation 
layer, or may be combined with other schema derivation methods (such as 
sample-data inference or type introspection) to produce a composite semantic 
schema. For example, a government dataset published as a CSV file may ship with 
a separate PDF data dictionary that describes each column in plain English; the 
system may ingest the PDF, extract the column descriptions, and use them as the 
natural-language semantic annotations for the CSV columns without requiring 
manual schema authoring. Where the accompanying documentation is 
incomplete—for example, describing some columns but not others—the system 
may supplement the documented columns with automatically inferred descriptions 
derived from sample data values or type metadata.

The semantic schema constitutes the sole input to the mapping layer; the data 
sources themselves need not share a common type system, naming convention, or 
structural format.

#### Semantic Correspondence Identification

The mapping layer ingests the semantic schemas of two or more data sources. A 
generative model is prompted (or otherwise configured) to identify semantic 
correspondences between attributes across the sources. A correspondence may be 
any of the following, without limitation:

- **One-to-one correspondence:** A single attribute in source A maps to a 
single attribute in source B (for example `cust_name` maps to 
`customer_full_name`).
- **One-to-many correspondence:** A single attribute in source A maps to a 
combination of attributes in source B (for example `full_name` in source A maps 
to `first_name` and `last_name` in source B, requiring a split transformation).
- **Many-to-one correspondence:** Multiple attributes in source A combine to 
produce a single attribute in source B (for example `first_name` and 
`last_name` in source A map to `full_name` in source B, requiring a 
concatenation transformation).
- **Many-to-many correspondence:** Multiple attributes in source A jointly 
determine multiple attributes in source B (for example `street`, `city`, 
`state`, `zip` in source A map to `address_line_1`, `address_line_2`, 
`postal_code` in source B, requiring a recombination transformation).
- **Conditional correspondence:** An attribute in source A maps to different 
attributes in source B depending on the value of a discriminator field (for 
example `phone` in source A maps to `mobile_number` if `phone_type == "mobile"` 
and to `landline_number` if `phone_type == "landline"`).
- **Non-correspondence:** An attribute in source A has no semantic equivalent 
in source B (for example an internal audit timestamp with no counterpart in the 
target schema).

The generative model may use any combination of the natural-language 
descriptions, type metadata, statistical profiles, sample data values, and 
accompanying documentation to determine correspondences. The model is not 
limited to syntactic name matching and may identify correspondences even when 
column names share no lexical overlap.

#### Transformation Logic Synthesis

For each identified correspondence, the generative model synthesizes 
transformation logic that defines how data from the source attribute(s) is 
converted to the target attribute(s). The transformation logic may be expressed 
in any executable or declarative format, including without limitation:

- a general-purpose programming language (for example Python, JavaScript, Java, 
Go, Rust, Scala, or any equivalent);
- a data query or manipulation language (for example SQL, SOQL, Cypher, or any 
equivalent);
- a data processing framework expression (for example PySpark, Pandas, Dask, 
Ray, Flink, or any equivalent);
- a declarative mapping specification (for example JSON, YAML, XML, or any 
structured format that declares source-to-target correspondences and 
transformation rules);
- a domain-specific mapping language (whether Turing-complete or 
non-Turing-complete);
- a workflow or pipeline definition (for example Airflow DAG, dbt model, 
Prefect flow, or any equivalent);
- any combination of the foregoing.

The transformation logic may include any combination of the following 
operations, without limitation: direct field assignment, string concatenation, 
string splitting or parsing, substring extraction, date or time format 
conversion, type casting or coercion, null or missing value handling (including 
default substitution, conditional logic, error handling, logging, metric 
emission, or any equivalent), mathematical or statistical computation, lookup 
or join against a reference table, conditional branching based on source 
attribute values, filtering or exclusion of source rows, and multi-source 
consolidation or conflict resolution.

The generative model may produce a complete executable program, a function or 
method, a declarative mapping document, a SQL query or set of queries, a data 
pipeline definition, or any combination of these. The output format is not 
constrained to any single representation.

#### Validation and Optional Feedback Loop

Synthesized transformation logic is passed to a validation engine that may 
perform any combination of the following checks (all optional and extensible):

- verification that all referenced source and target attributes exist in the 
declared schemas;
- type compatibility verification (for example confirming that a string 
concatenation operation targets string-typed attributes, or that a date parsing 
operation targets a string with a recognizable date format);
- cardinality verification (for example confirming that a many-to-one mapping 
declares a combining transformation and that a one-to-many mapping declares a 
splitting transformation);
- null-handling verification (confirming that nullable source attributes have 
declared fallback or default behavior where the target attribute is 
non-nullable);
- data loss detection (flagging source attributes that have no corresponding 
target attribute and no explicit omission or exclusion declaration);
- round-trip verification (where feasible, confirming that applying the 
transformation to sample source data and then applying the inverse 
transformation recovers the original values within an acceptable tolerance);
- sample-data dry run (executing the transformation logic against a finite 
sample of source rows and checking that output values conform to the target 
schema's type, range, and nullability constraints);
- static analysis of generated code (for example syntax checking, linting, type 
checking, dependency analysis, or security analysis where the transformation 
logic is expressed in a general-purpose programming language);
- any other static or dynamic safety or correctness analysis.

If the transformation logic is rejected, the validation engine may generate a 
structured error description that is optionally fed back to the generative 
model as a corrective prompt, eliciting revised logic. The feedback loop may be 
iterated any number of times or omitted entirely.

#### Execution and Dynamic Re-mapping

Once validated, the transformation logic is deployed to a data integration 
pipeline or execution environment. The execution engine reads source data, 
applies the transformation logic, and writes the resulting data to the target 
system.

Upon any change in a source schema (column added, removed, renamed, retyped), 
upon addition or removal of a data source, upon detection of data drift 
(statistical distribution of source values changing beyond a threshold), or 
upon user request, the mapping layer may invalidate affected transformation 
logic and regenerate replacement mappings. This dynamic re-mapping does not 
require modification of the source or target systems themselves.

#### Multi-Source Reconciliation

Where three or more data sources must be reconciled into a common target 
schema, the mapping layer may synthesize transformation logic that declares 
correspondences across all sources simultaneously. The generative model may 
identify attributes that are semantically equivalent across three or more 
sources and synthesize consolidation rules (for example preferring the non-null 
value from the most recently updated source, applying a priority ordering 
across sources, or merging values according to domain-specific conflict 
resolution logic). Multi-source reconciliation may include conflict resolution 
rules expressed in any executable or declarative format.

#### Non-Limiting Implementation Details and Variations

The generative model may be a large language model, a fine-tuned model, a 
smaller specialized model, a symbolic reasoner, or any hybrid. Validation may 
be purely static, may incorporate sample-data dry runs, may incorporate full 
shadow execution against a copy of the production data, or may be omitted. The 
system may operate in a batch ETL context, a streaming ELT context, a real-time 
data virtualization context, a one-time data migration context, or any 
combination.

Semantic schemas may be cached, versioned, and reused across multiple mapping 
operations. The system may maintain a registry of previously synthesized 
transformation logic and reuse or adapt it when the same pair of data sources 
is encountered again with minor schema changes.

Any of the foregoing components, steps, or features may be performed in any 
order, combined, iterated, omitted, or replaced by functional equivalents. The 
use of natural-language schemas, generative synthesis of transformation logic, 
validation, and dynamic re-mapping may each be practiced independently or in 
any combination.

#### Illustrative Examples (Non-Limiting)

**Example A – CSV to Relational: Customer Data Migration.**
A legacy system exports customer data as a CSV file with columns `cust_id`, 
`name`, `addr1`, `addr2`, `city_st`, `zip`, `phone`, `created`. The target 
system is a relational database with columns `customer_id`, `first_name`, 
`last_name`, `street_address`, `apartment_number`, `city`, `state`, 
`postal_code`, `phone_number`, `account_created_at`. The semantic schemas for 
both sources are generated automatically by sampling rows and prompting a 
generative model to describe each column. The mapping layer identifies that 
`name` corresponds to the combination of `first_name` and `last_name` 
(requiring a split operation), that `addr1` maps to `street_address`, that 
`addr2` maps to `apartment_number`, that `city_st` must be split into `city` 
and `state`, that `phone` maps to `phone_number` with a format normalization, 
and that `created` maps to `account_created_at` with a date format conversion. 
The generative model synthesizes a Python function that performs all 
transformations. The function is validated by static type checking and a dry 
run against sample rows, then deployed to the migration pipeline.

**Example B – Government Dataset with Data Dictionary.**
A municipal government publishes a CSV file of building permits with columns 
`permit_id`, `appl_date`, `val_est`, `sq_ft`, `class_cd`, `contractor_nm`. The 
CSV ships with a PDF data dictionary that describes each column in plain 
English: `appl_date` is "the date the permit application was received, in 
MM/DD/YYYY format"; `val_est` is "the estimated dollar value of the 
construction work"; `class_cd` is "a code indicating the building class 
(1=residential, 2=commercial, 3=industrial)". The system ingests the PDF, 
extracts the column descriptions, and constructs a semantic schema for the CSV 
without manual annotation. A target analytics platform requires columns 
`permit_number`, `application_date` (ISO 8601), `estimated_value`, 
`square_footage`, `building_class` (string label), `contractor_name`. The 
mapping layer identifies the correspondences using the data dictionary 
descriptions, synthesizes SQL transformation logic that converts `appl_date` 
from `MM/DD/YYYY` to `YYYY-MM-DD` and converts `class_cd` from numeric codes to 
string labels via a CASE expression, validates the SQL against the target 
schema, and deploys it.

**Example C – Multi-Source Reconciliation: Product Catalogs.**
Three independently authored product catalog databases must be merged into a 
unified catalog. Database A uses `sku`, `product_name`, `price_usd`. Database B 
uses `item_code`, `title`, `cost`. Database C uses `product_id`, `name`, 
`list_price`. The semantic schemas include natural-language descriptions 
clarifying that `price_usd` is a retail price in USD, `cost` is a wholesale 
cost in USD, and `list_price` is a manufacturer's suggested retail price in 
USD. The mapping layer identifies that `sku`, `item_code`, and `product_id` are 
semantically equivalent identifiers and synthesizes a PySpark transformation 
that maps all three to a unified `product_id` column. The transformation 
includes a priority rule that uses Database A for retail pricing where 
available, falls back to Database C's `list_price` with a 15% markup, and 
excludes Database B's `cost` from the retail price mapping while preserving it 
in a separate `wholesale_cost` column.

**Example D – Schema Drift Detection and Re-mapping.**
A data pipeline ingests daily CSV exports from a third-party vendor. The 
vendor's CSV schema changes without notice: the column `customer_email` is 
renamed to `email_address` and a new column `email_opt_in` is added. The 
pipeline's existing transformation logic references `customer_email` and fails 
validation on the next ingestion cycle. The mapping layer detects the schema 
change, ingests the new semantic schema (generated automatically from the new 
CSV header and sample rows), identifies that `email_address` is semantically 
equivalent to the previously mapped `customer_email`, synthesizes revised 
transformation logic that maps `email_address` to the target `email` column and 
optionally maps the new `email_opt_in` column to a target `marketing_consent` 
column, validates the revised logic, and deploys it without manual intervention.

**Example E – Conditional Mapping.**
A source system has a single `phone` column and a `phone_type` column. The 
target system has separate `mobile_number` and `landline_number` columns. The 
mapping layer identifies the conditional correspondence and synthesizes a 
Python function containing conditional branching: if `phone_type == "mobile"`, 
the value is written to `mobile_number`; if `phone_type == "landline"`, the 
value is written to `landline_number`. The validation engine confirms that the 
discriminator field is referenced in the conditional logic and that the target 
columns are nullable (since not every source row will populate both).

**Example F – JSON to Relational: API Response Ingestion.**
A REST API returns JSON responses with nested fields: `user.profile.firstName`, 
`user.profile.lastName`, `user.contact.emails[]` (an array of email objects 
each with `address` and `type` fields). The target system is a relational 
database with a `users` table (`first_name`, `last_name`, `primary_email`) and 
a separate `user_emails` table (`user_id`, `email`, `email_type`). The semantic 
schema for the API response is derived from the API's OpenAPI specification 
document, which contains natural-language descriptions of each field. The 
mapping layer identifies the correspondences, synthesizes a SQL transformation 
that flattens the nested JSON into the two relational tables, handles the array 
of emails by inserting one row per email into `user_emails`, and selects the 
email with `type == "primary"` for the `primary_email` column in the `users` 
table.

Many additional embodiments will be apparent to those of ordinary skill in the 
art.

#### Advantages

The disclosed systems and methods enable heterogeneous data sources to be 
semantically mapped without manual specification of column correspondences, 
handle naming divergence and structural granularity mismatches that defeat 
purely syntactic matching algorithms, maintain a clean separation between 
generative synthesis and deterministic execution, and adapt dynamically to 
schema changes without requiring pipeline reconfiguration. The approach is 
format-agnostic: it applies with equal utility to relational databases, CSV 
files, JSON documents, API schemas, Parquet files, and any structured or 
semi-structured data source. The approach further accommodates data sources 
that ship with accompanying documentation (such as data dictionaries or 
codebooks) by ingesting such documentation directly as the semantic schema, 
eliminating the need for manual annotation in cases where column descriptions 
are already available.

### NOVEL ASPECTS DEDICATED TO THE PUBLIC

The following are dedicated to the public domain and are intended to serve as 
prior art against any later attempt to patent them:

- the general concept of using natural-language semantic schemas describing 
data source attributes as the primary or sole input to a generative model that 
identifies semantic correspondences between attributes of heterogeneous data 
sources and synthesizes executable transformation logic;
- the synthesis of transformation logic in any executable or declarative 
format, including general-purpose programming languages, SQL or other query 
languages, data processing framework expressions, declarative mapping 
specifications, domain-specific languages (whether Turing-complete or 
non-Turing-complete), pipeline or workflow definitions, or any combination 
thereof;
- the combination of generative synthesis with a validation engine that 
performs type compatibility, cardinality, null-handling, data loss, dry-run, 
static analysis, or round-trip verification of synthesized transformation 
logic, optionally including a corrective feedback loop;
- dynamic invalidation and re-synthesis of transformation logic in response to 
schema changes, data drift, or data source addition or removal, without 
requiring modification of the source or target systems;
- the automatic derivation of semantic schemas from sample data values, 
statistical profiles, database catalog introspection, source code analysis, or 
type signature extraction, and the use of such derived schemas as input to 
generative-model-based mapping synthesis;
- the ingestion of accompanying documentation—including data dictionaries, 
codebooks, data manuals, schema specification documents, PDF reports, README 
files, or separate metadata files provided alongside a data source—as the 
semantic schema or as input to semantic schema generation, whether used 
directly, converted into a structured format, or combined with other schema 
derivation methods;
- the synthesis of multi-source transformation logic that reconciles three or 
more heterogeneous data sources into a common target schema, including conflict 
resolution and priority rules;
- the identification and synthesis of one-to-many, many-to-one, many-to-many, 
and conditional correspondences between data source attributes, including 
splitting, concatenation, recombination, and discriminator-based conditional 
transformations;
- any system or method that performs semantic correspondence detection, 
transformation logic synthesis, validation, and execution of data mappings 
between heterogeneous data sources, including but not limited to relational 
databases, CSV files, JSON documents, XML documents, Parquet files, Avro 
records, API response schemas, and fixed-width text files;
- all combinations, sub-combinations, independent practice of individual 
features, and obvious variations of the foregoing, including systems in which 
one or more of the described steps or components (validation, feedback, dry 
run, multi-source reconciliation, conditional mapping, automatic schema 
derivation, data dictionary ingestion, dynamic re-mapping, etc.) are omitted.

Individual elements and sub-combinations are also dedicated to the public. The 
intent of this disclosure is to prevent the patenting of the described systems, 
methods, and concepts, whether claimed broadly or narrowly.

---

*This disclosure is published solely to establish prior art and to dedicate the 
described systems, methods, and concepts to the public domain. It is not a 
patent application. No patent rights are claimed. All described subject matter 
is dedicated to the public.*
