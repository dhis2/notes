**Date**: 2021-01-06

**Attending**: I didnt keep attendance. I think we were 14 people tho.

**Next Meeting**: January 20, 2021 @ 15:00

## Agenda

*When*: January 6, 2021 @ 15:00 CET *Where* : Remote

# Agenda

- General updates:
  - Holiday Debrief
  - Welcome to @deboragaleano @KaiVandivier @mediremi !
  - (again) GitHub Discussions in the Notes repo!
  - 2.36 priorities
    - App Cache deprecation (Data Entry App) - @amcgee @Birkbjo 
    - PWA + Offline Dashboard - @janhenrikoverland @edoardo @jenniferarnesen @martinkrulltott @Sharmyn28 @amcgee @cooper-joe 
    - App Platform ports w/ feature toggling (2.35+) and up-to-date shell
      - Scheduler App - @ismay 
      - Settings App - @amcgee 
      - Maps App (blocked by Plugin builds, no feature toggling) - @amcgee @turban 
      - Update deps in all apps - @amcgee 
      - WHO DQ App: move to server-side outlier calculations - @HendrikThePendric
    - Continuous Delivery & App Hub updates - @Birkbjo @amcgee 
- Updates from active working groups
  - Cypress - @HendrikThePendric @varl (out Jan) @Mohammer5 (out Jan)
  - PWA & Offline/Responsive Dashboard - (see above)
  - Plugin builds - @amcgee @jenniferarnesen @edoardo 
  - UI & Platform updates - @ismay @HendrikThePendric @cooper-joe @amcgee @edoardo 
- Discussions
  - Live app previews @paschalidi https://github.com/dhis2/notes/discussions/183
  - Cleanup Notes and Jira @amcgee @varl (off Jan)
  - Others? @dhis2/front-end 



# Notes

* General updates:

  - Welcome to [@deboragaleano](https://github.com/deboragaleano) [@KaiVandivier](https://github.com/KaiVandivier) [@mediremi](https://github.com/mediremi) !

  - (again) GitHub Discussions in the Notes repo!

    Discussion: Instead of creating new issues it is suggested to start using the discussion feature on GitHub. The feature can be used for questions, Q&A, RFCs, ideas etc. 
    Advantages: threaded discussions, mark answers. 

  - 2.36  priorities

    Discussion: 30 working days before the soft freeze

    - App Cache deprecation (Data Entry App) - [@amcgee](https://github.com/amcgee) [@Birkbjo](https://github.com/Birkbjo)

      Discussion: We want to update the apps using it to use the service workers.

    - PWA + Offline Dashboard - [@janhenrikoverland](https://github.com/janhenrikoverland) [@edoardo](https://github.com/edoardo) [@jenniferarnesen](https://github.com/jenniferarnesen) [@martinkrulltott](https://github.com/martinkrulltott) [@Sharmyn28](https://github.com/Sharmyn28) [@amcgee](https://github.com/amcgee)

      Discussion: There has been quite a bit of progress here. 

    - App Platform ports w/ feature toggling (2.35+) and up-to-date shell

      - Scheduler App - [@ismay](https://github.com/ismay)

        Discussion: At the moment isn't ready to go in. Wahed has been the one working worked on it, whom is no longer part of dhis2. However as of now, most of the blockers are resolved. Ismay willl take over this work. In 30 days we arent 100 percent sure if it can be ready for review.
        Austin will talk with Wahed and discuss about the app, this will be sort of handover. Also Hendrik suggested he would like to be included.

      - Settings App - [@amcgee](https://github.com/amcgee)

      - Maps App (blocked by Plugin builds, no feature toggling) - [@amcgee](https://github.com/amcgee) [@turban](https://github.com/turban)

        Discussion: Austin and Bjorn gave progress update.

      - Update deps in all apps - [@amcgee](https://github.com/amcgee)

        Discussion: Austin gave progress update.

    - Continuous Delivery & App Hub updates - [@Birkbjo](https://github.com/Birkbjo) [@amcgee](https://github.com/amcgee)

      Discussion: Birk gave update on the topic. There is wip on the topic. 

      Two things we want to look into is a) we want to be able to enable continuous delivery. b) We want to have the authentication with the backend in place.

    - Extra topic 
      Discussion: Hendrik and Austin will connect with Ulaf regarding the data quality app.

* Updates from active working groups

  - Cypress - [@HendrikThePendric](https://github.com/HendrikThePendric) [@varl](https://github.com/varl) (out Jan) [@Mohammer5](https://github.com/Mohammer5) (out Jan)

    Discussion: Hendrik is about to release the network shim. New version of cypress-cli v5 is released. 

  - PWA & Offline/Responsive Dashboard - (see above)
    - PWA
    
        Discussion: Austin had an mvp on that that he tested with some people on their apps.

    - Responsive Dashboard
    
        Discussion: Jan is making progress on the work. Milagros and Jeniffer are the main people working on it.
        Jeniffer works on the responsivness of the app. This part is in PR. Overall is looking pretty good. 
        Milagros, is work in progress. Couple of details is left.

    - Offline design update from Joe
    
        Discussion: Joe has a design proposal for offline connectivity for mobile and desktop. The concept is there and it is basically ready to be implemented. Mobule version is 90 percent there.
        There will be an upcoming meeting with Jan, Joe

  - UI & Platform updates - [@ismay](https://github.com/ismay) [@HendrikThePendric](https://github.com/HendrikThePendric) [@cooper-joe](https://github.com/cooper-joe) [@amcgee](https://github.com/amcgee)

    * ui cons 

      Discussion: are released and people can use it. There is also a strategy for migration that Joe has worked on. There is a breaking change to ui v5, the change is that if you have been using the old icons you want to be careful because the old icons have been removed.
      Relevant discussion on slack [link](https://meet.google.com/linkredirect?authuser=1&dest=https%3A%2F%2Fdhis2.slack.com%2Farchives%2FC0BP0RABF%2Fp1607611797449000).

    * sharing dialog
    
      Discussion: Icons were missing but now are there.

  - Plugin builds - [@amcgee](https://github.com/amcgee) [@jenniferarnesen](https://github.com/jenniferarnesen) [@edoardo](https://github.com/edoardo)

    Discussion: Austin has looked into this. We wanna keep this in the radar.

  - Extra topics

    Discussion: Martin brought up [DHIS2-9878](https://meet.google.com/linkredirect?authuser=1&dest=https%3A%2F%2Fjira.dhis2.org%2Fbrowse%2FDHIS2-9878). There will be a meeting for that where usecases will be discussed.

* Discussions

  - Live app previews [@paschalidi](https://github.com/paschalidi)

    Discussion: People where asked if they would find it of any use. There was in general positive reactions. Lets try something thats low efford and move on (possibly netlify since we already worked with that).

  - Cleanup Notes and Jira [@amcgee](https://github.com/amcgee) [@varl](https://github.com/varl) (off Jan)

  - Others? [@dhis2/front-end](https://github.com/orgs/dhis2/teams/front-end)