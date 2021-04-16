When: April 13, 2021 @ 15:00 CET
Where: Online
Attending: Austin, Viktor, Bjørn, Christos, Debora, Edoardo, Ismay,
Jan-Gerke, Joakim, Joe, Kai, Martin, Simona, Hendrik, Médi-Rémi,
Jennifer, Jan Henrik, Birk

# Agenda

## Introductions!

  - Welcome Simona!

## Decisions

### Standardize application file layout #248 
    
Discussion: https://github.com/dhis2/notes/discussions/257

Goal was unambiguous rules, difficult to define across all
application sizes.

Guidelines: 

1. Have similar organisation strategies between all our apps
2. Organise by-function, not by-type
3. Avoid ambiguity (i.e. no conceptual overlap in folder names)
4. Avoid generic folder names, and attempt to chose names that
   immediately reveal what’s inside
5. Accept that a project-structure is not a static thing you can
   define up-front, the structure should evolve with the app

Rules:

1. Routes live under `src/pages`, one React component file per route
2. Components live under `src/components` and should contain React components
3. React components (JSX) are NOT allowed in any other directories,
    which should contain business logic and utilities.

Conclusion is that the 5 guidelines above and the 3 rules are adopted, and will be written up
and documented.

## Task Forces & Updates

### PWA / Offline Caching

Platform side is working on recording network calls, start and stopping. [spec](https://docs.google.com/document/d/1uaftvVvZdDppTXFCRXF19WaS9NKVq0BG8dus_mRe_w0/edit#heading=h.jd28kwz1a5xn)

Analytics side is focusing on the dashboard app and aligning with the
API that the platform will provide and what should be cached, and what
should not be cached.

### Continuous Delivery

Over the next few weeks all our core apps are going to be uploaded to
the App Hub.

Need to update our release toolchain to publish to the App Hub as a
semantic-release plugin.

### Developer Outreach

Good turn out for the developer meet ups on last Friday. The developer
community is growing, and fun to see interaction between the community
members.

Joined Android and Webapp academy for advanced topics first week of May
over the course of 4 days. Currently working on the agenda.

Advanced topics like i18n, testing, and security.

Collaborators needed, please reach out to Debora if you would like to
present.

If you don't want to present, you can help by producing guides for the
developers.dhis2.org site. Check this [document](https://docs.google.com/document/d/1-QfPhG80_EVSN1X6z4CTjYeTo2fbTEt3tgNNnPPvBjo/edit?usp=sharing) to get an idea of what kind of content to write/add. 

### PR Previews

Got OK to use Netlify, ready to move ahead with this.

Next step is to whitelist the PR urls, and setup the actions.

### Large collections APIs

Now that Platform is used for national installations with COVID
vaccinations we are hitting restrictions in terms of collections 
(and particularly nested collections) with tens of thousands of 
children, that are difficult to manage given restrictions in the API.

Backend is working on:

-   Partial update support. JSON Patch specification is being
    implemented.

-   New Gist API is worked on that will be a more performant variant that
    doesn't return all the nested collections. Will contain a suite of
    queries and selectors to help when asking for data.

From the Frontend side:

-	The current view is that our users expect an "atomic-update-UI" for editing
	objects. With this we mean that all fields, including the nested collection
	inputs on one form and the users edits everything in one go.

-	This viewpoint is based on historical user feedback from times where we did
	in fact have a separate UI section for managing these nested collections
	managed separately, and this was not appreciated.

-	However, we all agreed that we should probably not assume this viewpoint is
	necessarily still correct. There could have been issues with the old UI that
	would have been solved easily. And also, given the fact that our current input
	components aren't really suitable for the new way of managing nested
	collections, we don't know what our "atomic-UI" would look like.

We should:

1.	Implement a UI design for both "atomic updates" and "separate nested
	collection management sections".

2.	If not too much work, implement a POC for both (the user-app is a good app
	to do this in)

3.	Get user feedback, preferably after interqacting with our POCs, but
	alternatively we could also just discuss the designs with them

Relevant meeting minutes:
https://github.com/dhis2/notes/blob/master/decisions/2021/03/18-large-nested-collections.md

### Others?

#### cli-style updates

Check out the `@dhis2/cli-style@alpha` release and see what has changed
(spoiler: a lot!)

#### cli-utils-docsite

Feature in docsite to use react-docgen, will keep parallel `jsdoc` support for
non-React documentation.
  
