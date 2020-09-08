# 2.35: View user authority changes

In version 2.35, the impact of the existing authority for viewing users called `F_USER_VIEW` has changed.

## Context

DHIS 2 is currently being too liberal in allowing users with little privilege access to user information. At the same time, certain web apps require access to user information to function properly. There is a need to balance the concern of privacy and usability of apps.

To accommodate apps which need access to user information, a new API endpoint has been added at `/api/userLookup` , which offers a minimal representation of user information. This endpoint is open for all authenticated users, and web apps should prefer to migrate to this endpoint.

## Impact

The impact of this change is the following:

* Exporting user metadata through the `/api/metadata` endpoint now requires the `F_USER_VIEW` authority.
* Accessing the `/api/users` endpoint still requires the `F_USER_VIEW` authority (no change in behavior).
* User roles which are intended for end users, i.e. not user administrators, should no longer include the `F_USER_VIEW` authority. All apps including the Tracker Capture app (except the user management app) now use the user lookup API and no longer requires the `F_USER_VIEW` authority. This applies to the tracker capture app and the messaging app.
