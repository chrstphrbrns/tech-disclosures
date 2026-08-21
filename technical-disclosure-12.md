**DEFENSIVE TECHNICAL DISCLOSURE**

**Systems and Methods for Automated Classification and Routing of
Source-Code Modification Requests from Non-Technical Users Including
End-Users and Customers**

**Publication Date:** 2026-08-21
**Disclosure Number:** CB-2026-0012

---

### FIELD OF THE DISCLOSURE

The present disclosure relates generally to software development
workflows and, more particularly, to systems and methods that enable
non-technical users—including customers, end-users, product managers,
business stakeholders, and any other persons without software development
proficiency—to propose or effectuate small source-code changes
or minor feature additions while automatically determining whether a
proposed change requires review by a technical specialist, and routing
accordingly, and further providing mechanisms for the requesting user to
review, approve, reject, or request modifications to generated changes
before or after technical review.

### BACKGROUND

Existing approaches to enabling non-technical users to modify software
typically fall into two extremes: fully no-code platforms that abstract
away source code entirely (limiting expressiveness and producing
vendor-locked artifacts), or full development environments that require
technical proficiency. Systems that route non-technical requests
to technical specialists typically do so without first generating a
concrete code change, leaving the specialist to implement the change
from scratch. Further, existing systems generally do not provide a
mechanism for the original requesting user to review a generated
change in a non-technical representation and approve, reject, or
request modifications before the change is applied or reviewed by a
specialist. There is a prior-art gap for systems that operate directly
on source code, permit non-technical users (including customers or other
end-users) to initiate concrete modifications, automatically classify the
risk and complexity of each proposed change, route high-risk changes to
technical specialists, and allow the requesting user to participate in
an approval or change-request loop at one or more stages of the workflow.

### SUMMARY

Described herein are systems and methods for receiving a source-code
modification request from a non-technical user (including customers,
end-users, and any other non-developer stakeholders), automatically
generating a concrete code change from the request, automatically
classifying the request according to its estimated complexity,
scope, and risk, and either applying the modification autonomously or
routing it to a technical specialist for review. The system may further
present the generated change to the requesting user in a non-technical
representation and allow the requesting user to approve, reject, or
request modifications to the change. This requester-review step may
occur before classification, after classification but before specialist
review, after specialist review, after specialist modification, or at
any suitable point in the workflow. When require-review is determined,
the system may notify one or more technical specialists and present the
proposed change alongside contextual information. The specialist may also
approve, modify, reject, or request changes. All classification, routing,
notification, application, requester-review, and specialist-review steps
are optional and may be omitted, combined, reordered, or replaced with
equivalent mechanisms.

### DETAILED DESCRIPTION

#### General System

A system for automated classification and routing of source-code
modification requests from non-technical users may include, but is not
limited to, the following components:

- **Request Interface**: A user-facing interface through which a
non-technical user submits a source-code modification request. The term
"non-technical user" as used herein includes, but is not limited to,
customers of a software product or service, end-users of a software
application, product managers, business analysts, marketing personnel,
operations staff, domain experts, or any other person who is not
a software developer or who lacks proficiency in directly modifying
source code. The request may be expressed in natural language, through
a structured form, through voice input, through selection from a menu of
pre-defined modification types, or through any suitable input mechanism.

- **Change Generation Component**: A component configured to produce a
concrete source-code change from the user's request. This may include
generating a diff, patch, file-level replacement, or any suitable
representation of a code modification. The change generation component
may employ one or more automated code generation techniques, including
but not limited to template-based generation, rule-based transformation,
model-based generation (e.g., statistical or neural language models),
retrieval-augmented generation from existing codebases, or any suitable
combination thereof.

- **Requester Review Component**: An optional component configured
to present the generated change to the requesting non-technical user
in a non-technical representation and receive the requesting user's
disposition. The non-technical representation may include, but is not
limited to: a natural-language description of what the change does,
a before/after comparison of user-facing behavior, a visual preview
of the affected UI (rendered, mocked, or simulated), a summary of
affected files or features described in non-technical terms, or any
suitable representation that conveys the effect of the change to a person
without source-code literacy. The requesting user may approve the change,
reject the change, request modifications (e.g., by providing additional
natural-language feedback or selecting from suggested alternatives),
or defer (taking no action). The requester review component may present
multiple candidate changes and allow the requesting user to select among
them. The requester review component may be invoked at any suitable point
in the workflow, including but not limited to: immediately after change
generation, after classification but before specialist routing, after
specialist review, after specialist modification, or at multiple points.

- **Classification Component**: A component configured to evaluate the
generated change and assign a classification indicating whether the change
is likely suitable for autonomous application or likely requires human
review. The classification may be based on one or more attributes of the
change, including but not limited to: number of files affected, number
of lines changed, types of files affected (e.g., configuration, business
logic, test, infrastructure), presence of security-sensitive operations,
presence of external API calls, presence of database schema modifications,
estimated blast radius, cyclomatic complexity delta, presence of new
dependencies, modification of public interfaces, alignment with existing
codebase patterns, confidence score of the change generation component,
whether the requesting user approved or requested modifications to the
change, or any suitable attribute.

- **Routing Component**: A component configured to determine a
disposition for the change based on the classification and route the
change accordingly. Dispositions may include auto-apply, require-review,
or reject. When require-review is determined, the routing component may
select one or more technical specialists based on any suitable criteria,
including but not limited to: area of expertise, current availability,
workload, historical review latency, ownership of affected files (e.g.,
CODEOWNERS-style attribution), or any suitable criterion.

- **Notification Component**: An optional component configured to notify
selected technical specialists of a pending review. Notifications may
be delivered through any suitable channel, including but not limited
to: email, instant messaging, ticketing systems, pull request comments,
dashboard alerts, or any suitable mechanism. The notification component
may also notify the requesting user of status changes, including but
not limited to: change routed for review, change approved by specialist,
change modified by specialist, change rejected, or change applied.

- **Review Interface**: An optional component configured to present
the proposed change to a technical specialist with contextual
information. Contextual information may include: the original user
request, the generated diff, classification attributes and scores,
affected files and their ownership, test results, static analysis results,
related historical changes, the requesting user's approval or modification
request (if the requester review component was invoked), or any suitable
context. The review interface may allow the specialist to approve,
modify, reject, or request further information. When the specialist
modifies the change, the modified change may be routed back through the
requester review component for the requesting user's approval, or may
be applied directly, at the system's discretion or based on configuration.

- **Application Component**: A component configured to apply an approved
or auto-classified change to the source code. Application may involve
writing to a version control system, creating a commit, opening a pull
request, deploying to a staging environment, triggering a build or
test pipeline, or any suitable action. The application component may
require approval from the requesting user, the technical specialist,
or both before applying the change, or may apply autonomously based
on classification.

- **Feedback Component**: An optional component configured to
record the outcome of each request (auto-applied, requester-approved,
requester-rejected, requester-modified, reviewed and approved, reviewed
and modified, rejected) and feed this outcome back into the classification
component to improve future classification accuracy. Feedback may
be stored in any suitable data store and used for model retraining,
threshold adjustment, rule updates, or any suitable improvement mechanism.

#### Requester Review Workflow Detail

The requester review component may present the generated change to
the requesting non-technical user using any suitable non-technical
representation. Illustrative representations include:

- **Natural-language summary**: A plain-language description of what the
change does, what files or features it affects, and what the user will
observe differently after the change. For example: "This change updates
the text on the login page from 'Enter your email' to 'Enter your email
address'. No other parts of the application are affected."

- **Before/after behavioral comparison**: A description or visualization
of the application's behavior before and after the change, focusing on
user-observable effects rather than code-level details.

- **Visual preview**: A rendered, mocked, or simulated preview of
the affected user interface, showing the state before and after the
change. This may include screenshot comparison, live preview, interactive
prototype, or any suitable visual representation.

- **Impact summary**: A non-technical description of what files, features,
or components are affected, described in terms a non-developer can
understand (e.g., "This change affects the login page only" rather than
"This change modifies src/components/LoginForm.tsx line 42").

The requesting user may take any suitable action, including:

- **Approve**: Indicate that the change matches their intent and should
proceed.
- **Reject**: Indicate that the change does not match their intent and
should not proceed.
- **Request modifications**: Provide additional natural-language feedback
describing how the change should be altered. The change generation
component may then produce a revised change based on the original request
plus the modification feedback, and the requester review component may
present the revised change for another approval cycle.
- **Select among candidates**: When multiple candidate changes are
presented, the requesting user may select one, reject all, or request
modifications to one or more.
- **Defer**: Take no action, allowing the system to proceed based on
default behavior (which may be to proceed with classification and routing,
or to hold pending user action).

The requester review loop may iterate any number of times. For example,
the requesting user may request modifications, receive a revised change,
request further modifications, and approve on the third iteration. The
system may impose a limit on iterations or may allow unlimited iterations.

The requester review component may be positioned at any suitable point
in the workflow. Illustrative orderings include:

- **Pre-classification requester review**: The change is presented
to the requesting user before classification. If the user approves,
the change proceeds to classification. If the user rejects or requests
modifications, the change is revised or discarded before classification
resources are expended.

- **Post-classification, pre-routing requester review**: The change is
classified first. If classified as auto-apply, the change is presented
to the requesting user for approval before autonomous application. If
classified as require-review, the change is presented to the requesting
user for approval before routing to a specialist.

- **Post-specialist-review requester review**: The specialist reviews
and optionally modifies the change. The modified change is then presented
to the requesting user for approval before application.

- **Multi-stage requester review**: The requesting user reviews at
multiple points—for example, approving the initial generated change,
then approving the specialist's modifications before application.

All orderings are optional and may be combined, reordered, or omitted.

#### Classification Criteria and Thresholds

The classification component may employ one or more classification
techniques, including but not limited to: rule-based classification using
static thresholds, scoring models (linear or non-linear), machine-learned
classifiers, heuristic-based assessment, comparison against a corpus of
historical changes and their outcomes, or any suitable technique.

Classification may produce a binary disposition (auto-apply
vs. require-review) or a multi-level disposition (e.g., auto-apply,
require-review, require-senior-review, reject). Multiple classification
signals may be combined using any suitable method, including weighted
scoring, logical conjunction or disjunction, probabilistic combination,
or hierarchical rules.

Illustrative classification attributes and their use:

- **Scope attributes**: Number of files modified, number of lines
added or removed, number of functions or methods touched, depth of
call-tree impact. Higher scope values may increase the likelihood of a
require-review disposition.

- **Risk attributes**: Whether the change touches authentication,
authorization, payment processing, data deletion, external API calls,
database schema, infrastructure configuration, or other security-sensitive
or operationally critical areas. Presence of risk attributes may increase
the likelihood of a require-review disposition.

- **Confidence attributes**: A confidence score associated with the
change generation component's output. Lower confidence may increase the
likelihood of a require-review disposition.

- **Conformity attributes**: Degree to which the generated change conforms
to existing codebase conventions, patterns, and style. Lower conformity
may increase the likelihood of a require-review disposition.

- **Test coverage attributes**: Whether the change is covered by existing
or generated tests, and whether those tests pass. Lack of test coverage or
test failures may increase the likelihood of a require-review disposition.

- **Requester disposition attributes**: Whether the requesting user
approved, rejected, or requested modifications to the change (if the
requester review component was invoked). A requester rejection may trigger
re-generation rather than classification. A requester modification
request may increase the likelihood of a require-review disposition,
as iterative refinement may indicate ambiguity or complexity.

All thresholds, weights, and combination methods are configurable and may
be tuned per-repository, per-team, per-change-type, per-requesting-user,
or per any suitable dimension.

#### Change Generation Detail

The change generation component may operate on source code represented
in any suitable form, including but not limited to: plain text files,
abstract syntax trees, intermediate representations, or any suitable
representation.

The change generation component may receive, as input, any combination of:
the user's natural-language request, the current state of the relevant
source files, metadata about the repository (e.g., language, framework,
dependencies), historical changes to the affected files, existing code
patterns and conventions, modification feedback from the requesting user
(if the requester review component was invoked and the user requested
modifications), modification feedback from a technical specialist (if
the specialist modified the change), or any suitable context.

The output of the change generation component may be a diff in any
suitable format (unified diff, git diff, patch file, structured edit list,
or equivalent), a full file replacement, a set of file operations (create,
modify, delete, rename), or any suitable representation of a code change.

#### Routing and Specialist Selection Detail

When a require-review disposition is determined, the routing component
may select one or more technical specialists using any suitable
method. Selection methods may include:

- **Ownership-based**: Selecting specialists who are designated owners
or maintainers of the affected files or directories, using any suitable
ownership mapping (e.g., CODEOWNERS files, git blame attribution,
explicit team assignments, or equivalent).

- **Expertise-based**: Selecting specialists whose documented expertise
areas match the technologies, languages, or domains touched by the change.

- **Availability-based**: Selecting specialists who are currently
available, based on status indicators, calendar information, current
review queue depth, or any suitable availability signal.

- **Round-robin or load-balanced**: Distributing review requests among
eligible specialists to balance workload.

- **Escalation-based**: Routing to progressively more senior specialists
based on the severity of the classification or the number of prior
rejections.

Multiple selection methods may be combined in any suitable order or
hierarchy.

#### Specialist Review Workflow Detail

The review interface may present the technical specialist with any
suitable combination of:

- The original non-technical user's request, in its original form.
- The generated code change, rendered as a diff, side-by-side comparison,
inline annotation, or any suitable visualization.
- Classification attributes, scores, and the determined disposition
with rationale.
- The requesting user's approval, rejection, or modification request
(if the requester review component was invoked).
- Automated analysis results, including but not limited to: static
analysis output, test execution results, security scan results, dependency
impact analysis, or any suitable automated assessment.
- Historical context, including prior changes to the affected files,
prior similar requests and their outcomes, or any suitable historical
information.

The specialist may take any suitable action, including: approve
as-is, approve with modifications (editing the generated change before
application), reject with rationale, request additional information from
the requesting user, escalate to another specialist, or defer.

When the specialist modifies the change, the modified change may be
routed back to the requesting user via the requester review component
for a further approval cycle, or may be applied directly, depending on
system configuration or the specialist's explicit choice.

#### Autonomous Application Detail

When an auto-apply disposition is determined, the application component
may apply the change autonomously. Autonomous application may include
any suitable combination of: writing the change to the working tree,
creating a version control commit, pushing to a remote repository,
opening a pull request, merging a pull request, triggering a continuous
integration pipeline, deploying to a staging or production environment,
or any suitable action.

The system may enforce one or more safety constraints on autonomous
application, including but not limited to: requiring successful test
execution before application, requiring successful build before
application, limiting autonomous application to certain branches
or environments, rate-limiting autonomous applications, requiring a
cooling-off period between autonomous applications, requiring requester
approval before autonomous application, or any suitable constraint.

#### Non-Limiting Implementation Details and Variations

Any step, component, or sub-process described herein may be omitted,
combined, reordered, or replaced with an equivalent mechanism. Common
variations include, but are not limited to:

- The system may operate on a single repository or across multiple
repositories.
- The system may be integrated into an existing development platform
(e.g., a web-based code hosting service, an IDE plugin, a CI/CD pipeline,
a chat bot, a customer support portal, an in-app feedback mechanism,
or any suitable platform) or may operate as a standalone service.
- The change generation component may produce multiple candidate
changes, and the classification component may classify each candidate
independently, selecting the highest-confidence candidate that meets
auto-apply thresholds. The requester review component may present multiple
candidates to the requesting user for selection.
- The system may support iterative refinement from either or both the
requesting user and the technical specialist, with the change generation
component producing revised changes based on feedback from either party.
- The system may maintain an allowlist or blocklist of change types
that are always auto-applied or always require review, regardless of
classification output.
- The system may support user-specific or team-specific classification
tuning, allowing different thresholds for different users or teams based
on trust level, historical accuracy, or any suitable factor.
- The requester review component may be omitted entirely, with changes
proceeding directly to classification and routing without requesting
user approval.
- The notification component may be omitted entirely, with routing
instead populating a review queue that specialists check periodically.
- The feedback component may be omitted, with classification parameters
remaining static.
- The system may operate in a fully offline or air-gapped environment,
with all components hosted locally.
- The system may use any suitable programming language, runtime, storage
mechanism, communication protocol, or deployment architecture.
- The requesting user may be an external customer of a software service,
and the source-code changes may be to the software service that the
customer uses, allowing the customer to request and approve modifications
to the product they consume.
- The system may support a multi-party approval workflow, requiring
approval from both the requesting user and a technical specialist before
application, or from either one alone, depending on configuration.

#### Illustrative Examples (Non-Limiting)

**Example 1**: A customer of a web-based application submits a request
through an in-app feedback form: "Change the placeholder text on the login
page from 'Enter your email' to 'Enter your email address'." The change
generation component produces a single-line diff modifying a string
literal in a frontend component file. The requester review component
presents the change to the customer as a natural-language summary:
"This change updates the login page placeholder text from 'Enter your
email' to 'Enter your email address'. No other parts of the application
are affected." The customer approves. The classification component
determines: 1 file affected, 1 line changed, no security-sensitive areas,
high confidence, high conformity, requester approved. The disposition is
auto-apply. The application component commits the change and opens a pull
request with an auto-merge label. No technical specialist is notified.

**Example 2**: An end-user of a software product submits a request:
"Add a feature where users can delete their own account." The change
generation component produces changes across 4 files: a new API endpoint,
a database migration, a frontend confirmation dialog, and a route
registration. The requester review component presents the change to the
end-user as a natural-language summary and visual mock of the confirmation
dialog. The end-user approves. The classification component determines:
4 files affected, 87 lines changed, touches authentication and data
deletion (security-sensitive), medium confidence. The disposition is
require-review. The routing component identifies two specialists who own
the affected files and have expertise in the authentication domain. The
notification component sends each specialist an alert with a link to
the review interface. One specialist reviews the change, modifies the
database migration to add a soft-delete column instead of hard deletion,
and approves. The modified change is routed back to the requester review
component, which presents the modification to the end-user as an updated
summary: "The delete account feature has been updated to soft-delete
your account (data retained for 30 days) instead of permanently deleting
it immediately." The end-user approves the modified change, and the
application component commits it.

#### Advantages

- Enables non-technical users, including customers and end-users, to
contribute concrete, reviewable source-code changes to the software
products they use without requiring proficiency in development tools or
programming languages.
- Allows requesting users to review and approve generated changes in
non-technical representations, ensuring the generated change matches
the user's intent before technical review resources are expended or the
change is applied.
- Reduces the burden on technical specialists by automatically handling
low-risk, high-confidence, requester-approved changes without requiring
human review.
- Provides a structured, auditable workflow for determining which changes
require expert review, reducing the risk of unreviewed high-impact
modifications.
- Supports iterative refinement from both the requesting user and the
technical specialist, allowing changes to converge on a correct result
through feedback loops at multiple stages.
- Allows classification thresholds and routing rules to be tuned
per-repository, per-team, per-change-type, or per-requesting-user,
accommodating varying risk tolerances and trust levels.

### NOVEL ASPECTS DEDICATED TO THE PUBLIC

The following are dedicated to the public domain and are intended to
serve as prior art against any later attempt to patent them:

- A system for receiving a source-code modification request from a
non-technical user (including customers and end-users), automatically
generating a concrete code change from the request, presenting the change
to the requesting user in a non-technical representation, and receiving
the requesting user's approval, rejection, or modification request.
- The use of any combination of scope attributes, risk attributes,
confidence attributes, conformity attributes, test coverage attributes,
and requester disposition attributes to classify a generated code change
as auto-applicable or review-required.
- The presentation of a generated code change to the requesting
non-technical user using natural-language summaries, before/after
behavioral comparisons, visual previews, or impact summaries, and
receiving approval, rejection, or modification requests therefrom.
- The iterative refinement of a generated change based on modification
feedback from the requesting user, the technical specialist, or both,
with the change generation component producing revised changes based on
such feedback.
- The routing of a specialist-modified change back to the requesting
user for a further approval cycle before application.
- The automatic selection of one or more technical specialists for
review based on file ownership, expertise, availability, workload,
or any suitable criterion.
- The presentation of a generated code change to a technical specialist
with classification rationale, automated analysis results, historical
context, and the requesting user's approval or modification request.
- The autonomous application of classified changes subject to safety
constraints including test execution, build verification, branch
restrictions, rate limiting, cooling-off periods, or requester approval.
- The recording of review outcomes—including requester approvals,
requester rejections, requester modification requests, specialist
approvals, specialist modifications, and rejections—as feedback to
improve future classification accuracy.
- The generation of multiple candidate changes with independent
classification, requester selection among candidates, and selection of
the highest-confidence candidate meeting auto-apply thresholds.
- The use of allowlists or blocklists to override classification output
for specific change types.
- User-specific, team-specific, or customer-specific classification
tuning based on trust level or historical accuracy.
- Multi-party approval workflows requiring approval from both the
requesting user and a technical specialist, or from either one alone.
- All combinations, sub-combinations, independent practice of individual
features, and obvious variations, including systems in which one or more
steps are omitted.

---

*This disclosure is published solely to establish prior art and to
dedicate the described systems, methods, and concepts to the public
domain. It is not a patent application. No patent rights are claimed. All
described subject matter is dedicated to the public.*
