**DEFENSIVE TECHNICAL DISCLOSURE**

**Systems and Methods for Predictive Prior Art Generation Based on
Entity-Specific Filing Trajectory Analysis and Anticipatory Disclosure
Synthesis**

**Publication Date:** 2026-08-20
**Disclosure Number:** CB-2026-0009

---

### FIELD OF THE DISCLOSURE

This disclosure relates generally to computer-implemented intellectual
property analytics and automated defensive publication. More specifically,
it relates to systems and methods for analyzing historical patent filing
patterns, prosecution histories, and technical trajectories associated
with specific inventors, companies, or sectors to predict future patent
applications, and for automatically generating and publishing defensive
technical disclosures targeting those predicted applications before they
are filed.

### BACKGROUND

The strategic value of defensive publishing lies in establishing prior art
before a patent applicant files a claim. However, conventional defensive
publishing is reactive, relying on human actors to identify current
trends and draft disclosures. High-volume patent filers—particularly
in software, artificial intelligence, and computing systems—often
file applications following predictable strategic patterns. A company
may file a core system patent, followed by a series of continuation
or divisional applications claiming minor variations, specific user
interfaces, integration with adjacent technologies, or incremental
algorithmic optimizations.

These filing trajectories are often deterministic. If an entity has
a history of filing a continuation patent adding "machine learning
optimization" to every core routing or dispatch system it patents, the
appearance of a new core routing patent from that entity strongly predicts
a future continuation adding machine learning to that specific system.

Current prior art systems do not proactively model the filing behavior of
specific entities to anticipate their future claims. There remains a need
for automated systems that ingest entity-specific filing histories, model
their proprietary claim-drafting patterns and technological trajectories,
predict the likely subject matter of their unfiled applications, and
speculatively generate enabling defensive disclosures to pre-empt those
specific predicted applications.

### SUMMARY

Disclosed are systems, methods, and computer-readable media that predict
future patent filings from specific entities and automatically generate
targeted defensive prior art. A system ingests patent portfolios,
prosecution histories, and non-patent literature associated with
target entities. A trajectory modeling engine analyzes the sequential
relationships between an entity's filed applications to identify
proprietary patterns in claim construction, technology integration, and
continuation strategy. A predictive engine extrapolates these patterns
to forecast the subject matter and likely claim structure of unfiled
applications. A generative model synthesizes an enabling technical
disclosure detailing the predicted invention. An automated publication
interface publishes the synthesized disclosure, establishing targeted
prior art against the entity's predicted filing strategy.

Any of the described steps or components may be combined, omitted,
reordered, or replaced by functional equivalents.

### DETAILED DESCRIPTION

#### General System

A computing system comprises one or more processors and one or more
non-transitory computer-readable media storing instructions that, when
executed, realize the following non-limiting components (which may be
present in any subset or combination):

- an entity data ingestion interface acquiring patent portfolios,
assignment data, and prosecution histories for target entities;
- a trajectory modeling engine analyzing sequential filing patterns and
claim evolution;
- a predictive claim engine forecasting future application subject matter;
- a generative disclosure engine synthesizing anticipatory technical
disclosures;
- a validation engine verifying technical enablement and novelty;
- an automated publication interface distributing validated disclosures.

#### Entity Data Ingestion and Feature Extraction

The system ingests historical data associated with a specific assignee,
inventor, or technological sector. Non-limiting data sources include:
- granted patents and published patent applications;
- patent assignment records;
- prosecution histories, including office actions, responses, and
interview summaries;
- continuations, divisionals, and CIP (continuation-in-part) linkages;
- technical whitepapers, product documentation, and engineering blogs
published by the entity.

The ingestion interface extracts features representing the entity's
filing behavior. Non-limiting features include:
- **Temporal filing cadence:** Average time between a parent application
and subsequent continuations.
- **Claim augmentation patterns:** Frequent additions made during
prosecution or via CIP to overcome prior art (e.g., a propensity to add
"using a neural network" or "via a distributed ledger" to base system
claims).
- **Technology integration vectors:** Standard adjacent technologies the
entity combines with its core inventions (e.g., a logistics company that
systematically files continuations integrating its routing systems with
"biometric authentication" or "predictive weather modeling").
- **Inventor network graphs:** Co-inventorship patterns indicating which
teams or individuals are likely to file next in a specific technology
area.

#### Trajectory Modeling

The trajectory modeling engine processes the extracted features to build
a predictive model of the entity's filing behavior. Non-limiting modeling
techniques include:

- **Sequence modeling:** Treating an entity's portfolio as a time-ordered
sequence of technological concepts. Models such as Recurrent Neural
Networks (RNNs), Transformers, or Hidden Markov Models predict the next
likely concept in the sequence given the most recent filings.
- **Graph-based propagation:** Constructing a graph where nodes
are technologies or claim elements, and edges represent historical
co-occurrence or continuation relationships. The system predicts future
filings by propagating probability mass through the graph from the
entity's most recent filings.
- **Prosecution strategy clustering:** Clustering the entity's historical
office actions to identify which claim limitations they most frequently
add to survive 35 U.S.C. 102 or 103 rejections, thereby modeling their
specific "novelty survival" vocabulary.

#### Predictive Claim Generation

The predictive claim engine generates a forecast of the entity's unfiled
applications. Given a recently published parent application by the target
entity, the engine outputs one or more predicted future applications.

The prediction includes:
- **Predicted subject matter:** The core technological concept of the
future application (e.g., "applying reinforcement learning to the dispatch
routing engine of the parent application").
- **Predicted claim limitations:** The specific vocabulary or limitations
the entity is likely to add based on their historical prosecution
patterns.
- **Predicted filing window:** The estimated timeframe in which the
application will be filed, based on the entity's temporal cadence.

#### Anticipatory Disclosure Synthesis

The generative disclosure engine synthesizes a defensive technical
disclosure targeting the predicted application. A generative model (e.g.,
a large language model) is prompted with:
- the predicted subject matter and claim limitations;
- the text of the parent application;
- the entity's historical prosecution vocabulary.

The generative model is instructed to synthesize an enabling technical
disclosure (under 35 U.S.C. 112 standards) that describes the predicted
invention. The disclosure is drafted to explicitly anticipate the
predicted claim limitations.

For example, if the trajectory model predicts that a ride-sharing entity
will file a continuation adding "generative AI-based driver profiling"
to its core dispatch system, the generative engine produces a disclosure
titled "Systems and Methods for Generative AI Driver Profiling in Dispatch
Routing," detailing exactly how such a system would be built and operated.

#### Validation and Automated Publication

The validation engine evaluates the synthesized disclosure. Non-limiting
checks include:
- **Enablement verification:** Confirming the disclosure contains
sufficient technical detail to allow a person of ordinary skill to
practice the predicted invention.
- **Collision detection:** Checking the predicted concept against very
recent filings to ensure the concept has not already been filed by the
target entity or others.
- **Targeted publication:** Publishing the disclosure to repositories
indexed by patent examiners (e.g., IP.com, public technical blogs,
arXiv) with metadata tags optimized for search algorithms used by the
USPTO or EPO, ensuring the examiner will locate it during prosecution
of the predicted application.

#### Non-Limiting Implementation Details and Variations

The trajectory model may be specific to a single entity, or it may be
a sector-wide model trained on the filing patterns of all major filers
in a specific CPC class, with entity-specific embeddings used to tune
the output. The system may operate continuously, monitoring an entity's
new publications and automatically generating a queue of anticipatory
disclosures. The system may also generate disclosures targeting the
specific "novelty survival vocabulary" identified during prosecution
clustering, effectively blocking the entity's most common workaround
strategies.

Any of the foregoing components, steps, or features may be performed
in any order, combined, iterated, omitted, or replaced by functional
equivalents.

#### Illustrative Examples (Non-Limiting)

**Example A – Continuation Strategy Pre-emption.**
An entity has a historical pattern of filing a base patent for a
"data processing system," followed within 6 months by a continuation
adding "edge computing deployment," and within 12 months by a second
continuation adding "homomorphic encryption for data transit." The
entity recently published a base patent for an "automated inventory
reconciliation system." The trajectory model predicts a continuation
adding edge computing, and a second adding homomorphic encryption. The
generative engine immediately synthesizes and publishes a disclosure
titled "Edge Computing and Homomorphic Encryption in Automated Inventory
Reconciliation," pre-empting both predicted continuations.

**Example B – Sector-Wide Technology Integration Prediction.**
Analysis of a specific technology sector (e.g., last-mile delivery
robotics) reveals a high probability that companies in this sector
will file patents integrating "large language model natural language
interfaces" into their robotic control systems within the next 18
months. The system identifies a company that has just filed a patent
for a "robotic package retrieval arm." The predictive engine forecasts
an integration patent. The generative engine synthesizes a disclosure
detailing "LLM-Driven Natural Language Command Interfaces for Robotic
Package Retrieval," establishing prior art against the sector-wide trend
as applied to this specific company's new base system.

**Example C – Prosecution Vocabulary Saturation.**
A target entity frequently overcomes obviousness rejections by amending
claims to include the limitation "wherein the optimization is performed
via a quantum-inspired annealing simulation." The system identifies a
new patent application from this entity claiming a "network bandwidth
allocation system." The generative engine synthesizes a defensive
disclosure detailing "Quantum-Inspired Annealing for Network Bandwidth
Allocation," specifically saturating the exact claim limitation the
entity is statistically most likely to add during prosecution.

Many additional embodiments will be apparent to those of ordinary skill
in the art.

#### Advantages

The disclosed systems and methods automate the prediction of future patent
filings based on entity-specific behavioral patterns. By generating and
publishing enabling disclosures directed to the exact subject matter and
claim limitations an entity is predicted to file, the system proactively
saturates the prior art landscape. This pre-empts the issuance of
predictable continuation and divisional patents, forcing entities to
claim further afield or abandon predictable farming strategies.

### NOVEL ASPECTS DEDICATED TO THE PUBLIC

The following are dedicated to the public domain and are intended to
serve as prior art against any later attempt to patent them:

- the general concept of ingesting an entity's historical patent filings
and prosecution histories to model their specific sequential filing
trajectories, claim augmentation patterns, or technology integration
strategies;
- the use of sequence modeling, graph propagation, or clustering on
patent portfolio data to predict the subject matter, claim limitations,
or filing window of an entity's unfiled applications;
- the automated generation of an enabling technical disclosure using a
generative model conditioned on a predicted future patent application;
- the synthesis of defensive disclosures specifically targeting an
entity's historical "novelty survival vocabulary" or common prosecution
workaround limitations;
- the automated publication of anticipatory disclosures with metadata
optimized for discovery by patent examiners during future prosecution;
- any system or method that performs entity trajectory modeling,
predictive claim generation, anticipatory disclosure synthesis, and
targeted publication in any combination;
- all combinations, sub-combinations, independent practice of individual
features, and obvious variations of the foregoing, including systems
in which one or more of the described steps or components (validation,
prosecution history analysis, sector-wide modeling, etc.) are omitted.

Individual elements and sub-combinations are also dedicated to the
public. The intent of this disclosure is to prevent the patenting of
the described systems, methods, and concepts, whether claimed broadly
or narrowly.

---

*This disclosure is published solely to establish prior art and to
dedicate the described systems, methods, and concepts to the public
domain. It is not a patent application. No patent rights are claimed. All
described subject matter is dedicated to the public.*
