**Date**: 2020-08-11

**Attending (speaking)**: Jennifer, Jan-Gerke, Austin, Edoardo, Birk, Martin, Joe, Christos, Milagros, ...

**Next Meeting**: September 2, 2020 @ 15:00 CET

## Agenda

1. Continuous delivery
2. Independent app release strategies
3. Dev Academy
4. SameSite cookies

## Links

DHIS2 account required.

- [Meeting recording](https://drive.google.com/file/d/16smAiZlZXQlSDUwB5JZLKYsuG27njG0h/view) 
- [CD Proposal](https://docs.google.com/document/d/1LXi2-CeIAtZwTntFcVXC1EbaUT1oLL3CEqvqcqmAr_s/)

## Notes

### Continuous Delivery

Most work to be done on the backend.

Move apps end-point away from `/dhis-web-dashboards` to
`/apps/dashboards`. That will look for local installs of the app
(through App Hub, App Management).

If not found, it falls back to the bundled version.

Consider setting up 301 redirect from `/dhis-web-dashboards` to
`/apps/dashboards`.

Any challenges? General consensus is that it should work, since
redirects happen on the browser and are respected. The redirect is
necessary.

3rd party apps will move from `/api/apps` to `/apps` to bring them
inline with 1st party apps. We need to ensure we do the right thing wrt
caching and invalidating files.

### Independent App Release Strategies

How are we going to structure releases in terms of our development and
testing process.

Proposal in [CD Proposal](https://docs.google.com/document/d/1LXi2-CeIAtZwTntFcVXC1EbaUT1oLL3CEqvqcqmAr_s/).

-   Backend won't change their process.
-   Applications won't need to worry about patch releases.
-   Libraries and Applications require new processes (see doc).
-   Tracking all versions and libraries in JIRA is tricky.

### Dev Academy

Second workshop, next week, Tuesday to Friday. Good engagement and
assignments.

Working on content, if anyone wants to join, let Austin know -- help is
always welcome !

Currently looking to hire for a new position put out for developer
advocacy and outreach.

### SameSite Cookies

See [the developer
blog](https://developers.dhis2.org/2020/08/cross-origin-cookies/) for
more information.

Chrome and Firefox are rolling out a feature that disrupts application
developers workflows, since we rely on cross-domain cookies during
development.

Looking at token based authentication for the future.
