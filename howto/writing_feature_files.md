# Writing feature files

<!-- index {{{ -->
* [Introduction](#introduction)
* [Summary](#summary)
* [Scenario titles](#scenario_titles)
* [The `Given` step](#the_given_step)
  * [Describing the current state](#the_given_step-describe_state)
  * [Tense](#the_given_step-tense)
  * [Active / Passive](#the_given_step-active_passive)
* [The `When` step](#the_when_step)
  * [Describing what the interacting entity does](#the_when_step-describe_interaction)
  * [Active / Passive](#the_when_step-active_passive)
  * [Tense](#the_when_step-tense)
* [The `Then` step](#the_then_step)
  * [Describing what should happen](#the_then_step-describe_assertion)
  * [Active / Passive](#the_then_step-active_passive)
  * [Tense](#the_then_step-tense)
  * [Modal verbs](#the_then_step-modal_verbs)
* [Grammar](#grammar)
  * [Passive / active voice](#grammar_passive_active)
    * [Active voice](#grammar_passive_active-active)
    * [Passive voice](#grammar_passive_active-passive)
      * [Definition](#grammar_passive_active-passive-definition)
      * [How to change passive to active](#grammar_passive_active-passive-active_to_passive)
  * [Present / past tense](#grammar_present_past)
    * [Present tense](#grammar_present_past-present)
    * [Past tense](#grammar_present_past-past)
  * [Modal verbs](#grammar_modal_verbs)
    * [Modal verbs](#grammar_modal_verbs)
<!-- }}} -->

<!-- Introduction {{{ -->
## Introduction
<a name="introduction" href=""></a>

As feature files are written using the English language, we need some rules to
standarize how we write these files. This document will serve the purpose of
being a reference to which developers can come back or point to.
<!-- }}} -->

<!-- Summary {{{ -->
<a name="summary" href=""></a>
## Summary

### Scenario title

* Scenario titles should describe the surrounding context rather than the
implications

### Given

* Describe the current state
* Use past tense when describing an action that has happened
* Use present tense when describing a given state
* Always use the passive voice

### When

* Describe the actions of the scenario
* Always use present tense
* Always use the active voice

### Then

* Describe what should happen
* Always use present tense
* Always use affirmative voice
* Always use the passive voice
<!-- }}} -->

<!-- Scenario {{{ -->
<a name="scenario_titles" href=""></a>
## Scenario titles

Scenario titles should describe the surrounding context rather than the
implications. This can be used to give real-life examples of what users do and
the respective steps detail the behavior of the scenario.

```feature
# wrong
Scenario: Move item from list A to list B

# right
Scenario: The user clicks the 'move to list B' button

-----

# wrong
Scenario: Switch position of the firt two items

# right
Scenario: The user drags and drops the first item after the second one
```
<!-- }}} -->

<!-- Given {{{ -->
<a name="the_given_step" href=""></a>
## The `Given` step

<a name="the_given_step-describe_state" href=""></a>
### Describing the current state

These steps define the current state, they do not describe what needs to be
done to get there:

```feature
# wrong
Given the user logged in

# right
Given the user is logged in
```

The difference in this example is sublte, which is intended.
In the wrong example an action is performed and no concrete state was
mentioned. It's unclear what the resulting state will be after the user has
logged in.

The right example on the other hand describes the current sitution, regardless
of what happened to get there. The user could've logged in himself, he could've
been logged in automatically as his session is still valid, he could've used
oAuth2 or a simple basic auth. Regardless of how the user has been logged in,
the state is clear: The user is logged in.

As interpretation of the two examples above depends on the individual, the two
examples can be interpreted as being identical in meaning. To keep the `Given`
steps consistent across the entire project, all those steps need to define the
given state. Here's an example that's more obvious:

```feature
# wrong
The user clicks on the import "metadata" sidebar link

# right
The user is on the "metadata" import page
```

It's uncertain what happens when clicking on the link. It could be that a Modal
with further options will be opened or the sidebar is broken, which should be
covered in its own test and should not interfere with the functionality of the
feature that operates on the metadata import page.

<a name="the_given_step-tense" href=""></a>
### Tense

Generally, this could be written in either the past or present. This does not
need to be restricted as either past or present can sound more natural, which
differs from case to case.

Actions normally sound more natural when written in the past (`Given the reset
button was clicked`), while describing states sounds more natural in the
present (`Given the sidebar is rendered`).

<a name="the_given_step-active_passive" href=""></a>
### Active / Passive

The `Given` step should always be in the passive voice as it describes a state,
even if the state is a action that has happened in the past.
<!-- }}} -->

<!-- When {{{ -->
<a name="the_when_step" href=""></a>
## The `When` step

<a name="the_when_step-describe_interaction" href=""></a>
### Describing what the interacting entity does

Contrary to the `Given` steps, the `When` steps describe what's actually
happening in the scenario. 

<a name="the_when_step-active_passive" href=""></a>
### Active / Passive

As these are the steps that describe what's happening in the scenario, these
have to be active.

```feature
# wrong
When the submit button is clicked

# right
When the user clicks the submit button
```

As active sentences needs a subject, you should use the term "user" if there is
no other subject. It's totally fine to mention the "user" here as the
term is not limited to an actual person because accessiblity and testing
software are using the interface as well and therefore are users as well.
(See the [Grammar](#grammar-passive-active) section for more information about
active/passive and how to convert a passive voice to an active one)

<a name="the_when_step-tense" href=""></a>
### Tense

`When` steps always have to be in the present tense.
<!-- }}} -->

<!-- Then {{{ -->
<a name="the_then_step" href=""></a>
## The `Then` step

<a name="the_then_step-describe_assertion" href=""></a>
### Describing what should happen

The `Then` steps describe what should happen, they have to use a modal verb (a
list of possible values is further down) to indicate the expected behavior.
Using modal verbs instead of just describing the expected state expresses
uncertainty, which means that the behavior should constantly be tested (that's
a good thing).

```feature
# wrong
Then the input is focused

# right
Then the input should be focused
```

<a name="the_then_step-active_passive" href=""></a>
### Active / Passive

As these steps are in the affirmative voice, these are naturally in the passive
voice as well.

<a name="the_then_step-tense" href=""></a>
### Tense

`Then` steps always have to be in the present tense, as they're a result of
what happens after the already-in-present-tense `When` steps

<a name="the_then_step-modal_verbs" href=""></a>
### Modal verbs

The possible modal verbs are defined in the
(RFC keyword definition)[https://tools.ietf.org/html/rfc2119], which are:

```
1. MUST   This word, or the terms "REQUIRED" or "SHALL", mean that the
   definition is an absolute requirement of the specification.

2. MUST NOT   This phrase, or the phrase "SHALL NOT", mean that the
   definition is an absolute prohibition of the specification.

3. SHOULD   This word, or the adjective "RECOMMENDED", mean that there
   may exist valid reasons in particular circumstances to ignore a
   particular item, but the full implications must be understood and
   carefully weighed before choosing a different course.

4. SHOULD NOT   This phrase, or the phrase "NOT RECOMMENDED" mean that
   there may exist valid reasons in particular circumstances when the
   particular behavior is acceptable or even useful, but the full
   implications should be understood and the case carefully weighed
   before implementing any behavior described with this label.

5. MAY   This word, or the adjective "OPTIONAL", mean that an item is
   truly optional.  One vendor may choose to include the item because a
   particular marketplace requires it or because the vendor feels that
   it enhances the product while another vendor may omit the same item.
   An implementation which does not include a particular option MUST be
   prepared to interoperate with another implementation which does
   include the option, though perhaps with reduced functionality. In the
   same vein an implementation which does include a particular option
   MUST be prepared to interoperate with another implementation which
   does not include the option (except, of course, for the feature the
   option provides.)
```
<!-- }}} -->

<!-- Grammar {{{ -->
<a name="grammar" href=""></a>
## Grammar definitions

<a name="grammar_passive_active" href=""></a>
### Passive / active voice

<a name="grammar_passive_active-active" href=""></a>
#### Active voice

> In grammar, an active voice is a type of a clause or sentence in which a
> subject performs an action and expresses it through its representative verb.
> To simply put it, when a subject performs an action directly, it is in active
> voice. It then uses transitive verb to show the action.
>
> Style guides usually encourage the use of active voice, because it is clear
> and direct. For example, “Some customers prefer mulled ale. They keep their
> mugs on the hob until the ale gets as hot as coffee. A sluggish cat named
> Minnie sleeps in a scuttle beside the stove” (The Old House at Home, by
> Joseph Mitchell). All of these sentences are in active voice, as the verbs
> “refer,” “keep,” “get” and “sleep” are in active mode.
>
> (Source: https://literarydevices.net/active-voice/)

<a name="grammar_passive_active-passive" href=""></a>
#### Passive voice

<a name="grammar_passive_active-passive-definition" href=""></a>
##### Definition

> The passive voice is a grammatical "voice". The noun or noun phrase that
> would be the object of a corresponding active sentence (such as "Our troops
> defeated the enemy") appears as the subject of a sentence or clause in the
> passive voice ("The enemy was defeated by our troops").
>
> The subject of a sentence or clause featuring the passive voice typically
> denotes the recipient of the action (the patient) rather than the performer
> (the agent).
>
> (Source: https://en.wikipedia.org/wiki/English_passive_voice)

<a name="grammar_passive_active-passive-active_to_passive" href=""></a>
##### How to change passive to active

> To change passive voice to active voice, make the agent of the sentence into
> the subject, and turn the old subject into the object.
>
> (Source: https://github.com/dhis2/notes/pull/94)

<a name="grammar_present_past" href=""></a>
### Present / past tense

<a name="grammar_present_past-present" href=""></a>
#### Present tense

> The present tense is used for actions in a time which are happening now.
> In order to explain and understand present tense
>
> (Source: https://en.wikipedia.org/wiki/Present_tense)

<a name="grammar_present_past-past" href=""></a>
#### Past tense

> In languages which have a past tense, it thus provides a grammatical means of
> indicating that the event being referred to took place in the past
>
> (Source: https://en.wikipedia.org/wiki/Past_tense)

<a name="grammar_modal_verbs" href=""></a>
### Modal verbs

> The modal verbs of English are a small class of auxiliary verbs used mostly
> to **express modality** (properties such as possibility, obligation, etc.)
>
> (Source: https://en.wikipedia.org/wiki/English_modal_verbs)
<!-- }}} -->
