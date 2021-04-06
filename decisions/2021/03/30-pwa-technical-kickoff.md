# Dashboard PWA

Attending: Jennifer, Martin, Médi, Kai, Joe

## Previous Discussion

(from previous meeting with Jan, Karoline)
Karoline to find a country / countries for GAVI or CHAI malaria country for alpha/beta 
Jan check with Joe on UI status for Dashboard & Headerbar

## Notes
- Austin to convene Platform PWA/offline group this week, come up with design spec
    - Austin - create smaller, more targeted Jira issues and like to big one
- Jan and Analytics team design against spec for 3 weeks
- Meeting next week to discuss implementation plan (14h 2021-04-08)
- Platform implements spec for 3 weeks
- April 23rd deadline for initial implementations
- April 30th deadline for integration, alpha release on App Hub
- May 15th target beta release

Final release in 2.37?

## TODO
- Everyone take a look at the [specs](https://docs.google.com/document/d/1uaftvVvZdDppTXFCRXF19WaS9NKVq0BG8dus_mRe_w0/edit), see what you think is missing, see if you agree these goal deadlines are feasible
- JIRA cleanup and expansion
- Platform team take a look at designing a first pass at offline caching API design

## Decisions
- DECISION: need interactivity, don’t try to generate static images
- DECISION: use “minimum period of inactivity” first, investigate adding “loaded” then “rendered” callbacks to plugins

