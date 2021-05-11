When: April 21, 2021 @ 13:00 CET
Where: Remote
Who: Hendrik, Médi-Rémi, Edoardo, Ismay, Kai, Jan-Gerke, Austin

# Agenda

## Programmatic handling of state

-   No documentation on the current way of handling callbacks

-   Programmatic handling of open/close states

    -   Prefer props over state

-   Consider the cost/benefit of breaking compatibility.

SUGGESTION: We could have different signatures for ui-elements and
ui-composes.

SUGGESTION: For next major version of UI switch event signature for
callbacks to `(event, payload) => {}`.

DECISION: To avoid breaking the callback signature for components when
refactoring them into "style components", we can wrap the on-handlers in
the components so they use the `(payload, event)` signature but still
allow prop-spreading and forwardRef.

DECISION: Where possible pass the `event` value, and where not, we
replicate native behaviour and return `next` value.

## UI path forward

Development and progress on the UI library has stalled as it is hard
to strike the right balance of composition to remain flexible for
known and unknown use cases.

Clear goals for the UI library are needed to be able to make
decisions that take us in that direction.

What can we do that furthers our goals, but doesn't trigger breaking
changes?

NEXT ACTION: Schedule a UI breakdown workshop to figure out a way
forward: https://calendar.google.com/event?action=TEMPLATE&tmeid=MW4zb21icm9pYjFtMjJqZzJiMnI4MTI4M3AgY19hZWJwb2xrbWZ2YW5qY2ZnZjhmOTZibmJpOEBn&tmsrc=c_aebpolkmfvanjcfgf8f96bnbi8%40group.calendar.google.com
