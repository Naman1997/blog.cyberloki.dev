+++
authors = ["Naman Arora"]
title = "My Linux Beginnings"
date = "2024-04-15"
description = "Beginning of my linux experience"
tags = [
    "linux desktop",
]
categories = [
    "linux desktop",
]
series = ["Linux"]
+++

# Preface
I've always been a big Linux guy. I started running Linux back while I was studying for my bachelors. Since I had no clue which distro was good or bad, I had to go with the most meme-worthy one. I started out with Arch Linux because I saw a meme that went like: "I run Arch btw" on reddit. I didn't quite get what the hype was all about initially, had I known the pain and suffering that I will have to go through just to get the system to boot, I would thought twice before taking the jump.

# The day of reckoning
I still remember the day I decided to install Linux. I had a nice Asus Laptop with an i5-7200U and 8GB of RAM. This was the only machine I had back in college. This presented an interesting challenge where I had to open up the Arch wiki on my smartphone and figure out the install process on a small screen. Back in college, I didn't exactly have the fastest internet nor the best hardware to be doing this.

Another interesting fact is that [archinstall](https://github.com/archlinux/archinstall) did not exist back then. I absolutely love the project and believe that it's the sole reason that I've stuck to Arch for so long. 

And so, with my USB armed with the magic of Free and Open-source, I began my journey and booted up my laptop into the Arch installer. Arch is one of the distros that are liked by people because it sticks to the basics. The black screen with nothing but a blinking cursor was the real start of an amazing journey.

The first hurdle that I ran into was Wifi. I didn't had access to any Ethernet and was actually planning to install the system over a mobile hotspot. After searching the manual for around 5 mins, I found the commands for connecting Wifi. After fiddling with `iw` for what seemed like an eternity, I was finally connected to the internet.

Rest of the install setup was a breeze, most cli tools had a tui interface. The docs were intuitive enough to figure out the right options that I needed. After running `pacstrap` and rebooting the computer, I was crazy tired. I realize now that it was crazy in the first place to attempt this, but hey, a college student with time to kill don't have anything better to do sometimes.

After all that, I was left with a black screen after almost a 4 hour install process. The first install had gone badly. What I haven't told you yet dear reader, is the fact that my laptop also came with an Nvidia discrete GPU.

What I hadn't realized at the time was that the install had actually gone successfully. However, my screen could not display anything because I chose to install the wrong drivers. My laptop was too new back then and nouveau didn't have the right code to get this thing to work.

At this point, I should have backtracked my steps and tried to figure out where I went wrong. However, being a broke student with their only laptop not working while assignments might show up anytime didn't inspire much motivation for such mental gymnastics.

# The point of no return

I realized at this point that there was no way to rollback to windows. Setting up a windows ISO requires me to open a browser, download an ISO and to burn the ISO onto a USB drive. All of this requires another working system!

I panicked and attempted to boot into the installer again. This time, the display worked again and I was greeted with the cursor on a black screen again. I was relieved that I didn't actually break my only system and confused why it didn't actually work.

Despite being the IT whiz at my house, my skills were not enough for this task. So, I did what any good engineer would do in my shoes. I attempted the install again.

After another 4 hours, it was clear that I was doing something wrong. I decided search for the symptoms on Google. After looking around for an hour or so, I came across a person having the same issues as me. Following that thread lead me to understand what I was doing wrong.

# Proprietary drivers FTW?

Using the proprietary drivers sounded like a bad idea back then. It still does, if I'm being honest, but it fixed my system back then and I couldn't be more grateful.

Although I'm not exactly happy about running proprietary drivers on my machine today, I do need to give credit where credit is due. From my experience, the proprietary drivers have always had better compatibility and performance on all my devices. I do hope that this changes with the advent of projects like NVK in the future.

# Conclusions
- Don't try experiments on your only machine.
- Make sure to make a backup image/disk on a
separate disk if you do.
- For the love of all that is holy, do not try Arch as your first distro.
