---
layout: post
title: Installing Microsoft Security Essentials on Windows Server 2012 R2
subtitle: some devops today!
bigimg: ../img/analog.jpg
---

### I've got a Windows Server 2012 R2 on Azure (thanks to a friend, so I'm not paying for it). I use it for development and recently realized that I haven't got any AV on it!

Most solutions are paid, but I don't need one, I want to feel secure and MSE is definitely enough - I don't download torrents, movies etc, just basci web browsing like github, etc. Here's how to install a basci AV from Microsoft on it - just for safety.

The only thing you need to know that this is a 'hack' - that means that MSE is not supported to work on 2012 R2.
Instructions: 

1) Download a copy of MSE from Microsoft: http://windows.microsoft.com/en-us/windows/security-essentials-all-versions

2) Right Click on the "mseinstall.exe".

3) Click on Properties.

4) Click on the "Compatibility"-tab.

5) Locate the "Compatibility mode"-section.

6) Check "Run this program in compatibility mode for:".

7) Select From the (now active) dropdown menu "Windows 7".

8) Open a Command Prompt as Administrator.

9) cd to your Downloads folder (ie. cd C:\Users\%username%\Downloads).

10) Run "mseinstall /disableoslimit" and follow the installer prompts to install MSE on your Windows Server 2012.

thanks to: http://www.pwrusr.com/system-administration/microsoft/2-free-microsoft-windows-server-2012-antivirus-solutions
