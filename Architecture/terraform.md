# **What is Terraform?**
- a tool that allow us to automate and manage our infra, platform and services that run on the platform (For infra provisioning)
- Open-source
- Declarative (we just have to define what we want for the end-result, Terraform will figure how to execute it and settle for us)

# **Ansible and Terraform**
1. Ansible:
- Mainly a infra configuration tool
- More mature

2. Terraform
- Mainly infra provisioning tool
- relatively new
- more advanced in orchestration

# **Terraform Architecture**
- has mainly 2 parts, **CORE** and **STATE**
- **CORE** Takes the terraform configuration prepared (what to create/configure) by the users, take the Terraform **STATE** (where it keeps the up-to-date state of how the current setup of the infra looks like), compared the current state and the desired state, and figures out what needs to be done (created/updated/destroyed)