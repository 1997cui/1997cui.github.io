---
layout: post
title:  "My ISP in Seattle area: Ziply Fiber"
date: 2025-07-02
categories: Life
tags:
    - Ziply Fiber
    - ISP
    - Seattle
    - Internet
    - Fiber Optic
    - Broadband
    - Xfinity
---

<span style="font-size:large;color:red">If you want to give Ziply Fiber a try, use [my refer link](https://refer.ziplyfiber.com/tianyic-24) to get $100 credit!</span>

# How to find out a good ISP for my home?

As I am working in Tech Field, a lot of my friends asks me what is my ISP and how to deal with Xfinity. I'd like to discuss this topic here today.

First, all the residential ISPs some time ago is highly subsidized by the FCC and Federal funds. A lot of times, it is not ecnomical for the ISPs to build out new networks, see the comments of u/jwvo on [this post](https://www.reddit.com/r/ZiplyFiber/comments/kzngy9/any_plans_of_expansion_south_of_bellevueredmond/).

**The easiest way to find out who serve you is use FCC broadband map, see [here](https://broadbandmap.fcc.gov/)**, just enter your address and see all the providers. Fiber is better than cable, and cable is better than anything else. If you can get fiber, get it. If you can get cable, get it. If you can only get DSL, well, you have no choice. Below I will discuss my past experience with ISPs in Seattle area.

# How to find a good plan for a given ISP?

**Read** [the broadband facts labels](https://www.fcc.gov/broadbandlabels)! A lot of times, the ISP hide it under the bottom of the page, please please check it.

Here is an example of hidden broadband facts label provided by Xfinity:
![Here is an example of hidden broadband facts label provided by Xfinity](/wp-content/uploads/2025/isp/hidden_facts.png)

Click the expand label, and **read them line by line**:
![Sample broadband facts label](/wp-content/uploads/2025/isp/label1.png)

Here you can find the upload speed, after-promotion pricing and the datacap, which, is typically buried in the find print. ISPs only show you the download speed in their advertisement.
<span style="color:red">***Took a screenshot of it and save it before ordering***</span>. In case of a dispute, you can use it as the evidence.


# Xfinity

Xfinity is notorious for their bad customer service and bait-and-switch promotion pricing. If you want to cancel it, you have to call in and wait forever, there is a lot of frictions to deal with them. Previously, they have a 1.2TB data cap until they just [removed it a couple days ago](https://corporate.comcast.com/press/releases/comcast-new-national-xfinity-internet-packages-unlimited-data-advanced-wifi-gateway). I personally never went over the cap, but it makes me pretty nervous about that. 

They are using the cable technology, so the latency is higher than fiber, and the speed is asymmetric. The upload speed is lowered. If your xfinity upload speed >= 50Mbps, you are in a **[Enhanced Speed Markets](https://www.xfinity.com/hub/internet/faster-upload-speeds)**, which means you need not only need to get a DOSCIS 3.1 modem, but the ones that are specifically certified by Xfinity which offers a higher upload speed. I uploaded a pdf [here](/wp-content/uploads/2025/isp/2024.08.14 Full List of Compatible Devices.pdf), but it may not be the latest one. As the time I wrote this in 2025, the URL is [here](https://www.xfinity.com/support/internet/customerowned).

The good thing about Xfinity is that their service is widely available, decently reliable (Although when the power is out, they are out too) at where I live near Seattle. They offer `/60` ipv6 prefix, works pretty good (Compared with Quantum Fiber, Ziply Fiber and WaveG).

Previously, I've used the trick that at the end of the promotion period, I canceled the service, and let my roommate to sign up a new account with the same address, and activate it immediately. No service disruption at all. As long as the new account is established, the old account will be canceled automatically. Nowadays, this trick is not needed since they have the 5 year price guarantee now. So, at most, you only need to do it once every 5 years.

# [Ziply Fiber](https://refer.ziplyfiber.com/tianyic-24)

This is the ISP I am currently using. The signup and installation process is pain in the butt, it took me half a year and endless followups to get the service installed. When I moved into where I live now, the previous owner did not use Ziply Fiber and there is no fiber buried. 

After calling them, they need a couple weeks to a month to bury the cable from the handhole in the front of my neighbor's house to the sidewall of my garage. After that, the technician from Ziply Fiber came to my place to do the indoor installtion, which, only found out that there was no spare fiber from their Hub/splitter to the handhole in front of my neighbor's house and they just left. A couple months later, I scheduled another appointment, and the result is the same, technician came, no fiber, and left. This repeated a couple times, until I escalated this issue multiple times. They finally applied a permit from the city (Took several weeks for them to prepare, and took another month for the city to issue the permit). Then it is the forever wait for their contractor to pull the cables and close the permit. Then, wait for another couple weeks for them to update the system, activate the port, and finally another technician came and installed the ONT. The technician who worked for Ziply Fiber is very nice and the ONT installation is a breeze (See below). 

However, the whole installation process is very painful, and I had to push the project till the end (I felt I was working to get this done). To be honest, if all process is smooth, the installation should had worked out easily. However, in the case of any difficulties, there is absolutely lack of communications between their back office, the different contractors (Who installed the fiber from handhole to the sidewall of my garage, permit and pull fiber etc.), an their technicians. I felt like I was working as a project manager to get this done. 😂 Ziply Fiber really should pay someone to do this job.

While I was painfully pushing the project, I run my own fiber/Ethernet wiring around my place to make sure they are terminated and ONTs can be installed in a central location that I preferred, I also installed cameras and access points etc, spent me a lower couple thousands.

Till now, they have no IPv6 at all, but the symmetric speed, no data cap, lower latency and more reliable buys me in.I am currently on their 1Gbps plan for $60/month for the first year, and after than it will be $90/month, honestly, it is not cheap. I havn't decided what to do after the first year, but I will probably stay with them for a while.

After the installtion, the service works great, and never let me down, one bonus point is that their [VP u/jwvo](https://www.reddit.com/user/jwvo/) is very active on Reddit, and he is very responsive. If there are any issues general customer care cannot resolve, he is pretty good at it.

The speed looks like this:
```bash
ctyi@cuiDesktop:~/software/ookla-speedtest-1.2.0-linux-x86_64$ ./speedtest -s 51693 

   Speedtest by Ookla

      Server: Ziply Fiber - Bothell, WA (id: 51693)
         ISP: Ziply Fiber
Idle Latency:     2.66 ms   (jitter: 0.21ms, low: 2.42ms, high: 2.80ms)
    Download:   926.47 Mbps (data used: 418.6 MB)                                                   
                  8.05 ms   (jitter: 0.62ms, low: 2.07ms, high: 10.60ms)
      Upload:   940.79 Mbps (data used: 423.3 MB)                                                   
                  4.83 ms   (jitter: 0.71ms, low: 2.43ms, high: 6.58ms)
 Packet Loss:     0.0%
  Result URL: https://www.speedtest.net/result/c/3ce33b02-6706-42ce-9b67-7715fd5b5e1a
```
<span style="font-size:large">If you want to give Ziply Fiber a try, use [my refer link](https://refer.ziplyfiber.com/tianyic-24) to get $100 credit!</span>