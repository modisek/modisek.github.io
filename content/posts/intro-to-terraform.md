---
title: "terraform and ansible"
date: 2021-11-27T18:23:11+02:00
draft: false
cover: imgs/website.jpg
---

I wanted to use both ansible and terraform in a project for practice purposes and came up with a simple infrastructure to host my website in a ec2 instance using nginx.Terraform is used to provision infrastructure ie create an ec2 instance while ansible is used for configuration management ie installing all the software in the ec2 instance 

### prerequisites
install the following using your distro package manager 
- terraform
- ansible
- set up aws credentials

### main

- use the aws provider

```
provider "aws" {
  region = var.aws_region

}

```

- create ec2 instance
```

resource "aws_instance" "server" {
  ami                         = var.ami
  instance_type               = var.aws_instance_type
  key_name                    = aws_key_pair.admin_key.key_name
  security_groups             = ["${aws_security_group.base_security_group.name}"]
  associate_public_ip_address = true

  tags = { Name = "nginx instance" }



  provisioner "local-exec" {
    command = "ansible-playbook -u root -i '${aws_instance.server.public_dns},' ansible/provision_nginx.yaml"
  }
}
```

- create a security group to allow traffic through ssh
this is how you get access to the ec2 instance
```
resource "aws_security_group" "base_security_group" {
  name        = "base_security_group"
  description = "Base security group"

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name = "base_security_group"
  }

}
```

- create ssh keys and send them to the ec2 instance

- use local-exec provisioner to execute ansible playbooks
```
 provisioner "local-exec" {
    command = "ansible-playbook -u root -i '${aws_instance.server.public_dns},' ansible/provision_nginx.yaml"
  }
}
```

 - nginx config 

```

server {
    listen 80;

    root {{ document_root }}/{{ app_root }};
    index index.html index.htm;

    server_name {{ server_name }};

    location / {
        default_type "text/html";
        try_files $uri.html $uri $uri/ =404;
    }
}
```
- ansible to install, start and copy website files to the approriate folders

```

---
- name: configure nginx
  hosts: localhost
  become: yes
  vars:
    server_name: "{{ ansible_default_ipv4.address }}"
    document_root: /var/www
    app_root: public
  tasks:
    - name: install nginx
      apt:
        update_cache: yes
        name: nginx 

    - name: start nginx
      shell: sudo systemctl start nginx

    - name: copy files to the server
      synchronize:
        src: "{{ app_root }}"
        dest: "{{ document_root }}"

    - name: apply nginx template
      template:
        src: ../nginx.conf.j2
        dest: /etc/nginx/sites-available/default
      notify: Restart nginx

    - name: Enable new site
      file:
        src: /etc/nginx/sites-available/default
        dest: /etc/nginx/sites-enabled/default
        state: link
      notify: Restart nginx

    - name: allow acces to port 80
      ufw:
        rule: allow
        port: '80'
        proto: tcp

  handlers:
    - name: Restart nginx
      service:
        name: nginx
        state: restarted

```

 - variables 

```
variable "aws_region" {
  default     = "af-south-1"
  description = "AWS region"
}

variable "aws_ssh_admin_key_file" {}

variable "ami" {
  default = "ami-08a4b40f2fe1e4b35"
}

variable "aws_instance_type" {
  default = "t3.micro"
}

```
 - keys.tf 

```
resource "aws_key_pair" "admin_key" {
  key_name   = "admin_key"
  public_key = file("${var.aws_ssh_admin_key_file}.pub")

}

```
### Summary
i used ansible by calling it inside of terraform using local-exec provisioner to configure my ec2 instance

