**DEFENSIVE TECHNICAL DISCLOSURE**

**Systems and Methods for Client-Side Code Sandboxes with Multi-Model AI 
Assistance, Selective Code Modification, and Branching Conversation History**

**Publication Date:** 2026-08-19
**Disclosure Number:** CB-2026-0003  

---

### FIELD OF THE DISCLOSURE

This disclosure relates to software development tools and, more specifically, 
to client-side execution environments (including but not limited to a web 
browser, browser extension, embedded webview, desktop application framework 
using web technologies, or equivalent runtime) that combine live code editing 
and runtime preview or execution feedback with multi-model 
artificial-intelligence assistance presented in a dedicated interface region 
(including but not limited to a separate tab, panel, pane, window, sidebar, or 
equivalent UI partition), selective application of model-generated code changes 
(including in-line or in-situ preview of each model’s reply before 
application), and tree-structured conversation history that preserves and 
restores associated code states.

### BACKGROUND

Conventional client-side code sandboxes provide an editor and runtime preview 
or execution feedback but lack native support for simultaneous or sequential 
interaction with multiple AI models. Existing AI coding assistants typically 
maintain a single linear interaction thread and apply suggested code changes in 
an all-or-nothing manner. They do not permit independent application or 
reversion of modifications originating from different models, do not provide an 
in-line or in-situ preview of each model’s proposed changes against the 
current code before commitment, and do not represent interaction history as a 
navigable tree in which each node is associated with a recoverable code state. 
There remains a need for integrated systems that supply these capabilities 
within a self-contained client-side environment in which the AI interface 
occupies a dedicated interface region.

### SUMMARY

Disclosed are systems, methods, and computer-readable media realizing a 
client-side application (or set of executable resources) that integrates:

- a code editor and runtime preview or execution feedback sandbox; and
- a multi-model AI assistant interface (including but not limited to a chat 
interface, command-line interface, inline suggestion interface, or equivalent) 
presented in a dedicated interface region.

Each model may propose code modifications. Before any modification is applied, 
the system supports an in-line or in-situ preview of that model’s reply 
against the existing code. A user may then selectively apply or revert the 
modifications proposed by any individual model independently of the others. 
Interaction history is maintained as an explicit tree structure; the user may 
branch from any prior node, navigate to any node, and cause both the assistant 
display and the sandbox code state to restore to the exact state associated 
with that node.

The systems and methods may be implemented entirely client-side using standard 
web or native technologies. Model inference may occur via calls to remote or 
local endpoints. Any of the described features may be combined, omitted, or 
varied.

### DETAILED DESCRIPTION

#### General System

A computing environment executing within a client-side runtime comprises one or 
more of the following non-limiting components, which may be realized together 
or in any subset:

- a sandbox pane containing a text editor for source code of any programming, 
markup, or styling language(s) (including but not limited to HTML, CSS, 
JavaScript, TypeScript, Python, or Rust) together with a runtime preview or 
execution feedback (for example via iframe, shadow DOM, terminal output, or 
equivalent) that reflects the current code state;
- a multi-model AI assistant interface presented in a dedicated interface 
region, providing a message list, input field, and controls for addressing one 
or more AI models (identified by name, endpoint, API key, or other suitable 
identifier);
- a state manager that maintains an interaction tree and associates with each 
node a snapshot (or equivalent representation) of the sandbox code state 
existing at that node.

The system may run wholly client-side. Persistence across sessions is optional 
and may employ any suitable storage mechanism or export format.

#### Multi-Model Interaction

A user may select any subset of available models and issue a prompt to any 
selected subset of models, whether concurrently, sequentially, or in any 
combination thereof. As used herein, "model" encompasses distinct models, 
distinct configurations of the same model, distinct providers serving the same 
model, or any other distinguishable source of AI-generated suggestions. Each 
model returns a response that may contain natural-language text and/or one or 
more proposed code modifications (expressed, for example, as unified diffs, 
search-and-replace blocks, full-file replacements, or any other suitable 
format). Responses are visually distinguished by model identity using any 
convenient means (color, label, avatar, or equivalent) and appear within the AI 
assistant's dedicated interface region.

#### In-Line or In-Situ Preview of Model Replies

Before any proposed modification is applied to the sandbox code, the system 
provides an in-line or in-situ preview of that model’s reply. The preview may 
temporarily render the effect of the proposed changes in the existing runtime 
preview or execution feedback pane, in a side-by-side or overlaid view, via a 
non-destructive temporary code state, or by any other means that allows the 
user to inspect the visual or functional result against the current code 
without committing the change. The user may accept, reject, or further edit the 
previewed modification on a per-model basis.

#### Selective Application and Reversion of Code Modifications

For any code-bearing response the system presents the proposed modifications 
together with per-model controls that may include “Preview”, “Apply”, 
“Revert”, or equivalent actions.  

After optional preview, applying a modification originating from one model 
updates the sandbox code with respect to that model’s proposal. Modifications 
previously applied from other models remain intact except where overlaps occur, 
in which case any suitable conflict-detection or merge presentation (for 
example line-based diff, longest-common-subsequence, three-way merge UI, or 
conflict markers) may be employed.  

Reverting a given model’s modifications restores the sandbox code to a state 
that excludes the modifications previously applied from that model, by any 
suitable mechanism (including but not limited to snapshot restoration, inverse 
patch application, line-level removal, or re-derivation from the associated 
tree node). An independent history or undo stack may optionally be maintained 
per model so that successive applies and reverts from the same model can be 
traversed independently.

Where modifications from different models are interdependent, the system may 
employ any suitable dependency-tracking or cascading-revert mechanism, or may 
present the user with a notification of the dependency and permit manual 
resolution.

#### Conversation History Tree and Navigation

Every user message and every model response is recorded as a node in a tree (or 
equivalent directed acyclic structure). A new branch may be created when a user 
replies to a non-leaf node or explicitly elects to branch from a chosen node.  

Each node stores, or references, at least:

- the interaction messages associated with that point in the conversation;
- a representation of the sandbox code state as it existed at the time that 
node was reached in the conversation; and
- linkage information to parent and child nodes.

A visualization of the tree (collapsible outline, graph, timeline, mind-map, or 
any other suitable presentation) permits the user to select any node. Selection 
of a node restores:

- the assistant interface to the messages that existed at that node;
- the sandbox editor and runtime preview or execution feedback to the code 
state associated with that node; and
- the set of currently applied per-model modifications to match the recorded 
state.

From the restored node the user may continue the conversation (creating a new 
child branch) or may perform any other tree operations such as pruning, 
merging, renaming, or exporting branches.  

#### Non-Limiting Implementation Details and Variations

The system may be realized with ordinary web or native technologies and may 
execute entirely inside a client-side environment; the only external dependency 
is the set of AI model endpoints (remote or local). In one implementation, the 
AI assistant interface occupies a dedicated interface region. Code-state 
representations may be full-text snapshots, operational-transformation patches, 
content-addressable hashes, or any other compact form. In-line or in-situ 
previews may be implemented by any non-destructive temporary rendering 
technique. Conflict detection may employ any conventional diff or merge 
algorithm. The conversation tree and its associated code states may be exported 
as a portable artifact (including but not limited to a JSON structure, archive 
file, or repository commit sequence) and imported into another instance of the 
environment or a compatible system. Persistence, export, import, multi-user 
collaboration, additional language support, server-side assistance, or any 
other extension may be added or omitted.  

Any of the foregoing components, steps, or features may be performed in any 
order, combined, iterated, omitted, or replaced by functional equivalents. The 
selective-apply mechanism (including optional pre-application preview), the 
tree-structured history, the node-associated code snapshots, and the placement 
of the AI interface in a dedicated region may each be practiced independently 
or in any combination.

#### Illustrative Examples (Non-Limiting)

**Example A.** A user opens a blank HTML sandbox and, in a dedicated interface 
region, selects three models and issues a prompt requesting a responsive 
navigation bar. Each model returns a distinct implementation. The user invokes 
an in-situ preview of model 1’s suggestion (the runtime preview temporarily 
shows the result without altering the underlying code), then applies it. The 
user next previews and applies a complementary styling suggestion from model 2 
while leaving model 3’s suggestion unapplied. The user later reverts only 
model 1’s changes; model 2’s styling remains.  

**Example B.** After several exchanges the user navigates back to an earlier 
node in the interaction tree. Both the assistant transcript (shown in its 
dedicated interface region) and the exact code state (including which models’ 
modifications were then applied) are restored. The user branches from that node 
and explores an alternative design path, again using in-line previews before 
committing further changes.  

Many additional interaction patterns and implementation choices will be 
apparent to those of ordinary skill in the art.

#### Advantages

The disclosed systems and methods enable a developer to solicit suggestions 
from multiple AI models (presented in a dedicated interface region), inspect 
each suggestion via in-line or in-situ preview against the current code, and 
selectively incorporate or reject those suggestions within a single live 
sandbox while retaining the ability to explore alternative conversational and 
code trajectories without irreversible commitment. The combination of 
independent per-model control with pre-application preview and recoverable 
node-associated code states provides a degree of exploratory flexibility not 
present in linear, single-model assistants or conventional sandboxes.

### NOVEL ASPECTS DEDICATED TO THE PUBLIC

The following are dedicated to the public domain and are intended to serve as 
prior art against any later attempt to patent them:

- the general concept of a client-side code sandbox (including but not limited 
to a browser-resident sandbox) integrated with a multi-model AI assistant 
interface presented in a dedicated interface region (including but not limited 
to a separate tab), supporting selective, independent application and reversion 
of code modifications originating from different models or model 
configurations, together with in-line or in-situ preview of each model’s 
reply before application to the existing code;
- the maintenance of interaction history as a navigable tree (or equivalent 
branching structure) in which each node is associated with a recoverable 
sandbox code state, such that selection of a node restores both the assistant 
context (in its dedicated interface region) and the corresponding code state;
- any system or method that combines multi-model AI interaction in a dedicated 
interface region, per-model selective code-change control with optional 
pre-application in-line/in-situ preview, and tree-structured history with 
node-associated code snapshots inside a client-side execution environment;
- client-side implementations using standard web or native technologies, 
optional persistence mechanisms, any form of conflict handling, any 
visualization of the history tree, any technique for representing or restoring 
code states, and any non-destructive preview technique;
- all combinations, sub-combinations, independent practice of individual 
features, and obvious variations of the foregoing, including systems in which 
one or more of the described steps or components are omitted.

Individual elements and sub-combinations are also dedicated to the public. The 
intent of this disclosure is to prevent the patenting of the described systems, 
methods, and concepts, whether claimed broadly or narrowly.

---

*This disclosure is published solely to establish prior art and to dedicate the 
described systems, methods, and concepts to the public domain. It is not a 
patent application. No patent rights are claimed. All described subject matter 
is dedicated to the public.*
