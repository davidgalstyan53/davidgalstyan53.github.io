---
layout: post
title: "Spring Blog 0: Brute-Forcing"
---

I thought it would be fun to make a brute force script. Of course, brute-forcing isn't exactly the most efficient method of password cracking, but it can still be used. Also, I've never tried to make a brute force tool, so I decided to look into it.

Just to go over it, brute-forcing is a method of hacking that requires the hacker to try every single string combination possible to crack a password. So if my password was "LisaIsCool" (see what I did there?), I would have to try every single combination of characters until I finally get to the correct password. There are a few reasons why this particular type of attack isn't ideal nowadays:

1. You'll need quite a bit of computing power to be able to crack any decent password
2. If you don't have sufficient computing power, really strong passwords could potentially take decades, or even much longer to crack
3. Many popular websites have account lockouts after too many unsuccessful login attempts, rendering a brute force attack useless
4. Most websites, along with local workstations in the workplace (assuming you have a competent SysAdmin) have strict minimum requirements for password strength

Anyway, let's get to the actual tool. I got this tool from "Magic Code" from YouTube, and I'll hopefully be testing this out for my next blog post.

The Python script reads as follows:

	import random
	import pyautogui
	chars = "abcdefghijklmnopqrstuvwxyz0123456789"
	chars_list = list(chars)
	
	password = pyautogui.password("Enter a password : ")
	
	guess_password = ""
	
	while(guess_password != password):
		guess_password = random.choices(chars_list, k=len(password))
		
		print("<============="+ str(guess_password)+ "===============>")
		
		if(guess_password == list(password)):
			print("Password : " + "".join(guess_password))
			break


	
	
