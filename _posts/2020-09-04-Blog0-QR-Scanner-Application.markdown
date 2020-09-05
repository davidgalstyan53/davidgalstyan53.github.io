---
layout: post
title: "Blog 0: QR Scanner Application"
---

I must admit, I found myself to be a bit short for words here. For the past couple of weeks I haven't spent much time looking into some of the things that I had been planning to look into to prepare me for CIT480. Those things would have included:

- Terraform
- Ansible
- Playing around with my newly acquired AWS Education credits
- Building on my knowledge of Docker

Instead, most of my time has gone towards planning out my group's project for CIT496P. Since Professor Kaplan has decided to revamp the course into a DevOps practicum, we've actually seen a massive influx of CompSci students (eww) take the course to fill in the "Dev" roles on each team. Despite being a CIT major, I've actually taken in interest taking one of the "Dev" roles in the team, mainly due to my working (and still improving) knowledge of full stack development.

### What will the application do?

The application is a QR Attendance system meant to be used by CSUN students to log into their respective courses. Students will be required to:
1. Log into their CSUN accounts on their phones (using our mobile app)
2. Log on to the attendance site (also built by us), and choose the course they are attending
3. If the student wishes to check in, they will be prompted with a QR code, which they will scan with their phone application
4. If the student can not attend class, there will be an option for the student to request an absence excuse
5. Instructors will also be able to log in to the site to view their course attendance records, course rosters, and attendance excuse submissions from students.

### How do we plan to achieve this?

The attendance site will be built and hosted on a LAMP stack on an AWS server. The database schema is currently being constructed by other team members. As of right now, the plan is as follows:

1. Build the mobile application with Java using Android Studio
2. The backend of the entire web and mobile applications will be built with PHP and a MySQL database
3. The PHP user login and session tracking will largely re-use code that used I built my final COMP484 project (a user login and registration system) with.

### What are some issues that we will run into?

Where do I start?

1. Students can easily share their login information to falsely check into a class
2. The database schema will likely take some time to draw out and Build
3. While Android Studio provides an extremely beginner-friendly platform, it will take some time to transition to building mobile applications
4. Even if the Android application deployment is a success, we would also have to go about building the application for iOS as well

### Overall?

There are some fixes that we have in mind for the issues above, but these are still pending, as the project is still in it's early stages. I'm planning to write another blog post about this project once we are finished with our first sprint. Until then, I'm hoping to look into writing about automation tools if I get the chance this upcoming week.
