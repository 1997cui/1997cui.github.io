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

# Latest update as of May 2026

<span style="font-size:large;color:red">I am no longer using Ziply Fiber for now due to the price increase and running out of the promotion period. I am currently using **Xfinity**.It currently offers $50 for 1Gbps with 5 years price guarantee at my address for now. Use [My Link](https://referafriend.xfinity.com/1997cui!1018da34fe!a) if you are interested.</span>

# Key Takeaways

- Use the [FCC broadband map](https://broadbandmap.fcc.gov/) to see all available ISPs at your address.
- Always check the [broadband facts labels](https://www.fcc.gov/broadbandlabels) for real plan details (upload speed, after-promotion pricing, data cap).
- Fiber > Cable > DSL for speed, reliability, and latency.
- Xfinity is widely available but has customer service and pricing issues.
- Ziply Fiber offers symmetric speeds and no data cap, but installation can be slow and communication is lacking.

# How to find out a good ISP for my home?

As I work in the tech field, a lot of my friends ask me what my ISP is and how to deal with Xfinity. I'd like to discuss this topic here today.

First, all the residential ISPs some time ago were highly subsidized by the FCC and federal funds. A lot of times, it is not economical for the ISPs to build out new networks. See the comments of u/jwvo on [this post](https://www.reddit.com/r/ZiplyFiber/comments/kzngy9/any_plans_of_expansion_south_of_bellevueredmond/).

**The easiest way to find out who serves you is to use the FCC broadband map, see [here](https://broadbandmap.fcc.gov/)**. Just enter your address and see all the providers. Fiber is better than cable, and cable is better than anything else. If you can get fiber, get it. If you can get cable, get it. If you can only get DSL, well, you have no choice. Below I will discuss my past experience with ISPs in the Seattle area.

# How to find a good plan for a given ISP?

**Read** [the broadband facts labels](https://www.fcc.gov/broadbandlabels)! A lot of times, the ISP hides it at the bottom of the page. Please, please check it.

Here is an example of a hidden broadband facts label provided by Xfinity:
![Here is an example of hidden broadband facts label provided by Xfinity](/wp-content/uploads/2025/isp/hidden_facts.png)

Click the expand label, and **read them line by line**:
![Sample broadband facts label](/wp-content/uploads/2025/isp/label1.png)

Here you can find the upload speed, after-promotion pricing, and the data cap, which is typically buried in the fine print. ISPs only show you the download speed in their advertisement.
<span style="color:red">***Take a screenshot of it and save it before ordering***</span>. In case of a dispute, you can use it as evidence.

# ISP Comparison Table

| ISP           | Technology | Symmetric? | Data Cap | IPv6 | Price (1st yr) | Price (after) | Notes |
|---------------|------------|------------|----------|------|----------------|---------------|-------|
| Xfinity       | Cable      | No         | No (as of 2025) | Yes  | Varies         | Varies        | Widely available, 5-year price guarantee |
| Ziply Fiber   | Fiber      | Yes        | No       | No   | $60/mo         | $90/mo        | Installation can be slow, great support on Reddit |

# Xfinity

Xfinity is notorious for their bad customer service and bait-and-switch promotion pricing. If you want to cancel, you have to call in and wait forever; there is a lot of friction to deal with them. Previously, they had a 1.2TB data cap until they just [removed it a couple days ago](https://corporate.comcast.com/press/releases/comcast-new-national-xfinity-internet-packages-unlimited-data-advanced-wifi-gateway). I personally never went over the cap, but it made me pretty nervous.

They use cable technology, so the latency is higher than fiber, and the speed is asymmetric. The upload speed is lower. If your Xfinity upload speed is >= 50Mbps, you are in an **[Enhanced Speed Market](https://www.xfinity.com/hub/internet/faster-upload-speeds)**, which means you not only need to get a DOCSIS 3.1 modem, but one that is specifically certified by Xfinity to offer higher upload speed. I uploaded a PDF [here](/wp-content/uploads/2025/isp/2024.08.14%20Full%20List%20of%20Compatible%20Devices.pdf), but it may not be the latest one. As of the time I wrote this in 2025, the URL is [here](https://www.xfinity.com/support/internet/customerowned).

The good thing about Xfinity is that their service is widely available and decently reliable (although when the power is out, they are out too) where I live near Seattle. They offer a `/60` IPv6 prefix, which works pretty well (compared with Quantum Fiber, Ziply Fiber, and WaveG).

Previously, I've used the trick that at the end of the promotion period, I canceled the service and let my roommate sign up a new account with the same address and activate it immediately. No service disruption at all. As long as the new account is established, the old account will be canceled automatically. Nowadays, this trick is not needed since they have the 5-year price guarantee now. So, at most, you only need to do it once every 5 years.

This is the ISP I am currently using. The signup and installation process is a pain in the butt; it took me half a year and endless follow-ups to get the service installed. When I moved into where I live now, the previous owner did not use Ziply Fiber and there was no fiber buried.

After calling them, they needed a couple weeks to a month to bury the cable from the handhole in front of my neighbor's house to the sidewall of my garage. After that, the technician from Ziply Fiber came to my place to do the indoor installation, only to find out that there was no spare fiber from their hub/splitter to the handhole in front of my neighbor's house, so they just left. A couple months later, I scheduled another appointment, and the result was the same: technician came, no fiber, and left. This repeated a couple times, until I escalated this issue multiple times. They finally applied for a permit from the city (took several weeks for them to prepare, and took another month for the city to issue the permit). Then it was the forever wait for their contractor to pull the cables and close the permit. Then, wait for another couple weeks for them to update the system, activate the port, and finally another technician came and installed the ONT. The technician who worked for Ziply Fiber was very nice and the ONT installation was a breeze (see below).

However, the whole installation process was very painful, and I had to push the project till the end (I felt I was working to get this done). To be honest, if all processes were smooth, the installation should have worked out easily. However, in the case of any difficulties, there is absolutely a lack of communication between their back office, the different contractors (who installed the fiber from handhole to the sidewall of my garage, permit and pull fiber, etc.), and their technicians. I felt like I was working as a project manager to get this done. 😂 Ziply Fiber really should pay someone to do this job.

While I was painfully pushing the project, I ran my own fiber/Ethernet wiring around my place to make sure they were terminated and ONTs could be installed in a central location that I preferred. I also installed cameras and access points, etc. It cost me a lower couple thousand.

Till now, they have no IPv6 at all, but the symmetric speed, no data cap, lower latency, and more reliability buy me in. I am currently on their 1Gbps plan for $60/month for the first year, and after that it will be $90/month. Honestly, it is not cheap. I haven't decided what to do after the first year, but I will probably stay with them for a while.

After the installation, the service works great and has never let me down. One bonus point is that their [VP u/jwvo](https://www.reddit.com/user/jwvo/) is very active on Reddit, and he is very responsive. If there are any issues general customer care cannot resolve, he is pretty good at it.

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