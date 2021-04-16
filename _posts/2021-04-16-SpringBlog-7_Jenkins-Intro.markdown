Since we really didn't get a chance to get into Jenkins in class, I wanted to try it out myself. Installing Jenkins in pretty simple on MacOS or Linux:
- Install Homebrew (if you already have it, make sure it's updated)
- Enter the following command:
	$ brew install jenkins-lts
- To start Jenkins, just enter the following:
	$ brew services start jenkins-lts

Once it's started, you'll go to your browser, and navigate to "localhost:8080". Keep in mind that Jenkins, by default, is set to serve on port 8080 upon installation, so be mindful if you have anything else set up running on port 8080. After navigating to the site on your broswer, you'll be asked to put in an administrator password that was set during installation. To find the password, simply CAT the file (note: if permission is denied, simply run it again with sudo):

	$ cat /var/root/.jenkins/secrets/initialAdminPassword 
	Output: [password]
	
In order to keep things simple, you can keep the Jenkins address to localhost:8080. If you want to host it on an AWS instance or server, you can change the address to whatever location you want for that instance. Since we only want this running on our local machine right now, keep it at localhost:8080.

After inputting your user info, you'll be greeted with the Jenkins dashboard. Now, I have no idea how to use Jenkins at the moment. But now that we have Jenkins installed and running, I'll be able to play around and see what I can come up with for next week's blog.

Oh, and if you're a Windows user and want to install Jenkins, here's some advice: don't.
