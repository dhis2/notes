Date: 2020-04-28\
Attendees: Ismay, Jan-Gerke, Viktor

# Agenda

Simplification and consistency of the form controls, e.g. Radio, Checkbox, Switch, Field, *Field-components.

Touched on future changes we want to explore for ui@6 as well.

# @dhis2/ui-core

- Drop the Field component
- Re-implement as a generic form field
- Refactor all *Field components to use re-implemented Field
- Move as *Field components to widgets

# @dhis2/ui-widgets

- Provide default translations and strings

# @dhis2/ui-forms

- Use more explicit style for controls instead of e.g. `options`.
- Require consumers to specify type="radio" or "checkbox".
- Component that can show error messages for a group.
- Propose to rename the forms components to have e.g. FF as a suffix: `InputFieldFF`, `TextAreaFieldFF`, etc.

# Future

- Propose to move back to string based props for status and variants: `status="error"` and `variant="primary"`.
- React-like vs. HTML-like API: https://github.com/dhis2/ui/issues/29
