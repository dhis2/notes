# 2019-09-12 @dhis2/team-apps Workflow Iteration

## Attending

Viktor, Hendrik, Erik, Ismay, Jan-Gerke, Birk

## Automated functional tests

There has been lots of talks about how we need to improve our test
coverages to promote software quality and stability as first-class
traits of our system.

There are some trade-offs at the start while we establish the
infrastructure for the technology and we get used to working with the
new workflow of writing feature specifications and build functional
tests. We consider this an investment that pays off itself.

At the start of 2019 there was a cross-team initiative for how to build
out our functional test infrastructure, and while it has lost momentum
and focus, Cypress was the best choice.

As for writing the "feature files", also known as specifications, we
will go for the tried-and-true [Gherkin](https://cucumber.io/docs/gherkin/) specification language used by
[Cucumber](https://cucumber.io/docs/).

An example of a feature spec:

```gherkin
Feature: Show search results in hierarchy

  Scenario: Show all already displayed units while search term is empty on focus
    Given the user focuses the search input field
    Given the user has not typed anything yet
    Then all previously visible organisation units are still displayed

  Scenario: Search result is loading
    Given the user has entered a search term
    When the results are being loaded
    Then all organisation units are hidden
    Then the loading spinner is displayed

  Scenario: Some organisation units were found
    Given the user has entered a search term
    When some organisation units were found
    Then the found units are shown
    Then the unit's path is reflected in the tree structure
    Then the unit's parents are displayed but disabled

  Scenario: No organisation units were found
    Given the user has entered a search term
    When no organisation units were found
    Then a text to inform the user is displayed
```

### Conclusion

- [Cypress](https://www.cypress.io/) for functional tests
- Specifications (feature files) using Gherkin
- Regression test specs for bugs, also using Gherkin to ensure that
  fixed bugs stay out of the system
- Does **not** replace "other" tests like unit tests
- Does replace Zephyr test cases (need to figure out how to integrate
  this with QA)
- Jan-Gerke to organise a session to demonstrate how it fits together

## Better communication across the entire frontend team regarding libraries and shared components

**Conclusion**: We are building a lot of developer tools and libraries, and need to be better at:

- Documentation, in particular surrounding the scope of what a
  tool/library should do and the design that drives it

- Talking to the entire @dhis2/front-end team about them so they get
  used widely and help us have a uniform codebase

## Lower barrier to voice chat

**Conclusion**: Sometimes it's better to take a 15 minute call over a 1
hour slack discussion when there are open-ended questions that needs to
be discussed. We have been avoiding voice chats out of perceived respect
for other's time, which is great, but sometimes the best thing is just
to have a quick call.

_Bonus: It's also nice from a team cohesion perspective to talk to
colleagues "with voice" instead of text._

## Focus on e.g. a few large refactors at a time, opting to have more devs working on the same thing

**Conclusion**: We tend to have multiple application refactors in
progress with fewer developers (often _one_). We want to shift to have a
focus on one or two "bigger" things at any time, and more developers
working on them at the same time:

- It helps with building a cohesive code base across apps
- Better team work
- Spread knowledge between apps to avoid creating information silos

## Manage discussions in dhis2/notes stricter to ensure one thing is discussed in each issue

**Conclusion**: The dhis2/notes issue tracker has been a great
improvement for having discussions over time in a more async way than
Slack allows. We have hit a problem where some issues start to deal with
multiple discussions in the same thread, which due to the linear nature
of GitHub issues makes it hard to follow along.

We need to be better at breaking out "off-topic" discussions into new
issues to track and deal with those discussions.

## Where can we keep sensitive information that's good to have but not to expose publically?

**Conclusion**: Some ideas that were bounced around included a Keybase team so we can
share more sensitive information. We already utilise Keybase encrypted
storage to share passwords, so we could use that.

Another idea was to use a DHIS2 private notes repo, but our GitHub plan
does not allow private repositories, so that's a no-go.

Keybase is viable, but no consensus around this yet.
