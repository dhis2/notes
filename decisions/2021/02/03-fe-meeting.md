**Date**: 2021-02-03

**Attending**: Austin, Birk, Bjørn, Christos, Debora, Edoardo, Hendrik,
Ismay, Jan Henrik, Jan-Gerke, Jennifer, Joakim, Joe, Kai, Martin,
Médi-Remi, Milagros

**Next Meeting**: February 17, 2021 @ 15:00

# Agenda

## General updates


## Working group updates

-   **Cypress**
    
    Finishing up the PRs from December, one for codemods to help with
    upgrading consuming code bases automatically, another for the
    network shim functionality.

-   **PWA & Offline/Responsive Dashboard**

    Responsive: finished the implementation, awaiting testing to
    finalize.

    Some learnings surrounding on switching to a different component
    causes re-renders.

    Offline: changes coming in soon, so they can be tested.

    Headerbar will need changes in terms of responsiveness _and_ in
    terms of offline compability.

-   **Plugin builds**

    Based around dynamic modules, which is its own point.

-   **UI & Platform updates**

    Looking into the "drifting Tooltip" problem.

    Might be a fix possible in the Popper modifiers.

-   **Developer portal proposal and community plans**

    Revamp the developer hub to have a single place for all the
    developer docs, including blogs, guides, etc.

    Docusaurus seems like a possible candidate to replace Docsite.

    Needs a decision around Docusaurus.

    Developer outreach by meetups, inviting external devs to Slack, etc.

    Move forward with Docusaurus v2, try it out in cli-utils-docsite by
    replacing what we currently have, and see how the "default" render
    looks, then trying to roll it out to other libraries, see how that
    goes.

## Dynamic runtime modules

-   Problem: a library needs to be statically updated in each
    application on every change.

    Solution: use a federated app shell that can dynamically load
    applications and inject components so it only needs to be updated in
    one place (the shell).

-   Full documentation is available [here](https://www.dropbox.com/s/eum0j1s4mdnc0es/Dynamic%20Modules%20and%20Plugins%20-%20Spec.pdf?dl=0)

-   Demo: https://romantic-morse-3fe5bf.netlify.app

-   Enables running individual pieces of an application locally to debug
    remote applications.

-   SystemJS doesn't automatically do version detection at runtime, is
    something that we need to do through module federation in Webpack 5.

-   Next steps: works quite well, needs to be prototyped in the context
    of a real Platform application.

-   Hopefully do some more stress testing surrounding which dependencies
    are singletons (and aren't), and boundaries between modules.
    Resolving other libraries can be tricky and needs to be explored.

-   Between shell and app the interface can be light-weight, not a lot
    of coupling between them.

-   First version would be around the shell, second around the plugins,
    and third how we share common libraries without breaking changes.

-   An application is still completely self-contained, gracefully falls
    back from dynamic loading it falls back to loading the bundled
    dependencies.

-   Supports other frameworks (e.g. Angular) to be mounted in the Shell.
