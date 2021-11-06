# ansible-autodeploy
Ansible automatic deploy 

## Terraform part: https://github.com/af009/ansible-project
## Ansible part: Automatic deploy with Ansible
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
### a. `cd ~/.ssh`
### b. `nano id_rsa` (copy the private key here)
### c. `chmod 400 id_rsa` (read only)
### d. Create a file called inventory:
```
[staging]
vm1-stage ansible_port=221 ansible_host={your-node-vm-ip} ansible_user={your-vm--username}
vm2-stage ansible_port=222 ansible_host={your-node-vm-ip} ansible_user={your-vm-username}
vm3-stage ansible_port=223 ansible_host={your-node-vm-ip} ansible_user={your-vm-username}

[production]
vm1-pro ansible_port=221 ansible_host={your-node-vm-ip} ansible_user={your-vm-username}
vm2-pro ansible_port=222 ansible_host={your-node-vm-ip} ansible_user={your-vm-username}
vm3-pro ansible_port=223 ansible_host={your-node-vm-ip} ansible_user={your-vm-username}

```
### e. Create a file called ansible.cfg:
```
[defaults]
inventory = inventory
private_key_file = ~/.ssh/id_rsa
```

### f. Check the connection: `ansible all -i inventory -m ping`

## 4. Create a file called vars-stage.yml in the vars folder
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

## 5. Create a file called vars-prod.yml in the vars folder
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

## 6. `ansible-playbook -i inventory playbook.yaml` (Execute the playbook)
## 7. Done!
