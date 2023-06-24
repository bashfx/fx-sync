# Xsync

## Bash
 XSYNC(3) bash utility for spawning rsync with an fswatch listener. Pretty janky but works. Temporary home untiL I move into 
its final @basfx/fx-xsync home.

## Note
 Please note that this is only been tested on latest mac os and may not work on other linux systems (atm) for things like sed that 
may have a different implementation. Note that this also requires fswatch (brew install fswatch).

 Please also note that the script will need some major cleanup so consider this a beta if you decide to use it.

## Install

First specify your $XSYNC_HOME prefix which will be the home directory for all files used by XSYNC in your .profile. XSYNC will look 
for your default config file in $XSYNC_HOME. 

Config file format is SSH_HOST LOCAL_DIR HOSTD_DIR one per each line. You can have multiples of the same host in case your syncing 
multiple directories. SSH_HOST is the host entry in your .ssh/config where you have already setup SSH keys on your local and remote 
server. XSYNC has not been tested to handle RSYNC ssh connections without a pre-made key.

Warning -- first make sure you have essential files backed before attempting sync, and its best to test with a set of dummy 
directories to make sure everything is working ok before running live files. "Works on my machine"

## Usage

xsync help *prints commands and options*

xsync <cmd> --trace *trace flag shows additional debug msgs level 2*
xsync <cmd> --debug *debug flag prints non essential info level 1*
xsync <cmd> --quiet *shuts off all non-essential outputs and only prints essentials*
xsync <cmd> --delete *enables deleted file sync on rsync, by default it only syncs writes*
xsync <cmd> --config *set a custom path for the config file that should be used*

xsync run  *iterates through the config file to start an fswatch and rsync handler for each entry*
xsync stop *kills all fswatch and child rsync processes, which just uses PID-1 to find the child*
xsync pause <N> *pause the FSWATCH JOB with index N*
xsync restart <N> *restart the FSWATCH JOB with index N*
xsync now  *list all watchers and their status*

*there are additional utility commands mostly for debugging*

## Final Note

Now that I have the basics working it may be a minute before I get around to fully debugging/cleaning up but feel free to toy around 
and if you have any recommendations please let me know. 
