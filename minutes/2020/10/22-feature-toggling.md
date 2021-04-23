**Date**: 2020-10-22

**Attending**: Christos, Jan-Gerke, Hendrik, Ismay, Jan Henrik, Edoardo,
Austin, Viktor, Jennifer, Milagros, Martin, Birk, Joakim, Bjørn

## Agenda

1.  Feature toggling based on Server Version

## Links

-   [Recording (DHIS2 account required)](https://drive.google.com/file/d/1T3mZkaTrVTLczz9tEFjMpzZoUPlhxaAD/view?usp=drivesdk)
-   https://github.com/dhis2/app-platform/issues/381

## Notes

-   We don't lose the ability to backport and use version branches.

-   We do want to move away from backporting.

-   Getting full benefits would involve building it into the App
    Platform and rolling it out wide scale before we need to create
    version branches.

-   Challenges related to when working with in memory data structures,
    they need to be version agnostic.

-   Complex applications may have trouble with this, and Redux
    applications may have problems as well.

-   Normalization of data from the API.

-   Do this going forward, for example, look at the features we need for
    2.36, and figure out the use cases based on that, and take a first
    stab at an implementation.

-   Implementing pilot solution for simpler cases, and then scaling it
    up in a spike for more complex cases.

-   We have some idea of the general use cases, so we can document
    those and start with them.

-   We are not aiming for merging past branches into the "future"
    branches at this point.

-   A working group can proceed with gathering use cases and designing a
    solution that supports chosen use cases.

-   Once we have a proof of concept that we think will work, we pilot it
    where the use cases are supported, and then do targeted spikes in
    more complex scenarios to make sure we are solving the right
    problems.
