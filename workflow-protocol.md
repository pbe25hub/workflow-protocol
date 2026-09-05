# Collaborative Development Workflow Protocol

## 1. Purpose and authority

This protocol defines a reusable collaboration workflow among the user, ChatGPT Work, and Codex for projects hosted on GitHub. It separates task design, implementation, independent review, user-controlled merge handoff, delegated merge and cleanup, and final confirmation through one governing implementation Issue, a dedicated feature branch, and a pull request. GitHub's native parent/sub-issue hierarchy may provide planning context, but it does not combine or replace these per-task workflow identities.

The workflow is designed to:

- keep each task small, safe, and reviewable;
- make the agreed implementation contract explicit;
- isolate implementation from the base branch;
- expose the complete proposed repository change to independent review;
- preserve repository-state continuity throughout implementation and correction;
- preserve an explicit user-controlled gate before delegated merge and cleanup; and
- apply without project-specific modification.

The words **must**, **must not**, **should**, and **may** are normative.

### Sources of instruction

The collaboration uses three complementary information layers:

1. [The workflow protocol](https://github.com/pbe25hub/workflow-protocol/blob/main/workflow-protocol.md) is the canonical source of truth for how the user, ChatGPT Work, and Codex collaborate.
2. The project-root `README.md` is the project-specific overview and documentation index. It owns or identifies all project-wide conventions, and every participant must follow every convention relevant to their task, including conventions for code, commit subjects, pull-request titles and bodies, final merge subjects, and other project metadata. It also points to the relevant sources of truth for architecture, implementation, testing, validation, generated-artifact maintenance, and other project-specific concerns.
3. The governing GitHub implementation Issue is the canonical implementation contract for one agreed task.

ChatGPT Work and Codex must retrieve this protocol from its canonical repository and read the consuming project's `README.md` and the relevant documents it references before planning, implementing, or reviewing a task. They must not assume that all project knowledge appears directly in `README.md`. Unless explicitly qualified otherwise, project file paths, repository state, branches, and governing Issue and pull-request identities throughout this protocol refer to the consuming project being worked on, not automatically to the protocol repository. The consuming project's README remains the owner or index of its conventions; detailed commit grammar, accepted prefixes, architecture, validation commands, and operational preferences belong there or in its referenced project documentation.

The governing implementation Issue may request an intentional change to documented behavior, architecture, or ownership, but it must not bypass this protocol. It must make the requested change and any necessary consistency work explicit. If the governing implementation Issue, this protocol, `README.md`, or referenced project documentation is missing, ambiguous, or contradictory, the party that discovers the problem must stop the affected work, describe the missing decision, and ask the user to resolve it. This does not prohibit Work from developing architecture, conventions, ownership boundaries, or sources of truth with the user. Neither Work nor Codex may silently or unilaterally resolve the gap or infer authorization. The user's agreed decision must be recorded in the governing implementation Issue before Codex resumes the affected work. Where applicable, that Issue must require Codex to update relevant project documentation before or together with implementation that depends on that decision.

### Canonical location and protocol revisions

The canonical branch URL displays the current `workflow-protocol.md` on `main`. Reviewed and merged protocol changes become available through that same ordinary GitHub file view without a separate publication workflow, site build, release, or publishing job. A fresh retrieval is required to observe updates; an existing conversation or cached copy does not automatically refresh.

At task start, Work and Codex must each retrieve the adopted protocol and verify the full source commit SHA used. Resolve the canonical repository's current `main` to a full commit SHA and retrieve `workflow-protocol.md` at that exact commit so the content and revision evidence match. Record the source repository, file path, full commit SHA, and immutable file link in the task's implementation or review evidence as appropriate: Work records its starting revision in the governing Issue or planning evidence and its reviewed revision in the required review comment; Codex records its starting revision and any reconciled revisions in the pull-request implementation evidence. The immutable link uses the verified full commit SHA in place of `main`. Recording a SHA identifies the rules used; it does not replace the moving canonical URL, create a manually maintained release, or require a publishing job.

Before every independent review, Work must freshly check the adopted protocol's current revision against the task's recorded revision and inspect any difference. Immediately before merge, Codex must freshly check it against the revision recorded in Work's approval and any documented reconciliation. These protocol checks are additional to, and do not replace or weaken, the consuming-repository continuity and exact head/base checks.

If the adopted protocol changes during an active task, Work and Codex must explicitly inspect and reconcile the change before proceeding with affected work. Record the previous and current full source commit SHAs, immutable links, the content difference, and its effect on the task, validation, review, and authorization. A source commit change with identical protocol content must also be verified and recorded. Do not silently switch rules or rely on approval assessed against materially different rules. Material changes to the implementation contract require user agreement and an explicit Issue update under Section 4; changes that materially affect the rules underlying review or authorization invalidate approval and require complete Work re-review, a new required verdict comment, and the user's forwarding of the new approval-comment link before merge. If the effect is unclear, treat approval as invalid. A verified revision change with no material effect on the applicable rules may be recorded as such, but it does not excuse any other approval-invalidating event.

If required protocol content or its revision cannot be retrieved or verified, stop the affected work and report the concrete retrieval or verification blocker. Do not silently substitute a stale cached version.

For amendments to this protocol itself, the already-adopted version governs implementation, independent review, authorization, merge, cleanup, and final confirmation of the proposed amendment. Retrieve and record that adopted source separately from the proposed PR content, and reconcile intervening adopted changes under the rules above. Proposed rules take effect only after adoption; a PR cannot use its own unmerged wording to relax its review or merge requirements.

## 2. Parties and responsibilities

### User

The user must:

- discuss and agree with ChatGPT Work on one small, coherent implementation task before its governing Issue is created or finalized;
- start a new Codex conversation for the governing implementation Issue and provide its GitHub reference;
- resolve material scope changes, unexpected repository state, conflicts, identity limitations, and authorization decisions;
- forward Work's current, unsuperseded canonical review-comment link to the existing Codex conversation when choosing to initiate the applicable correction or approved merge path;
- use forwarding of an approval-comment link as the deliberate authorization gate for only the verified merge and post-merge sequence defined by this protocol;
- forward Codex's final merge and cleanup report to Work for independent completion confirmation; and
- begin the next implementation task with a new governing Issue and a new Codex conversation.

### ChatGPT Work

ChatGPT Work, called **Work** below, is the non-implementing architect, QA engineer, independent reviewer, and advisor.

Work must:

- discuss ideas with the user and challenge them against current repository state and documentation;
- propose one small, coherent task at a time;
- create or finalize the governing GitHub implementation Issue only after the user agrees on the task;
- make the governing Issue a precise implementation contract;
- when the user has agreed to use a tracking-only parent, create and maintain that Issue and its native sub-issue relationships as accurate planning metadata;
- read the repository, governing implementation Issue, pull request, commits, checks, and relevant documentation;
- independently review the complete current pull request against the governing implementation Issue and repository;
- approve it or request concrete, scope-preserving changes;
- immediately record every completed review in a required top-level pull-request conversation comment;
- immediately provide the user a complete chat summary of that review and the canonical comment link;
- independently confirm the final GitHub-visible merge state after the user forwards Codex's final report; and
- avoid implementing its own recommendations.

Work may create and update planning and review metadata, including Issues, labels, Issue comments, pull-request comments, and review decisions.

Work must not create or modify:

- repository files;
- implementation branches or commits;
- tags or releases;
- repository workflows or settings; or
- implementation history.

Work must not merge or close a pull request.

### Codex

Codex is the sole implementation role.

Codex must:

- read the governing implementation Issue, this protocol, `README.md`, and relevant referenced documentation;
- verify repository-state continuity before creating or modifying implementation state;
- create and work on a dedicated feature branch for the governing implementation Issue;
- implement only the governing implementation Issue's agreed contract;
- follow documented architecture, ownership boundaries, and conventions;
- inspect affected project artifacts for consistency;
- perform validation appropriate to the complete result;
- commit and push the implementation only to the feature branch;
- open and maintain the pull request that represents the complete proposed change;
- address requested changes in the same Codex conversation; and
- fetch and verify the current, unsuperseded Work review comment after the user forwards its canonical link;
- execute the exact verified merge and post-merge sequence only after a forwarded approval-comment link authorizes it; and
- report state, validation, and failures honestly.

Codex must not:

- approve its own pull request;
- merge the pull request or perform post-merge cleanup before the user forwards a valid Work approval-comment link;
- implement directly on the base branch;
- silently broaden or redefine the governing implementation Issue; or
- invent or silently redefine project architecture.

## 3. Core principles

All parties must apply these principles:

- Work on one coherent task at a time.
- Prefer small, explicit, safe, and reviewable changes.
- Keep scope precise.
- Do not add speculative refactoring, unrelated cleanup, or "while I am here" changes.
- Preserve existing behavior unless the governing implementation Issue explicitly requests a behavior change.
- Use documented project patterns and sources of truth.
- Prefer simple, direct solutions over unnecessary abstraction.
- Keep implementation, tests, validation, documentation, metadata, and generated artifacts consistent where applicable.
- Keep exactly one governing implementation Issue for each task and pull request, including when that Issue is a child of a tracking-only parent.
- Use independent Work review; Codex must not act as the independent reviewer or approve its own pull request.
- Treat the user's forwarding of the current, unsuperseded canonical Work review-comment link as the role attestation and the only standing trigger for Codex's delegated merge and cleanup path.
- Make the complete proposed change visible in the pull request.
- Verify repository state and continuity at each phase.
- Protect unrelated, unexpected, staged, unstaged, and untracked content as user-owned work.
- Prefer read-only checks and dry runs when they provide sufficient evidence.
- Require explicit user authorization before mutating external runtime state unless documented project instructions clearly authorize that mutation.

Parallel read-only investigation is allowed, but it must not broaden the governing implementation Issue or combine unrelated changes.

Creating and updating the GitHub planning and review metadata assigned to each role, Work's required review-comment and final-confirmation actions, Codex's normal feature-branch, commit, push, and pull-request actions, and the narrowly defined delegated merge and cleanup sequence are authorized workflow actions once their respective prerequisites in this protocol are met. They do not authorize deployment or mutation of infrastructure, services, production data, or any other external runtime state.

When an external mutation is already fully defined and explicitly authorized, Work or Codex must attempt it immediately: the agent's next external operation must be the corresponding mutation attempt. Announcing that it will immediately perform an external action also commits the agent to making that attempt next. In either case, the agent must not insert another repository inspection, planning cycle, or preparatory status update unless genuinely new information has arisen that could invalidate the target, authorization, content, or safety of the action. The agent must identify any such information specifically and must not claim that the action is in progress or complete before attempting it. After the attempt, it must report only the result confirmed by the external system. If the action cannot be attempted, the agent must stop and report the exact blocker.

The delegated path in Sections 13 and 14 is conditional on its mandatory current-state verification. Fetching and verifying the linked comment, completing the exact pre-merge checks, and performing the required post-draft-transition reverification are parts of that authorized sequence rather than prohibited preparatory delay. Once the applicable verification passes, Codex's next external mutation must be the next authorized transition, merge, or branch-deletion action in that sequence.

When Codex requests authorization to mutate external runtime state, it must identify:

- the external system;
- the state that may change;
- why the mutation is necessary; and
- the safer read-only or dry-run alternative it considered.

## 4. GitHub Issue roles and the implementation contract

### Issue categories and hierarchy

A normal **implementation Issue** is the canonical implementation contract for exactly one small, coherent task. It governs one new Codex conversation, one dedicated feature branch, the task's commits, and one pull request through independent review, user-authorized merge and cleanup, and final confirmation.

A **tracking-only parent Issue** is an Issue that:

- represents a roadmap, initiative, or other multi-task body of work;
- tracks progress through GitHub's native sub-issue relationships;
- is planning and coordination metadata;
- is not itself an implementation contract;
- must not govern a Codex implementation conversation;
- must not receive an implementation branch, commit, pull request, or Issue-closing pull-request body; and
- may contain completed, active, and future sub-issues.

This distinction is strict: a tracking-only parent is planning metadata, while each implementation Issue is an independent implementation contract. Except where this protocol explicitly says **tracking-only parent Issue**, **parent**, or **roadmap**, the capitalized term **Issue** means the one governing implementation Issue.

Every implementation sub-issue must remain a complete, standalone implementation contract under this protocol. Each implementation child must have:

- one coherent task;
- its own new Codex conversation;
- its own dedicated feature branch;
- its own commits and pull request;
- its own Work review and canonical verdict comment;
- its own user-controlled merge authorization;
- its own merge, cleanup, and final confirmation; and
- its own Issue number in all Issue-backed commit subjects, pull-request titles, pull-request bodies, and controllable final merge subjects.

The governing child Issue number must not be replaced by the parent Issue number in implementation metadata. Native parent/sub-issue relationships do not introduce a multiple-Issue commit-subject or pull-request-title grammar and do not weaken the one-governing-Issue-per-implementation-pull-request rule.

After user agreement, Work may create and maintain tracking-only parent Issues and their native sub-issue relationships as planning metadata. Work must state prominently in every such parent that it is tracking-only and must not be handed to Codex for implementation. When Work creates or finalizes roadmap children, it must keep the parent's child list and status representation accurate. Codex may read a tracking-only parent for context, but it must act only on the separately provided governing implementation child Issue. If Codex is handed only a tracking-only parent, it must stop and request the governing implementation child Issue rather than creating implementation state.

Completing one child does not imply completion of its tracking-only parent. A child closes only through its own verified workflow. The parent must remain open while any required child remains incomplete, and Work must independently confirm the relevant child's completion before representing that child as complete in the roadmap hierarchy. Work may close the parent only after all required children are complete and the user agrees that the tracked roadmap outcome is finished. Closing a tracking-only parent must not authorize or trigger any implementation merge, branch deletion, local cleanup, or other implementation lifecycle action.

### Discussion and agreement

Exploratory discussion must remain in conversation until the design is sufficiently settled to form one coherent task. Work must not require an Issue for an undeveloped idea.

After the user agrees on an implementation task, Work creates or finalizes one governing implementation Issue in the intended repository. That Issue becomes the canonical implementation contract. The conversational handoff must contain the governing implementation Issue reference and a direction to implement it. It must not duplicate or compete with the Issue through an in-chat task specification; doing so violates this protocol. The governing implementation Issue is the sole implementation contract, even when it belongs to a native parent/sub-issue hierarchy. If a handoff includes an in-chat task specification, Codex must state explicitly that it is disregarding that specification and must not implement it. If such a message reveals a missing, ambiguous, or contradictory contract decision, Codex must stop until the user and Work resolve the decision and Work explicitly updates the Issue under the contract-change rules below. This restriction does not alter Codex's obligation to follow this protocol, `README.md`, or relevant referenced project documentation, and it does not prevent phase-specific user decisions or authorizations that this protocol expressly assigns to the user.

### Issue content

Every implementation Issue and tracking-only parent Issue created or finalized under this protocol must begin with this exact first line:

```markdown
Read and strictly follow [the workflow protocol](https://github.com/pbe25hub/workflow-protocol/blob/main/workflow-protocol.md); following it is mandatory.

```

A blank line must immediately follow that line. This requirement applies to Issues governed by this workflow and does not prescribe wording for unrelated Issues created outside it.

After that required blank line, a tracking-only parent Issue must prominently state this exact paragraph:

```markdown
Tracking-only roadmap Issue. This is not an implementation contract and must not be handed to Codex for implementation.
```

Implementation child Issues retain all implementation-contract content requirements below; the tracking-only notice does not belong in an implementation Issue.

The implementation Issue must identify, as applicable:

- the objective and rationale;
- the requested outcome;
- relevant repository context and documentation;
- the precise scope;
- constraints and invariants;
- acceptance criteria;
- validation requirements; and
- explicit exclusions or non-goals.

The implementation Issue should link to existing project sources of truth instead of unnecessarily duplicating them. Its repository and Issue identity must be unambiguous.

### Contract changes

A material change to the agreed outcome, scope, constraints, or acceptance criteria requires:

1. explicit user agreement; and
2. an explicit update to the Issue contract.

Codex must stop when such a change is proposed and must not continue until both requirements are satisfied. Codex must not infer authorization from informal, stale, ambiguous, or contradictory comments.

Implementation-level corrections that preserve the contract may be recorded in pull-request review comments. If a proposed correction changes the contract, Work must treat it as a material Issue change rather than disguising it as an implementation detail.

If the revised work no longer forms one small, coherent task, the parties must separate it into a new Issue and a new Codex conversation.

## 5. Task and conversation lifecycle

Every new implementation task begins with one agreed governing implementation Issue and a new Codex conversation. The user provides that Issue reference, and Codex uses the Issue rather than a duplicated conversational specification or a tracking-only parent as its contract.

The same Issue, feature branch, pull request, and Codex conversation remain in use for scope-preserving corrections to that task. Corrections do not create a new task.

The normal lifecycle is:

1. discussion and user agreement;
2. Issue creation or finalization;
3. Codex intake and initial-state verification;
4. feature-branch creation;
5. implementation and validation;
6. commit and feature-branch push;
7. pull-request creation or update;
8. independent Work review;
9. correction and complete re-review when required;
10. Work's required top-level review comment and complete chat summary with its canonical link after every review;
11. user forwarding of the current Work review-comment link to Codex;
12. correction and return for complete Work re-review when the linked verdict requests changes;
13. exact approval and current-state verification when the linked verdict approves;
14. draft-to-ready transition when needed, followed by state reverification;
15. guarded merge-commit merge and confirmed remote feature-branch deletion;
16. safe local post-merge cleanup;
17. Codex's complete final report;
18. user forwarding of that report to Work; and
19. Work's independent final confirmation.

The next implementation task starts with a new governing Issue and a new Codex conversation only after the current task's outcome is clear.

## 6. Repository-state continuity

Codex must establish and preserve a continuous, phase-appropriate account of the local repository, remote branches, Issue, and pull request. State inspection should be read-only wherever practical.

Continuity evidence must cover, as applicable:

- the exact GitHub repository and Issue identity;
- the active branch and current `HEAD`;
- the selected base branch and base commit;
- the feature branch and its starting and current commits;
- configured remotes, upstreams, and effective normal-push destinations;
- local and remote branch heads, ahead/behind state, and outgoing commits;
- staged, unstaged, and recursively discovered untracked content;
- the pull-request identity, repository, base branch, feature branch, and head commit SHA;
- the current Issue contract and its material edit state;
- the adopted protocol's source repository, path, full commit SHA, immutable link, and any revision-change reconciliation required by Section 1;
- the canonical linked Work review comment, its stable comment identity and material edit state, its recorded review identity, its technical verdict, and whether a later applicable verdict supersedes it;
- the pull-request title, body, validation disclosure, commit history, effective diff, mergeability, and required checks;
- generated artifacts or other state that can affect the proposed change; and
- the commit SHA and effective pull-request state to which a review decision applies;
- the confirmed merge result, merge commit, final subject, Issue state, and remote feature-branch state; and
- the matching local repository, active branch, upstreams, relevant branch heads, and working-tree state before and after authorized cleanup.

Codex must use current remote evidence when remote state matters. If access needed to establish that state is unavailable, Codex must stop rather than guess.

### Clean initial baseline

Before creating or switching to the feature branch and before editing, Codex must inspect the complete repository state. The expected baseline is:

- the repository matches the Issue's repository;
- the intended base branch is unambiguous;
- the current base commit is identified;
- `HEAD` is attached to the expected branch;
- the base branch has the expected upstream and an unambiguous remote identity;
- the locally known and current remote base state have no unexpected divergence;
- the base branch contains no outgoing implementation commits;
- the effective normal-push destination is not unexpected or contradictory; and
- the working tree has no staged, unstaged, or untracked content.

Untracked directories must be inspected recursively. Ignoring a path in a summary does not make its content safe to overwrite.

If the baseline is dirty, detached, behind, ahead, diverged, ambiguous, inconsistent with the Issue, or otherwise unexpected, Codex must stop before creating the feature branch or editing. It must report the exact condition and leave the user to decide how it is resolved.

### Feature-branch establishment

After the initial baseline succeeds, Codex may create and switch to one dedicated, Issue-related feature branch at the verified base commit. The branch name must follow documented project conventions when they exist. This protocol does not impose an exact naming formula.

Codex must verify that an existing local or remote branch with the selected identity is expected before using it. An unexpected collision, existing pull request, different starting commit, or unrelated branch history is a continuity mismatch.

A new feature branch normally has no upstream before its first push. Codex may establish only that branch's unambiguous corresponding remote ref and upstream as part of its first normal push. A missing or changed upstream after initial publication, or an ambiguous or conflicting first-push destination, requires a stop and user decision.

Immediately after branch creation, Codex must verify that:

- the active branch is the intended feature branch;
- its starting commit is the verified base commit; and
- the working tree remains clean.

### Phase-specific continuity

Before editing or resuming implementation, Codex must confirm that it is on the expected feature branch and that its base, Issue contract, and working-tree state are the expected state for the current phase.

Before committing, Codex must inspect the complete staged, unstaged, and untracked state and confirm that every change belongs to the Issue. Outgoing commits may be expected on the feature branch before publication, but they must all belong to the current Issue.

Before every push, Codex must verify:

- the active feature branch and its upstream or intended first-push destination;
- the local and remote feature-branch heads;
- the complete outgoing commit set;
- the ancestry from the recorded base commit;
- the working-tree state; and
- that a normal push will affect only the intended feature branch.

Before declaring a pull request ready for review, Codex must verify that:

- the local feature-branch `HEAD`, remote feature-branch head, and pull-request head are the same commit;
- the current remote base head and effective diff are understood, with no unresolved relevant remote change;
- the pull request targets the intended repository and base branch;
- the pull request uses the intended feature branch;
- the pull request links the correct Issue;
- all intended files and commits are pushed and visible in the pull request; and
- all remaining staged, unstaged, and untracked content has been reported.

Relevant content absent from the pull request cannot be considered reviewed. A pull request is not ready while any intended content is absent or while unexpected or unrelated working-tree content remains unresolved.

Before applying a requested correction, Codex must verify that:

- the local feature-branch `HEAD`;
- the remote feature-branch head; and
- the reviewed pull-request head

all equal the commit SHA to which the change request applies. Codex must also verify the working tree, pull-request identity, base branch and reviewed base context, and Issue contract. Any unexpected difference requires a stop before correction.

Before Codex merges through the delegated path, it must apply every exact-state verification and stop condition in Section 13. The current pull-request head and current base head must equal the exact SHAs in Work's approval record, and the repository, pull request, base branch, feature branch, Issue contract and material edit state, and complete reviewed representation must still be the recorded ones.

### Continuity mismatch

If continuity does not match the expected phase state, Codex must:

- stop before further editing, committing, pushing, or correcting;
- report the exact local, remote, Issue, branch, or pull-request difference;
- preserve all existing content and commits;
- not discard, overwrite, stash, stage, reinterpret, or silently absorb unexpected work;
- not silently pull, merge, rebase, reset, amend, force-push, rewrite history, or resolve conflicts; and
- require the user to resolve the state or explicitly authorize a safe, narrowly defined response.

User authorization for a recovery action does not preserve an earlier review. If the effective pull request changes, the complete current pull request must be reviewed again.

The draft-to-ready transition expressly authorized in Section 13 does not itself invalidate approval because it changes no reviewed implementation or substantive metadata. All other approval and continuity rules still apply, and Codex must reverify the state required by Section 13 after that transition.

## 7. Implementation and consistency policy

Codex must:

1. implement only the requested outcome;
2. preserve behavior outside the requested change;
3. follow documented architecture, ownership, naming, style, and conventions;
4. inspect every materially relevant artifact category, including implementation, configuration, tests, validation, generated artifacts, documentation, and metadata where applicable;
5. update related artifacts only when the Issue requires it;
6. avoid knowingly leaving project documentation or derived content inconsistent;
7. report materially relevant areas inspected but intentionally left unchanged, with a concise reason;
8. avoid scope expansion when documentation or architecture is insufficient; and
9. validate the complete result rather than only the latest edit.

If the current change contains unrelated concerns that do not form one coherent task, Codex must stop and report the problem. Codex must not hide it behind a broad summary, branch, pull request, or commit history.

Codex must not mutate external runtime state merely because repository implementation is authorized. Runtime validation or application that can change an external system requires the explicit authorization described in Section 3.

## 8. Validation

Validation must be proportionate to the project, task, and risk. Depending on what is affected, appropriate checks may include:

- tests;
- builds;
- linters;
- static analysis;
- format checks;
- schema checks;
- consistency checks;
- generated-file verification;
- dry runs; and
- Git status and diff checks.

Validation may occur in phases. Before commit and push, Codex must run all Issue-required local or pre-publication checks that are available and authorized, together with other proportionate available checks. It must report every relevant check that is not run, unavailable, or authorization-dependent. Checks that require a pushed commit, pull request, or GitHub environment run after publication. Opening or updating a pull request, including changing its draft status only to trigger checks, does not itself declare the pull request ready for Work review.

For every relevant validation check Codex performs or considers, Codex must report one of these states accurately:

- **Passed**: the check ran successfully.
- **Failed**: the check ran and reported a failure.
- **Not run**: Codex did not execute the check and gives the reason.
- **Unavailable**: the required tool or environment was not available.
- **Authorization required**: the check would require permission that has not been granted.

Codex must never imply that a check passed when it was not executed. Pending, running, cancelled, or otherwise incomplete GitHub checks must be disclosed using their actual GitHub state and must not be described as **Passed**. Native GitHub check states are reported separately rather than translated into the five-state vocabulary for Codex validation.

A convention violation found during Codex verification or Work review is blocking until it is resolved or explicitly handled under this protocol.

When Codex or Work verifies authored commit history, GitHub-recorded pull-request metadata, or a final merge subject, it must apply the applicable convention owned by `README.md` and compare every required Issue and pull-request reference with actual GitHub state. A missing, incorrect, unlabeled, duplicated, misordered, or unrelated Issue or pull-request reference is blocking.

An Issue-required Codex validation that does not have a **Passed** result prevents the pull request from being declared ready for Work review unless the Issue explicitly establishes another reported result as expected and acceptable. A newly failed required check or newly invalid validation evidence must be resolved or independently reassessed before merge.

A required GitHub check that is pending, running, cancelled, or otherwise incomplete prevents final review handoff and merge until it reaches an acceptable terminal state. This rule does not establish which checks a project must require.

Codex and Work must not poll an incomplete external check indefinitely. If a required external check remains pending, the agent must report its current state and wait for a new user request or an external completion signal before checking again. The pending check remains blocking wherever this protocol already makes it blocking.

Validation should be deterministic, read-only where practical, concise, and actionable. Expected outcomes and validation requirements must come from the Issue and documented, version-controlled project sources. Mutable external state may supply observed actual state, but it must not silently redefine the expected state.

Codex must validate the complete current result after every correction, not only the correction itself. The pull request must report relevant omitted checks and their reasons as well as checks that ran.

## 9. Commit and feature-branch push

Codex is authorized to commit and push implementation only on the dedicated feature branch after the continuity requirements are satisfied, pre-publication validation has been performed and reported under Section 8, and no blocking result remains. Post-publication validation then follows Section 8. Issue agreement does not authorize any implementation commit or push to the base branch.

### Commit

Before committing, Codex must:

1. inspect the complete change relative to the recorded base;
2. reconcile every staged, unstaged, and untracked path;
3. confirm that every included change belongs to the Issue;
4. confirm that all required consistency work is present;
5. review the relevant validation state;
6. stage only the intended change; and
7. verify the proposed commit message against the convention defined in `README.md`.

Codex may create one or more coherent commits appropriate to the task. Commit messages and history must accurately represent the implementation. This protocol does not impose a particular commit count. Section 13 requires the merge-commit strategy for the delegated merge path.

After each commit, Codex must inspect the actual recorded commit message and confirm that it conforms to the convention defined in `README.md`. Codex must also inspect the resulting commit, branch, and working-tree state. If staging, a hook, or the commit operation produces an unexpected change or failure, Codex must stop and report it. Codex must not silently amend, reset, or repair the result. Published commit history must not be rewritten without the user's explicit authorization.

### Push

Before pushing, Codex must apply the push continuity checks in Section 6. The push must be a normal push affecting only the intended feature branch.

The first push may create the corresponding remote feature branch and establish its upstream when the destination is unambiguous. Subsequent pushes must use the verified existing upstream. Codex must not silently change a remote or upstream.

Codex must not automatically:

- force-push;
- merge or rebase;
- reset or amend;
- resolve divergence or conflicts; or
- rewrite history.

If the push fails, Codex must preserve the local commits and report:

- the current branch;
- the local head SHA;
- the intended remote ref and upstream;
- the locally known remote head;
- the outgoing commits;
- the push error; and
- the complete working-tree state.

Codex must not silently retry or perform recovery. Before a user-authorized retry of the same unchanged push, Codex must reverify the complete relevant state. Any authorized history rewrite or force update invalidates prior review and requires independent review of the complete updated pull request.

## 10. The pull request as the review artifact

The pull request is the canonical review artifact. It replaces private or conversation-only representations of the proposed repository change.

The pull request must:

- comply with the pull-request metadata conventions owned or identified by `README.md`;
- identify the target repository, base branch, and feature branch unambiguously;
- represent the complete proposed repository change;
- contain no unrelated changes;
- provide a concise summary of the complete change;
- describe relevant consistency and architecture considerations;
- record the adopted protocol revision evidence and any reconciliation required by Section 1;
- report all Codex validation results using the status vocabulary in Section 8;
- report current GitHub checks using their native states;
- identify intentionally omitted validation and the reason;
- identify relevant documentation and generated-artifact impact;
- disclose known limitations or unresolved concerns; and
- expose the complete committed diff, commit history, and current full head commit SHA.

The title, body, changed files, commits, and validation report must coherently describe one task.

Before pull-request creation or update, Codex must check the proposed title and body against the conventions owned or identified by `README.md`. After the operation, Codex must inspect the title and body recorded by GitHub and check them against those conventions. Subject to existing authorization requirements, Codex must correct mutable nonconforming pull-request metadata before handing the pull request to Work for review.

Before marking the pull request ready for Work review, Codex must:

1. commit and push every intended file;
2. verify that local `HEAD`, the remote feature branch, and the pull-request head are identical;
3. inspect the complete pull-request diff and commit history;
4. confirm that the Issue link, base branch, feature branch, title, and body are accurate;
5. update the pull-request body with the complete current validation and consistency information;
6. confirm that the actual commit history and GitHub-recorded pull-request metadata comply with all applicable conventions owned or identified by `README.md`; and
7. report any remaining staged, unstaged, or untracked content.

A relevant file that is not committed and visible in the pull request is not part of the proposed change and cannot be reviewed. Unexpected remaining content requires the stop behavior in Section 6.

After any correction, Codex must push the additive correction commit or commits, update the pull-request body to reflect the new head SHA, verify the pull-request head, and repeat the full readiness check. Fixing published commit history through amend, rebase, or another history rewrite requires explicit user authorization; a review comment alone does not provide it.

## 11. Independent pull-request review

Work must check and reconcile the adopted protocol revision under Section 1 before every independent review. Work must review the complete current pull request, not merely the latest commit or correction. Work must read the Issue, relevant project documentation, complete diff, every changed file, commit history, validation evidence, and current checks. Work must independently inspect the actual commit history and the pull-request title and body recorded by GitHub, checking each against the conventions owned or identified by `README.md`.

The review must cover at least:

- compliance with the Issue;
- correctness and safety;
- minimality and scope;
- architecture and ownership boundaries;
- documentation consistency;
- tests and validation;
- generated artifacts;
- compatibility and drift risk;
- hidden coupling and side effects;
- complete changed-file coverage;
- pull-request title and body accuracy;
- compliance with every applicable project-wide convention owned or identified by `README.md`;
- commit-history accuracy; and
- coherence as one task.

If any relevant file or evidence is missing from the pull request, Work must withhold approval.

Work must treat a nonconforming Codex-created commit as a blocking finding, not merely a stylistic observation. Commit messages and history must continue to represent the implementation accurately.

Work must independently verify that authored commits use the applicable authored-commit form, the GitHub-recorded pull-request title uses the applicable pull-request-title form, and the pull-request body contains the required Issue-closing syntax when applicable. Work must also verify that the planned final merge subject uses the applicable pull-request-bearing form; that any referenced Issue is the governing child implementation Issue rather than a tracking-only parent; and that every Issue and pull-request number matches actual GitHub state. `README.md` owns the grammar and detailed formatting rules for these forms.

### Review decision and identity

A review decision applies only to the exact:

- GitHub repository;
- pull request;
- base branch and full reviewed base commit SHA;
- feature branch;
- Issue contract and its material edit state at review time; and
- reviewed full head commit SHA.

The review evidence must also identify the adopted protocol's source repository, file path, full commit SHA, immutable source link, and any reconciled revision change under Section 1.

After every complete independent review, Work must immediately add a top-level pull-request conversation comment that states one technical verdict: **approved** or **changes requested**. Posting this required comment is an authorized Work review-metadata action and does not require separate user authorization.

The required comment must identify at least:

- the technical verdict;
- the adopted protocol revision evidence and any reconciliation required by Section 1;
- the GitHub repository and pull request;
- the governing Issue and its material state;
- the base branch and exact reviewed full base commit SHA;
- the exact reviewed feature branch;
- the exact reviewed full head commit SHA; and
- the findings or confirmation supporting the verdict.

An approval comment must state that approval applies only to the recorded review identity and is invalidated by any applicable state change. A changes-requested comment must identify every concrete, scope-preserving finding, the required correction, and the requirement for complete re-review after correction.

When distinct GitHub identities support it, Work may additionally use a formal GitHub approval or request-changes review. A formal review does not replace the required top-level comment, and a formal protected-branch approval is not required by this protocol.

Because Work and Codex may operate through the same GitHub identity, GitHub identity alone may not prove which role authored a comment. The user's forwarding of the required comment's canonical link to the existing Codex conversation serves as the role attestation and authorization boundary.

Once Work posts the required comment, that canonical comment itself, including its stable GitHub comment identity, content, and material edit state, becomes part of the review identity. A later complete required Work review comment for the same repository, pull request, Issue and material state, base branch and reviewed base SHA, feature branch, and reviewed head SHA supersedes every earlier verdict for that review state, even when the head and base SHAs are unchanged. Work and Codex must treat only the latest applicable required verdict comment as current.

After posting the comment, Work must immediately summarize the complete review result in chat so the user does not need to open the pull request to understand it. The chat response must include the canonical link to the posted comment. Work must not wait for another user request before posting the comment or providing this summary.

If Work cannot complete the review or post the required comment, it must report the exact blocker and must not leave a chat-only approval or change request that Codex could treat as actionable. Work's technical approval does not itself merge the pull request; only the user's later forwarding of that exact approval-comment link initiates and authorizes the verified delegated path in Section 13.

### Approval invalidation

Any of the following invalidates a previous approval:

- a new commit on the feature branch;
- a force update or other history rewrite;
- a pull-request base-branch change;
- any movement of the base branch after review, whether or not it appears materially relevant;
- a material change to the Issue contract; or
- an adopted protocol change that materially affects the rules underlying review or authorization, or whose effect is unclear, under Section 1;
- a material change to the pull-request title, body, validation disclosure, or other reviewed representation;
- deletion, replacement, or material editing of the canonical approval comment; or
- a later applicable required Work verdict comment, including one for the same head and base SHAs.

A newly failed required check also prevents reliance on the earlier approval until Work reassesses the complete current pull request. If it is unclear whether a change affects the reviewed result, approval must be treated as invalid.

Approval never transfers from an earlier head SHA, base SHA, canonical comment, or review identity to a later one. Work must review the complete current pull request again after an invalidating event and must produce a new required top-level comment and complete chat summary with its canonical link.

## 12. Requested changes and correction

When the user forwards a canonical Work comment whose verified verdict requests changes, Codex must fetch the actual linked GitHub comment and verify that its canonical comment identity and material edit state, repository, pull request, Issue and material state, base branch and reviewed base SHA, feature branch, and reviewed head SHA match the intended correction identity. Codex must fetch the complete current pull-request conversation and verify that no later applicable required Work verdict comment supersedes the forwarded comment. Codex must not rely only on quoted, pasted, summarized, or reported comment text. If Codex cannot determine whether a later comment is an applicable Work verdict, it must stop rather than act on a potentially stale review.

When Work requests changes, it must:

- identify each concrete problem;
- state the required scope-preserving correction;
- distinguish implementation correction from a material contract change; and
- require validation of the complete corrected result.

If the correction would change the outcome, scope, constraints, or acceptance criteria, the user must agree and Work must update the Issue before Codex continues.

Before correcting, Codex must perform the correction continuity check in Section 6. Unexpected differences among the local branch, remote feature branch, reviewed pull-request head, base branch, or Issue contract require a stop and user decision.

When continuity matches, Codex must:

1. apply only the requested correction;
2. preserve the rest of the agreed implementation;
3. validate the complete updated result;
4. create an accurate additive commit or commits;
5. push normally without unauthorized history rewriting;
6. update the complete pull-request body and validation report; and
7. repeat the pull-request readiness checks.

Work must then review the complete updated pull request at its new head SHA. Review of only the correction delta is insufficient.

Every complete re-review must produce a new required top-level Work comment and a new complete chat summary containing that comment's canonical link. The new canonical comment is a new review identity and supersedes every earlier verdict for the same review state. An earlier approval or change request does not transfer to a later canonical comment, head SHA, base SHA, or review identity.

If a requested commit-history correction requires amend, rebase, force-push, or another rewrite, Codex must stop for explicit user authorization. Any authorized rewrite produces a new review identity and requires a complete new review.

## 13. Merge authorization and final continuity

Codex may commit and push only to the dedicated feature branch as part of implementation or correction. Nothing may reach the base branch until Work has approved the exact review identity and the user has forwarded the canonical approval-comment link to the existing Codex conversation.

The forwarded link is the deliberate user-controlled gate. Forwarding it explicitly initiates and authorizes only the verified merge and post-merge sequence in Sections 13 and 14. Until the link is forwarded, Codex must not merge or perform post-merge cleanup. Issue agreement, Work approval without the forwarded canonical link, and quoted, pasted, summarized, or reported comment text do not authorize this sequence. Work must not merge or modify repository implementation state.

### Approval-comment verification

Codex must fetch the actual GitHub comment identified by the forwarded canonical link. It must verify the stable GitHub comment identity, content, and material edit state; that the linked comment is the intended Work approval record; and that the recorded repository, pull request, governing Issue and material state, base branch and exact reviewed base SHA, feature branch, and exact reviewed full head SHA match the intended identities. Codex must fetch the complete current pull-request conversation and verify that no later applicable required Work verdict comment supersedes the forwarded approval, including when a later verdict records the same head and base SHAs. If Codex cannot determine whether a later comment is an applicable Work verdict, it must stop rather than merge. Because GitHub identity alone may not distinguish Work from Codex, the user's forwarding of the canonical link is the role attestation; it does not excuse any comment, content, supersession, or continuity mismatch.

### Exact pre-merge verification

Immediately before merge, Codex must fetch current evidence and verify that:

- the linked comment is the actual, unchanged, and latest applicable Work approval record for the intended repository and pull request;
- the adopted protocol revision has been freshly verified against the approval's recorded revision, with any change inspected and reconciled under Section 1 and no unresolved effect on the applicable rules or approval;
- the repository, pull request, governing Issue, base branch, and feature branch match the recorded review identities;
- the current full head SHA exactly equals the approved head SHA;
- the current full base SHA exactly equals the reviewed base SHA;
- the Issue contract and its material edit state are unchanged;
- the pull-request title, body, validation disclosure, commit history, and effective diff remain the reviewed representation;
- the pull request is mergeable and has no merge conflict;
- every Issue-required validation has an acceptable result; and
- no required GitHub check is failed or incomplete.

Any base-branch movement after review invalidates approval for this delegated merge path, even when it appears unrelated. Codex must stop and require a fresh complete Work review rather than deciding whether the movement is materially relevant. Any other mismatch, blocker, missing evidence, or approval-invalidating event must also stop the merge. Codex must report the exact condition and must not silently repair, reinterpret, or bypass it.

### Draft-to-ready transition

If the approved pull request remains a draft after every pre-merge check passes, Codex must mark it ready for review as an authorized merge-preparation action. This transition alone does not invalidate approval because it changes no reviewed implementation or substantive metadata. Codex must then fetch current evidence again and reverify at least the exact current head SHA, exact current base SHA, adopted protocol revision and any required reconciliation, mergeability, conflict state, and required checks before merging.

### Guarded merge commit

Codex must merge the approved pull request using GitHub's merge-commit strategy. It must not use squash-and-merge or rebase-and-merge for this delegated path.

Immediately before executing the merge, Codex must determine the governing implementation Issue, if any, and the actual pull-request number; construct the final merge-commit subject using the convention owned by `README.md`; inspect the resulting subject; and explicitly set it where the merge interface permits. Codex must not duplicate that convention's grammar in this protocol.

The merge operation must be guarded by the exact approved head SHA. If GitHub cannot guarantee the expected head or the required final subject, Codex must stop rather than merge with ambiguous metadata. Codex must treat GitHub's confirmed merge result and resulting merge commit SHA as authoritative, then inspect GitHub's recorded final subject and verify that it conforms to the convention owned by `README.md`. A failed or ambiguous merge attempt, or a nonconforming recorded subject, does not authorize a retry, branch deletion, cleanup, or any silent recovery.

This delegated path mandates only its merge-commit strategy. This protocol does not otherwise mandate branch-protection configuration, an exact feature-branch naming convention, separate bot identities, or required-check configuration.

### Remote feature-branch deletion

Only after GitHub confirms that the pull request merged successfully may Codex ensure that the exact reviewed remote feature branch is deleted. If GitHub deleted it automatically, Codex must verify its absence. If it still exists, Codex may delete exactly that reviewed feature branch under this standing authorization and must verify its absence afterward.

Codex must not delete any other remote branch and must not force-delete the reviewed branch. A merge failure does not authorize any branch deletion. A remote-deletion failure must stop local cleanup and be reported as a partial outcome.

## 14. Completion

Merge success, remote-branch cleanup, local cleanup, and final Work confirmation are separate outcomes. A successfully merged pull request alone does not complete the implementation task.

### Safe local post-merge cleanup

Only after GitHub confirms the merge and the remote feature branch's absence may Codex perform local cleanup in the matching repository. Before cleanup, Codex must verify that the local repository, active feature branch, working tree, remotes, upstreams, and relevant local and remote branch heads match the expected reviewed and merged state. Unexpected staged, unstaged, recursively discovered untracked, divergent, detached, or mismatched state requires a stop before cleanup.

When continuity matches, Codex must:

1. fetch from the intended remote and prune deleted remote refs;
2. switch to the local base branch;
3. fast-forward it to the verified remote base using a fast-forward-only operation;
4. delete the local feature branch using safe merged-branch deletion; and
5. verify the final synchronized clean state and local and remote feature-branch absence.

Codex must not automatically:

- force-delete a local or remote branch;
- reset, rebase, merge locally, stash, discard, or overwrite content;
- resolve divergence or conflicts;
- rewrite history; or
- broaden cleanup beyond the exact Issue feature branch.

If a cleanup step fails or exposes unexpected state, Codex must stop, preserve the repository, and report the exact partial outcome. A successful merge must not be misreported as fully completed cleanup. Completed merges and their published history must not be rewritten without the user's explicit authorization.

### Codex final report

After the authorized merge and cleanup sequence ends, Codex must provide a complete chat report that identifies:

- the repository, governing Issue, and pull request;
- the linked Work approval-comment identity;
- the Work-approved full head SHA and reviewed full base SHA;
- the actual merge status, merge strategy, merge commit SHA, and final subject;
- the Issue state;
- the remote feature-branch state;
- the local active branch and its synchronization with the remote base;
- the local feature-branch state;
- the complete working-tree state;
- required-check and validation state where applicable;
- every cleanup action completed; and
- any failure, partial completion, remaining concern, or state Work cannot independently verify.

Codex must distinguish GitHub-confirmed facts from locally observed facts. The linked Issue may close through the pull request's closing relationship; Codex must report its actual state and must not silently close it or other project metadata.

### Final Work confirmation

The user forwards Codex's complete final report to Work. Work must then independently inspect and confirm all GitHub-visible state, including the reviewed approval identity, merged pull request, approved head, resulting merge commit and subject, governing Issue state, remote feature-branch state, and relevant final checks or concerns.

Work must assess the completeness and internal consistency of Codex's reported local evidence but must explicitly state when it cannot independently observe the local repository. Work must summarize the final confirmation in chat. The Issue implementation task is complete only after this final Work confirmation.

As part of that confirmation, Work must independently verify that GitHub's recorded final merge subject uses the applicable pull-request-bearing form owned by `README.md`, references the governing child implementation Issue rather than a tracking-only parent when applicable, and contains Issue and pull-request numbers that match actual GitHub state.

If the final state is incomplete or contradictory, Work must report the exact remaining work rather than confirming completion. If the user declines or cannot initiate the delegated path, or if any step fails, the parties must report the actual outcome. The next implementation task begins with a new governing Issue and a new Codex conversation only after the current task's outcome is clear.

## 15. Exceptional states

Codex and Work must apply these stop conditions consistently:

- **Dirty initial baseline:** Codex stops before branch creation or editing and reports all staged, unstaged, and untracked content.
- **Wrong or ambiguous repository or Issue:** Work or Codex stops until the canonical identities are resolved.
- **Insufficient or contradictory documentation:** The party that finds the gap stops and asks the user for the missing decision.
- **Unavailable or changed adopted protocol:** Work or Codex stops affected work when required protocol content or its full source revision cannot be retrieved or verified, reports the concrete blocker, and does not substitute a stale cached copy. An intervening revision requires explicit inspection and reconciliation under Section 1, with contract updates and complete re-review where applicable; proposed protocol amendments cannot authorize themselves.
- **Ambiguous base branch, remote, upstream, or destination:** Codex does not guess or configure an unintended destination.
- **Unexpected divergence or outgoing base commits:** Codex does not include, merge, rebase, reset, or otherwise reinterpret them.
- **Unexpected local or remote feature-branch state:** Codex stops before editing, correcting, or pushing.
- **Unrelated or multiple concerns:** Codex does not combine them into a misleading branch or pull request.
- **Material contract change:** Codex stops until the user agrees and the Issue is explicitly updated.
- **Failed required validation or incomplete required check:** Codex reports the state and does not declare the pull request ready unless the Issue explicitly defines a validation failure as expected and acceptable. An incomplete required GitHub check must reach an acceptable terminal state.
- **Unavailable or authorization-dependent evidence:** Codex reports the exact limitation instead of implying that validation or continuity succeeded.
- **Commit failure or unexpected hook mutation:** Codex preserves and reports the resulting state without automatic repair.
- **Push or pull-request update failure:** Codex preserves commits, reports local and remote state and the error, and performs no silent retry or recovery.
- **Review or comment-posting failure:** Work reports the exact blocker and leaves no chat-only verdict that Codex may treat as actionable.
- **Missing or unverifiable forwarded comment:** Codex does not act on quoted, pasted, summarized, inaccessible, ambiguous, or mismatched review text.
- **Superseded or ambiguously current forwarded verdict:** Codex fetches the complete current pull-request conversation and does not correct, transition, merge, delete, or clean up unless the forwarded canonical comment is the latest applicable required Work verdict, including when later comments record the same head and base SHAs.
- **Correction continuity mismatch:** Codex does not apply the correction until the user resolves the difference.
- **Conflict:** Codex does not resolve it without explicit user authorization.
- **Invalidated approval or moved base:** Codex does not merge or judge relevance; Work must completely review the current pull request and create a new required comment before the user may forward a new approval link.
- **Pre-merge mismatch or unavailable evidence:** Codex reports the exact condition and does not repair, reinterpret, bypass, or merge.
- **Draft-transition mismatch:** Codex stops if the required post-transition head, base, mergeability, conflict, or check evidence no longer matches.
- **Merge failure or ambiguous result:** Codex performs no silent retry, branch deletion, or cleanup and reports the GitHub-confirmed state.
- **Remote feature-branch deletion failure:** Codex stops before local cleanup and reports the confirmed merge separately from incomplete remote cleanup.
- **Dirty or mismatched local cleanup baseline:** Codex preserves the repository and does not switch, update, stash, discard, or delete anything.
- **Fast-forward or safe local-branch deletion failure:** Codex stops without reset, rebase, local merge, force deletion, or other recovery and reports every completed cleanup step.
- **Incomplete or contradictory final state:** Work reports the exact remaining work and does not confirm task completion.

Unexpected repository, branch, history, destination, conflict, identity, or authorization decisions belong to the user. Neither Work nor Codex may discard user work or silently recover through destructive cleanup, rebasing, resetting, amending, history rewriting, force-pushing, or conflict resolution.

## 16. End-to-end workflow

This end-to-end workflow applies separately to every implementation task, including every implementation child of a tracking-only parent. It does not apply to the tracking-only parent itself.

1. Work retrieves and records the adopted protocol revision under Section 1; the user and Work discuss an idea against current consuming-project repository state and documentation.
2. Once the idea forms one small, coherent task, the user agrees on it.
3. Work creates or finalizes the governing implementation Issue as the canonical implementation contract.
4. The user starts a new Codex conversation and provides the governing implementation Issue reference.
5. Codex retrieves and records the adopted protocol revision under Section 1 and reads the Issue, this protocol, the consuming project's `README.md`, and relevant referenced documentation.
6. Codex verifies the clean initial repository, selected base branch, remotes, upstream, destination, and local and remote continuity.
7. Codex creates the dedicated governing-Issue-related feature branch at the verified base commit.
8. Codex implements only the governing Issue contract and validates the complete result.
9. Codex commits the coherent implementation and normally pushes only the feature branch, establishing its unambiguous upstream on the first push when necessary.
10. Codex opens or updates the pull request, links the governing implementation Issue, verifies that all intended content is committed and pushed, and reports complete validation and working-tree state.
11. Work checks and reconciles the adopted protocol revision, independently reviews the complete current pull request, and immediately posts the required top-level verdict comment bound to the exact review identity with protocol revision evidence.
12. Work immediately gives the user a complete chat summary and the canonical link to that comment.
13. The user forwards the canonical Work comment link to the existing Codex conversation.
14. Codex fetches and verifies the actual linked GitHub comment, its stable identity and material edit state, and the complete current pull-request conversation rather than relying on reproduced text; a later applicable required Work verdict supersedes it even when the head and base SHAs are unchanged.
15. If the verified comment requests changes, Codex verifies correction continuity, applies only scope-preserving corrections, validates the complete result, creates additive conforming commits, pushes normally, updates the pull request, and returns it for complete Work re-review.
16. Every complete Work re-review produces a new required top-level comment and complete chat summary with its canonical link; earlier approvals do not transfer.
17. If the verified comment approves, Codex freshly checks and reconciles the adopted protocol revision immediately before merge and verifies exact equality of the current and reviewed head and base SHAs and every other approval, Issue, pull-request representation, mergeability, validation, and check prerequisite.
18. If the approved pull request is a draft, Codex marks it ready and reverifies the current head, base, adopted protocol revision and any required reconciliation, mergeability, conflict state, and required checks.
19. Codex inspects and, where permitted, explicitly sets a conforming final subject, then performs a merge-commit merge guarded by the exact approved head SHA.
20. After GitHub confirms the merge, Codex verifies or performs deletion of only the reviewed remote feature branch.
21. After remote deletion is confirmed, Codex verifies the local cleanup baseline, fetches and prunes, switches to the base branch, fast-forwards it only, safely deletes the merged local feature branch, and verifies the final clean synchronized state.
22. Codex provides the complete final report, distinguishing GitHub-confirmed from locally observed facts and distinguishing merge success from cleanup success.
23. The user forwards Codex's final report to Work.
24. Work independently confirms all GitHub-visible final state, accurately limits claims about local state, and summarizes its conclusion in chat.
25. The task becomes complete only after Work's final confirmation; the next implementation task then begins with a new governing Issue and a new Codex conversation.
