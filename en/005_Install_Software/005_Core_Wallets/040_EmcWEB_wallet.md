## EmcWEB wallet

<div style="style=”width:50%”"><img style="float:left;" src="EmcWEB.png" alt="EmcWEB is a web-based wallet running on your own server." width="384"></div><div style="style=”width:50%”"><img src="EmcWEB_UI.png" alt="EmcWEB has a full user interface." width="384"></div>

<br>

EmcWEB is an emercoin daemon, EmcSSH installation, and web wallet configured for fast deployment on the Microsoft Azure platform, or hosted on your own server.

### Fast Deploy EmcWEB on Microsoft Azure Marketplace

For fast deployment on Azure, click the following button.
<div style="overflow:hidden;"><a href="https://azure.microsoft.com/marketplace/partners/emercoin/emercoin/"><img style="float:left;" src="Deployaz.png" alt="Deploy on Microsoft Azure."></a></div>

<br>

### Deploy EmcWEB on your own server

Minimum system requirements are: 1 GB RAM or 512 MB RAM + SWAP 1 GB 

#### For Ubuntu 16.04 LTS (x64)
```bash
$ apt-key adv --keyserver keyserver.ubuntu.com --recv B58C58F4
$ add-apt-repository 'deb http://download.emercoin.com/ubuntu xenial emercoin'
$ apt update && DEBIAN_FRONTEND=noninteractive apt -y install mysql-server redis-server && apt -y install emcweb
$ emcweb-setup -C
```
Optionally, to quickly create a login and password to enter the web-wallet, use the command <code>emcweb-setup -G -C -R = ‘YOUR_MYSQL_ROOT_PASSWORD’</code> (Where ‘YOUR_MYSQL_ROOT_PASSWORD’ is the password of the user ‘root’ in MySQL that you specified during the installation process).

After executing these commands, you need to go to the IP address of the web server and continue to configure emcweb already through the web interface.
Parameters for connecting to Emercoin RPC can be taken from the file <code>/etc/emercoin/emercoin.conf</code>
 
#### For RedHat/CentOS 7:
```bash
$ rpm -ivh http://download.emercoin.com/rhel/el7/RPMS/emercoin-release-1.0-1.el7.centos.noarch.rpm
$ yum -y install mariadb-server redis emcweb
$ systemctl restart emercoind httpd supervisord redis mariadb
$ systemctl enable  emercoind httpd supervisord redis mariadb
$ emcweb-setup -C
```
* Optionally, to quickly create a login and password to enter the web-wallet, use the command <code>emcweb-setup -G -C</code>
After executing these commands, you need to go to the IP address of the web server and continue to configure emcweb already through the web interface.
Parameters for connecting to Emercoin RPC can be taken from the file <code>/etc/emercoin/emercoin.conf</code>

After that, you can point your browser to the server’s IP and follow instructions to continue setup.
Please note: SElinux is not supported!

#### For Debian 8 (x64, ARM)
```bash
$ apt-key adv --keyserver keyserver.ubuntu.com --recv B58C58F4
$ echo "deb http://download.emercoin.com/debian jessie emercoin" > /etc/apt/sources.list.d/emercoin.list
$ apt update && DEBIAN_FRONTEND=noninteractive apt -y install mysql-server redis-server && apt -y install emcweb
$ emcweb-setup -C
```
* Optionally, to quickly create a login and password to enter the web-wallet, use the command <code>emcweb-setup -G -C -R = ‘YOUR_MYSQL_ROOT_PASSWORD’</code> (Where ‘YOUR_MYSQL_ROOT_PASSWORD’</code> is the password of the user ‘root’ in MySQL that you specified during the installation process).

After executing these commands, you need to go to the IP address of the web server and continue to configure emcweb already through the web interface.
Parameters for connecting to Emercoin RPC can be taken from the file <code>/etc/emercoin/emercoin.conf</code>

