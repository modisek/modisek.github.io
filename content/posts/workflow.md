---
title: "My workflow"
date: 2022-01-02T11:25:52+02:00
draft: false
---

### How to move fast in bash

##### 1. Use an autojumper to move between directories

An autojumper caches visited directories in its database and allows for direct jumping to known directories eliminating the need to type out the full path.I useone called zoxide, but they are may others worth trying out.
* it has some sort of  fuzzy pattern matching and allows me to type only part of the name of the directory 

[zoxide demo](https://github.com/ajeetdsouza/zoxide/blob/main/contrib/tutorial.webp)
  
##### 2. Intelligent history search 

Search in history only for commands that start with what you have typed, eg. if i type cd and use the up arrow i get commands i typed before that start with cd and can cycle betwwen them.

(this snippet should be inserted into the ~/.bashrc file)
```
# Up Arrow
bind '"\e[A": history-search-backward'

# Down Arrow
bind '"\e[B": history-search-forward'

```

##### 3. shortcuts

Use shortcuts to move faster in bash, most common shortcuts i use: 

* CRTL-a :start of the line 
* CTRL-E :end of line 
* CTRL-K :delete everything from the cursor to the end
* !! access the last commands
* can also do !!:0 to get the first word in the last command
* CRTL-R for a serachable history( replace the default with fzf to have a nicer experience)

##### 4. other options that can be added to bash

(this snippet should be inserted into the ~/.bashrc file)
```
#automatically correct spelling mistakes 
shopt -s cdspell
shopt -s dirspell

# go to a directory without starting the command with cd
shopt -s autocd

```

##### 4. get a fuzzy finder( fzf)

Fzf is described as a general purpose command-line fuzzy finder and it just takes lines from stdin,presents an interactive menu that can be used to select an item and that item is printed to stdout.

It is fast and can be used in scripts.It presents a list menu that can be operated using up and down arrows on the keyboard and enter to make a selection, and typing is allowed to filter through the list.

An example of a script utilizing fzf.this script used find command to return a list of directories( -type d) and their subdirectories to a depth of 2( to reduce the number of items that will be returned), then rm -rf command is run with the path of whatever directory is selected.

```

selected=$(find ~/ -maxdepth 2 -type d | fzf)
rm -rf $selected

```
#### My Tmux workflow

##### What is tmux?

Tmux is a terminal multiplexer, this means that it can be used to divide a terminal window into many terminal windows and panes,and each will run a independent bash instance, so you could run vim on one pane and have another bash pane where you can run commands like starting up servers etc.

Tmux keeps all that is open in a session allowing the terminal emulator to be closed but the session remain in the background  and can attached to later, this is also useful in case where you are connected throught to another host via ssh, if tmux is running on the host when you lose your ssh connection the session will keep on running on the background in the server and you can attach to it an continue where you left off.

Tmux can be scripted to open predetermined panes an windows, automating the process

tmux provides commands such as:
* **new** to create session
* **send-keys** to execute commands and send key strokes

this can be used to automate Tmux

##### Example:

 * uses fzf to return list of directories containing projects
``` 
    selected=$(find ~/projects ~/ ~/terraform -mindepth 1 -maxdepth 1 -type d |fzf)
    ```
 * create session and use the name of selected directory as the session name 
     
   ```
   SESSION=$(basename "$selected" )
    tmux new -s $SESSION -d
    ```
  
 * open the project in vim in one pane
 ```
 
    tmux send-keys -t $SESSION 'vim .' C-m
 
 ```
 * create another pane
 
 ```
 
    tmux split-window -h -t $SESSION
 
 ```
 
 * if the session with that name already exist attach to it

```

#!/usr/bin/env bash


if [[ $# -eq 1 ]]; then
    selected=$1
else

    selected=$(find ~/projects ~/ ~/terraform -mindepth 1 -maxdepth 1 -type d |fzf)
    echo selected
fi

if [[ -z $selected ]]; then 
    exit 0
fi

SESSION=$(basename "$selected" )

# SESSION=${PWD##*/}

SESSIONEXISTS=$(tmux list-sessions | grep $SESSION)

if ["$SESSIONEXISTS" = ""]
then
    cd $selected
    tmux new -s $SESSION -d
    tmux send-keys -t $SESSION 'vim .' C-m
    tmux split-window -h -t $SESSION
    tmux attach -t $SESSION
else
    tmux attach -t $SESSION

fi

```
Tmux running with vim on one pane and running hugo local server on the other pane

![vim and tmux](/imgs/vim-and-tmux.png)


