# hadoop

Pre Requisite:


1) Enable ssh for Root user.
2) ##adduser hduser

"adduser hduser; passwd hduser"
groupadd hadoop; useradd hduser -g hadoop; usermod -aG wheel hduser


3) Add following Paramiter in "/etc/sysctl.conf" file

"#disable ipv6"
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1
vm.swappiness=10

4)  Run following command befor run the setup.

    "echo never > /sys/kernel/mm/transparent_hugepage/defrag" 
    "echo never > /sys/kernel/mm/transparent_hugepage/enabled"

add them in /etc/rc.local file.

5) Download the latest CDH intallation .bin file in "manager-server" from below location and execute the commands.
    
    wget http://archive.cloudera.com/cm5/installer/latest/cloudera-manager-installer.bin
    
    $ chmod u+x cloudera-manager-installer.bin
    $ sudo ./cloudera-manager-installer.bin
7) And follow the step by step instraction to install. 
    

