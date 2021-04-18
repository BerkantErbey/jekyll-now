---
published: true
---
In this post, I will explain
* What is Ansible?
  * RedHat defines it as follow "Simple, **agentless** it automation that anyone can use". Agentless means that there is no need for any ansible service to work in the environment to be managed.
* How to install Ansible?

  sudo apt update && sudo apt install software-properties-common -y

  sudo apt-add-repository --yes --update ppa:ansible/ansible

  sudo apt install ansible -y

Checking whether is working

```ansible all -m ping --ask-pass```
   

* Simple use-case demo (Installing a software)

Sometimes we need to install package/software to many servers. In such cases, we can use the automation tool like Ansible.
Thanks to Ansible, we can perform parallel and multiple tasks

At first , we create project folder

  mkdir -pv testLab
  cd testLab

We write the machines in the inventory file to determine which machines the commands will run on.
  ```
  # hosts.txt (Inventory file)
  [test]
  192.168.1.143
  ```

I solved the authentication problem on the host machine by adding the main machine's public key under the authorized_keys file (/root/.ssh/authorized_keys)

We can list tasks in myPlaybook.yml with this command  

	ansible-playbook --list-tasks myPlayBook.yml
    
This playbook contains 3 tasks.

1.Remove tixati program on host

2.Add qbittorrent's repo to host

3.Install qbittorrent to host




  {% gist 87c1ab6de1f3fd40728db58e2d7e4097 %}


We run our commands on desired machines with the following command

  	ansible-playbook -i hosts.txt myPlayBook.yml

  
