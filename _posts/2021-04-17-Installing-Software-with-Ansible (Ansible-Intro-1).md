---
published: true
---
In this post, I will explain
* What is Ansible?
  * RedHat defines it as follow "Simple, **agentless** it automation that anyone can use". Agentless means that there is no need for any ansible service to work in the environment to be managed.
* How to install Ansible?
```sudo apt update && sudo apt install software-properties-common
   sudo apt-add-repository --yes --update ppa:ansible/ansible && sudo apt install ansible```

* Simple use-case demo (Installing a software)

Sometimes we need to set alarms while working on computer. In such cases, we can use the terminal instedad of phone, website or gui-app.

Basically, we are waiting for a certain time and play sound for alarm. We will use **sleep** command to wait for a certain time.
To play audio we will use any media player that can work from terminal.

The parameter we write after the **sleep** command specifies the time we wait.

```sleep 5s```

(s->second, m->minute, h->hour)

We will use **&&** to run two commands together in terminal.

```command1 && command2```

I will use **MPV** as the media player. First of all, let's run command to add ppa of MPV.
```sudo add-apt-repository ppa:mc3man/mpv-tests```

MPV works like that

```mpv filename```

Let's run our two commands together:

```sleep 25m && mpv Music/alarm.ogg```

After 25 minutes, the audio file we want it to play will be played. Setting up an alarm in the terminal is that simple.
