Date: 2020-04-21\
Attendees: @dhis2/front-end 

# Frontend Info Meeting

Hi Team, it has been a while since the last meeting so this summary is going to be shorter
and less formal than usual as there are no decisions recorded and this was mostly a recap and
information meeting.

## Agenda

- Long-term Frontend Vision and Goals
- Practical information during Viktor's parental leave

### Practical info

- Viktor (@varl) is on parental leave from **2020 May 4** to **2020 September 14**.

- In the meantime, Viktor's responsibilities will be split:

  - Austin (@amcgee) will take on the role of **Frontend Lead** (@dhis2/front-end).
  - Birk (@birkbjo) will take on the role of **Team Apps Lead** (@dhis2/team-apps).
  - The **PDM** work Viktor does will be covered through a combination of the Team Lead, 
    Frontend Lead, Shurajit, Lars, and Phil.

- Will reply to messages on an arbitrary schedule, but roughly this applies if you need a response within[0]:

   - a minute: **phone call**
   - an hour: **sms / Signal**
   - a day: **Slack**
   - a week: **e-mail**
   
### Long-term Frontend Vision and Goals

- Austin presented the 6-12 months plan to: improve maintainability, consistency, and scalability of our application suite:

> 1. **Maintainability** (Application lifecycle overhaul)
>    - Continuous application releases delivery & deployment (App Hub, App Platform)
>    - Decouple web apps from DHIS2 Core (Core, App Platform)
>    - General, robust version toggling in apps (App Runtime, individual apps)
> 2. **Performance, Reliability** (technical and implementation)
> 3. **Usability** (system-wide, cross-functional, user-focused)

- DHIS2 is the capital-P **Platform** and we are developing tooling to make it easy to develop robust applications for our platform.

- We do so through our **App Platform** which is a framework with established best practices, codified into the framework itself.

- The App Platform is an umbrella for all of the tooling that supports building a DHIS2 application, including (not limited to)
  the **Runtime** and **UI** components.
  
- The @dhis2/front-end team collectively shares responsibility for our application framework, and it is encouraged to cross-pollinate
  to make sure that our framework covers all of the use cases for different applications.
  
- To enable better and faster contributions, we need to write better docs to aid understanding the structure and purpose of our libs and tools. That
  will help drive decisions like what goes where.
   
## Footnotes

[0] My son retains the right to cause the response times to be unreliable, any complaints can be piped directly to `/dev/null`.
