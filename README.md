# Nexus9000v Automation

The code used in my **[NX-OSv 9000 Automation](https://www.trueneutral.eu/tag/labs.html)** series of blog posts where I explore setting up a development environment for NX-API automation.

- [Part 1 Code](https://github.com/cmsirbu/nx9kv/blob/master/1/) - [Blog Post](https://www.trueneutral.eu/2017/nxosv-1.html) - vagrant setup with some MAC address shenanigans
- [Part 2 Code](https://github.com/cmsirbu/nx9kv/blob/master/2/) - [Blog Post](https://www.trueneutral.eu/2017/nxosv-2.html) - ansible (eventually) gets to configure something
- [Part 3 Code](https://github.com/cmsirbu/nx9kv/blob/master/3/) - [Blog Post](https://www.trueneutral.eu/2018/nxosv-3.html) - in which everything actually works (**USE THIS**)
    + **Backing up configs to git with ansible** - [Code](https://github.com/cmsirbu/nx9kv/tree/master/3/config_backup/) - [Blog Post](https://www.trueneutral.eu/2019/ansible-cfg-git.html)
 
 
 Example code:
 
 
 - name: run multiple commands on remote nodes and specify output format
  nxos_command:
    commands:
      - command: 
        - configure terminal
        - snmp-server enforceGlobalPriv
        - role name metrics
        - rule 1 permit read
        - end
        - configure terminal
        - snmp-server user wavefront metrics auth md5 cisco123 priv aes-128 cisco123
        - show snmp user

    - name: save config
      nxos_config:
        save_when: always
        timeout: 30
        provider: "{{ ssh }}"


        user: wavefront
        group: network-operator
        authentication: md5
        pwd: cisco123

        authentication: md5
        encrypt: True
        group: "network-operator"
        # version: 3
        state: present
        user: wavefront
        privacy: "{{ ansible_snmp_privacy_auth }}"
        pwd: "{{ ansible_snmp_user_auth }}"