---
title: Increasing the test coverage of our apps
layout: post
categories: [blog]
tags: [js, packages, code-style, test-coverage]
author: Mohammer5
---

Refactoring code with poor test coverage is always difficult.
The front end apps have a few tests in place but by far not enough,
so we'll need to do something about it.

## Add tests

If you've followed the discussion in the team-apps chat on the 17th Jan 2019,
you'll see the we agreed on the following things:

* Each PR should contain a few test
* React (or other view) components don't need to be tested
  * This can be done by e2e tests, with cypress or should be done in component libraries

Ideally you'll test new code 100% and add tests for bugs that you're fixing.<br>
Also adding a few tests when you encounter old code can be of use, but like
I said, you don't need to overdo it.

This way we'll get towards a better test coverage slowely without stopping
implementing bugs/features.

## Reviewing PRs

When you're reviewing a PR and you see that it doesn't add any tests whatsoever,
do not accept the PR.<br>
Send it back and request a view tests.

## TDD

This is just my opinion, but I think that adding tests before writing new code
has a few advantages:

1. You'll add tests without having to thing about it
(who wants to add tests after finishing the feature)
1. You'll have to think more about the code, discovering edge cased you might've
overlooked otherwise

It's difficult to do in the beginning as it's an entirely new way of approaching
coding, I found the following rule of thumb to be helping a lot:

```
Whenever you create a new file, add the test file right away,
write your tests, then fill the actual file with code.
```

This works especially well with having one function/class per file,
but this, I assume, will start a huge discussion again about whether
it makes sense to do so or not.
