**Date**: 2020-11-24

**Attending**: Jan-Gerke, Ismay, Austin, Viktor, Joe, Hendrik

## Agenda

-   Way forward for the UI Icons package

## Links

-   Initial PoC: https://github.com/dhis2/ui/pull/304
-   SVGr PoC: https://github.com/dhis2/ui/pull/313
-   Allow setting componentName when using svgr-cli: https://github.com/gregberge/svgr/issues/501
-   Example showcase: https://dhis2.github.io/design-specs/ui-icons-platform/index.html 

## Background

Joe created hundreds of icons that should be used in DHIS2 applications
and libraries, and we need to come up with a way to use and distribute
the SVG icons without manually converting all of them to React
components.

The first proof-of-concept
[discussed](https://github.com/dhis2/ui/pull/304) was to generate React
components based on template strings, and the
[follow-up](https://github.com/dhis2/ui/pull/313) was to do it
using SVGr that relies on abstract syntax trees to generate components.

## Notes

-   We will go ahead with the
    [SVGr](https://github.com/dhis2/ui/pull/313) CLI based approach, and
    eventually move to the Node API if we need more control.

-   We will move forward with the simplest API:

    -   Size in the name
    -   Variant in the name
    -   Color needs to be a prop

    E.g. `<IconDown24 color="#fff" />`, `<IconAddCircle16 />`

-   A noted downside with svgr cli is that we cannot modify the
    `componentName`
    
    Pending feature request: https://github.com/gregberge/svgr/issues/501

-   We will generate the React components from the SVGs at build time,
    and **not** include the generated React components in the VCS.

-   CRA supports importing svgs directly, but we cannot rely on all
    consumers having a specific file-loader setup.

    For such setups we distribute the optimized SVG files in the bundle,
    so they can be referenced directly.

    This could be used for e.g. Angular apps as well.

-   We settled on using number sizes in the component names, though we
    have the option of adding e.g. small/medium/large variants down the
    line if we see the need for it or if it makes the DX better.

-   Would the UI Icons be helpful for Android? Yes, but it's not a top
    priority to figure out right now.

-   We are including padding in the SVG icon file, for the reason that
    there is a content area within the icon so that there is room for
    e.g. another variant to have additional weight.

    We accept that alignment may not always be perfect.

-   Distribution:
    
    -   Include the Sketch file in ui-icons as the "source"
    -   Include the optimized svgs in the npm package
    -   Include the generated React components in the npm package

-   We will want some form of showcase for our icons in the docs, e.g.
    https://dhis2.github.io/design-specs/ui-icons-platform/index.html

-   We will have a breaking change in UI so that we can move icons from
    ui-icons to components that need them, implement the svgr PoC, and
    then switch out the icons to the re-usable ones.

-   Ismay will take the lead to move this forward.
