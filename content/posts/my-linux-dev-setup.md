---
title: "My Linux Dev Setup"
date: 2021-11-19T18:57:07+02:00
draft: false
cover : "imgs/preview.png"
---

### Why linux
I have been using linux for a few years now and honestly i dont see myself going back to a non unix like operating system anytime soon,as a developer linux offers me powerful tools that help me be productive.The commandline is way more efficient and allows me to automate with ease some of my most common tasks.I have written a few bash scripts that help me with a few common daily things i do like watching youtube videos through mpv media player, a script to automate tmux so i can start working on a project faster.

 I prefer linux distributions that allow me to build my setup from scratch, they just provide the base system and i can choose what software to install.This reduces bloat, allows me to choose software that is lightweight, this is important because i have lackluster hardware.I use an old lenovo laptop with low  amount of Ram, and to add salt to injury the Ram is soldered into the motherboard meaning that it cant be upgraded,it was unusable with windows so i threw linux ont it and gave it a new life, also utilized **zram** to better use the ram that is available, its barely usable but way better than when it had windows on it.The distro i went with is void linux, an independent distribution built from scrath that uses xbps as its package manager and uses runit as the init system,it has been likened to openbsd om many occasions.Its lightweight and its init system is easier to understand than systemd.

check it out at [void linux](https://voidlinux.org/)
This is part of a series i am doing on my linux setup
1.  > [my linux setup(overview)](#)
2. [setting up linux using ansible]({{< ref "/posts/ansible-dev-laptop.md" >}})
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

Due to the low memory i chose not to use a desktop environment but rather a **window manager**, the latter being lightweigt and also has cool features such as tilling and better use of screen real estate in my opinion since there are no window decorations and other useless fluff.The wm i chose is called cwm an Xorg window manager, its floating by default but can also tile at the press of a button, it gets out of my way and provides searching for windows if you opened too many windows and struggling to find your way to the app you need.

 I have been thinking of moving away from Xorg to wayland, but i have struggled to get the same experience in wayland as i do in x11, wayland and wayland compositors are still a work in progress and i havent had time to look at how to configure a wayland compositor to get the same setup am used to, but if i do move away from x11 i will try hikari since it is the spiritual successor to cwm, i have taken a look at it, the documentation on it is rather lacking.

My editor of choice is neovim since it doesnt use a lot of ram and starts up quickly, with their 0.5 release neovim became even more powerful with the addition of a native lsp and tressiter for syntax highliting, also its modal style of editing is both unique an impressive , i use a colourscheme i created myself, wanted calming colours that are easy to look at for extended periods of time,the plugins that i use most is telescope, a fuzzy finder that allows me to open files very quickly

### Tmux to create an ide like setup
Tmux is used to multiplex my terminal so i have multiple panes on one terminal,this allows me to have an editor in one pane and also have a terminal in which i can run commands such as launching a server, testing etc

### Misc
The bar at the top is basically a bash script i wrote that is piped into a program knowns as dzen
i prefer terminal applications to gui since they have less memory requirement

The tuis and lightweight apps that i use are:
- mpd & ncmpcpp to play music
- zathura for viewing pdf
- pcmanfm for viewing files 
- imv/feh for viewng images
- mpv for playing videos
- autojump to quickly go to directories
- fzf to find files

> definition of some terms
  **zram** compresses stuff before its put on ram so you can fit more things in ram,makes it seem like the computer has more ram, this comes at the expense of some performance hit due to compression and decompression
  **window manager** is a lightweigt alternative to heavy desktop enviroments like gnome for example




link to my dotfiles: [dots](https://github.com/modisek/dotfiles)
