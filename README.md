# Workflow protocol

This repository is the canonical home of a project-agnostic development collaboration protocol for the user, ChatGPT Work, and Codex on GitHub.

- The user agrees on tasks, resolves decisions, and authorizes merge and cleanup by forwarding Work's current canonical approval-comment link.
- Work creates or finalizes Issues, independently reviews the complete pull request, and confirms completion.
- Codex implements on a dedicated feature branch, validates, opens and maintains the pull request, and performs the guarded merge and cleanup only after the required authorization.

## Canonical document and adoption

Read and strictly follow [the workflow protocol](https://github.com/pbe25hub/workflow-protocol/blob/main/workflow-protocol.md); following it is mandatory.

The canonical URL displays the current `workflow-protocol.md` on `main` through GitHub's ordinary file view. Reviewed and merged changes become available at that same URL without a separate publication workflow, site build, release, or publishing job. Retrieve it afresh to observe updates: an existing conversation or cached copy does not automatically refresh. Full source commit SHAs and immutable file links in task evidence identify the rules actually used; they do not replace the moving canonical URL or create manually maintained releases.

To adopt the protocol, a consuming project should explicitly record its adoption and link to the canonical document from its README or applicable instructions. Work and Codex retrieve the adopted protocol at task start, record and check its revision as the protocol requires, and also read that project's README and relevant referenced documentation. Future implementation and tracking-only roadmap Issues use the protocol's exact mandatory opening, with the additional tracking-only notice where applicable. Each implementation task uses the consuming project's own Issue, branch, commits, and PR.

The consuming project's README remains the owner or index of its conventions, architecture, validation commands, and operational preferences. Adoption does not relocate that documentation. Publishing this repository does not automatically migrate existing homelab tasks, consumers, or ChatGPT project instructions; that migration is separate work.

## Provenance and bootstrap authority

The complete protocol was imported from repository `pbe25hub/homelab`, path `docs/ai/workflow-protocol.md`, at commit `29085a8a68916969d86afd59d9ed4f986e8238ab`: [immutable source document](https://github.com/pbe25hub/homelab/blob/29085a8a68916969d86afd59d9ed4f986e8238ab/docs/ai/workflow-protocol.md). This is the adopted version after homelab PR #56. Only the document is imported; its intentional adaptations establish the shared source location, consuming-project context, and protocol revision handling.

This repository uses the protocol for its own development. For the initial extraction, [this repository's Issue #1](https://github.com/pbe25hub/workflow-protocol/issues/1) explicitly adopts the pinned homelab source above as the one-time bootstrap authority. That already-adopted version governs implementation, independent Work review, the user's forwarded approval-comment link, guarded merge and cleanup, and final confirmation of this extraction. The proposed document cannot authorize its own adoption. Homelab Issue #55 and PR #56 are provenance only; this repository's Issue and actual PR govern the extraction.

The canonical `main` file URL does not exist until the initial PR merges. During review, validate the document through the implementation PR's feature-branch file view and immutable head link. After the authorized merge, verify that the canonical URL is publicly accessible and matches the approved result, and obtain Work's independent final confirmation. After that verified adoption, the merged canonical document governs subsequent development; later amendments are reviewed and authorized under the already-adopted version, with proposed rules taking effect only after adoption.

## Development conventions

This README owns this repository's development conventions. Maintain ordinary Markdown with one physical source line per prose paragraph, without hard wrapping. Preserve line breaks in structures whose meaning depends on them, including lists, tables, code blocks, and explicit line breaks.

Use a dedicated Issue-related feature branch and a PR targeting `main`. Never implement directly on `main`. Keep amendments scoped to the agreed Issue and follow the adopted protocol's merge-commit strategy, independent review, authorization, and cleanup requirements.

### Change metadata

Accepted prefixes are `docs` for documentation changes and `chore` for maintenance. Use `docs` for this bootstrap implementation. Prefixes are lowercase, followed by a colon and one space. Summaries must be concise, imperative, accurate, and have no trailing period.

Authored commits and PR titles use these forms:

```text
<prefix>: <imperative summary> (issue #<governing-issue-number>)
<prefix>: <imperative summary>
```

The first form applies to Issue-backed work, including all correction commits; the second is the general form for work without an Issue. A PR title summarizes the complete change. Authored feature-branch commits and PR titles must omit their own PR number, including after a PR exists. Do not rewrite history to add that number.

Final merge subjects use these forms once the actual PR number exists:

```text
<prefix>: <imperative summary> (issue #<governing-issue-number>, pr #<actual-pr-number>)
<prefix>: <imperative summary> (pr #<actual-pr-number>)
```

The first form applies to Issue-backed merges; the second applies to merges without an Issue. These general metadata forms do not authorize bypassing the protocol's governing-Issue requirement for implementation tasks. Inspect and explicitly set the final merge subject as required by the protocol.

The labels `issue` and `pr` are literal and lowercase. Append references in one parenthetical block, with the governing Issue first and the actual PR second when both apply, separated by a comma and one space. Numbers must match this repository's actual GitHub identities. A tracking-only parent must not replace the governing implementation child. Missing, incorrect, unlabeled, duplicated, misordered, or unrelated references are nonconforming.

An Issue-backed PR body must separately include GitHub closing syntax for the governing Issue, such as `Closes #1` for this bootstrap task. Title metadata does not replace the closing reference. The body must describe the complete change, protocol revision evidence, validation results and omissions, and relevant limitations. Verify authored subjects and GitHub's actual recorded PR title and body before review, and the planned and actual final merge subject at the appropriate merge phase. These conventions apply prospectively; they do not require rewriting the repository's initial commit or other completed history.

### Validation

Validation is proportionate to this documentation repository:

1. For the initial extraction, compare the complete imported protocol against the pinned source, enumerate and review every intentional adaptation, and verify that every existing section and safeguard remains. For later amendments, compare against the adopted revision and agreed Issue.
2. Check Markdown structure, paragraph wrapping, references, the exact mandatory Issue opening, and the distinction between moving canonical links and immutable evidence. Trace an ordinary consuming-project task, an in-progress protocol revision change, and a protocol-amendment PR to verify authority and review requirements.
3. Inspect the complete scoped diff and staged, unstaged, and recursively discovered untracked content. For Issue #1, only `README.md` and root-level `workflow-protocol.md` may change.
4. Run `git diff --check` before commit; check the complete committed PR diff as well. Verify authored commit metadata, GitHub-recorded PR metadata and closing reference, and the planned final merge subject against the actual governing Issue and PR.
5. Validate the feature-branch document during bootstrap review; after authorized merge, confirm the public canonical document matches the approved result. Work must independently review the complete PR and independently confirm completion.

This repository has no documentation generator, build, test suite, or configured CI workflow at bootstrap. Documentation generation is not applicable unless an existing applicable mechanism is discovered. Report checks that ran and any omitted, unavailable, or inapplicable checks accurately; do not claim a build, generation step, or automated check passed when none ran. No publishing mechanism is required.
