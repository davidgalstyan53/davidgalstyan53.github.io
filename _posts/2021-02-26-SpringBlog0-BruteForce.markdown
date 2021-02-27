---
layout: post
title: "Spring Blog 1: Implementing Caesar's Cipher in Python"
---

As you can tell, I've been trying my hand at security for the past year. This post will cover an extremely ancient cipher known as Caesar's Cipher. The exact history isn't important because the only Caesar that I care about quite frankly is the one who sells me deliciously cheap pizza (deliciously cheap, not delicious).

The algorithm for the cipher is extremely simple. In Laymen's terms:
1. Establish a number from 0-9 for a key
2. Write a message
3. Take the number from the key, and shift each letter in your message to the right by that many positions

For example: With a key of 3, letter A would shift to the right by 3 positions. Here are some examples for a key of 3:
- A ----> D
- C ----> F
- X ----> A 

This is the implementation I drew up in Python:

	def generate_key(n):
	    letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
	    key = {}
	    counter = 0
	    for c in letters:
		key[c] = letters[(counter + n) % len(letters)]
		counter += 1
	    return key

	def encrypt(key, message):
	    cipher = ""
	    for c in message:
		if c in key != " ":
		    cipher += key[c]
		else:
		    cipher += c
	    return cipher


	key = generate_key(3)
	muhCipher = encrypt(key,"PIZZA PIZZA")
	
If we print "muhCipher", we end up getting the following:

	SLCCD SLCCD
	
I am currently working on setting up a "decrypt" function, but if we needed to reverse the cipher, we would need to know the key. In this case, we know that the key is 3. So if we want to print "PIZZA PIZZA" again, the following line will decrypt the cipher by shifting each letter back 3 spaces:

	print(encrypt(generate_key(-3), muhCipher))
	

