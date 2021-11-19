---
title: "My Linux Dev Setup"
date: 2021-11-19T18:57:07+02:00
draft: false
cover : "imgs/preview.png"
---

### why linux
I have been using linux for a few years now and i dont see myself going back to windows machine anytime soon,as a developer linux offers me powerful tools that help me be productive.the commandline is way more efficient and allows me to automate with ease some of my most common tasks

i prefer linux distributions that allow me to build my setup from scratch, they just provide the base system and i can choose what software to install, this reduces bloat, allows me to chose sooftware that is lightweight, this is importatnt because i have luckluster hardware, i use an old lenovo laptop with low ram, and to add salt to injury the ram is soldered into the motherboard meaning that it cant be upgraded.it was unusable with windows so i threw linux ont it and gave it new life, also utilized zram to better use the ram that is available, its barely usable but way better than when it had winows on it.the istro i went with is void linux, an independeent distribution built fro scrath that uses xbps as its package manager and uses runit as the init system,it has been likened to openbsd om many occasions

check it ou at [void linux](https://voidlinux.org/)

### details of my Setup

| item  | details          |
| ----- | --------         |
| os    | void linux(musl) |
| wm    | cwm              |
| term  | uxterm           |
| Ide   | nvim + tmux      |
| font  | terminus         |


### cwm window manager

due to the low memory i choose not to use a desktop environment but rather a window manager, the latter being lightweigt and also has cool features suc as tilling andbetter use of screen real estate in my opinion since there are no window decorations and other useless fluff.The wm i chose is called cwm an Xorg window manager, its floating by default but can also tile at the press of a button, it gets out of my way and provides searching for windows if you opened too many windows and struggling to find your way to the app you need

 I have been thinking of moving away from Xorg to wayland and will try hikari since it is the spiritual successor to cwm

editor of choice is neovim, its doesnt use a lot of ram and starts up quickly, with their 0.5 release neovim became even more powerful with the addition of a native lsp and tressiter for syntax highliting, also its modal style of editing is both unique an impressive 

### tmux to create an ide like Setup
tmux is used to multiplex my terminal so i have multile panes on one terminal,this allows me to have an editor in one pane and also have a terminal in which i can run commands such as launching server, testing etc

link to my dotfiles: [dots](https://github.com/modisek/dotfiles)