# 2019-11-11 @dhis2/team-apps Meeting

## Attending

Viktor, Austin, Jan-Gerke, Ismay, Hendrik, Birk, Erik

## Maintenance App Refactor

We are ready to work on it and have started prototyping: https://github.com/dhis2/mar-y/

Not currently a priority, but it is something we need to spend time on when we
can.

Getting it up to a technical standard we can maintain is the first priority,
switching out UI components to the DHIS2 ones.

When it comes to improvements and functional changes to the Maintenance
application, it is a bit stickier, as any changes to the Maintenance
application triggers a lot of work related to updating training materials and
training for people. We should gather requirements and write specs for changes
we think would be inline with our way of work.

Input from the field from Austin:

- Import/Export app cannot import GML
- Import/Export app is used to configure dhis2 instead of the Maintenance app

## Error reporting

Related issues:

- https://github.com/dhis2/notes/issues/76
- https://jira.dhis2.org/browse/DHIS2-5400
- https://jira.dhis2.org/browse/DHIS2-3481

What we want to do is:

- Extend the functionality of the Usage Analytics app

- Build a library so that applications can report various metrics
  that get visualised in the usage analytics app.

- Extend the APIs for the usage analytics to enable additional
  metrics (requires backend work).

- Collect the data at the instance level and iteratively add more
  features. "Send data to DHIS2 Core Team" can be a later feature.

Next step is to schedule a meeting to set up a proposal to anchor the
discussion across teams in a context.

## Positioning engine and feature files

Tricky to write perfectly the first time.

Nice to have to steer discussions and keep them on topic and relevant.

### Actions

1. Focus on the functionality we need
1. Use that to drive the decision on what engine to use
1. From there decide on how to implement the components

## Remote culture

Concerns with regards to the remote culture:

- Feeling of being disconnected to discussions that happen in Oslo.

- Hard to get a timely response from other teams.

There is an understanding that these problems make sense from a historical
perspective, but if DHIS2 is going to move forward with a remote-friendly
organisation then we need to continue to put in the work to improve the
situation.

### Actions

- On an individual level, try to reach across teams and make contact.

- Other teams use Slack differently and do most of their talking in direct
messages.

- Would be nice if people that get a lot of questions set up a "question hour"
in their calendar where they are known to be available.

- Cross-team (Frontend/Backend) meetings.

- Favour open communication over private.

- Passive information streams are helpful for awareness of what is going on.

- Open communication channels should be preferred over closed.

- Document remote principles

## Documentation

We need different types of documentation. Good example:
https://www.divio.com/blog/documentation/

Questions that should be considered:

- How do we introduce externals to our ecosystem?

- How do we give a technical reference?

- How do we give a FAQ for common problems?

### Actions

- Identify documentation gaps.

- Clarify scope for libraries.

- Contribution documentation.

- A way to find the developers portal from dhis2.org.

- Document what the point of the dev portal is on the first page (better landing page).

## General thoughts for future discussions

- How do we keep ourselves accountable to our decisions?

- Quarterly team focus meeting for contextualising our work

- Roadmaps for the entire app platform (includes ui libraries, etc.)
