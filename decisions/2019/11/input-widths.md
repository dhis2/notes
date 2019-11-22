# 21/11 Meeting: Input widths

### Attending

- Ismay
- Joe
- Viktor

### Goals
- Establish a system for handling the width of input-type components  and `Field` components

### Defenitions

- **'input-type' component:** refers to `input` (single and multiline) and `select` (single and multi)
- **Field components:** refers to components that contain a `label`, `helpText`, `errorText` and input-type components


## Input width with and without status icons

- A status icon adding width to an input-type component could result in broken layouts and unintended consequences

**Conclusion:** When present, status icons will reduce the width of the sibling input

## Custom widths on input-type components

- removing the ability to control the width of an input-type element simplifies the component now and for future development (e.g. media queries and responsiveness)
- input components can inherit the width of the parent/wrapper, so apps can easily control the width

**Conclusion:** Remove `width` property from input-type components: input, select, textarea

## Custom widths on `Field`-type components

- `Field` components need the ability to define a width for the input because a label could be longer than the input (E.g. "Enter the number of dosages given" label on a 50px width input)

**Conclusion:** `Field` components to expose an `inputWidth` property that will define the width of the input-type component inside the `Field`. The width of the label/help text will be 100% and would be set by controlling the width of the wrapper/parent element.

## Minimum width on input-type components

- input type components need a minimum width to avoid cases where rendering a status icon can take so much of the width as to render the input unusable.

**Conclusion:** Input-type components to have a defined minimum width, supplied by the design team for each component.

## Actions

- @cooper-joe to supply min-width values for all input-type components (completed: [#605](https://github.com/dhis2/ui-core/issues/605))
- add `inputWidth` prop to all `Field` components
- remove `width` props from all input-type components
- ensure status icons do not add width to all input-type components
