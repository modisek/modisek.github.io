---
title: "My Linux Dev Setup"
date: 2021-11-19T18:57:07+02:00
draft: false
cover : "imgs/preview.png"
---

### Why linux
I have been using linux for a few years now and i dont see myself going back to windows machine anytime soon,as a developer linux offers me powerful tools that help me be productive.The commandline is way more efficient and allows me to automate with ease some of my most common tasks.

 I prefer linux distributions that allow me to build my setup from scratch, they just provide the base system and i can choose what software to install, this reduces bloat, allows me to chose sooftware that is lightweight, this is importatnt because i have luckluster hardware, i use an old lenovo laptop with low Ram, and to add salt to injury the Ram is soldered into the motherboard meaning that it cant be upgraded.it was unusable with windows so i threw linux ont it and gave it new life, also utilized zram to better use the ram that is available, its barely usable but way better than when it had winows on it.The distro i went with is void linux, an independent distribution built from scrath that uses xbps as its package manager and uses runit as the init system,it has been likened to openbsd om many occasions

check it ou at [void linux](https://voidlinux.org/)
This is part of a series i am doing on my linux setup
1.  > [my linux setup(overview)](#)
2. [setting up void using ansible]({{< ref "/posts/ansible-dev-laptop.md" >}})
### Details of my Setup

| item  | details          |
| ----- | --------         |
| os    | void linux(musl) |
| wm    | cwm              |
| term  | uxterm           |
| Ide   | nvim + tmux      |
| font  | terminus         |
| bar   | dzen2            |


### Cwm window manager

Due to the low memory i chose not to use a desktop environment but rather a window manager, the latter being lightweigt and also has cool features suc as tilling andbetter use of screen real estate in my opinion since there are no window decorations and other useless fluff.The wm i chose is called cwm an Xorg window manager, its floating by default but can also tile at the press of a button, it gets out of my way and provides searching for windows if you opened too many windows and struggling to find your way to the app you need

 I have been thinking of moving away from Xorg to wayland and will try hikari since it is the spiritual successor to cwm

My editor of choice is neovim, its doesnt use a lot of ram and starts up quickly, with their 0.5 release neovim became even more powerful with the addition of a native lsp and tressiter for syntax highliting, also its modal style of editing is both unique an impressive 

### Tmux to create an ide like setup
tmux is used to multiplex my terminal so i have multile panes on one terminal,this allows me to have an editor in one pane and also have a terminal in which i can run commands such as launching server, testing etc

### Misc
The bar at the top is basically a bash script i wrote that is piped into a program knowns as dzen
i prefer terminal applications to gui since they have less memory requirement

The tuis and lightweight apps that i use are:
- mpd & ncmpcpp to play music
- zathura for viewing pdf
- pcmanfm for viewing files 
- imv/feh for viewng images
- mpv for playing videos


link to my dotfiles: [dots](https://github.com/modisek/dotfiles)
