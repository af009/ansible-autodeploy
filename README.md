# ansible-autodeploy
Ansible automatic deploy 

## Terraform part: https://github.com/af009/ansible-project
## Ansible part: Automatic deploy apps with Ansible
#### In this part we use Ansible to deploy our app in the infrastructure created in the first part (Terraform).




## How to use?

## **1- Install ansible**
```
 sudo apt update
 sudo apt install software-properties-common
 sudo add-apt-repository --yes --update ppa:ansible/ansible
 sudo apt install ansible -y
 ```

## **2- Clone the project**
```
git clone https://github.com/af009/ansible-autodeploy
```


## **3- Connect the controller (machine)  to the nodes**
## 1. `cd ~/.ssh`
## 2. `nano id_rsa` (copy the private key here)
## 3. `chmod 400 id_rsa` (read only)
## 4. Create a file called inventory:
```
[hosts]
vm1 ansible_port=221 ansible_host={your-node-vm-ip} ansible_user={your-vm-username}
vm2 ansible_port=222 ansible_host={your-node-vm-ip} ansible_user={your-vm-username}
vm3 ansible_port=223 ansible_host={your-node-vm-ip} ansible_user={your-vm-username}
```
## 5. `ansible all --key-file ~/.ssh/id_rsa -i inventory -m ping` (we pass the key path in the first run) after then we can just run: <br /> 
`ansible all -i inventory -m ping`
## 6. Create a file called vars-prod.yml in the vars folder
```yml
---
vm_username: your vm username
PGPASSWORD: your postgres password
PGUSERNAME: your postgres username
PGHOST: your postgres host
PGPORT: 5432
PGDATABASE: your postgres DB name
PORT: 8080
HOST: 0.0.0.0
NODE_ENV: development
HOST_URL: Your host URL
COOKIE_ENCRYPT_PWD: superAwesomePasswordStringThatIsAtLeast32CharactersLong!
OKTA_ORG_URL: your Okta URL
OKTA_CLIENT_ID: your Okta ID
OKTA_CLIENT_SECRET: your Okta Secret

```
## 7.  Pass the vars-prod.yml path to the playbook file
## 8. `ansible-playbook -i inventory --ask-become-pass playbook.yaml` (Execute the playbook)
## 9. We run again from points 6 to 8 with the "staging" variables
## 10. Done!
