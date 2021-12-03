---
title: "Setting up linux using ansible"
date: 2021-11-27T18:13:27+02:00
draft: false
cover : "imgs/code.jpg"
---

> image: https://unsplash.com/@ngeshlew

Automation is all the rage nowadays with concepts like infrastructure as code being very popular in all parts of computing, and since my setup hasnt changed much in years i decided it would benefit me to automate it so that the next time i need to reinstall i would not have to install and set up everything by hand.I had already hosted my dotfiles on git and used those in my previous installs, but this time i wanted to automate the installation of the applications as well not just their settings.

This is part of a series i am doing on my linux setup
1. [my linux setup(overview)](https://modisek.github.io/posts/my-linux-dev-setup/)
2. >[setting up linux using ansible](#)*

#### prerequisites
* You need to have ansible installed
* Some modules are dependent on your distribution eg. for your package manager, am using xbps since i am on void linux, and this is not a tutorial for ansible

#### Ansible
- set up ssh
I used ansible vault to encrypt ssh key and will move it to the new system

- install apps
Install all the application i will need in the new system, since am using void linux am using the xbps module, xbps being the package manager of void linux

```
 - name: install essesntials
  become: true
  xbps: name={{item}}
  with_items:
    - xorg-minimal
    - cwm
    ...
```
- set up git
Set up my git email and username 

```
- name: set up email(git)
  git_config:
    name: user.email
    scope: global
    value: "user@example.com"

- name: set up username(git)
  git_config:
    name: user.name
    scope: global
    value: "John Doe"
```
- apply the dotfiles
use stow to symlink my dotfiles
```

- name: install stow
  xbps: name=stow

- name: clone dotfiles
  ansible.builtin.git:
    repo: 'git@github.com:modisek/dotfiles.git'
    dest: "{{ lookup('env', 'HOME')}}/.dotfiles"
    recursive: yes
    update: yes
    accept_hostkey: yes
    version: master

- name: stow the files
  shell: cd $HOME/dotfiles/setup.sh

```
- start services
Start services, in void linux services are enable by symlinks


```
- name: Starting services
  become: yes
  file:
    src: "/etc/sv/{{item}}"
    dest: "/var/service/{{item}}"
    state: link
  with_items:
    - iwd
    - dbus
    - openntpd
    - sshd
    - tlp
    - ufw
    - zramen
    ...

```

#### summary

With this setup and can be up and running in a short amount of time if i needed to reinstall, this also has the advantage that its self documenting and i know exactly how i have set up my system

Below is the repository for the scripts:
[repository](https://github.com/modisek/ansible)
