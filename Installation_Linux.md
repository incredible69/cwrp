# Introduction #

This article describes how to install CityWide gamemode on Linux operating systems (tested on CentOS).

# Details #

First, you need compiled AMX. You can compile it on Linux as well as on Windows. SA:MP included PAWN compiler and IDE in SA:MP Server for Windows: http://www.sa-mp.com/download.php. You can find required .inc files in Downloads section.

MySQL can be easily installed on RedHat/Fedora based operating systems with Yum.

```
yum install mysql mysql-devel
```

Download and extract SA:MP server for Linux:

```
cd /tmp
wget http://files.sa-mp.com/samp03asvr_R4.tar.gz
tar xzf ./samp03asvr_R4.tar.gz
mv samp03 samp
mv samp /home/samp
```

Upload compiled gamemode to /home/samp/gamemodes. Download MySQL plugin for SA:MP (http://forum.sa-mp.com/index.php?topic=23931.0). Instructions below are for CentOS:

```
cd /tmp
wget http://lostgangwarz.free.fr/downloads/samp-mysql-centos.tar.gz
tar xzf ./samp-mysql-centos.tar.gz
mv ./libmysqlclient.so /home/samp
mv ./sampmysql.so /home/samp
```

Add

```
plugins sampmysql.so
```

to /home/samp/server.cfg, and make these changes:

```
rcon_password [your-rcon-password-here]
gamemode0 cwrp 1
```

You can use this script to keep SA:MP server running (upload it to, lets say, /home/samp/checksamp.sh):

```
#!/bin/sh
log=samp.log
dat=`date`
samp="/home/samp/samp03svr"
cd /home/samp

echo "${dat} watchdog script starting." >>${log}
while true; do
        echo "${dat} Server exited, restarting..." >>${log}
        mv /home/samp/server_log.txt /home/samp/server_log.`date '+%m%d%y%H%M%S'`
        ${samp} >> $log
        sleep 2
done
```

Change its permissions to make the script executable:

```
chmod +x /home/samp/checksamp.sh
```

Now lets start the server:

```
nohup /home/samp/checksamp.sh &
```

If the server isnt running properly, check /home/samp/server\_log.txt for errors.