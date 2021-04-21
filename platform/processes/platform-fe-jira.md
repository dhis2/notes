# Platform (FE) JIRA Workflow

> 0. [Quick links](#quick-links)
> 0. [Workflow](#workflow)
> 0. [Filter structure](#filter-structure)

## Quick links:

-   Dashboards:
    -   [PFE: Dashboard](https://jira.dhis2.org/secure/Dashboard.jspa?selectPageId=10505)
    -   [PFE: Triage](https://jira.dhis2.org/secure/Dashboard.jspa?selectPageId=11125)
    -   [PFE: 2.37](https://jira.dhis2.org/secure/Dashboard.jspa?selectPageId=11123)
    -   [PFE: 2.36](https://jira.dhis2.org/secure/Dashboard.jspa?selectPageId=11124)
    -   [PFE: 2.35](https://jira.dhis2.org/secure/Dashboard.jspa?selectPageId=11126)
    -   [PFE: 2.34](https://jira.dhis2.org/secure/Dashboard.jspa?selectPageId=11127)
-   Filters:
    -   Base:
        -   [PFE Components](https://jira.dhis2.org/issues/?filter=10841)
        -   [PFE Issues](https://jira.dhis2.org/issues/?filter=11061)
    -   Backlog:
        -   [PFE Backlog: Triage](https://jira.dhis2.org/issues/?filter=11058)
        -   [PFE Backlog: Accepted](https://jira.dhis2.org/issues/?filter=11057)
        -   [PFE Backlog: Prioritised](https://jira.dhis2.org/issues/?filter=11028)
        -   [PFE Backlog: Planned](https://jira.dhis2.org/issues/?filter=11202)
    -   Worklog:
        -   [PFE Worklog: In progress](https://jira.dhis2.org/issues/?filter=11839)
        -   [PFE Worklog: In review](https://jira.dhis2.org/issues/?filter=11840)
        -   [PFE Worklog: Testing](https://jira.dhis2.org/issues/?filter=12037)
        -   [PFE Worklog: Failed verification](https://jira.dhis2.org/issues/?filter=11408)
        -   [PFE Worklog: Completed](https://jira.dhis2.org/issues/?filter=12038)
    -   [Search for "**PFE**" in "Search Filters" for more](https://jira.dhis2.org/secure/ManageFilters.jspa?filterView=search)

## Workflow

The JIRA workflow is based on the JIRA principles from the [Operations
Handbook](https://github.com/dhis2/operations-handbook/#jira). The
handbook is intentionally light on details so that each team can
establish principles that work for them.

What follows is how PFE implements the Agile principles for JIRA in a
Kanban-a-like model.

### Overview

0.  [PFE Backlog: Triage](https://jira.dhis2.org/issues/?filter=11058)
0.  [PFE Backlog: Accepted](https://jira.dhis2.org/issues/?filter=11057)
0.  [PFE Backlog: Prioritised](https://jira.dhis2.org/issues/?filter=11028)
0.  [PFE Backlog: Planned](https://jira.dhis2.org/issues/?filter=11202)
0.  [PFE Worklog: In progress](https://jira.dhis2.org/issues/?filter=11839)
0.  [PFE Worklog: In review](https://jira.dhis2.org/issues/?filter=11840)
0.  [PFE Worklog: Testing](https://jira.dhis2.org/issues/?filter=12037)
    -   [PFE Worklog: Failed verification](https://jira.dhis2.org/issues/?filter=11408) \
        or,
    -   [PFE Worklog: Completed](https://jira.dhis2.org/issues/?filter=12038)

### 1. Triage

All "open" tickets that PFE is reponsible for. This is the inflow of
tickets from The World.

Tickets in this filter are triaged and either rejected or accepted.

### 2. Accepted

Once an ticket passes through the triage, it is "accepted" in the sense
that it is reproducible, or a feature that makes sense, and that the
core team will look closer at it and figure out what do do with it.

It may still be rejected at this point, so "accepted" means that the
report itself has passed an initial check. It is not a guarantee that
the ticket will be worked on.

### 3. Prioritised

Given that the ticket is something that should be worked on, it needs to
be assigned a priority. It is not enough to say "low/medium/high" as we
have hundreds of tickets within each of those buckets.

To get a better idea of what the priority of an ticket should be, it is
assigned an "internal rank" between `1` and `1000`; higher number means higher
priority.

### 4. Planned

Once an ticket has an "internal rank", it can be transitioned to the
"planned" status.

At this point, an ticket is ready to be implemented.

The "planned" filter is sorted from highest "internal rank" to lowest,
and a developer should always pull the highest priority ticket to work
on.

### 5. In progress

Once an ticket has been pulled into "in progress" and work has been
started it is worked on until its completion. 

Only in exceptional cases is a developer asked to halt work on an
ongoing ticket, and focus on another ticket.

If you feel that "work is coming in from the side" and bypasses the
workflow, let the person know that you would be happy to work on it, but
that they need to go through the team leader.

If you are comfortable that the issue is critical to fix, a heads up
(over Slack or e-mail)k to the team leader explaining the situation is
enough.

### 6. In review

Issues that are ready for review show up in this filter after
transitioning from "in progress".

Ideally this is purely a checklist operation where we check:

-   That all the code has been merged to the relevant branches
-   The code has been reviewed
-   All documentation has been updated
-   The manual and automatic test suites pass
-   The information in the ticket is up-to-date and reflects the work
    that was done

### 7. Testing

The transition from "In review" to "Testing" is a handover to the QA
team for verification.

This handover comes with a contract, which is that the ticket complies
with our "[Definition of Done](https://github.com/dhis2/operations-handbook/#definition-of-done)". A short recap:

-   Implementation is complete (e.g. feature complete, automated tests)
-   Documentation is complete (e.g. updated, removed, or created)
-   Verification and validation is complete (e.g. code review ok, test
    suites pass, code de-linted)

If the ticket does not pass these criteria, but should still be moved to
"Testing", a comment must be added to the ticket with an explanation for
why the ticket is exempt from the DoD.

For example, if no documentation updates are needed, it needs to be
stated so in a comment.

#### a. Failed verification

Ticket that fail QA will be put in a "needs update" status and show up
on the "failed verification" filter. These should be considered high
priority, following our principles of prioritizing the completion of
work that has been started.

#### b. Completed

If the ticket passes QA, then it will be transition to "done" and be
visible in the "completed" filter. This is mostly used to pull out
ticket that can be demoed at the [Milestone
demos](https://github.com/dhis2/operations-handbook/#demos).

## Filter structure

Filters in PFE ("Platform Frontend") build on each other to make
administration easier.

### The building blocks

The lowest filter is "[PFE
Components](https://jira.dhis2.org/issues/?filter=10841)", which is a
filter that lists all the components that we want tickets from. The PFE
team has a lot of components we are responsible for, so listing them out
in each filter is a maintenance nightmare. If the "PFE Components"
filter is updated, the changes cascade through _all_ other PFE filters.

The "[PFE Issues](https://jira.dhis2.org/issues/?filter=11061)" filter
is used to display _all_ of the PFE tickets; past and present, open and
closed. This filter can pull in additional tickets that aren't based on
components if need be. The result should always paint a complete picture
of the responsibilities of the PFE team.

### Subset filtering

Using the "[PFE Issues](https://jira.dhis2.org/issues/?filter=11061)"
filter as a base, we can start to run queries against all the tickets to
create more specific subsets in a simple (and most importantly,
maintainable!) way.

All other filters are constructed using this principle.

-   [PFE Backlog: Planned (2.36)](https://jira.dhis2.org/issues/?filter=12025) is based on:
-   [PFE Backlog: Planned](https://jira.dhis2.org/issues/?filter=11202) which is based on:
-   [PFE Issues](https://jira.dhis2.org/issues/?filter=11061) that further filters:
-   [PFE Components](https://jira.dhis2.org/issues/?filter=10841)

### Gotchas

Always, _always_, refer to a filter by the `id`.

> :x: Bad:
> ```filter = "PFE Issues"```

> :heavy_check_mark: Good:
> ```filter = 11061```

