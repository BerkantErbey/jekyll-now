---
published: true
---


## Setting Alarm at Terminal


In this post, I will explain how to set up an alarm at the terminal.

Sometimes we need to set alarms while working on the computer. In such cases, we can use the terminal instead of phone, website or an gui-app.

Basically, our logic will be to wait for a certain time and play sound. We will use “** sleep **” command to wait for a certain time. To play audio We will use any media player that can work from cli.

	sleep 5s
    
The parameter we write after the sleep command specifies the time we wait.

s->second , m->minute h->hour

We will use “** && **” to run two commands together in the terminal.

command1 && command2
    
I will use “** MPV **” as the media player. First of all, let's run command to add ppa of mpv.
	
    sudo add-apt-repository ppa:mc3man/mpv-tests

Then run the command to install MPV

	sudo apt update && sudo apt install mpv
    
MPV works like that
	
    mpv filename
    
Let's run our two commands together

	sleep 25m && mpv alarm.ogg
    
After 25 minutes, the audio file we want it to play will be played. Setting up an alarm in the terminal is that simple.
