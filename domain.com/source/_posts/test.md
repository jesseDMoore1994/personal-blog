title: WSL2
author: Jesse Moore
tags: []
categories: []
date: 2020-12-27 22:57:00
---
# What a nightmare.

## Background:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;I somehow managed to get WSL2 to work on my desktop machine. I had some downtime following Christmas this year and felt inspired to get a suitable development environment set up on my desktop windows PC. What can I say, I found [this article](https://www.hanselman.com/blog/scott-hanselmans-2021-ultimate-developer-and-power-users-tool-list-for-windows) by Scott Hanselman and thought "Yeah sure, that seems like a good way to spend the day after Christmas". I'm a Linux guy. My professional job works primarily in a linux development environment and let me tell you I have never been so grateful. All this said, there are a couple of reasons why I put myself through this excercise in humility.

- My roommates prefer Windows. We share my desktop as a game platform, streaming endpoint, general purpose device. I could convert my desktop to Arch, install i3-gaps, and have the time of my life. The problem there is that my family (The beautiful people that they are) will never appreciate the elegance of tiling window managers. I can say, "It's simple, ctrl+d to open the launch menu, type in google-chrome, and hit enter: Boom! Internet Access!" until my face is blue, it doesn't change the fact that the interfaces I feel comfortable with look like a scene from Hackers to them. As such, I'm trying to find a happy balance between my needs as a power user and theirs as persons who are blissfully unaware of the nagging itch of **GOD I REALLY WISH I COULD JUST TYPE A COMMAND TO INSTALL THIS SOFTWARE INSTEAD OF USING THIS .MSI INSTALLER.**
- Self preservation. God forbid I ever have to work primarily on a Windows machine. Should that unfortunate fear becomes a reality, I would like to have a system in place to at least be a functional employee (If I can at least administer the new machine...). The end result from setting up WSL2 and getting the Ubuntu 20.04 is actually decent. I'm a simple guy, I do most of my linux development using tmux and vim, so having a simple Ubuntu command line is enough for me. Some strange obscurities sure, but it feels "Linux-y" enough that I can get some work done.
- New experience. While I despise Windows for reasons that I will get into by detailing this WSL2 process, I still recognize that this is a valuable learning experience. In case I don't get to choose your deployment or learning environment, sometimes all you can do is make do. For this fact, I want to be more adept in the environment. By setting up this environment I'm hoping to become more familiar with the bizzaro world of development in .NET land. 

## What I did:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Referring back to [Scott's blog](https://www.hanselman.com/blog/scott-hanselmans-2021-ultimate-developer-and-power-users-tool-list-for-windows), I followed his tips for installing two items, WSL and Windows Terminal. The installation for WSL in his blog entry points directly to Microsoft's documentation [here](https://docs.microsoft.com/en-us/windows/wsl/install-win10?WT.mc_id=-blog-scottha). It's a dry read but it gets the job done... *Is what I would like to say.* For the life of me I would love to know the magical incantation is to getting painless and easy Windows installs, but I have long suspected (although I cannot prove) that its actually impossible. My primary complaint here IS NOT the documentation, the documentation works and it works well. I'm sure it for most people who don't punish and abuse their computers it probably works without a hitch, but I am not that user. The great part about using Linux is that when I encounter a problem, I'm probably not the first person to encounter it. A quick google search of the descriptive error message will tell me that I'm missing a developer package or I've got an out of software version. You don't have the same luxury in Windows. Instead, you get greeted by something like the following.

```
Uh oh, Windows hit a problem, try again later or restart your PC.

Error Code: 0x80070005
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The Store app for Windows, for some reason or another, could not download the Ubuntu 20.04 image from the microsoft store. I reverted to my natural programmer caveman tendencies: "No problem, I'll do some research, fix the problem, and be on my way". Oh how optimistic I was. How in the world am I expected to figure this out? From where I'm from, I'm told specific and informative errors about the cause of my problem. All I get from the message above is an error code and something I would tell my mom in the case that her modem "stopped working". No details or directives that I could follow here besides what essentially equates to sit and spin.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;I spent MULTIPLE hours googling things like `microsoft store 0x8007005 cannot download`. Turns out, `0x8007005` is windows speak for "Generic Permissions Error". Great, now at least I know what I'm dealing with, so I refined my search and started looking for answers. I went from [thread](https://answers.microsoft.com/en-us/windows/forum/windows_8-windows_store/cant-install-apps-from-store-error-0x80070005/1da61861-26ee-41b4-ada9-8ac516b0107a), to [thread](https://appuals.com/fix-error-0x80070005-on-windows-10-store/), to [thread](https://windowsreport.com/windows-10-store-error-0x80070005/) trying to find the fix for my problem. I Tried the following in my quest to get WSL2 working on my machine.

- Resetting Windows Store with WSReset
- Giving everyone access to `%localappdata%/packages`
- Verifying that Windows is up to date.
- Verifying that Store is up to date.
- Run the Windows troubleshooter tool.
- Performed a ZFS scan.
- Checked my date/time settings.
- Clearing the Store cache.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The sad part is, somehow or another one/many/all of these fixed the problem, but I can't say for certain what that was. For all I know, I had to reboot 20 times in a row to fix the problem. My suspicion is that the packages folder that was giving me the headache. Most of the error walkthroughs suggest starting there and thats probably a good idea. They all specify making sure that the users NT group has access permissions to the folder, but everyone *seemed* like the NT group that would work for me. I say *seemed* because it didn't work after the configuration change, I was trying two or three of the items from this list and then rebooting because it seems like every Windows troubleshooting step ends with "...then reboot your machine". After adjusting the permissions to everyone and rebooting the machine the Ubuntu app downloaded and installed like I hadn't spent 4 hours of my life trying to solve it.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Anyways, after figuring out that fiasco; smooth sailing all around. If someone else ever runs into this problem I would probably tell them to side step the windows store entirely and download the tools directly. Windows maintains downloads for the Linux distro's supported by WSL. You lose out on automatic updates from the Windows store, but how often are you realistically going to upgrade an Ubuntu LTS release? Don't waste 4 hours of your life. Get the image by downloading the appx and install it, and spend your remaining 3 hours and 45 minutes doing what you were planning on doing.

## What I learned:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; I learned that I don't know anything about the inner mechanations of Windows. I suspect that if I keep this up I will be a little bit better in black box debugging. I also learned that the Windows documentation is decent, its not Arch Wiki good, but it can get you there granted the following:

- You have a clean install.
- You have some basic technical know-how.
- You have the patience to sync time into cryptic errors.

## What I gained:

I now have WSL2 and Windows Terminal on my home desktop! Once I got the Ubuntu command line I got right back into the groove with oh-my-tmux and oh-my-zsh. Now my roommates and  I can watch Burn Notice on Hulu while I bash my head against the keyboard!

![WSL2 and WT screen capture](/images/wsl2_and_wt.PNG)



