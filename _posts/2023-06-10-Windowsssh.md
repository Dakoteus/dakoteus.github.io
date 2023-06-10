---
layout: post
title:  "Windows Permission denied (password,keyboard-interactive)"
date: 2023-06-10 03:14:30 -0400
categories: jekyll update
---
<p align="center">
  <img src="/assets/images/cringe.png">
</p>
I had an ongoing issue where, randomly, I couldn't ssh anymore. I got the following "Permission denied (password,keyboard-interactive)". On stack, there's many answers that involve simply modifying the sshd_config, and I never changed this so I knew it wasn't the issue. Even so, trying these solutions failed. Finally, I enabled and looked at the debug logs. I found many errors, but also this one:

24172 2023-06-10 15:07:09.476 User ssh2 not allowed because shell\
c:\\program files\\powershell\\7\\pwsh.exe does not exist

Yes, ssh2, because I already tried nuking ssh along with the entire user "ssh" lol.
Anyways, this is the important error. Apparently there's a

\HKEY_LOCAL_MACHINE\SOFTWARE\OpenSSH\DefaultShell

key in regedit. It was set to a powershell path that did not exist. I dont think it ever existed. I don't know... Regardless, I just had to change this to where I know powershell lives, which for me was 

C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe

There ya go, if you were getting that error in the dbg logs, it's probably fixed now...\
Now... I guess, lets hope that path doesn't get changed?

Anyways, this problem has been eating at me for a long time and I had to dig to scrape up this solution.\
So I'm just putting it here to help a fellow computer user out.

cheers,\
dako

p.s. i want to post more, just havent had the time, we'll see 