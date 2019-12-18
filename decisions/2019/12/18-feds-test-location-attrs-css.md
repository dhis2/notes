# 2019-12-18 @dhis2/front-end decision board meeting

## Tests co-location with apps or in a standalone repo ([#74](https://github.com/dhis2/notes/issues/74))

**Proposal** ([replicated](https://github.com/dhis2/notes/issues/74#issuecomment-563938270)):

- Tests should live with the Application.

- We should produce TAP compatible test reports.

- We should provide a way to consolidate all tests so they can be run as
  a single verification suite for QA.

**Conclusion**: Move ahead with the proposal. There is an exceptional case
where we have cross-application tests. We'll deal with that separately.

We have apps today that do cross-app linking, which creates an
assumption that the apps are available in an instance -- which may not
be the case. We need a mechanism to handle that that is nicer than a 404
error.

## `data-test-id` attributes in Apps and Libs ([#54](https://github.com/dhis2/notes/issues/54))

Additonal discussions:

- [ui-core/#641](https://github.com/dhis2/ui-core/pull/641)
- [Slack thread](https://dhis2.slack.com/archives/CBM8LNEQM/p1575274441006700)

**Proposal** ([replicated](https://github.com/dhis2/notes/issues/54#issuecomment-563937288)):

- Use data-test as the attribute.

- Hand-written strings for the data-test attribute (no automatic
  generation).

- Components in libraries should accept a dataTest prop so that the
  data-test string can be overridden.

- Ship the data-test attribute with the production build, as there is a
  strong wish from our users to have stable ids that they can use to
  build their own test suite.

**Conclusion**: Move ahead with proposal.

## What to use for CSS styling in apps/components ([#79](https://github.com/dhis2/notes/issues/79))

**Proposal** ([replicated](https://github.com/dhis2/notes/issues/79#issuecomment-563933328)):

- **Apps**: Use **CSS Modules**
  ([`filename.module.css`](https://github.com/facebook/create-react-app/blob/0327d8952ad3bb229c26b1a1d793b42755135b84/packages/react-scripts/config/webpack.config.js#L514-L525))
  as the preferred style solution.

- **Libs**: For component libraries we still need an efficient way to
  ship CSS and markup as a unit so let's keep **Styled JSX** in UI
  libraries.

Conclusion: Move ahead with the proposal.

