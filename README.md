# aws-ssm-ansible-playbook

## To create an IAM Role

IAM -> EC2 -> AWS System Manager -> create an IAM role

![image](https://github.com/kohlidevops/aws-ssm-ansible-playbook/assets/100069489/b2002770-8488-480c-a084-39b6eee5736e)

## To launch instances with IAM Role

EC2 -> Launch Instances -> ubuntu22 -> associate IAM role which is created in last step -> then launch instances

![image](https://github.com/kohlidevops/aws-ssm-ansible-playbook/assets/100069489/b663b1da-e529-4837-b10e-546ced55ea5a)

## System Manager SSM

### To update and install ansible to all nodes

AWS -> SSM -> Run Command -> Shellscript

![image](https://github.com/kohlidevops/aws-ssm-ansible-playbook/assets/100069489/d3956422-e2c8-4613-bbff-f0b2c5d10ad6)

```
#!/bin/bash
sudo apt-get update -y
sudo apt-get install ansible -y
```

![image](https://github.com/kohlidevops/aws-ssm-ansible-playbook/assets/100069489/8b591619-4d9a-4ff6-b309-295ebb7ccdc7)

![image](https://github.com/kohlidevops/aws-ssm-ansible-playbook/assets/100069489/201f12d0-e25e-49ef-a5aa-32a45b2f21a6)

Then run 

![image](https://github.com/kohlidevops/aws-ssm-ansible-playbook/assets/100069489/45631c84-1672-4dd6-b06a-d11c96ff4e7c)

### To run Ansible playbook

AWS -> SSM -> Run Command -> Ansible Playbook

![image](https://github.com/kohlidevops/aws-ssm-ansible-playbook/assets/100069489/fc09b333-6ac9-43df-aef5-c6ffac186421)

Select -> Ansible playbook

![image](https://github.com/kohlidevops/aws-ssm-ansible-playbook/assets/100069489/f312ec6a-5627-41b5-bfcc-ba271cbae50b)

Your playbook here

![image](https://github.com/kohlidevops/aws-ssm-ansible-playbook/assets/100069489/efab0cee-a134-449e-85c2-0edeaff97c5c)

```
---
- name: Install Apache on Ubuntu
  hosts: all
  become: yes  # Run tasks with sudo

  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes

    - name: Install Apache2
      apt:
        name: apache2
        state: present

    - name: Start Apache2 service
      service:
        name: apache2
        state: started
        enabled: yes
```

Select your target instances

![image](https://github.com/kohlidevops/aws-ssm-ansible-playbook/assets/100069489/6addeccd-c24b-4fef-8696-50cc5fa70e80)

You can give timeout here

![image](https://github.com/kohlidevops/aws-ssm-ansible-playbook/assets/100069489/76af3325-fcb0-4ecd-a502-a73822ab05fc)

You can configure the logs location which is used to store a output

![image](https://github.com/kohlidevops/aws-ssm-ansible-playbook/assets/100069489/bf546f15-8a3e-4b41-9e0b-6da6a8594e3c)

You can configure the SNS to notify the command status

![image](https://github.com/kohlidevops/aws-ssm-ansible-playbook/assets/100069489/f7171471-4b81-401f-ba73-0e20b8eb81eb)

Then Run the playbook

![image](https://github.com/kohlidevops/aws-ssm-ansible-playbook/assets/100069489/bd0e483f-3dfe-44b7-aff6-a3218a71c101)

Now I can able to access the Apache default page 

![image](https://github.com/kohlidevops/aws-ssm-ansible-playbook/assets/100069489/c2972cde-7dac-48ea-a209-195d8197e6d2)
