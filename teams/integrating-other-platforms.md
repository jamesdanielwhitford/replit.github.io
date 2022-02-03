# Integrating With Other Platforms

Teams for Education enables integration with platforms such as Google Classrooms. Project code can also be embedded.

In this tutorial, you'll learn how to:
* Integrate with Google Classrooms
* Embed projects

## Google Classrooms Integration 

With Replit's Google Classroom integration, teachers can quickly add every student in their Google Classroom to a Team and easily share Replit projects as Google Classroom assignments.

Students and teachers can easily build and collaborate on [Replit](https://replit.com/) from a Chromebook, [download it from the Google Play Store](https://play.google.com/store/apps/details?id=com.replit.twa) to their device, or find it on the [Chromebook App Hub](https://chromebookapphub.withgoogle.com/apps/replit-teams-for-education). 

*Soon, teachers who have added their students to Replit through Google Classroom will also be able to integrate their Google Classrooms gradebooks with Replit's [Projects Overview](https://docs.replit.com/teams/reviewing-submissions)!* 

View a demo of these functionalities [here](https://www.loom.com/share/e2bb4abf6ad84fa28e19859d1089354f). 

### Adding Students to a Team from Google Classrooms
To add your students from Google Classrooms into a Replit Team for Education, click "Manage team members" at the top of your Team, and select "Invite Via Google Classroom".

This will prompt you to connect your Replit Team for Education with your Google Classroom, and select students from your Google Classroom to add to your Teams roster. 

<img style="width: 600px" src="/images/teamsForEducation/invite_via_gc.png" />

### Creating Assignments in Google Classrooms from Replit 

To create an assignment in Google Classroom directly from your Teams for Education dashboard, click on the dropdown menu next to a Team Project, and select "Share to Google Classroom". This will automatically create an assignment in your Google Classroom with a link to your Replit Project. 

<img style="width: 600px" src="/images/teamsForEducation/create_assignment_gc.png" />

## Embedding projects

To embed a project, follow the simple steps below or follow along with our [video walkthrough](https://www.loom.com/share/788fb7ade7154c83baf0df6ecf1fe102):

*Please note that to access their project in an iframe, students must be added to the team and logged into their Replit account.*

1. Click on the three dot menu found on the right side of each project.
2. Copy the embed code. This will provide you with an [iframe](https://docs.replit.com/Teams/EmbedProjects) which you can paste into HTML or copy the project link.
3. Paste it wherever you are trying to embed the project, and you'll be good to go!

<img style="width: 600px" src="/images/teamsForEducation/embedProjectsImage.png" />

The embed code you copy will look like the example below:

```
<iframe width="100%" height="600px" src="https://replit.com/team/{team name}/{project name}"></iframe>
```

The screenshot below shows what the embedded code would look like:

<img style="width: 600px" src="/images/teamsForEducation/embedded-code.png" />