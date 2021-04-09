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
	
Here's some sample output (note that I entered "Hello my name is David" as input when prompted):

	b'\xeaKs\x02\xdd\x1c:\x879|v\xa3(=\x0f\x80\xf1\x97n\xf7o\xf6b'
	b'\xa2.\x1fn\xb2<W\xfe\x19\x12\x17\xceM\x1df\xf3\xd1\xd3\x0f\x81\x06\x92C'
	b'Hello my name is David!'
	
The 'b' prefix indicates that the following text is encoded as a byte object. As you can see, the first item printed is our KeyStream, then the cipher, followed by our original message. One thing that I tried to do is test to see if I could find a collision. Because I can't really post hundreds of lines of text here, I simply ran the functions twice in the same run. This time, I used the text 'david' as input:

	b'q\x9c;\xb5\xe4'
	b'\x15\xfdM\xdc\x80'
	b'david'
	b'n\xc3\x11\xebU'
	b'\n\xa2g\x821'
	b'david'
	
The keystream is generated randomly, which means that the cipher is also randomly generated when paired with the message. If you capture the cipher, but have the wrong key, you would be able to decrypt the message, but this would only result in an incorrect message being displayed. I had assumed that with enough computing power, one could simply be able to guess the key if they captured the cipher, but that is apparently not the case. I'm not too sure why it's so impossible because I haven't gotten around to the explanation to that implementation, but this is definitely one of the more fascinating cryptographic algorithms I've seen so far. 
