---
layout: post
title:  "Hack the box: Getting your invite code"
date:   2020-03-16 23:14:36 +0800
categories: Walkthrough
tags: ["Hack The Box"]
comments: true
image: 
    feature: htb.jpg

---

This post documents the complete walkthrough of getting your invite code to register with Hack The Box. If you are uncomfortable with spoilers, please stop reading now.

<!--more-->

## What is Hack the Box ?

Hack The Box is an online platform that allows you to test and advance your skills in Cybersecurity. The platform contains assorted challenges( real world simulations or CTFs) that are continuously updated. Needless to say, Hack the box is beyond resourceful if you want to level up your cybersecurity skills; especially as a beginner.

## But Wait ... How do I join ?

To join, you have to "hack" yourself in. Don’t worry, I will try to simplify my guide as much as i can and hope it can help you get in. However, I highly recommend that you first try to get in(on your own), and only use this article as a guide in case you need help.


## So Let's GO !!!

First, visit the official [Hack the Box](https://www.hackthebox.eu) website. 

![htb.png](/hackdome/assets/images/posts/HTB-invite-code/htb.png)

As you scroll down to read more information, you will eventually see a join button ; please click on it.

![htb-joinnow.png](/hackdome/assets/images/posts/HTB-invite-code/htb-joinnow.png)

You’ll then be directed to https://www.hackthebox.eu/invite to join Hack The Box.

![htb-invite.png](/hackdome/assets/images/posts/HTB-invite-code/htb-invite.png)

##### Oh no ..... Did i misplace the invite code ?

No worries. We can right click on the page and choose the Inspect Element option. Under the Debugger tab, i am able to see what scripts have been embeded within the website.

![htb-jscheck.png](/hackdome/assets/images/posts/HTB-invite-code/htb-jscheck.png)

Going through the javascript ..... Seems like a dead end to me . Sigh .....

![htb-calm.png](/hackdome/assets/images/posts/HTB-invite-code/htb-calm.png  "calm.js")

![htb-frontend.png](/hackdome/assets/images/posts/HTB-invite-code/htb-frontend.png  "TL;DR")

#### But wait ....  this function looks interesing

![htb-inviteapi.png](/hackdome/assets/images/posts/HTB-invite-code/htb-inviteapi.png  "Shine Like a Diamond")

Let's run it within the developer console and see what comes up. As expected, you will get a status code 200 and data as shown below:

![htb-makeinvitecode.png](/hackdome/assets/images/posts/HTB-invite-code/htb-makeinvitecode.png)

Could it really be so easy and simple ? The code is just right there. 

#####Bazzinga !!!! 

From the enctype:"ROT13", it tells me that there's decoding to be done.


    0: 200                                                                        
    
    data: Object { data: "**Va beqre gb trarengr gur vaivgr pbqr,
    znxr n CBFG erdhrfg gb /ncv/vaivgr/trarengr**", **enctype: "ROT13"** }
    


![lotr-ring.gif](/hackdome/assets/images/posts/HTB-invite-code/lotr-ring.gif)

Now lets head over to decode the code with ROT13.

![ROT13-decode.png](/hackdome/assets/images/posts/HTB-invite-code/ROT13-decode.png)

##### New Lead !!!! Lets do a post request as seen then.

Firing up the terminal and perform a post command.

    curl -XPOST https://www.hackthebox.eu/api/invite/generate

and heres the results we gotten and we got another code. Looking out at the format, this code needs some decoding.

    {"success":1,"data":{"code":"S0VLWUItRE9STUktUkZWV0EtRlFKSFItRVBEWkk=",
    "format":"encoded"},"0":200}

Heading over to another website for decoding. Pasted the code in and press decode , now we wait.

![one-eternity-later.png](/hackdome/assets/images/posts/HTB-invite-code/one-eternity-later.png)

![htb-b64decode.png](/hackdome/assets/images/posts/HTB-invite-code/htb-b64decode.png)

Now, finally go to https://www.hackthebox.eu/invite and paste the Invite Code you got in the textbox asking for the same.

And **YES** You’re in! You can sign up on the site now and become a member.

![htb-ctf.png](/hackdome/assets/images/posts/HTB-invite-code/htb-ctf.png)

So you sure you wanted to continue on this journey ???

![ruready.png](/hackdome/assets/images/posts/HTB-invite-code/ruready.png)
