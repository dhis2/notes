# App Hub architecture meeting

Date: 2020-04-15\
Attending: Viktor, Erik, Birk

# Agenda

We have had some difference in coding style in the App Hub, and it is time we figure out a way forward
that everyone is happy with.

We have one issue regarding the architecture, and one PR that has been open a long time.

- https://github.com/dhis2/app-hub/issues/139

Other topics to discuss included how to handle Knex transactions, isolate test data between tests, etc.

# How to handle database transactions

On the topic if we should handle transactions inside of functions or outside, we have decided to handle transactions
on the outside.

The technical reason for this is that a `db` instance of Knex and a `trx` instance are interchangable, so by handling
the transaction on the outside, our functions work in both cases, and do not have to think about using `.transacting()`
and handling commit/rollback situations.

To make this usage clear, these are the actions we agreed to take:

- Rename `trx` and `db` params to `knex`.
- Add jsdoc that functions accept either a Knex DB or a Transaction instance.
- Erik: Refactor functions to not use `.transacting` internally
- Isolate unit test data using transactions in tests

# What to do in terms of filtering

Related: https://github.com/dhis2/app-hub/pull/194

After some clearing up some misunderstandings we are in agreement that this filter plugin
will cover our needs. There are a few unresolved items that need to be addressed before we
can merge this PR:

- Birk: see if we can get Swagger docs to work properly
- Erik: use the filter-plugin to keep a feel for how it works, and document any questions or parts
  that will need clarification for other developers.
- Birk: writes clarifying docs based on Erik's feedback

# Future actions

Erik and Birk will have weekly syncs to discuss App Hub architecture and active PRs. Larger PRs may also
warrant peer reviews over voice chat instead of attempting to review them in isolation solely using GitHub.

