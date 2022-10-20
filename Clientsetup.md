# Nagios-Monitoring-Tool

# Installing prerequisite packages
```
 sudo yum install -y gcc glibc glibc-common openssl openssl-devel perl wget -y
cd /tmp
```

# Installing nrpe plugin
```
wget --no-check-certificate -O nrpe.tar.gz https://github.com/NagiosEnterprises/nrpe/archive/nrpe-3.2.1.tar.gz

sudo tar xzf nrpe.tar.gz
```
- Now Compile downloaded files
```

cd /tmp/nrpe-nrpe-3.2.1/
sudo ./configure --enable-command-args
sudo make all
sudo make install-groups-users
sudo make install
sudo make install-config

sudo echo >> /etc/services
sudo echo '# Nagios services' >> /etc/services
sudo echo 'nrpe    5666/tcp' >> /etc/services

sudo make install-init
```

- Now starting the service
```
sudo systemctl enable nrpe.service
```
- Now add the servers ip so that both client and server can communicate
```
sudo vi /usr/local/nagios/etc/nrpe.cfg 
```
- Edit the following line and add the servers ip after the comma
allowed_hosts=127.0.0.1,

- Now starting the service

```
systemctl start nrpe.service


service nagios-nrpe-server restart
```
