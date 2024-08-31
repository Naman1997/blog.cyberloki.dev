+++
authors = ["Naman Arora"]
title = "My Linux Beginnings"
date = "2024-04-15"
description = "Beginning of my linux experience"
tags = [
    "Hardware",
]
categories = [
    "Hardware",
]
series = []
+++


# Preface

Do you live in a house with no ethernet wiring? Do you have an old broken laptop that you'd like to salvage? Do you have a desktop that could use wifi, but wifi chips are too damn expensive?

If you answered 'yes' to all the questions above, then keep reading more to how I (and hopefully you) saved money by salvaging a broken laptop.

# Introduction

The tale begins when I was about to leave for Australia for my higher studies. I used to own a pretty badass PC with a 10th gen i7, 32GB of RAM, RTX 3070 and a bunch of networking cards for learning VLANS and other networking related things. This thing was a beast. I ran Proxmox as bare metal and passed through the intel iGPU to a Linux VM and passed through the RT3070 to a Windows VM. Now, this is a pretty complicated setup because you cannot actually access the Proxmox OS without networking. What I mean is that you need SSH or the Proxmox web GUI to be able to manage this OS, if the networking stack goes down for any reason, you cannot access the shell because well, that intel iGPU is actually invisible to the OS! There are ways around this, but maybe we'll get into that in another post.

For the purposes of this post, I could not leave such a complicated setup with my family. I could try and manage it remotely, but I would not be able to debug any issues in case Proxmox decided to push a bad update. My dad was the one who actually introduced me to Linux, but in this case I decided that Windows was a better choice if I wanted him to have a good experience.

# The problems begin

So now, I had windows installed and also had set up an alternate user with Tailscale installed in case I wanted to remote into the system. However, I had failed to realize that the OS was going to be the least of my problems in this transfer. My family decided they wanted the system to not be in my room, but in the living room. Now the reasoning behind this is beyond me to this date. The issue with such a move is that the WAN for our house entered from my room and basically ended there. Since we were renting the place, we were not allowed to drill any holes for wiring in Ethernet.

In any case, everyone decided that my old room was going to be used as a guest room and that I had to move my PC to the living room. And so, I moved the whole thing without the networking bits to the living room.

# But my puter!

No matter how powerful and amazing your computer is, it is basically useless if it isn't connected to a network. Soon everyone realized the same thing. Even though my dad wanted to use the PC for running some excel voodoo, he could not be bothered to copy and paste files from another computer only to process things on this one.

Similarly for me, I wanted to be able to access this thing using which I could basically emulate an entire Active Directory environment. For those who don't know, AD environments are the prime targets for hackers and it would be my job to secure such environments if I get good enough at it.

# Enter WiFi

So at this point, we realized that we would need a WiFi chip that we could slot in one of the M.2 slots that supports a Wifi card. You might find something like this in your motherboard manual.

{{< figure src=/images/I-heard-you-like-wifi/motherboard.png >}}

The only problem is that good Wifi chips are expensive in India. I would have spent the money, but I had an amazing idea.

I used to have a laptop whose motherboard essentially fried itself (thank you asus) and I wondered if I could salvage the Wifi chip. And so, I opened it up, pulled out the wifi card, plopped it onto the PC motherboard and voila! Now, the chip works, however it is not that easy - you also need a good antenna if you want to have any range. Laptops actually use the screen bezel as placeholders for these antennas! This way even though your laptop does not have huge antennas sticking out of it, it is able to pick up wifi signals.

# Time for a screwdriver!

I pulled out the wireless wires from my laptop and plugged them into antennas from an even older wifi router. This is an image of me opening up the display housing of my laptop. It houses the connector wires that plugged into the wifi chip.

{{< figure src=/images/I-heard-you-like-wifi/opening-the-screen.png >}}


The image below actually shows the wifi chip that is plugged into the motherboard along with the black and white wires that I extracted from the laptop's display housing.

{{< figure src=/images/I-heard-you-like-wifi/wifi-chip.png >}}

(Before you say anything about the dust, know that I tried lol)

The eagle eyed amongst you might have noticed some wires that are connected to the power pins. I actually had previously managed to break the power button of my case somehow. I had enabled wake-on-lan for the motherboard, but it didn't make sense to ask my family to set that up on their mobiles, so this was my solution.

Finally I zip tied part of an old router to the PC and connected its antennas to the wires coming from the wifi chip. Yes, it looks dumb and yes, it works.

{{< figure src=/images/I-heard-you-like-wifi/router-antenna.png >}}