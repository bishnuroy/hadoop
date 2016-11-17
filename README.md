# hadoop

Pre Requisite:


1) Enable ssh for Root user.
2) ##adduser hduser

"adduser hduser; passwd hduser"
groupadd hadoop; useradd hduser -g hadoop; usermod -aG wheel hduser


3) Add following Paramiter in "/etc/sysctl.conf" file

    #disable ipv6
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
    
8) This bin file will make the setup environment in "manager server"
    once setup is done it will give link with port number eg. "http://hostname:7180"(manager link).
    Open the link in browser and it will ask for user and password "admin"-"admin"

9)

<img width="1361" alt="screen shot 2016-11-17 at 2 13 55 pm" src="https://cloud.githubusercontent.com/assets/17826110/20382430/eff98746-acd1-11e6-96ae-57e99e7d95e8.png">

10)

![hadoop1](https://cloud.githubusercontent.com/assets/17826110/20382161/a19050e0-acd0-11e6-9208-b8e5d4ca1a68.jpg)

11)

![hadoop3](https://cloud.githubusercontent.com/assets/17826110/20382164/a192d68a-acd0-11e6-902a-fff16b2bcc60.jpg)

12)

![hadoop6](https://cloud.githubusercontent.com/assets/17826110/20382162/a19113d6-acd0-11e6-94b9-e31e2e29028a.jpg)

13)

![hadoop7](https://cloud.githubusercontent.com/assets/17826110/20382165/a1960058-acd0-11e6-895b-c5dd31dcff80.jpg)

14)
![hadoop8](https://cloud.githubusercontent.com/assets/17826110/20382166/a1bb3986-acd0-11e6-8c7c-de549b1a4db8.jpg)

15)
<img width="1397" alt="screen shot 2016-11-17 at 10 38 20 am" src="https://cloud.githubusercontent.com/assets/17826110/20382662/cc5a963a-acd2-11e6-8076-1bf9ff4609de.png">
