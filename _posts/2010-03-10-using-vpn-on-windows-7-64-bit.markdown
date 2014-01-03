---
author: tpb976
comments: true
date: 2010-03-10 14:43:19+00:00
layout: post
slug: using-vpn-on-windows-7-64-bit
title: Using VPN on Windows 7 64-bit
wordpress_id: 77
categories:
- Windows 7
tags:
- 64 bit VPN Client
- VPN Client
- Windows 7
---

After using the Windows 7 RC for the last few months, I finally had to update it once March 1st rolled around.  I had been using the 32-bit version but decided to go with the 64-bit for the full version.

Since I work from home sometimes I was going to need VPN access to my work machine.  I went to install the Cisco VPN client that we use and found that I couldn't install it since it only came in a 32-bit flavor.  I figured it would be easy to just get a 64-bit compatible version and I would be on my way.  I soon found out that Cisco doesn't offer a 64-bit version unless you purchase their "AnyConnect" software which is an additional charge.

Since I was already at home and needed a solution immediately I started searching around.  I soon came upon a piece of software that some  people of the forums said would work.  The software is [ShrewVPN](http://www.shrew.net/software) from [Shrew.net](http://www.shrew.net).

After I installation it took me a minute to figure out how to run it since it didn't add an entry into All Programs.  I browsed to Program Files/ShrewSoft/VPN Client and found a few application files to run.  I eventually found that ipseca.exe was the file I need to run.

Once the app loaded up it was pretty easy to configure since I had the Cisco configuration file (.pcf) from work. I selected File/Import from the menu and browsed the .pcf file.  Once it was selected I was able to connect to my work VPN without any problems!
