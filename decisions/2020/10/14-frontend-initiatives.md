**Date**: 2020-10-14

**Attending (Speaking)**: Austin, Viktor, Joe, Jan-Gerke, Jennifer, Christos,
Jan, Edoardo, Joakim, Ismay, Birk, Martin, ...

**Next Meeting**: Wednesday 28 October, 2020 @ 15:00

## Agenda

1.	UI Icons platform Call for User Stories (@cooper-joe )

2.	**Proposal** Synchronized library and app development

3.	Server Version Toggling

  	-	We now have server version detection 🎉 
  	-	Next up - version toggling runtime library (with dynamic imports)

4.	App modernization (platform coverage)

5.	Migrating `d2-ui` component to `ui-widgets`

 	-	Sharing Dialog
  	-	Layouts
  	-	Interpretations & Rich Text
  	-	More key components?

6.	Tech debt review

## Links

(DHIS2 account required)

* [Agenda](https://github.com/dhis2/notes/issues/130)
* [Meeting Recording](https://drive.google.com/file/d/1n4lSyIdzPiNV0BGSnOh7L1lKB26y_4mJ/view)
* [UI Icons user stories](https://docs.google.com/spreadsheets/d/1NPMll75-vrU-9vOERosZztMj0zZcbQPQiIH_chhubwY)

## Notes

### UI Icons user stories

Please add user stories to [https://docs.google.com/spreadsheets/d/1NPMll75-vrU-9vOERosZztMj0zZcbQPQiIH_chhubwY](the user story spreadsheet).

This is not about the API usage of icons, but how they will be used in the applications.

-	**Q**:	Is this the same library as the Android icon library?

	**A**:	Ideally, yes. There has been some overlap, but most of the icons
			on Android still come from Material Design. They also have vast library for
			domain specific icons that they get from the Core.

We probably will not incorporate them into our icons.

### Syncronized application and library releases

Proposal on how to orchestrate how we could continuously release applications
and libraries.

There are many moving parts, that we may want to consider doing independently.

This spurred a long discussion with a lot of questions and feedback, so the
conclusion is to revisit the proposal and clarify it, and cover practical areas
how it will all work together.

### Server Version Toggling, App modernization, migrating d2-ui components, tech debt review

We did not get to these points in the agenda, and they will be addressed the
next meeting.
