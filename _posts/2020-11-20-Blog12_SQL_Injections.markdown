---
layout: post
title: "Blog 12: Intro to SQL Injections"
---

This is a little embarassing, but I haven't actually PERFORMED a SQL injection before. I know what a SQL injection is, I've made sure my databases have proper input validation in order to prevent them, but I haven't actually tried performing one.

To put it shortly, a SQL injection is an archaic method of obtaining database information from a website by injecting SQL code directly into a form field. I say "archaic" because these aren't quite as common anymore, as most devs have figured out how to properly implement proper form validation on both the front and back end.


A common mistake with SQL code comes from the use of single quotes. Single quote are used when describing and pulling values from variables. Let's examine the following SQL code:
	
	SELECT * FROM USERS
	WHERE USERNAME = 'david123'
	AND PASSWORD = 'password' LIMIT 1;
	
Notice how each variable value starts and ends with a single quote. This is how strings are parsed in SQL. However, if you aren't paying attention, you may come up with code like this:

	SELECT * FROM USERS
	WHERE USERNAME = 'david123'
	AND PASSWORD = 'password'' LIMIT 1;
	
What's the issue here? Well, you'll notice that there are two single quotes closing off the string value 'password' for the PASSWORD value. This leaves us open for a SQL injection because we can essentially enter a bit of SQL code into the password field using addition string escape characters (in this case, a single quote). One of the most common bits of SQL injection is as follows (you would type this into the password field in this case):

	'OR 1=1--
	
Because of the botched bit of code in our script, entering the bit of code above will essentially execute the following:

	SELECT * FROM USERS
	WHERE USERNAME = 'david123'
	AND PASSWORD = 'password' OR 1=1--' LIMIT 1;
	
The logic of the code is as follows:
- All users are selected from the users table
- The user with the name 'david123' is selected
- The user must also have either a password reading 'password'...
- OR the value of 1 is equal to the value of 1...which is always TRUE.

Basically in this case, if true equals true, then the user's row will be displayed as if they actually typed in the correct password. Of course, this is just a small examples, but this is an example of SQL injection logic.
