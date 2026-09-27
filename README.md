# duckdns


```
https://www.duckdns.org/

```








### install


linux cron

if your linux install is running a crontab, then you can use a cron job to keep updated



we can see this with



```
ps -ef | grep cr[o]n
```


if this returns nothing - then go and read up how to install cron for your distribution of linux.

also confirm that you have <b>curl</b> installed, test this by attempting to run curl


```
curl
```

if this returns a command not found like error - then find out how to install curl for your distribution.

otherwise lets get started and make a directory to put your files in, move into it and make our main script

```
mkdir duckdns
cd duckdns
vi duck.sh
```


now copy this text and put it into the file (in vi you hit the i key to insert, ESC then u to undo)


you must change your token and domain to be the one you want to update
	

you can pass a comma separated (no spaces) list of domains
you can if you need to hard code an IP (best not to - leave it blank and we detect your remote ip)
hit ESC then use use arrow keys to move the cursor x deletes, i puts you back into insert mode



```
echo url="https://www.duckdns.org/update?domains=exampledomain&amp;token=a7c4d0ad-114e-40ef-ba1d-d217904a50f2&amp;ip=" | curl -k -o ~/duckdns/duck.log -K -

```



now save the file (in vi hit ESC then :wq! then ENTER)
this script will make a https request and log the output in the file duck.log
now make the duck.sh file executeable



```
chmod 700 duck.sh
```


next we will be using the cron process to make the script get run every 5 minutes


```
crontab -e

```

copy this text and paste it at the bottom of the crontab



*/5 * * * * ~/duckdns/duck.sh &gt;/dev/null 2&gt;&amp;1


now save the file (CTRL+o then CTRL+x)
lets test the script 



```
./duck.sh
```


this should simply return to a prompt
we can also see if the last attempt was successful (OK or bad KO)



```
cat duck.log

```
if it is KO check your Token and Domain are correct in the duck.sh script





### LOCAL


```
http://192.168.0.1/admin/index.html
http://192.168.0.1/admin/index.html#/functions/advanced/portsSettings

D-LINK
DIR-615 FW:1.0.2 

```


# HELP

```
https://www.duckdns.org/spec.jsp

https://blog.pishop.co.za/how-to-set-up-duck-dns-on-the-raspberry-pi/
https://portforward.com/

https://www.youtube.com/watch?v=fNzngoXfxzw

```