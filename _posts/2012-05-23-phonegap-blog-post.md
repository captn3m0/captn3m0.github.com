---
layout: post
title: Akira - Winning entry to the Adobe Express Apps Contest
tags:
- programming
- mobile
---

This is the obligatory blog post that comes along with winning the Adobe Express Apps Contest. 

#Contest Rules
The contest rules asked you to develop a mobile application, using Adobe Phonegap and related technologies(read Dreamweaver) in a time frame of hardly 18 hours. This duration was assuming that one does no sleep, which I did not.

The problem statement for the application was to create a mobile application for a SUV car manufacturer. The application had to be socially engaging and _use the hardware capabilities offered by the device_.

#Our Interpretation
We started with the problem statement as the complete guide for our application and ought bottom up for an application that would be the least and best amount of work to create an app that fulfils the app requirements.

We started off with a few wireframes, and features thrown around. At the end of the one hour mark, we had our feature list down to :

1. Owners can share pics of their cars. We wanted the application to be for the owners of the cars, which brings in a lot of additional data. Pic sharing was the most logical thing to do. We were thinking something like an Instagram Community where everybody posts pics about where they have been, their rigs and so on. 
2. A mileage meter. This was a slight gamification of the GPS data that we get. At the start of every journey/trip, you could mark it as such in the app, and we would record your position every 5 minutes. At the end of the trip, you could mark your ending point and see how much you travelled. Also important was the fact that we decided to show a number corresponding to every application user, showing how many miles he/she has travelled so far. Seeing that the next guy has travelled only so and so more miles than you may lead you to travel more.
3. Maps, obviously. A map for all the previous journeys that you have taken.

#Work
We tried to start with JQ.Mobi, which is an alternative to Jquery Mobile, but could not justify it, and switched to JQuery Mobile as it offered better  integration with Dreamweaver.

The basic application layout was done using a mix of JQuery Mobile and some custom css. I came across a very good service called Build Phonegap, that allows you to compile your Phonegap application online to different platforms. We started with basing our application on the [Phonegap Starter App on GitHub](https://github.com/phonegap/phonegap-start) which was quite good. The examples directory in the phonegap download is what we ended up using, though.

*Edit*: After working a lot more in mobile development, I have come to see a lot more frameworks, and find JQTouch to be quite the minimalist do-one-thing-well plugin.

The most difficult part was to get the application to compile for iOS, without paying the Apple Developer Licence. Since, I could not see myself selling iOS apps anytime soon in the Apple App Store, I was stuck with a jailbroken iPad + iPod Touch, and had to figure out out to compile.

The steps, which took me a lot of time to find on the internet, include :

1. Download and install the XCode and the Adobe Phonegap toolkit. I downloaded the latest version, 4.2 for xcode, which makes the process a bit easier.
2. Follow the instructions on [this youtube video](http://www.youtube.com/watch?v=n1ZDMmwYHdE) to allow xcode to compile your application without Code Signing.
3. Create a corvora application in xcode and follow [these instructions](http://wiki.phonegap.com/w/page/52010495/Getting%20Started%20with%20PhoneGap-Cordova%20and%20Xcode%204) to add the www folder to the application. 
4. Compile. If you have an iDevice connected, you should be able to compile and install your application in a single step.

You may need to change your application configuration to "Do not code sign" for this to work.

Getting all the above steps to work for the first time, on a borrowed MacBook Pro was a lot of work, for a mac noob like me. But at the end, getting to see the application getting launched on multiple devices and looking equally good was worth it.

The rest of the time was spent on getting the application features to work, while fighting off sleep. The end result was a still-incomplete application , which ran on multiple devices.

#Blackberry
Unfortunately, we were not able to run the app on the only Blackberry Phone that we had as Phonegap only supports Blackberry 5 as of now, while our phone had been upgraded to 6.

Our winning strategy from the start had been to dazzle the judges with an application running across multiple devices, and working equally good. We were pretty sure that none of the other contestants would put in so much effort to get it to run on non-android devices.

#Backend
I wrote the application backend in PHP limonade, a framework that i am quite used to. The concept was to give out a rest api to the application to use to Authenticate users and carry out backend tasks.

#Code
The code is obviously messy, as a result of being hacked in on a single 18 hour marathon. You may be able to get a few good ideas from the implementations, though. The entire code is available at my [akira](https://github.com/captn3m0/akira) and [akira-backend](https://github.com/captn3m0/akira-backend) repositories.


#Thoughts on Phonegap
My second slide in the presentation I did for the contest(made on Keynote on the Ipad, while walking to the contest room) says proudly "Phonegap is awesome". And i seriously mean that. I've got started in the world of mobile development, while not having to worry about cross browser compatibility issues, and the like. I can do stuff easily using the already existing technologies that I know and love. There are a ton of excellent Phonegap plugins out there, and many more being written right now.

I am really impressed with what a web developer could do with Phonegap, and its ease of use. The Adobe Developers promised me that the integration would be far better in Dreamweaver 6, which I might just try. Although, it was far easier for me to compile and install the application on an android phone, so I hardly used the emulator which I took the pains to install.

#Expectations
What I'd really love, though is a Phonegap simulator. Instead of having to install an android emulator, what if Dreamweaver comes with a Phonegap simulator. Since Phonegap is all javascript, it should be trivial to create basic UIs that look and feel like the native interface of the OS chosen. I would still have to do final tests on the emulator, which i believe are worthless, compared to running it on actual devices. My point is, installing the android emulator and getting the app to run in a emulator is really no big deal, but turns out be a huge time consuming step. For interested web developers, this could be skipped pretty easily, if only Phonegap had its own simulator.

This is all just theory, as you'd have to install the complete Android and ios sdk to compile it for your device, anyway. But it would be a welcome step.

#Presentation
The presentation was made as a string of screenshots developing the application, so its not really much help. But here it is anyway. [View Original](https://speakerdeck.com/u/captn3m0/p/akira-presentation).

<script async class="speakerdeck-embed" data-id="4f6effee933f08002201ea60" data-ratio="1.3333333333333333" src="//speakerdeck.com/assets/embed.js"></script>
 
#Prize
I won a PS3. Yay!

If you have any problems with the code, or the process, you can contact me at my [about page](/about)
