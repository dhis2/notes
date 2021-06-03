When: 2021-06-03 @ 14:00 CET \
Who: ismay, médi-rémi, austin, birk, kai, jan-gerke, hendrik, viktor

# Client-side caching

- [useSWR](https://github.com/dhis2/app-runtime/pull/828)
- [React Query](https://github.com/dhis2/app-runtime/pull/824)

## Notes

Requirements:

    -   Client side caching should be internal to the App Runtime.

        -   Important for cache normalizations and to support partial
            requests using e.g. the Gists API.

        -   Implementing React Query in all of our apps individually is
            incompatible with what the core mission of the App Platform.

Questions:

    -   Are there things that are fundamentally incompatible with what
        we want to try to do now? In the future?

    -   Is there an escape hatch to require that the data is up-to-date
        and skip the cache (force load)?

        -   https://react-query.tanstack.com/guides/query-invalidation

    -   Should we do caching at the Link layer instead, or in addition ?

Decisions:

    -   DECISION: Go with React Query integrated into the App Runtime.

        -   Better documentation.
        -   More features that we will need.
        -   Easier to remain non-breaking.

    -   DECISION: Merge it to `alpha` to start testing it by integrating
        it into Apps, to check for breaking changes, things that we have
        overseen, etc.

    -   DECISION: jan-gerke will join ismay to move this forward.

