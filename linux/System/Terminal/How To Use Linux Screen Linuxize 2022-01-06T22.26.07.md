How To Use Linux Screen Linuxize 2022-01-06T22.26.07
========================================



<https://linuxize.com/post/how-to-use-linux-screen/>

To find the session ID list the current running screen sessions with:

screen -ls
Copy
There are screens on:
    10835.pts-0.linuxize-desktop   (Detached)
    10366.pts-0.linuxize-desktop   (Detached)
2 Sockets in /run/screens/S-linuxize.
Copy
If you want to restore screen 10835.pts-0, then type the following command:

screen -r 10835
Copy
Customize Linux Screen
When screen is started, it reads its configuration parameters from /etc/screenrc and ~/.screenrc if the file is present. We can modify the default Screen settings according to our preferences using the .screenrc file.