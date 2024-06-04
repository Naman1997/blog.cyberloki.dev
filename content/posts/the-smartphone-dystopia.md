+++
authors = ["Naman Arora"]
title = "The smartphone dystopia"
date = "2024-06-04"
description = "How the you're being reprogrammed without root access!"
tags = [
    "Random",
]
categories = [
    "Random",
]
series = []
+++

# Introduction
Have you felt the need to constantly stay on your phone? Maybe your usage is not constant, but frequent? I've talked with my friends and family about the constant anxiety that we all feel when a smartphone is not in our hands. The root cause has been studied to death and we all know how the algorithms on various websites and apps have essentially reprogrammed our brains to crave more media.

I have a very similar struggle story with media consumption and in this post, I will discuss how I've managed to reduce my consumption over time. Take all of this advice with a bag of salt, because everyone is different and what worked for me, might not work for you.

## Changing file permissions
If we think of our brains as kernels of our operating system(soul?) we can make a very simple collrelation which I find hilarious. The file permissions under the dir `/etc/modules-load.d/` are misconfigured somehow! Those who are not familiar with this technical jargon, it basically means that companies have been modifying our brains(kernel) by taking advantage of our default core values. It's time we changed that.

Step one in getting your life back is admitting that you're addicted. Most people will have a hard time with step one. Not because it is something hard to admit, but because its hard to believe that you've let yourself go. The reason why YouTube, Instagram and other apps are such a big time sink is because time speeds up when we use these apps. We don't feel that 4 hours have passed. The only solution to this problem is to give yourself the actual statistics. Search for "Digital Wellbeing" in your smartphone settings. You should see some really crazy stats assuming that you've not been here before. The stats should also offer you a view where you're able to see your weekly usage as well.

My stats were horrible. To the point that I was wondering if I actually lived under a smartphone (Pun intended).

## Module uno
So, how do we change this situation? Here's what I did for starters. My instagram usage was the greatest time sink, so I started with that. I uninstalled instagram, but didn't delete my account  - this meant that I could still contact my friends over their website. Now, I don't have that many friends on Instagram, so it was possible that I could've deleted the account immediately. However, I still have some close friends that don't live near me anymore, and I want to stay in touch.

Now, you might think that that's a cope, and in some cases it might be. However, for me this one change did wonders. The web implementation of Instagram is such a mess that I hate using it. My daily usage went from around 3 hours a day to around an hour per week! That's a pretty good improvement. Now, you might think that my smartphone/media addiction has been cured since, well sorry to dissapoint but that's just now how it goes sometimes.

## Kernel Panics
Soon after making this change, I didn't have anything interesting to spend my time. Initially, I started to read some books, which was an improvement. The reason why books are a better media format is because you need to be actively paying attention in order to enjoy a book. However, it seems that I was not ready to quit just yet.

After my Instagram addiction ended, I got hooked on YouTube! Now this might seem like an improvement as I was now watching longer form content, however to tell you the truth, I don't remember which YouTube viedos I've watched last week. So overall, I'm not really gaining anything from wasting time there. Now, let's try the same solution for YouTube. I uninstalled the app and thought "Now my usage should drop similar to Instagram!". Oh how wrong I was. You see, YouTube unlike Instagram was designed first for the web. This means their website was actually better to use! Instead of reducing my usage, I ended up increasing it. My usage went from around 1 hour a day to around 4 hours a day.

This essentially put me in a worse position than before. Now, I thought that quiting YouTube cold turkey might be the right move. So, I did. I setup a Pi-Hole container on my network and basically blocked all requests from my devices that went to `*.youtube.com`. This actually backfired pretty badly. Whenever I got back from work or got tired after working on some project, I would take up my phone only to realize that YouTube was blocked. Now, here's the thing - if you are the one who configured the damn thing, then you're' also know how to remove it.

I would change my DNS settings and went back to doom scrolling again. The worse part is that once I changed the DNS settings, I would forget to revert it back for the next day!

This taught me that it was, in fact, a bad idea to quit cold turkey. Since then, I have changed the way I manage this addiction.
These are the steps that I followed for YouTube and other apps:
- Put a time limit on the apps taking more than 2 hours of your time
- Monitor the usage of your time per app
- Once the usage starts going down, immediately reduce the limit by 30 minutes
- Don't try to make drastic changes as you might just remove the time limit

Not having the phone in your line of sight will be the biggest improvement that you can make. Here are some simple thing I did to make sure that I stayed away from my phone in general:
- Turn off the internet and shove it in a drawer
- If someone wants to contact you, they can still call you
- If you're travelling/studying abroad - discuss a time to talk with your friends and family
- Understand that it is ok to miss random updates

## Kernel Optimizations
Now that your system is free to take up other things, you might suddenly feel the urge to pick up your phone again. In order to supress this feeling, you will need to distract yourself with other, better media. Not all media is bad. For example, I like to read Philosphy books at the local library in my free time. You might like reading a magazine while drinking coffee in your favourite Cafe. It all comes down to personal preference.

Whatever it is that you like doing, start with that. Slowly transition to other topics. You will not like all books and that is okay. What matters is that you read them instead of scrolling on your phone. Some people might also not like reading books, for them I recommend playing some games like Chess or Football. If you don't have enough interested people to play with you, then try walking in a park nearby. You can also go for trekking assuming that you live near hills. Basically go touch grass lol.

At this point, some people might start using youtube or other apps on their laptops. And as we all know, we don't exactly have a timer app on desktop OSs. Again, everyone is different, however, I didn't feel the urge to open youtube in my browser after I managed to stop my smartphone addiction.

However, I still made this change which might be useful to others. If you use Windows or Linux, you're able to redirect domains to some other IP. Assuming you're on Linux, you can update the hosts file like this:

```
echo '127.0.0.1  instagram.com' | sudo tee -a /etc/hosts
echo '127.0.0.1  www.instagram.com' | sudo tee -a /etc/hosts
echo '127.0.0.1  youtube.com' | sudo tee -a /etc/hosts
echo '127.0.0.1  www.youtube.com' | sudo tee -a /etc/hosts
cat /etc/hosts
```

After running the commands above, re-connect to your connection. You should not be able to visit these sites anymore from your browser.

## Custom modules
If you're still not able to reduce your screen time on your smartphone, you may try the following:
- Switch to a custom app launcher (I use Olauncher)
- Change colour profile of your phone to be Monochrome
- Restrict apps from sending you marketting notifications (Ex: LinkedIn, Google news, etc)

At the end of the day, you'll need to keep monitoring your screen time. Assuming it does not reduce to under 2 hours a day, you might need to take harsher actions. In this case, you can try the following:
- Only use your smartphone during work hours
- Shut it off after work
- Shove it in a drawer
- Use a dumb phone for contacting your family and friends (No Whatsapp, Instagram, etc)

Older dumb phones used to have a horrible mics - buy some good earphones to use for calls.

## Some crazy stats for motivating you!

Assuming that you use your smartphone for 5 hours a day on average, and you're 26 years old, you'll spend 11.67 years of your total life in front of your smartphone. Btw it gets worse if you're younger or spend more than 5 hours a day!

Check your results here: https://unplugged.rest/screen-time-calculator