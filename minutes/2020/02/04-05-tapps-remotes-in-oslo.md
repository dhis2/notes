# 2020-02-04 and 05

This minute is different than the others in the sense that we did not
take comprehensive notes during the multiple days of meetings, so this is a
recollection at best, and erroneous at worst. Either way, it does not
attempt to be a detailed document.

It does attempt to capture the overall themes and outcomes.

# Retrospective and planning

During the retrospective we touched on what works well, and laid plans
for the week.

## Remote culture

The problems [we
discussed](https://github.com/dhis2/notes/blob/master/decisions/2019/11/11-tapps-meeting-remote-errors-etc.md#remote-culture)
in November are still real, but there is an attitude that we are working
on them and cultural changes that time, so we don't expect any
short-term miracles.

@varl still needs to draft the remote principles into a document. Give
it a name and it is easier to absorb and talk about.

## Testing

We are improving our automated test suites and actively investing in
that area to support the overall long-term plan from management on
stability and robustness.

We have an open agenda (as opposed to hidden) that we want to replace
Zephyr-tests (manually executed) with Cypress (automatically executed)
to better support the QA team and processes.

## Team work

We have a good vibe going on, and are better at using the right forum
for communication (Slack vs. dhis2/notes vs. VoIP).

We still fall into the trap where a developer works solo on a large
project, and we want to pair up more to tackle the large projects in
[listed in the agenda](https://github.com/dhis2/notes/issues/89).

We have many examples of apps that have been written by a single dev,
and do not make sense to any other developer. We consider it one of the
root causes of our maintainability challenges.

# Testing and strategy

Since this was a big topic we set aside a day for it. We went over some
proposals, either directly or touched on them during discussions:

- [#90](https://github.com/dhis2/notes/issues/90)
- [#88](https://github.com/dhis2/notes/issues/88)
- [#85](https://github.com/dhis2/notes/issues/85)

## Unit vs. End-to-End

We decided that not everything needs to be a Cypress test, but
user-driven behavior should be tested end-to-end.

For more implementation detail oriented tests, we should prefer Jest.

The important take-away is that we have tests -- and Jest vs. Cypress
is left for consideration of the implementers and reviewers.

There is a preference towards testing behavior, including `onEvent`
handlers, through Cypress, as that is a more realistic test than through
simulated events.

## Toolkits

We have decided to standardize on Jest over alternatives such as Tape
and Lab for business logic.

Cypress is prefered over Selenium, WebDriver, etc. We have a [utility
library](https://github.com/dhis2/cli-utils-cypress/) to setup Cypress
with the recommended DHIS2 configuration.

We want to be able to generate TAP-compliant reports though for reasons
outlined in [previous
decisions](decisions/2019/12/18-feds-test-location-attrs-css.md).

# Refactor party

The second large meeting we had was the refactor party, in which we went
over each considerable project we are currently refactoring to bring
everyone on the team up to speed on them.

First reason is to raise awareness that these things are going on, and
the second reason is to yield enough of an understanding that other devs
can jump in and help out. See [Team Work](#team-work).

## Maintenance app

Primary dev: @Mohammer5

We discussed our strategy of doing inter-app linking between new and
old, and decided to forgo that strategy, instead going for an
incremental replacement that can be installed side-by-side with the
existing app.

1. This allows the community to come with feedback on the changes.
2. This minimizes the amount of overhead for organisations to re-create
   their training material.
3. This allows us to come up with better ways how to represent the
   information.

Tracked through:

- https://github.com/dhis2/mar-y/

## Import/Export app

Primary dev: @awgaan

This is a rewrite of the Import/Export app that is based off of the App
Platform.

We discussed some UI changes, and brought in @cooper-joe for the ride.

Tracked through:

- https://jira.dhis2.org/browse/DHIS2-8169
- https://github.com/dhis2/import-export-app/pull/385

## Scheduler app

Primary dev: @ismay

Went over current state of the refactor, what is blocking, what is
outstanding, and the overall structure.

The status is tracked through:

- https://jira.dhis2.org/browse/TECH-214
- https://github.com/dhis2/scheduler-app/pull/23

## App Hub

Primary devs: @erikarenhill, @birkbjo

Went over structure, and overall architecture of how the App Hub works,
and how it communicates with DHIS2.

The status is tracked through:

- https://jira.dhis2.org/projects/HUB

# Additional projects not covered

One week goes by fast, and we did not have a chance to cover:

- Continuous app delivery; next steps?
- Removal of core-resources-app
- Updating the headerbar across all apps
- Porting apps to App Platform
- Approvals app
- SMS app
