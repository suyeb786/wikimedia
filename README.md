# wikimedia
Install and configure  MediaWiki on CentOS system.



### Dependencies
1. Configuration Management Tool: Ansible
2. Operating System: CentOS-7
3. Containerization Tool: Docker or any(ex. LXC, RCT)

Note: Following steps are documented based on setup I have configured on my local machine due to full fledge environment unavailability and setups are enough for understanding and learning purpose.

### Steps
1. Install VirtualBox and deploy CentOS-7 VM on VirtualBox hypervisor
![image](https://github.com/suyeb786/wikimedia/assets/17975259/21351dfd-2e71-43c8-8636-8cc8ee4e40ea)

2. Install Docker and make sure it's up and running
![image](https://github.com/suyeb786/wikimedia/assets/17975259/039e9c6b-9612-45a2-a659-fb09f0d62479)

3. Deploy container and install Ansible on in it
![image](https://github.com/suyeb786/wikimedia/assets/17975259/049995f2-1a25-4505-9a33-c1b2fcd3165e)

4. Now we have our environment configured and we are ready to run our playbook we have developed in Ansible.

Check node on which we will be running our playbook is reachable and cofigured with passwordless authentication using key-value pair
```
ansible -m ping all
```

In my case I am running playbook on same(localhost) where ansible is installed, so for me server and client both are same
```
ansible-playbook wiki-media.yml
```
![image](https://github.com/suyeb786/wikimedia/assets/17975259/5c17470c-eb47-4a43-aa28-8740eccfb453)


Once playbook will be ran successfully we can check status of the services using following commands 
```
systemctl status httpd
systemctl status mariadb
```

![image](https://github.com/suyeb786/wikimedia/assets/17975259/e22f6667-5245-4b6b-9af0-4646c38993fb)

![image](https://github.com/suyeb786/wikimedia/assets/17975259/dfe020e7-a497-4ab0-ac4f-32cc64ff882f)


### Additional Configuration 
For storing any secret instead of ansible vault using any vault like HashiCorp is more safe and recommended.
```
ansible-vault encrypt secrets.yml

ansible-playbook wiki-media.yml --ask-vault-pass
```

For avoiding anisble vault prompt we can also use environment variable
```
export ANSIBLE_VAULT_PASSWORD_FILE=<vault password>
ansible-playbook wiki-media.yml
```
