**Defensive Technical Disclosure**

**Systems and Methods for Dual-Mode Expression Exploration in an Interactive 
Console, Including Data-Oriented Navigation of Selected Application Objects**

**Publication Date:** 18 November 2026  
**Disclosure Number:** CB-2026-0015

---

### Field of the Disclosure

This disclosure relates to interactive developer consoles and expression 
editors, and more particularly to console interfaces that combine conventional 
expression-completion assistance with data-oriented exploration of runtime 
values associated with a currently selected user-interface element or node.

### Background

Conventional developer consoles, expression editors, and REPL environments 
provide identifier- or token-based completion. Such mechanisms assist in 
constructing references to variables, object members, methods, and similar 
program constructs. They do not, however, provide a structured means of 
navigating the runtime value of an object as data. As a result, developers 
typically type an expression, evaluate it, inspect the resulting serialized or 
pretty-printed output, and then repeat the process to traverse nested 
structures. This multi-step workflow is especially burdensome when inspecting 
large or deeply nested objects, arrays, or other hierarchical data associated 
with a selected application element.

There remains a need for a console interface that can switch, while an 
expression is being composed, between conventional completion and a 
value-oriented explorer that reflects a selected object, supports 
keyboard-driven in-situ navigation, and can insert or update an expression path 
corresponding to the current navigation state.

### Summary

A console interface may present at least two exploration modes that can be 
toggled while a user is composing an expression. In a first mode, the console 
provides conventional completion candidates derived from identifiers, members, 
or methods available in the evaluation context. In a second mode, the console 
presents the value of a selected object or expression as a navigable hierarchy. 
The second mode may display child keys, array indices, and compact previews of 
child values; permit navigation into and out of nested objects and arrays; and 
update the composed expression so that a highlighted child or the current 
navigation position is represented by an expression path. The two modes, the 
navigation operations, the preview formatting, the expression-path updating, 
and any related features may be implemented in any combination, and any one or 
more optional features may be omitted.

### Detailed Description

#### General System

A system may include a console interface associated with a software 
application, a selection mechanism that identifies a user-selected object or 
node (for example, a canvas node, list item, table row, or diagram element), 
and an exploration module that maintains a value snapshot or live reference to 
the selected object. The system may evaluate user-entered expressions in a 
sandboxed or otherwise isolated context. The context may expose one or more 
named values associated with the current selection, such as an object 
descriptor, a result value, a run state, neighboring objects, configuration 
data, or other application-specific data. The console may be presented in a 
minimized form and expanded to a wider panel; any presentation arrangement may 
be used.

#### Dual-Mode Exploration and Mode Switching

The console may maintain at least two modes. The first mode may be a 
conventional completion mode in which entry of a character sequence causes the 
console to request completion candidates from a local completion service, a 
remote service, a language server, or any equivalent source. Candidates may be 
displayed in a selectable list, and a user may accept a candidate by pointer 
activation, keyboard activation, or automatic insertion. The second mode may be 
a data-oriented mode in which the console displays children of a value rather 
than completion candidates.

A user may switch between the modes using a predefined key combination, a 
visible mode control, a gesture, a voice command, or any equivalent control. 
The mode switch may preserve the current expression text, the current selection 
path, or both. The mode switch may be available whether or not a candidate list 
is currently displayed.

#### Data-Oriented Child Presentation

In the data-oriented mode, the console may determine children of a current 
value. For an object, children may be its enumerable or otherwise accessible 
property names. For an array, children may be numeric indices displayed using 
bracket notation. For a primitive value, the console may display the primitive 
representation and optionally treat it as a leaf. Each row may include a child 
key or index, a compact preview of the child value, and optionally a type 
indicator, kind glyph, metadata, or count. Previews may be abbreviated with an 
ellipsis after a configurable character limit. Children may be filtered, 
sorted, grouped, or annotated in any suitable manner. The presentation may 
optionally include array length, object key count, nullability, or other 
structural information.

#### In-Situ Navigation and Expression-Path Updating

While in the data-oriented mode, the console may maintain a navigation state 
comprising a root expression, a path of one or more keys or indices, and a 
selected child position. Navigation controls may move among sibling children, 
descend into a selected child that is an object or array, and ascend to a 
parent while restoring the child selection corresponding to the prior descent. 
The controls may be keyboard arrows, pointer gestures, buttons, or any 
equivalent input.

The console may display the current path in a header and update the composed 
expression to reflect the current path or the highlighted child. When a user 
confirms a highlighted child, the console may insert the full path 
expression—for example, a root followed by property accessors and bracketed 
indices—into the expression input. When the selected child is a leaf, 
confirmation may insert the current path. The path may be canonicalized, 
escaped, or formatted in any suitable notation.

#### Completion Modes and Candidate Presentation

The conventional mode may present candidates that include names available in 
the console context and, after a member-access operator, properties or methods 
of the referenced value. The candidate list may distinguish contexts, 
properties, and methods using glyphs, labels, colors, or metadata. The list may 
scroll so that a highlighted candidate remains visible and may support keyboard 
selection, pointer selection, and cancellation. The console may avoid 
presenting candidates that are not expressible in the selected access syntax, 
such as numeric array indices as member names. The console may update 
candidates asynchronously while preserving a displayed list to avoid visual 
flicker. The console may suppress presentation when there are no candidates.

#### Context Binding and Refresh

The console may bind to a currently selected object in an application canvas, 
list, table, diagram, or other interface. When the selection changes, the 
console may update the available root values, snapshot data, or live references 
supplied to the completion and exploration modules. Context updates may occur 
on selection change, value refresh, execution completion, or any suitable 
event. The context may include one or more of an object descriptor, a run 
state, a result value, neighboring objects, configuration, and application 
metadata. The console may optionally provide aliases, computed roots, or 
default roots for convenience.

#### Non-Limiting Implementation Details and Variations

Any steps, components, or features described herein may be omitted, combined, 
reordered, or replaced with equivalent functionality. The modes may be 
implemented in any suitable user-interface framework or operating system. The 
console may be embedded in a desktop application, web application, integrated 
development environment, debugging tool, or browser. The explorer may operate 
on immutable snapshots, live objects, proxies, serialized data, or virtualized 
representations. Navigation may support multi-selection, filtering, searching, 
history, bookmarks, value editing, and copy operations. The completion source 
may be local or remote. The expression input may be a single-line field, a 
multiline editor, or a command buffer. The console may optionally use 
code-generation restrictions, read-only proxies, frozen snapshots, or static 
checks to prevent mutation of explored values. Any combination or omission of 
these features is within the scope of the disclosure.

#### Illustrative Examples (Non-Limiting)

In one example, a developer is working in a browser-based application and 
selects a particular UI component (for instance, a card, form control, or list 
item) in the running interface. The console binds to the data associated with 
that selected component. The developer begins typing an expression and receives 
conventional completion candidates. They then switch to data-oriented mode. The 
console displays the top-level keys of the component’s data object together 
with compact value previews. Using arrow keys, the developer navigates into a 
nested props object, then into an items array, highlights a specific array 
element and a property within it, and confirms the selection. The full 
expression path is inserted into the console input, ready for evaluation or 
further editing.

In another example, a developer has just executed a command that returns a 
large API response object and now wishes to explore its structure without 
repeated evaluations. With the response bound as the current root value, the 
developer switches from conventional completion mode into data-oriented mode. 
The console presents the response’s child keys and abbreviated previews. The 
developer drills into a nested data array, moves among sibling indices, 
descends into one of the objects, and highlights a particular field. Upon 
confirmation, the console updates the expression input with the complete path 
(including bracket notation for the array index and property accessors), which 
the developer can immediately execute or refine.

#### Advantages

The described system reduces the number of evaluation cycles needed to inspect 
a nested value, makes object exploration available directly at the expression 
input, preserves context when switching between completion and exploration, and 
allows a selected child or current path to be converted into an executable 
expression with a single confirmation action.

### Novel Aspects Dedicated to the Public

The following subject matter is dedicated to the public domain and is intended 
to serve as prior art against any later attempt to patent it:

- A console interface that toggles between conventional expression completion 
and data-oriented exploration of a value associated with a current selection, 
including all combinations, sub-combinations, independent practice of 
individual features, and obvious variations, including systems in which one or 
more steps are omitted.
- Data-oriented exploration in which child keys, array indices, and compact 
value previews are presented as a navigable list, including filtering, sorting, 
virtualization, and ellipsis truncation.
- Navigation operations that move among siblings, descend into nested objects 
or arrays, and ascend while restoring selection state, with any suitable key, 
pointer, or gesture mapping.
- Updating a composed expression to reflect a current navigation path or a 
highlighted child so that confirmation inserts a complete expression path.
- Mode switching while an expression or candidate list is active, including 
preserving or resetting expression text and selection state.
- Context refresh upon selection change so that root values and snapshots 
correspond to the currently selected application object.
- Any combination or omission of the foregoing features.

---

*This disclosure is published solely to establish prior art and to dedicate the 
described systems, methods, and concepts to the public domain. It is not a 
patent application. No patent rights are claimed. All described subject matter 
is dedicated to the public.*
