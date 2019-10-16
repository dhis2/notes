# Popover position, 2019-10-15

Attending: Viktor, Ismay, Hendrik, Eric, Jan-Gerke

## Topic

There was an outstanding question in regards to how complex the positioning
logic should be; how it should behave.

## Outcome

#### Too complex to reach a decision
The topic turned out to be quite complex and the right amount of complexity
differs from component to component that will need positioning logic.

#### We need more information on what's needed
We've decided to create specs for every component that will have some sort of
positioning a element to an anchor element and then decide on the reuired
amount of complexity.

#### Third-party positioning engine
If complexity exceeds simple positioning logic, we might use an already
existing positioning engine instead of creating our own.

We had a brief look at two, but won't necessarily stick to these:
* [Tether.js](http://tether.io/)
* [Popper.js](https://popper.js.org/)

##### Third-party source code
As we didn't want to include any dependencies in `ui-core` before considering a
positioning engine, we decided that we'll read the source code of positioning
engines carefully in case we'd have to maintain it in case the original
maintainers won't do it themselves anymore.
