Continuing from last time, here's a full implementation of the OTP in Python 3:

	# -*- coding: utf-8 -*-
	"""
	Created on Fri Apr  2 20:52:03 2021

	@author: David
	"""

	import random

	message = input("Enter your message:\n")
	message = message.encode()

	def keystreamGen(n):
	    return bytes([random.randrange(0,256) for i in range(n)])


	def xorBytes(keyStream, message):
	    length = min(len(keyStream), len(message))
	    return bytes([keyStream[i] ^ message[i] for i in range (length)])

	keyStream = keystreamGen(len(message))
	cipher = xorBytes(keyStream, message)

	def printItems():
	    print(keyStream)
	    print(cipher)
	    print(message)

	printItems()
	
Since the actual steps are explained in the previous blog entry, I won't go into it here. What I wanted to get into is the idea of why it's so secure, and how I can attempt to break it (hint: I can't).

