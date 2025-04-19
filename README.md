🚀 Ansible AWS Mini Project
This mini-project shows how to automate AWS cloud infrastructure using Ansible – a powerful DevOps tool – along with AWS CLI. Using this project, you can launch EC2 instances, set up security groups, and install software automatically with a few commands 💻✨.

📑 Table of Contents

.📘 Introduction

.❓ Why This Project?

.🎯 Objectives

.⚙️ Technologies Used

.🛠️ Setup & Resources

.🚀 Steps to Run

.🌟 Features

.💡 Usage Guide

.📁 Project Structure

.🤝 Contributing

.📄 License


-📘 Introduction
Managing cloud infrastructure manually from the AWS Console is slow, repetitive, and can lead to errors 😓. With this project, you'll learn to:

*Write Ansible playbooks in YAML

*Use AWS CLI to communicate with your cloud account

*Provision AWS EC2 instances

*Install software (e.g., Apache/Nginx)

*Configure security groups for networking

❓ Why This Project?
✅ Great for cloud beginners learning DevOps
✅ Shows real-life infrastructure automation
✅ Learn by doing: clone, modify, and apply
✅ Project ready to add to your resume/portfolio 💼

🎯 Objectives
.🤖 Automate AWS resource creation using Ansible
.🔐 Set security rules (ports, IPs) automatically
.📦 Install and configure software on EC2 instances
.🔄 Re-run anytime to recreate or update your setup

⚙️ Technologies Used

Tool	Description
.🧩      Ansible	Automation tool to configure remote servers
.☁️      AWS CLI	Command-line tool to interact with AWS
.🧾      YAML	Used for writing Ansible playbooks
.🐍      Python	(Optional) For advanced AWS automation


🛠️      Setup & Resources
🔧 Prerequisites (Install These)
.✅ Ansible
.✅ AWS CLI
.✅ AWS Account (Free Tier is enough)

📁 Project Files You Get
.playbook.yml – the automation playbook
.inventory – where you define your EC2 IPs
.Sample README.md – this doc to guide you
.files/ – optional folder for extra scripts/files

🚀 Steps to Run (Easy Guide)
🔁 1. Clone the Project

git clone https://github.com/Manoj-kawasaki/ansible-aws-project.git
cd ansible-aws-project

🔐 2. Configure AWS CLI

aws configure

👉 Enter:
-AWS Access Key ID
-AWS Secret Access Key

🖥️ 3. Launch an EC2 Instance Manually (1st Time Only)
1.Go to AWS Console → Launch an EC2 instance
2.Choose Ubuntu 22 or Amazon Linux 2
3.Save the .pem key (e.g., your ec2insatnces)
4.Get its public IP

📋 4. Update the inventory File

[web]
your.ec2.public.ip ansible_user=ec2-user ansible_ssh_private_key_file=~/path/to/your insatnces key.

▶️ 5. Run the Playbook

 ansible-playbook -i inventory playbook.yml

 🔍 Breakdown:
.ansible-playbook: The command to run a playbook
.-i inventory:  Specifies the inventory file (you can rename it if needed, like -i hosts)
.playbook.yml:  The playbook file containing automation tasks
 It will:
.Connect to your EC2
.Install required software
.Print the status on screen
![Screenshot 2025-04-17 172238](https://github.com/user-attachments/assets/a5edcf6c-1310-4ce0-86d0-2884cd1f97d4)

🌟 Features
.✨ EC2 Provisioning
.🔐 Security Group Configuration
.📦 Web Server Installation (Apache/Nginx)
.💡 Reusable Automation
.📂 Clean Structure for Scaling the Project

💡 Usage Guide
1.✅ First Time? Follow the above guide line-by-line
✅ Use the .pem file to SSH into your EC2 and verify results

ssh -i ~/ansible.pem ec2-user@<your-ec2-public-ip>

2.🔍 Check if the installed services (e.g., Apache) are running:

sudo systemctl status apache2

🌐 If web server is installed, go to your browser:

http://<your-ec2-public-ip>
You’ll see the default Apache/Nginx page!

📁 Project Structure

ansible-aws-mini-project/
│
├── playbook.yml       # Main Ansible script
├── inventory           # Hosts file for Ansible
├── README.md           # Project Guide (You are here!)
└── files/              # Optional scripts/files

🧑‍💻for automating your ec2 insatnces u needed palybook.yml 
---
- name: Launch EC2 Instance on AWS
  hosts: localhost
  connection: local
  gather_facts: false

  vars:
   region: "default region"
    ami_id: "ami- # Replace with your AMI ID
    instance_type: "t2.micro"
    key_name: "your-key-name"         # Replace with your key pair name

  tasks:
    - name: Launch an EC2 instance
      amazon.aws.ec2_instance:
        name: "AnsibleInstance"
        key_name: "{{ key_name }}"
        instance_type: "{{ instance_type }}"
        image_id: "{{ ami_id }}"
        region: "{{ region }}"
        wait: yes
        count: 2
        state: running
      register: ec2

    - name: Add launched instance to dynamic inventory
      add_host:
        name: "{{ item.public_ip }}"
        groups: launched
      loop: "{{ ec2.instances }}"

- name: Configure launched EC2
  hosts: launched
  become: true
  vars:
    ansible_ssh_common_args: '-o StrictHostKeyChecking=no'

  tasks:
    - name: Install Apache web server
      apt:
        name: apache2
        state: present
        update_cache: yes


🤝 Contributing
Feel free to contribute and make it better! PRs are welcome 🤗

# Fork 🍴 → Clone 👇 → Modify ✍️ → PR 🚀
git checkout -b feature-xyz
git add .
git commit -m "Add xyz feature"
git push origin feature-xyz    


📄 License
This project is licensed under the MIT License 🧾
See the LICENSE file for more details.


## 👨‍💻 Author

- GitHub: [@Manoj-kawasaki](https://github.com/Manoj-kawasaki)
- LinkedIn: [Manoj Kumar](https://www.linkedin.com/in/manoj-kumar-49b84b2a0/)

