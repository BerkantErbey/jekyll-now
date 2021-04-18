---
published: true
---
In this post, I will explain
* What is Ansible?
  * RedHat defines it as follow "Simple, **agentless** it automation that anyone can use". Agentless means that there is no need for any ansible service to work in the environment to be managed.
* How to install Ansible?

```sudo apt update && sudo apt install software-properties-common
sudo apt-add-repository --yes --update ppa:ansible/ansible && sudo apt install ansible```

Checking whether is working

```
ansible all -m ping --ask-pass
```

* Simple use-case demo (Installing a software)

Sometimes we need to install package/software to many servers. In such cases, we can use the automation tool like Ansible.
Thanks to Ansible, we can perform parallel and multiple tasks



```ansible-playbook myPlayBook.yml -f 10```

```ansible-lint myPlayBook.yml```
