# IaC-network-cfg  

### Ansible instalation - local machine (Ubuntu 26.04)  
1. Create a local virtual environment  
$ python3 -m venv .venv  
2. Activate local environment  
$ source .venv/bin/activate  
3. Install Ansible with prefered SSH library  
$ python3 -m pip install ansible ansible-pylibssh  
4. run the playbook  
$ python3 -m ansible playbook -i inventory/hosts.yaml playbooks/cisco_test.yaml -vvv  

### Cisco device - initial config  
```
!
conf t
hostname R1
ip domain-name lab.local
!
!
crypto key generate rsa modulus 2048
!
username MYUSER privilege 15 secret MYSECRET
!
aaa new-model
aaa authentication login default local
aaa authorization exec default local
!
ip ssh version 2
!
! Might be already set
!line vty 0 4
! transport input ssh
!
! Mgmt interface
interface GigabitEthernet0/0
 description MGMT
 ip address 192.168.1.2 255.255.255.0
 no shutdown
!
```