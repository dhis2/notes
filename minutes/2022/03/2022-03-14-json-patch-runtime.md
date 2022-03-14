# JSON Patch support in App Runtime

Attending: Austin, Médi-Rémi, Austin

Proposal and reference for discussion: https://github.com/dhis2/app-runtime/pull/1023

Proposal **A**: Add an explicit JSON Patch type alongside 'create', 'update', 'delete'.

Proposal **B**: Expand "CRUD" with a "P" (patch)

Proposal **C**: Replace "CRUD" abstraction with arbitrary types

## Rationale:

Proposal **B** and **C** were rejected on the technical grounds that they require more work to implement and
adopt as they are breaking changes.

Proposal **A** still allows for **B** and **C** in the future using a deprecate/adopt/remove strategy, and
has a significant benefit of being a clean code change that is determined to be safe and low-risk.

## Decision:

Given that no identified options are lost to us in the future by going with **A** now, coupled with the
benefits of a clean and simple implementation the decision reached is:

- Add explicit type for JSON Patch (proposal **A**).
- Name should be: `json-patch` (lower case and slug).
- Released as a new feature and can be gradually adopted where JSON Patch is supported.
- Intent to deprecate the `partial` flag for `update`, however intentionally kept out-of-scope for this PR.
