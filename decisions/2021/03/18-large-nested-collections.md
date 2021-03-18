JIRA:

-   DHIS2-10699

Use cases:

1.  Browsing and editing in bulk
2.  Finding and changing a single option

Solution needs to scalable on backend/frontend.

-   Need a way to do paging

-   Scalable way to load and update a collection
    -   PUT requires the full payload
    -   PATCH allows partial updates
    -   Smaller more constrained API responses, large collections always 

-   Referenced embedded objects

-   JSON Patch spec
    -   Could be implemented in App Runtime
    -   Nice interface between frontend and backend

-   Collections API works well, but updating the main object without
    sending along the entire nested collection.

-   Separating requests leads to consistency issues.
    -   Worried about consistency for updating (single api call)
    -   Not worried about it for reading data (multiple api calls)

Design doc:

-   https://docs.google.com/document/d/1qyAHE1VNqbljpXVYmO6fND6L-cq7_QiZlC5tDN0GAAQ/edit#

Decision:

-   Morten looks JSON Patch
-   Jan looks into the API
-   New meeting in a few weeks
