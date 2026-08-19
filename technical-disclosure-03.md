**Defensive Technical Disclosure**  
**Title:** HTML Sandbox with Multi-Model AI Chat Window Supporting Selective Per-Model Code Modifications and Navigable Branching Conversation History Tree  

**Publication Date:** 2026-08-19
**Disclosure Number:** CB-2026-0003

**Field**  
Web-based software development tools, specifically browser-resident HTML/CSS/JavaScript sandboxes augmented by artificial-intelligence assistance. The disclosure addresses a single integrated system that combines live code editing and preview with a multi-model chat interface.  

**Background**  
Conventional HTML sandboxes provide an editor and live preview but lack native multi-model AI interaction. Existing AI coding assistants typically operate with a single linear chat thread and apply code changes in an all-or-nothing fashion. They do not support independent application or reversion of suggestions originating from different models, nor do they expose the conversation as a navigable tree that preserves distinct code states at each node. The present disclosure describes a practical browser-based system that supplies exactly those capabilities.  

**Summary of the Invention**  
A self-contained HTML application (or set of HTML/CSS/JS files) that renders:  
- a code editor and live preview sandbox, and  
- a chat window capable of simultaneous or sequential interaction with a plurality of AI models.  

Each model may propose code modifications. The user can selectively apply or revert the modifications of any individual model without affecting the others. Conversation history is maintained as an explicit tree; the user may branch from any prior node, revisit any node, and cause the sandbox code state to restore to the state associated with that node.  

**Detailed Description**  

1. **Core Components**  
   - Sandbox pane: a text editor (for HTML, CSS, and/or JavaScript) together with an iframe or shadow-DOM live preview that reflects the current code state.  
   - Chat pane: a scrollable message list and input field that can address one or more remote or local AI models (identified by model name, endpoint, or API key).  
   - State manager: an in-memory (or IndexedDB-persisted) structure that stores both the conversation tree and a versioned snapshot of the sandbox code at every node.  

2. **Multi-Model Interaction**  
   - The user may select any subset of available models and issue a prompt to all of them concurrently or to a chosen subset.  
   - Each model returns a response that may contain natural-language text and/or one or more proposed code diffs (unified diff, search-replace blocks, or full-file replacements).  
   - Responses are visually distinguished by model identity (color, avatar, or label).  

3. **Selective Application and Reversion of Code Modifications**  
   - For every code-bearing response the system extracts the proposed modifications and presents them with per-model controls: “Apply”, “Revert”, and optional “Preview”.  
   - Applying a modification from model A updates only the portions of the sandbox code that model A proposed; modifications previously applied from model B remain intact unless they overlap, in which case a conflict marker or three-way merge UI is shown.  
   - Reverting a model’s modifications restores the exact prior code fragments that existed before that model’s last apply operation, leaving all other models’ applied changes undisturbed.  
   - The system maintains an independent undo stack per model so that successive applies and reverts from the same model can be stepped through independently.  

4. **Conversation History Tree and Navigation**  
   - Every user message and every model response is recorded as a node in a tree.  
   - A branch is created whenever the user elects to reply to a non-leaf node or explicitly chooses “Branch from here”.  
   - Each node stores:  
     – the full chat messages visible at that point,  
     – the complete sandbox code snapshot that resulted from all applies performed up to that node, and  
     – references to its parent and children.  
   - A tree-view or graph visualization (collapsible outline, mind-map, or timeline) allows the user to click any node. Selecting a node:  
     – restores the chat pane to the messages that existed at that node,  
     – restores the sandbox editor and preview to the exact code snapshot stored with that node, and  
     – updates the set of currently applied per-model modifications to match the state recorded at the node.  
   - The user may continue the conversation from the restored node, thereby creating a new child branch, or may prune, merge, or rename branches.  

5. **Implementation Notes (enabling detail)**  
   - The entire system is realized with standard web technologies (HTML, CSS, JavaScript) and may run entirely client-side; model inference occurs via ordinary fetch/XHR calls to external or local endpoints.  
   - Code snapshots may be stored as plain strings, as operational-transformation patches, or as content-addressable hashes to minimize memory.  
   - Conflict detection on overlapping edits uses conventional longest-common-subsequence or line-based diff algorithms.  
   - Persistence across page reloads is optional and may employ localStorage, IndexedDB, or a downloadable JSON export of the tree.  
   - No server-side component is required beyond the AI model endpoints themselves; the sandbox, chat UI, selective-apply logic, and tree navigation execute wholly inside the browser.  

**Industrial Applicability**  
The system is immediately usable by any web developer, educator, or hobbyist who works with HTML/CSS/JavaScript inside a browser. It optimizes the single operational task of iteratively refining sandbox code under the guidance of multiple AI models while preserving the ability to explore alternative conversational and code paths without irreversible commitment.  

Publication of the foregoing description places the architecture, the per-model selective apply/revert mechanism, the conversation-history tree, the node-associated code snapshots, and the navigation semantics into the public domain, thereby establishing prior art against any later patent application directed to the same or an obvious variant of an HTML sandbox that combines multi-model AI chat, selective code-change control, and branchable conversational history.
