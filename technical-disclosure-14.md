**DEFENSIVE TECHNICAL DISCLOSURE**

**Systems and Methods for Staged Expansion of Partial User-Interface Concepts into Component-Complete Prototypes, Spatial Assembly Maps, and Contract-Faithful Application Implementations, Including Human, Machine-Assisted, or Mixed Performance of Any Stage**

**Publication Date:** 2026-09-10  
**Disclosure Number:** CB-2026-0014

---

### FIELD OF THE DISCLOSURE

The present disclosure relates to computer-implemented methods and systems for transforming a partially specified user-interface concept into complete component-level prototypes, recording spatial reconstruction, assembling a full behavioral prototype, and implementing an application constrained by that prototype. Any stage may be performed by a person, by one or more programmed or artificial-intelligence (AI) agents, or by any combination thereof.

### BACKGROUND

User-interface work often begins as an incomplete concept. Implementers commonly jump from that fragment to production code, mixing unfinished product decisions with framework structure. They may also refine a monolithic mock without recording component boundaries or placement. Automated assistants are sometimes used ad hoc at a single step (for example only to write code) without a disclosed pattern that permits an AI system to perform or assist inventory, completion of implied regions, harmony enforcement, mapping, assembly, review, or implementation. There is a need for a staged process that remains enabling whether stages are executed by humans, by AI agents, or both, including handoff of artifacts between human and machine participants.

### SUMMARY

A system or method may receive a partial concept artifact describing some portion of a user interface. The system may identify interface regions that are implemented or implied, emit a complete standalone prototype for each such region, emit a spatial reconstruction map that places those regions without requiring the regions to be interactive, optionally assemble the complete region prototypes according to the map into one full prototype, and optionally implement an application whose user-visible behavior matches that full prototype, including by substituting a mock data source that is later replaceable by a live data source. **Any stage, sub-step, decision, generation, classification, review, or gate in this process may be performed by one or more persons, by one or more AI or other programmed agents, or by any mixed or sequential collaboration among them.** Any of the foregoing stages may be omitted, combined, reordered, performed for a subset of regions, or practiced independently.

### DETAILED DESCRIPTION

#### General System

A non-limiting system may include one or more of: a concept ingest component; a region inventory component; a complete-prototype generator; a visual-harmony component; a spatial-map generator; an assembler; an implementation (port) component; and a review or approval gate. Each component may be realized as instructions executed by a general-purpose processor, as an AI model or agent (including large language models, multimodal models, tool-using agents, or any suitable successor), as a human operator, or as a workflow that assigns different components to different participants.

AI participation is optional at every stage and is not required at any stage. An AI agent may perform a stage end-to-end, draft an artifact for human edit, critique a human artifact, classify an input and route to a next stage, or stand idle while a person performs that stage. Multiple agents may work in parallel or in series. Humans may override, accept, reject, or revise any machine output. Stored skill files, prompts, rules, or policies may condition an agent’s behavior; such stored instructions are optional and may be omitted.

Artifacts may be stored as files, records, or any suitable medium. The user interface may target any suitable client. Implementation may use any suitable component-oriented presentation framework.

#### Use of AI at any stage

Without limitation, an AI agent **may**:

- classify a received artifact as a partial concept or a complete contract;  
- read concept structure, appearance, and behavior and propose or finalize a region inventory, including implied regions;  
- generate complete region prototypes (structure, presentation, and behavior);  
- extract or apply shared visual and interaction tokens;  
- generate or update a spatial reconstruction map;  
- assemble region prototypes according to the map;  
- list missing conventional affordances and pose determinations to a user;  
- implement application code and a substitutable mock data layer from an assembled prototype;  
- run checks (harmony drift, missing map regions, contract deviations) and revise artifacts;  
- persist status so a later human or agent session can resume.

An AI agent may use any suitable tools (file read/write, browsers, compilers, tests, design tools, or none). Model provider, model size, hosting location, and whether the agent is interactive or batch are non-limiting. Outputs of one agent may be inputs to another agent or to a person. The same method is practiced if no AI is used at all.

#### Concept ingest and classification

A received artifact may be classified as a partial concept or as an already-complete behavioral contract. Classification may consider whether states, controls, and regions are specified enough that a person of ordinary skill could treat the artifact as “build exactly this.” If the artifact is already complete, later expansion stages may be skipped. If no interface artifact exists, the method may stop or may first obtain a concept by any suitable means, including generation or critique by an AI agent. Classification may be performed by a person, an AI agent, or both.

#### Inventory of implemented and implied regions

The method may read the concept’s structure, appearance, and any accompanying behavior description. It may list discrete interface regions, each corresponding to a unit that would later be implemented as a separate presentation component. The list may include regions drawn in the concept and regions only implied by labels, empty areas, navigation, controls, or adjacent flow. For each region the method may record a name, whether it is implemented or implied, a one-sentence job, states to be specified, dependencies, and an output identifier. If two reasonable inventories would yield different region sets, the method may request a determination (from a person and/or another agent) before proceeding. A provided region list may be used instead of or in addition to automatic inventory.

#### Generation of complete region prototypes

For each inventoried region the method may generate a complete prototype sufficient to serve as a later behavioral contract for that region. In a non-limiting web embodiment, each prototype may be a standalone document containing structure, presentation, and behavior specifications together, openable and usable without the original concept page. Each complete prototype may implement controls and in-region navigation; supply states the region’s job implies; include sample data sufficient to exercise those states; and remain limited to that region’s job. A thin non-functional frame may be included so the region is readable in isolation. Implied regions that were never drawn may be completed in the smallest form consistent with the concept’s visual language. Weak implications may be confirmed rather than fabricated as new product areas. Generation may be wholly or partly AI-authored.

#### Visual and interaction harmony

Because region prototypes are later assembled into one product, the method may constrain them to a shared appearance and interaction grammar derived from the concept. Shared tokens may include color, type, space, radius, border, shadow, density, control anatomy, and chrome treatment. Tokens defined while completing an incomplete concept may be reused rather than restyled per region. An AI agent may optionally audit files for token drift and correct it. Exceptions may be recorded and still use the shared token set.

#### Spatial reconstruction map

The method may emit a reconstruction map that records how regions are placed in a single application shell. In a non-limiting embodiment the map is a static structured document that blocks out named regions without interactive behavior or live data. Each blocked region may carry an identifier corresponding to a complete region prototype. The map may specify parent/child relationships, order, columns, panes, sticky or fixed chrome, and overlay stacking precisely enough that assembly does not require reinterpreting the concept. Multiple shells implied by the concept may appear as separate labeled frames in one map. Every inventoried region, including implied empty regions, may appear. The map may be drafted or revised by an AI agent, a person, or both.

#### Assembly into a full prototype

After region prototypes are accepted or otherwise deemed complete, the method may compose them into one full prototype using the reconstruction map as the spatial contract. Acceptance may be human, automated (including AI review against a checklist), or mixed. The assembled artifact may be treated as the behavioral contract for implementation. Assembly may be manual, AI-performed, or mixed.

#### Contract-faithful implementation

Only after a full prototype exists may the method generate an implementation in a component-oriented application structure. The full prototype may define user-perceived behavior. Implementation may refactor internals so long as a user comparing prototype and implementation would not perceive a different product. Domain values may be moved into a mock or substitute data layer structured so that later substitution of a live backend does not require editing presentation components to change behavior. Implementation, mock authoring, and deviation listing may be performed by an AI agent, a person, or both.

Optionally, before implementation, the method may list conventional affordances missing from the prototype and obtain a determination whether to implement as-is or to add a minimal affordance. That listing and determination may involve an AI agent posing questions and a person answering, or any other mix. After explicit review and approval (human and/or policy-driven), the presentation layer may be treated as frozen except upon later explicit request.

#### Staging and routing

A controller or process may classify the current artifact and invoke only the next stage. The controller itself may be a person, an AI agent following stored routing instructions, or both. Stages may be gated so that implementation does not begin from a partial concept and so that isolated region prototypes are not implemented before assembly. Routing instructions may be encoded as reusable skill or policy documents consumed by an agent; such encoding is optional.

#### Non-Limiting Implementation Details and Variations

Any step or component may be omitted, combined, split, reordered, or replaced with an equivalent. **Any step may be executed by a human, by one or more AI agents, or by any collaboration pattern (draft/review, generate/critique, parallel alternatives, sequential handoff, or fully autonomous execution subject to an optional gate).** Region prototypes need not be single-file documents. The reconstruction map need not be HTML. Assembly may be omitted if a single complete prototype is authored directly. Implementation may target any suitable framework or remain at prototype. Mock data may take any suitable form. Harmony tokens may be duplicated or referenced from a shared source. Inventory and approval gates may be skipped when boundaries are unambiguous. AI systems may be local or remote, single- or multi-model, with or without tools. The method is practiced equally if AI is unused.

#### Illustrative Examples (Non-Limiting)

Example 1. A person supplies a partial page. An AI agent inventories chrome, search, collection, and an implied editor; writes complete standalone prototypes and a static blocking map; the person edits one prototype; the agent reassembles per the map; the same or another agent implements a component tree on mock records. Any of those agent steps could instead have been done by the person.

Example 2. A complete demonstration exists. A person classifies it as complete. An AI agent still emits a placement map and implements a substitutable mock-backed application matching the demonstration. Alternatively, the person implements without an agent. Both are within this disclosure.

#### Advantages

- Separates product completion from implementation structure.  
- Records placement independently of behavior.  
- Keeps separately authored regions consistent prior to composition.  
- Constrains implementation to user-perceived parity.  
- Permits AI assistance or AI execution at every stage without making AI a required element of the method.

### NOVEL ASPECTS DEDICATED TO THE PUBLIC

The following are dedicated to the public domain and are intended to serve as prior art against any later attempt to patent them:

- Classifying an interface artifact as a partial concept versus a complete behavioral contract and routing subsequent work accordingly, including routing performed by an AI agent.  
- Inventorying both implemented and implied interface regions that correspond to later presentation components, including inventory performed or assisted by an AI agent.  
- Generating, from a partial concept, a complete standalone prototype per region including implied states and sample data, including generation by an AI agent.  
- Constraining multiple region prototypes to a shared visual token set and interaction grammar, including automated drift detection and correction.  
- Emitting a non-interactive spatial reconstruction map that names each region and specifies placement with enough precision to assemble without reinterpretation, including map generation by an AI agent.  
- Assembling accepted region prototypes according to that map into a single full prototype that becomes the behavioral contract, including assembly by an AI agent.  
- Implementing an application from that assembled contract such that user-perceived behavior matches the prototype and domain data is isolated in a substitutable mock layer, including implementation by an AI agent.  
- Gating implementation until assembly (or an already-complete prototype) exists, and optionally freezing the presentation layer after approval, where gates may be human, AI, or mixed.  
- Optionally enumerating missing conventional affordances and obtaining a determination before implementation, including posing those determinations via an AI agent.  
- Performing **any one or more stages of the foregoing process with one or more AI or programmed agents**, with one or more humans, or with any mixed, sequential, or parallel collaboration, including systems in which AI is used at every stage and systems in which AI is used at none.  
- Encoding stage routing and constraints as stored instructions (skills, prompts, policies) consumable by an agent — and practicing the same stages without such stored instructions.  
- All combinations, sub-combinations, independent practice of individual features, and obvious variations, including systems in which one or more steps are omitted.

---

*This disclosure is published solely to establish prior art and to dedicate the described systems, methods, and concepts to the public domain. It is not a patent application. No patent rights are claimed. All described subject matter is dedicated to the public.*
