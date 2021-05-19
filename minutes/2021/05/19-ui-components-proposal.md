When: 2021-05-19 @ 10:00 CET
Who: ismay, austin, viktor, médi, kai, hendrik, jan-gerke  

# Agenda

1.  Structure
2.  Feedback
3.  Next steps

# Notes

## Requirements

-   Eliminate uncertainty about where components live
-   Good experience when working on the library itself
-   Flexibility in terms of extensions, and package/component composition
-   Internal restructure to facilitate work: no breaking changes

## Potential solutions

-   Component packages ([see ui/reorg](https://github.com/dhis2/ui/tree/reorg/components))
-   Monolith packages ([see old ui/1.0.0-beta](https://github.com/dhis2/ui-core/tree/de5584950e9b7827a24d7611c7f0984d5aa366cd/src))
-   Hybrid packages
    a.  core + separate widgets ([see d2-ui](https://github.com/dhis2/d2-ui/tree/master/packages))
    b.  separate core + widgets
    c.  elements + composes ([see rejected proposal](https://github.com/dhis2/ui/pull/549))
    d.  core + widgets ([see master](https://github.com/dhis2/ui))

## Reservations against proposal (component packages)

-   Dependency management between components
    -   During development with unpublished packages, could require manual additions before publish
    -   No implicit dependencies allowed, needs to be manually controlled for now
    -   Safe-guards against different versions of peer deps that are shared

-   Mental complexity in terms of relationships between components

-   Increased build times

-   Templates for new components + e.g. commands to create them

-   Conceptually, locked versions means the actual independence is not as great as implied

## Future questions

-   Future ui-contrib packages/namespace?
-   What do we do with ui-forms?

## Next steps

-   [List pros/cons for different solutions to be aware of the trade-offs](https://docs.google.com/document/d/1CJxndnkkvA_hYq9u9PbMO_dxr-wD5_baNQRPW11VZzw/edit?usp=sharing)
-   Next meeting we will decide on the structure.
