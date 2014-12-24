---
title: How to Remove Snuko/MyAntiTheft.com
author: Bob Orchard
excerpt: After ten months of attempting to contact those individuals behind Snuko, which was rebranded to MyAntiTheft, and receiving no response or any sort of public message – I got fed up with Snuko running on my computer.
layout: post
permalink: /articles/how-to-remove-snuko-myantitheft/
dsq_thread_id:
  - 1311609566
categories:
  - Articles
---
After ten months of attempting to contact those individuals behind Snuko, which was rebranded to MyAntiTheft, and receiving no response or any sort of public message &#8211; I got fed up with Snuko running on my computer.

<!--more-->

My trouble today started when I restarted my Macbook Air after manually performing some updates to some apps and for Mountain Lion. When I logged in, I noticed that I had not one, but FIVE Snuko icons on my toolbar. I've hunted and researched for ten months to no avail on how to get this infernal application off my computer. Needless to say &#8211; I have learned a lot on how the Mac OS works, and after some poking, prodding, and looking I got it off my computer. A big help was this article on the <a href="http://www.formaceyesonly.com/2011/04/26/start-taking-control-of-startup/" target="_blank">different startup process</a> types on a Mac.

<!--more-->

## Finding the &#8220;source&#8221;

The first was that there was a process running in Activity Monitor called USBMonitor. Well &#8211; since I have two usb ports, and not five, I knew something was up there. No information was available on the process, but that lead me to look into the Launch Daemons for my computer. A Launch Daemon runs when the computer runs, and even if the user isn't logged in. After looking at the list, I noticed two items that didn't match:

  * <span style="line-height: 16px;">com.sasvc.sasvc.plist</span>
  * <span style="line-height: 16px;">com.bmon.bmon.plist<br /> </span>

I removed them &#8211; and they came back. I then found that I needed to unload them from my Daemon Launch Control &#8211; and from there the removal was quite easy.

## Here's how I did it:

First &#8211; open up Terminal on your computer and enter the following command:

<p style="padding-left: 30px;">
  sudo bash
</p>

You'll then need to navigate to your Launch Daemon folder:

<p style="padding-left: 30px;">
  cd /Library/LaunchDaemons/
</p>

You're in the right folder, so now we'll unload them from Launch Control:

<p style="padding-left: 30px;">
  launchctl unload -w /Library/LaunchDaemons/com.bmon.bmon.plist
</p>

<p style="padding-left: 30px;">
  launchctl unload -w /Library/LaunchDaemons/com.sasvc.sasvc.plist
</p>

Now that we've unloaded them &#8211; we can remove them entirely:

<p style="padding-left: 30px;">
  rm com.bmon.bmon.plist com com.sasvc.sasvc.plist com
</p>

After removing the plist files &#8211; we now need to kill the processes, so use:

<p style="padding-left: 30px;">
  killall bmon sasvc
</p>

## Phew&#8230;&#8230;..

Now that we've done all that manual work &#8211; we can rest easy. Snuko/MyAntiTheft won't run again on your computer!