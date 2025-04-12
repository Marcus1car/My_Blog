+++
date = '2025-04-12T14:45:36+02:00'
title = 'Ansible 101 : What It Is, How It Works, and Why It Matters'
+++

I recently started digging more into Infrastructure as Code  (*IaC*) tools and *Devops* tools in general to gain skills and knowledge for my future internship. In this series of articles, I will go over multiple tools and topics. We will mainly cover the basics, concepts, and provide simple examples. If I end up doing a lab with a specific tool, I will publish an article for it.

Here we will cover one of the most popular IaC tools out there, `Ansible`.We will look at how it works, and where it fits in the world of IT automation.

#### What is Ansible ? 
It's an open-source automation tool used for configuration management, application deployment, and task automation. In short: it helps you manage a bunch of computers or servers from a central place, without needing to log into each one and run commands manually.

Think of it as scripting, but scalable, cleanly organized, and repeatable.
Additionaly Ansible is `agentless`, it connects through `SSH` meaning it can still communicate with the devices without requiring an application or service to be installed on the managed machines.

**The Basics**

* `Playbooks`  : These are the `yml`/`yaml` files that will describe the tasks that Ansible will perform.

* `Hosts` : This is our inventory of machines that we want to manage. You can group them, give them aliases, and define variables per group.

* `Modules` : Built-in tools that do specific tasks, like managing users, installing packages, or handling files.

* Idempotency : Instead from resintalling from scratch every time we update playbooks , Ansible will only check what needs to be changed.

Example snippet of a playbook :
```yml
- name: Install NGINX on Ubuntu
  hosts: webservers
  remote_user: ubuntu   
  become: true

  tasks:
    - name: Ensure NGINX is installed
      apt:
        name: nginx
        state: present

    - name: Ensure nginx is running
      service:
        name: nginx
        state: started
        enabled: true
```
This playbook checks if `NGINX` is installed on the *webservers* group, and if it is not, it will install it using the `apt` module (for Debian/Ubuntu). Then it ensures that NGINX is running by using the `service` module that can start/stop/restart services.

Example of `hosts.yml` :
```yml
webservers:
  hosts:
    first.example.com:
    second.example.com:
dbservers:
  hosts:
    one.example.com:
    two.example.com:
    three.example.com:
```
Here we declare the group *webservers*, which contains the machines `first.example.com` and `second.example.com`. So now everytime we call the *webservers*, it will take acount of both machines.

**What are the use cases ?**
Ansible is used pretty much everywhere in IT operations:

* Server provisioning: Automatically set up new servers with the right software and configurations.

* App deployment: Roll out your application across multiple machines with one single command.

* CI/CD pipelines: Automate deployment as part of your build/release workflow.

* Cybersecurity : Automate patching, enforce security baselines, or deploy honeypots and monitoring tools. It's also Security hardening like enforcing firewall rules, disabling unnecessary services, or maintaining system compliance.


#### Ressources 
Here are some additional resources for people who want to learn more about this tool:

[Ansible community documentation](https://docs.ansible.com/)
[Red Hat Starter Guide](https://www.redhat.com/en/ansible-collaborative/how-ansible-works)
[Installing Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)