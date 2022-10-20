# Install pre-requisite softwares like apache,php,gcc compiler and gd development  
# libraries on your ec2 machine 

```
sudo yum install httpd php -y
sudo yum install gcc glibc glibc-common -y
sudo yum install gd gd-devel -y
```
- Create user named nagios and set it password
```
sudo adduser -m nagios
sudo passwd nagios
123
123
```
- Now create a group named nagioscmd and add both user nagios and apache to that group
```
sudo groupadd nagcmd
sudo usermod -a -G nagcmd nagios
sudo usermod -a -G nagcmd apache
```

- Now create a seperate for downloaded items
```
mkdir ~/downloads
cd ~/downloads
```
- Following are the links for nagios and nagios plugins 
```
wget http://prdownloads.sourceforge.net/sourceforge/nagios/nagios-4.0.8.tar.gz
wget http://nagios-plugins.org/download/nagios-plugins-2.0.3.tar.gz
```

- Now extracting the tar ball
```
tar zxvf nagios-4.0.8.tar.gz
cd nagios-4.0.8
```
- Now run the configuration script with name of the group created already
```
./configure --with-command-group=nagcmd
```
- Now compile the Nagios source code using make command
```
make all
```
- Here we are compiling the various scripts 
```
sudo make install
sudo make install-init
sudo make install-config
sudo make install-commandmode
```
- Here type in your email address
```
vim /usr/local/nagios/etc/objects/contacts.cfg
  (configure email address)
```
- Compiles the web-interface script
```
sudo make install-webconf
```
- Creating the nagiosadmin account for login 
```
sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin  //for password change
```
- Now restarting the httpd will save the changes
```
sudo service httpd restart  
```
# NAGIOS PLUGIN
- Now as mentioned in the previous nagios-plugins file will be extracted 
- and source code will be compiled 
```
cd ~/downloads
sudo tar zxvf nagios-plugins-2.0.3.tar.gz
cd nagios-plugins-2.0.3
sudo ./configure --with-nagios-user=nagios --with-nagios-group=nagios
sudo make
sudo make install
sudo chkconfig --add nagios
sudo chkconfig nagios on
sudo /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg #verification files	
```
# Now access it here
```
http://<IP>/nagios
```

# Adding Linux clients
```
sudo vi /usr/local/nagios/etc/nagios.cfg ##adding linux clients
```
 - Add line
cfg_file=/usr/local/nagios/etc/objects/client.cfg
```
cd /usr/local/nagios/etc/objects

sudo cp  localhost.cfg   client.cfg

vi client.cfg
#add ip address 
# replace localhost with clientname

sudo service nagios restart 



sudo adduser -m nagios
sudo passwd nagios
123
123
```
