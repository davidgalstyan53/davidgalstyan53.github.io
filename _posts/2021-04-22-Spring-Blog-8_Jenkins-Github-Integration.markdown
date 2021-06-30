We'll go through how to create a job in Jenkins. After ensuring that Jenkins is up, running, and served through it's designated port, visit your Jenkins dashboard on your web browser, and login. On the dashboard, you'll want to:
- Click on "New Job"
- Create a job name (no spaces)
- Click on Freestyle Project

For this job, our goal is to create a job where we can monitor one of our GitHub repos. To make this work, we'll have to take one of our repos, and grab the repo link. For example, I used "https://github.com/davidgalstyan53/COMP484_Lab2.git", which is my old repo for a COMP 484 assignment. You can use any public repo for this. You can also use a private repo, but Jenkins will require credentials.

After clicking on "Freestyle Project", you'll want to click "OK". You can put a description for the job, which will appear on your Jenkins dashboard. Jenkins also gives several different options for source code management. Since we're using GitHub, of course, we want to choose "Git". 

There are also several different "Build Triggers" that you can set. One of them is "build periodically", which will allow us to use use cron syntax to schedule this job to run at whatever interval you use. Of course, there are endless options here, so it's best to choose whatever you want. If you don't understand cron syntax, you can easily click the question mark next to the cron field, and it will show you examples. For this project, we will choose to run this job once a day, at 6 AM, everyday, of every month. Cron syntax is as follows:

	[MINUTE] [HOUR] [DAYOFMONTH] [MONTH] [DAYOFWEEK]

So to make our job run everyday at 6 AM, all we need to put in the field is:
	
	0 6 * * *

There are many post build options, one of which allows us to save our test results to an XML doc, but we'll skip that for now. We can click on "Save" to save the job. 

That's it, we created our first job. Instead of waiting for 6 AM, you can go back to your dashboard, click on your job, and run the job manually. Each time you run the job, Jenkins will clone the repo to your local system, and scan for any changes in future builds. Changes will all be reported when detected on each build, so ours will run at 6 AM everyday. You can make a change to one of the files in the repo after your first build and see if there are any changes after you run the job again. 
