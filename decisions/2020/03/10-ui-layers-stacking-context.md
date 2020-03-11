# 2020-03-10, UI: Layering and stacking

## Attending

Hendrik, Jan-Gerke, Joe, Ismay, Viktor

## Context

History and links to related issues and PRs: https://github.com/dhis2/ui-core/issues/596

**TL;DR** is that we are not happy with the current solution and think
we should do better. The current solution was the best we could
implement given the pressure on getting a new major version out the door
as it was blocking other development efforts. It serves its purpose but
we suspect that there are limitations that we have not considered.

Hendrik has created a presentation documenting the [evolution and
current state of affairs + a new
proposal](https://docs.google.com/presentation/d/1xCNPx08bT9uNtlBXt3zQRpV0xQwCoFTjjvJQd3e-K6g/edit#slide=id.g7f074dd6e5_0_92).

## Proposals

### New recursive layer + stacking context implementation

https://github.com/dhis2/ui-core/pull/807

The idea is to have a more robust way to set a layer level, from which
then all nested layers will use stacking layers.

### Current implementation

https://github.com/dhis2/ui-core/pull/582

One option is to stick with the current implementation until known
issues come up that force us to reimplement a different technique.

The argument is that we have no known issues at the time of writing with
the current solution.

### Layer components implementation

A completely different approach would be to avoid having to
"reimplement" how CSS stacks layers and `z-index`:es by using components
to define what should appear where.

```
const LayerBase = () => (....) // we won't need this one
const LayerAlert = () => (....)
const LayerError = () => (....)

// index.html
<body>
  <div id="root" /> // basically LayerBase
  <div id="layer-alert" /> // created by LayerAlert
  <div id="layer-error /> // created by LayerError
</body>

// in the app
<LayerAlert> // will render the children into #layer-alter
  <Modal>
    <Select />
  </Modal>
<LayerAlert>
```

## Conclusion

- We find ourselves jumping into technical implementations before
  resolving the actual needs that we have.

- We need to take a step back to understand the needs and requirements for how our
  libraries are supposed to work and what use cases we support in terms
  of layers and popups.

- Limitations needs to be documented and have documentation on how the
  app should work to mitigate those shortcomings.

- We need to define the behavior of how our layers should stack in feature
  files.

- Based on those feature files, we need to write E2E tests to cover our
  current implementation.

- The E2E tests should be as realistic as possible, using the components
  the same way an App would.

- We can and should also test the final, low level, implementation for
  consistency.

- After we have established a baseline we can better evaluate any new
  proposals on how to deal with the layers.

## Next actions

- [ ] Hendrik and Jan-Gerke to figure out the specifications and document
  the feature files.
  
- [ ] Make sure to ping Joe to figure out use cases.

- [ ] Ismay wants to be pinged in the PR to help write E2E tests.
