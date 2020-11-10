**Date**: 2020-11-10

**Attending**: Jan-Gerke, Joakim, Jennifer, Christos, Ismay, Jan,
Martin, Viktor

## Agenda


- Overwriting Cypress functions in general
- Helpers to make it easier to get a `data-test` selector?
- [data-test attribute as class names](https://github.com/dhis2/notes/issues/90)
- [data-test attribute naming convention](https://github.com/dhis2/notes/issues/88)

## Notes

### `data-test` attributes

#### Naming

When it comes to naming conventions, we have good experiences using
prefixes for libraries to avoid collisions. For applications collisions
are not a problem, so using prefixes there is overkill.

The outcome is that `data-test` attributes should be hyphen-separated
groups with an optional prefix. Hyphens indicate hierarchy, so any
hyphens in the prefix are dropped.

Examples:

```
# library

dhis2-ui-chip
dhis2-ui-chip-remove
dhis2-ui-multiselect

# application

menu
menu-item
menu-item-button
```

#### Classnames

This turned out to be a non-issue, as there are alternative attribute
selectors we can use to target words inside of a `data-test` attribute.

E.g. given:

```
<div data-test="dhis2-component navigation" />
```

We can use both:

```
[data-test~="dhis2-component"]
[data-test~="navigation"]
```

### Developer documentation

We need to expand the docs for our Cypress utilities. It is very sparse
right now.

### Cook book/Recipes in the Cypress docs

As we iterate on our test code with Cypress, we need to take the time to
outline recipes in a "cook book" section under
cli-utils-cypress.dhis2.nu to allow us to extract useful patterns into
our toolkit for Cypress.

### Overwriting Cypress functions and Cypress helpers

As long as we attempt to use the order of selectors:

0.  label
0.  placeholder
0.  text contents
0.  alt text
0.  title
0.  display value
0.  role
0.  test ID

There is nothing preventing us from adding helper functions to make
test id selectors more ergonomic.

We reached a general consensus on adding new Cypress commands is
preferable over extending existing Cypress commands, so e.g. our
`Cy.get` extension would become, e.g. `Cy.getExpand`.

We also agreed on producing a breaking change and providing a codemod to
automate the migration.

This opens up the option of adding our own `Cy.containsExact` functions
in `@dhis2/cypress-commands`.

We also discussed the possibility of extending the current `get` /
`getExpand` with a `getLike` for a "contains match" (rather than an
"exact match" that the regular `get` provides). With a corresponding
extension for `find` -> `findLike` as well.

Example 

> getBySelLike yields elements with a data-test attribute that contains
> a specified selector.

Source:
https://docs.cypress.io/guides/references/best-practices.html#Real-World-Example
