**Date**: 2020-06-30

**Attending (16)**: Austin, Birk, Christos, Edoardo, Erik, Hendrik, Ismay, Jan, Jan-Gerke, Jennifer, Joakim, Joe, Lars, Martin, Milagros, Wahed

**Next Meeting**: Wednesday, August 5 @ 15:00 CET

## Agenda

- Proposal Ratification
  - [PeerDeps for wrapped external dependencies](https://github.com/dhis2/notes/issues/67)
  - [PeerDeps for Singletons](https://github.com/dhis2/notes/issues/67)
  - [Release Strategy](https://github.com/dhis2/notes/issues/101) - slower, avoid major releases where possible, not **complete** until propagated
  - [Jira vs. GH Issues](https://dhis2.slack.com/archives/CDX5CE15W/p1592488981276700)
  - Managing workload and context switching (see below)

## Links

(DHIS2 account required)

* [Meeting Recording](https://drive.google.com/file/d/1CPkBMWMy38iNu62K6FgiVYvANxmEw6mg/view)

# Notes

## Good News - Developer Workshop

- Successfully hosted first online DHIS2 application developer workshop last week!
- 30+ participants from 19 countries
- Huge thanks to Jan-Gerke, Hendrik, Christos, Milagros, Lars, and Wahed as well as Matthieu, Alice, and Grant for making this possible!
- Some room for improvement in preparing for the August workshop

## Proposals

### PeerDependencies for Wrapped External Dependencies

Notably applies to `prop-types`, `final-form`, and `react-final-form`

**Proposal**: Leave as-is for now, wrap and re-export dependencies from libraries that are clear extensions of an external library.
However, plan a formal investigation into the advantages and challenges of moving to peer dependencies for a later major release (across libraries)

**Status**: Approved

**Next steps**: Plan investigation into implications of moving to peer dependencies in a future major version

### PeerDependencies for Singletons

Notably applies to `react`, `react-dom`, `styled-jsx`, `@dhis2/app-runtime`, `@dhis2/d2-i18n` (until deprecated), `@dhis2/ui` or `@dhis2/ui-core`. 

**Proposal**: Always use peerDeps for things that MUST be singletons. Include these as dependencies in the app.

**Status**: Approved

**Next steps**:
1. Migrate all libraries to use peerDeps for singletons
2. We should evaluate a way to bundle transitive dependencies through `app-shell`

### Fewer, smaller major library releases

Notably applies to `ui`, `ui-*`, `app-platform`, `app-runtime`, `d2-i18n`, and `analytics`

**Proposal**: Follow these rules for major releases:

1. Any library release cannot be considered "complete" until it has been propagated to **every dependant library and app**.  Only at that point can Jira issues requiring changes to that library be marked complete and moved into testing.
2. Scope of major releases should be minimized - we should **not** combine many breaking changes into one release, and we should 
3. Breaking changes should be avoided, if possible, in favor of stability and API extensions.  Silent breaking changes (like renaming components or libraries and overloading a previously-used name) are forbidden unless absolutely necessary.  The goal is to fully understand the implications of a breaking change on **the entire DHIS2 ecosystem** before committing (and propagating) it.
4. Use pre-releases to test and validate breaking changes before actually cutting a major release
5. However, be disciplined when using `alpha` and `beta` channels - they shouldn't be long-lived to avoid scope creep
6. Define and use milestones to scope major releases (possibly in Jira, see below)
7. Try to keep unrelated features and fixes out of major releases to minimize scope creep

**Status**: Approved

**Next steps**:
1. Ensure we have pushed ui v5 to the entire ecosystem
2. Define a re-usable library release procedure and steps
3. Create a tool to show up-to-date version propagation status across the ecosystem

## Discussion - Jira vs GitHub

Current situation and challenges:
1. Jira is **and will remain** the canonical place for user-facing changes in DHIS2, but is not configured in a way that makes it possible to track library issues yet.
2. GitHub has become the place for technical, developer-facing issues.  Library releases are not easily connected to application or core releases, however.
3. It is increasingly difficult to keep track of issues in multiple places
4. We do not currently have a solid mechanism for linking Jira and Github issues together
5. High-level visibility into development progress is somewhat obscured by having issues in GitHub without links to Jira
6. Harder to find external contributors if issue tracking is in Jira and farther removed from the code in question
7. Hard to describe and talk about technical (code) APIs in Jira
8. Proposal: Discussions and proposals should maybe live in GitHub before moving to Jira
9. See DQ app proposal Jira issue

**Next Steps**: 
1. [Propose issue tracking procedure](https://docs.google.com/document/d/1AJxiNU1nJQxSPoC6BHsa8TkMaxLC85kbyQ9C8iaaUGQ/edit#) (Austin, contributions welcome)
2. Incorporate feedback from non-dev stakeholders (Austin)
3. Ratify proposal in next Frontend meeting (August 4)
