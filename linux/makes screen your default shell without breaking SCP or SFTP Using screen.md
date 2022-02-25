makes screen your default shell without breaking SCP or SFTP Using screen
========================================



<https://www.commandlinefu.com/commands/view/13589/makes-screen-your-default-shell-without-breaking-scp-or-sftp>

makes screen your default shell without breaking SCP or SFTP
[ "$TERM" != "dumb" ] && [ -z "$STY" ] && screen -dR
I changed my shell to screen by editing .bashrc, this stopped scp from connecting. Adding two tests before screen fixed them problem.
Sample Output
##### SCP before this fix #####
Must be connected to a terminal.