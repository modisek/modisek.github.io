---
title: "Playing With Openbsd"
date: 2021-12-09T00:25:03+02:00
draft: false
cover: "imgs/allen-ng.jpg"
---


Photo by <a href="https://unsplash.com/@nkboon1234?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Allen Ng</a> on <a href="https://unsplash.com/s/photos/thinkpad?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>

#### What is openBSD

Openbsd is a unix like operating system with a strong focus on security and  also emphasizes standardization and corectness, correctness is ensured by extensive auditing of the source,making sure that there are no bugs to exploit.Their website says that openbsd has had "Only two remote holes in the default install, in a heck of a long time! ", this goes to show how secure it is.for this reason it has been used mostly in firewalls and routers from different oems.

openbsd has the easiest installation by far,text based installer that asks you questions, if you are starting out or just looking for a simple setup accepting most defaults will get you a bootable system, the installation doesnt take a long time as well.

I decided to give it a try after hearing so many good things about it, since i dont have extra hardware lying around, i decided to try it in a vm, to give it a try, to learn how to use it, the ephemerality of it running on a vm is that i can take it down easily if i dont like it.


 #### How to get it and what to expect

I downloaded the iso file from their website, used virt manager to  create a vm, made a very simple install accepting most of the defaults, restarted
changed to cwm window manager since am already familiar with it, its the one am currently using on my void linux install.

i have always liked bsd projects and have used ports of them on linux for example i use cwm which is now the default wm on openbsd, i have used doas  to replace sudo, and i used ksh which is the default shell on bsd,so most of those where not new to me, but that is not to say i ddnt enccouter some differences to linux, for example some commands are different like to view storahge devices and so on


used syspatch to keep it upto date

```
syspatch 

```

learnt how to use the package manager, installed essential software like git vim etc

```
doas pkg_add git

```

learn how to manage services using rcctl

```
doas rcctl start sshd

```

I also found out that openbsd ships with a webserver httpd and a loadbalancer relayd and will play with those services to host a website.

#### Summary
I like it a lot so far, it is both lightweight and performant.Its missing some software from linux from the ports, but i can build most of what i need from source if its compatible with openbsd, and will encourage other people to try it. 

To be able to be replace my void install it would have to be able to do hardware accelleration(va-api) so am able to consume video content without the cpu going haywire, wayland support as well woul be appreciated


[openbsd](https://www.openbsd.org/)
