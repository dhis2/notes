# DHIS2 Notes

In [dhis2/notes](https://github.com/dhis2/notes) you will find:

-   Decisions
-   Meeting minutes
-   [Discussions](https://github.com/dhis2/notes/discussions)
    -   [Gotchas](https://github.com/dhis2/notes/discussions/categories/gotchas)
    -   [Agendas](https://github.com/dhis2/notes/discussions/categories/meetings)
    -   [Q&A](https://github.com/dhis2/notes/discussions/categories/q-a)
    -   [Specs and RFCs](https://github.com/dhis2/notes/discussions/categories/specs-rfcs)

Templates:

-   [Agendas](https://github.com/dhis2/notes/blob/master/TEMPLATE_AGENDA.md)
-   [Minutes](https://github.com/dhis2/notes/blob/master/TEMPLATE_MINUTES.md)

# Process

## Discussions and Proposals

Create an issue in GitHub so it can be discussed in the issue, and then a
[decision](#decision) will be taken in a meeting if necessary.

The limitations of GitHub Issues work to our advantage here, as there
are no threads within topics, so each issue MUST only discuss a single
topic.

If the topic derails or spawns a new side-discussion, that must be moved
to its own issue.

## Meeting minutes

Any type of minute from an ad-hoc meeting that has a conclusion should
be added here for posterity,

- stating who was in the meeting,
- what was disussed, and
- the conclusion.

This way e.g. two developers can discuss and decide on something
quickly, and push a PR for the rest of the team to read. If something
comes up during the PR, then it can be caught and changed before too
much time has passed.

This allows for two developers to move quickly, while keeping the team
informed about decisions taken underway that can be reviewed without
calling a meeting with the entire team.

## Decisions

A discussion should happen on an async basis, which enables everyone to
contribute at their own schedule and leisure. The team should be
comfortable with knowing that no decisions "just happen" so they have to
be reading Slack throughout the entire day.

Instead we trust that if there is a decision as a result of a meeting
we were not privy to, a PR with the outcome will be available to read
and comment on before decision is final.

# Structure for minutes and decisions

1. Create a markdown file with the date
   `DD-{keywords-describing-meeting}.md` as the name, under the correct
   directory `YYYY/MM`.

2. Raise a PR to get it approved and/or discussed, and finally merged
   from some of the meeting participants.

If you would like to see an example of how a meeting minute or decision
document can look, see [TEMPLATE.md](TEMPLATE.md).
