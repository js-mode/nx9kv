# Nexus9000v Automation

The code used in my **[NX-OSv 9000 Automation](https://www.trueneutral.eu/tag/labs.html)** series of blog posts where I explore setting up a development environment for NX-API automation.

- [Part 1 Code](https://github.com/cmsirbu/nx9kv/blob/master/1/) - [Blog Post](https://www.trueneutral.eu/2017/nxosv-1.html) - vagrant setup with some MAC address shenanigans
- [Part 2 Code](https://github.com/cmsirbu/nx9kv/blob/master/2/) - [Blog Post](https://www.trueneutral.eu/2017/nxosv-2.html) - ansible (eventually) gets to configure something
- [Part 3 Code](https://github.com/cmsirbu/nx9kv/blob/master/3/) - [Blog Post](https://www.trueneutral.eu/2018/nxosv-3.html) - in which everything actually works (**USE THIS**)
  - **Backing up configs to git with ansible** - [Code](https://github.com/cmsirbu/nx9kv/tree/master/3/config_backup/) - [Blog Post](https://www.trueneutral.eu/2019/ansible-cfg-git.html)

# Part 3 - in which everything actually works

Write-up can be found on **[my blog here](https://www.trueneutral.eu/2018/nxosv-3.html)**.

**Backing up configs to git with ansible** - [Code](https://github.com/cmsirbu/nx9kv/tree/master/3/config_backup/) - [Blog Post](https://www.trueneutral.eu/2019/ansible-cfg-git.html)

Commands needed after VirtualBox and Vagrant have been successfully installed:

For Nexus Devices -- below are the steps on a Mac to get a local environment set up.  If you are using another OS or need more detailed information please go to **[Cisco 9000v](https://www.cisco.com/c/en/us/td/docs/switches/datacenter/nexus9000/sw/7-x/nx-osv/configuration/guide/b_Cisco_Nexus_9000v/b_Cisco_Nexus_9000v_chapter_011.html#concept_B4B164C6D62E49A6998ED020531B639B)**

1. Download nxosv.9.2.3.box from \${URL}
2. vagrant box add --name n9000v nxosv.9.2.3.box # from within directory
3. vagrant up n9k1
4. brew install socat
5. socat unix-connect:/tmp/n9k1 stdin
6. This should log you into the switch with a serial connection. You now need to shut down the VM and change a few settings manually before continuing (\*\* note there is a lot output on the serial connection and you may need to wait several minutes before it is completely done. You should see a message about "The guestsheel has been enabled". After that, wait until you get the login prompt. )
   6a. Change network settings for Adapter 1 from NAT to Bridged Adapter and set Promiscuous Mode to Allow All (don't need port forwarding because we are going to set up a static IP that allows you to ssh into switch without needing specific port)
   6b. Now go back to the serial "socat" connection to the n9k1 switch and log in with "admin"/"admin".
   6c. enter following commands to set up static IP and mgmt access:


9) Make sure that you run "no password strength-check"
10) snmp-server host 10.10.0.144 version 3 priv wavefront udp-port 162
10) snmp-server host 10.10.0.144 use-vrf management udp-port 162
11) Force a trap i.e. interface Ethernet 1/3 & then "shutdown"