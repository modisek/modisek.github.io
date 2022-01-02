---
title: "Move to Wayland"
date: 2021-12-29T12:53:12+02:00
draft: false
---

In my previous linux setup blogpost i said i might switch to wayland from the aging Xorg, and the vulnerabilities that were found in Xorg weeks prior have fasttracked that switch and over the weeked i moved to sway.Sway being the most mature wayland compositor won me over, i had said that maybe will try hikari  but have been desuaded by the lack of documentation.
Sway is familliar to me since its a fork of i3, i have used i3 for a while in the past and the setup for both is simillar save for a few things which makes sense only on i3(xorg)
i have had to find alternatives to my programs that depend on x, for example xclip, dmenu, sxhkd etc wont work on wayland but alternatives are available and work just as well

#### What i have observed when running sway/wayland

* it has removed screen tearing that i was experiencing
* smooth when when scrolling in web browsers

* apparently it uses less power than Xorg

some programs need some enviroment variables set to run

```
#if not using systemd, use logind separately
 export LIBSEAT_BACKEND=logind
#mozilla firefox 
 export MOZ_ENABLE_WAYLAND=1
 
 export XDG_CURRENT_DESKTOP=sway
#gtk apps
 export GDK_BACKEND=wayland
 export CLUTTER_BACKEND=wayland
 
 ```
 
 ...and chrome need to be started with a few flags
 
 ```
 chromium \
 --enable-features=UseOzonePlatform \
 --ozone-platform=wayland 
 ```
#### Problems encountered
 
 The problems i have encouted so far is both chromium and firefox closing randomly and screen recording not working even when using the pipewire backend. will look for solutions to both those problems
