# IaC-network-cfg  

### Ansible instalation - official guide  

[Ansible Community Documentation](https://docs.ansible.com/projects/ansible/latest/installation_guide/intro_installation.html)

Use pip in your selected Python environment to install the full Ansible package for the current user:
```
python3 -m pip install --user ansible
```  

### Ansible instalation - local machine venv (Ubuntu 26.04)  
1. Create a local virtual environment  
```
python3 -m venv .venv
```
2. Activate local environment  
```
source .venv/bin/activate
```
3. Install Ansible with prefered SSH library  
```
python3 -m pip install ansible ansible-pylibssh
```
4. If necessary, add Ansible collection  
```
ansible-galaxy collection install cisco.ise
```
5. Verify installed collections  
```
ansible-galaxy collection list | grep cisco
```
6. Run the playbook  
```
python3 -m ansible playbook -i inventory/hosts.yaml playbooks/cisco_test.yaml -vvv
```  
Alternatively:  
```
ansible-playbook -i inventory/hosts.yaml playbooks/cisco_test.yaml
```  

> [!NOTE]
> In our case, **group_vars** folder must be in the same directory as the inventory file or the playbook(s) file.  

> [!NOTE]
> Limit inventory to a single host:  
> ```
> ansible-playbook -i inventory/hosts.yaml playbooks/cisco_test.yaml --limit cisco_router1
> ```  

### Cisco ISE

External RESTful Services (ERS) SDK: https://10.12.0.98:9060/ers/sdk  


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