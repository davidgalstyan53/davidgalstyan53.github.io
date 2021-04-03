Yay, more Python! Sorry, I need to learn Python for my job, so I might as well show a bit of what I've learned. This blog will be focusing on showing how to implement a One-Time-Pad in Python. Well... I haven't actually gotten around to implementing it yet, so I'll just describe the process then show the implementation next time.

Getting straight to the point, an OTP is an encryption method that takes a message, XOR's with a randomly generated key, and generates a cypher. So basically, to visually represent the process:

[message] --> [XOR] + [random key] --> [cipher]

And to decrypt:

[cipher] --> [XOR] + [same random key] --> [message]

In order to implement the OTP, we'll need to do the following:

- Generate a keysteam with a random key (n) as input, range 0 to 256, and return the number in bytes
- Figure out our XOR implementation (we'll take the length of our key, and the length of our message here, and XOR them)
- Either prompt user to input message or hardcode one and encode it in binary
- Take the keystream, implement that into the XOR function along with the message to produce your cipher
- To reverse the cipher, perform the same XOR function again, but XOR the keystream with the cipher instead of the message
- Your result should be the reversed cipher (your original message)

I should be able to spend a little more in my Python course to figure out exactly how to code this to make it functional by next week.

