# 🌟 Ansible-Docker-AWS 🚀

## 📝 Project Overview

This project automates the creation of **AWS** infrastructure using **Terraform**, installs **Docker** and **Docker Compose** via **Ansible**, and deploys a **WordPress** and **MySQL** stack using Docker containers. The infrastructure includes a **Virtual Private Cloud (VPC)**, a **public subnet**, and an **EC2 instance** (docker_server) to host the services.

---

## 🗂️ Project Structure

### 🚀 Terraform Infrastructure Setup

1. **VPC Creation**: A dedicated **Virtual Private Cloud (VPC)** to house the infrastructure.
2. **Public Subnet**: A **public subnet** within the VPC to host the EC2 instance.
3. **EC2 Instance**: A **docker_server** (Amazon Linux 2) where Docker will run, ready to deploy WordPress and MySQL via Docker Compose.

### 🤖 Ansible Automation

1. **Docker & Docker Compose Installation**: Ansible installs Docker and Docker Compose on the EC2 instance.
2. **Service Setup**: It ensures the Docker service is running and copies the necessary `docker-compose.yaml` file to the EC2 instance.
3. **Execution**: The playbook runs the services (WordPress and MySQL) using Docker Compose.

### 🐋 Docker-Compose Configuration

- **WordPress**: A robust content management system connected to a MySQL database.
- **MySQL**: A relational database system as the backend for WordPress.
- **Volume Persistence**: Docker volumes to store data and WordPress content, ensuring persistence across container restarts.

---

![AWS](https://github.com/user-attachments/assets/dafa58b6-f412-4e1e-b287-14e2ff3bf4af)

## 📈 Project Workflow

### ☁️ Step 1: Infrastructure Provisioning with Terraform

Using **Terraform**, we provision the required infrastructure:

- **VPC**: A network environment where resources will be isolated.
- **Public Subnet**: A subnet in the VPC that allows communication with the outside world.
- **EC2 Instance**: A virtual machine (Amazon Linux 2) where Docker will be installed.

Steps:

1. Create the **VPC**, **subnet**, and **EC2 instance** in Terraform configuration files.
2. Deploy using the following commands:
    ```bash
    terraform init
    terraform apply
    ```
![800](https://github.com/user-attachments/assets/47aeebe3-bef8-446b-8982-da42aa439ba8)

![900](https://github.com/user-attachments/assets/fecb68dd-11d7-4a06-a34b-7e160d71cdd3)

![1000](https://github.com/user-attachments/assets/03d1174c-9d49-4119-86b1-392a6d8bfdb0)

![500](https://github.com/user-attachments/assets/b6bc75b7-1e01-4050-bb1a-57b4a0a0f4a8)

![600](https://github.com/user-attachments/assets/e05321f3-dd0b-45c1-bad6-995f11b7752b)

![700](https://github.com/user-attachments/assets/12962538-bd5f-4011-9a55-8e9a197638d5)

---

### 🖥️ Step 2: Automate Docker & Docker Compose Installation with Ansible

An **Ansible playbook** is used to automate the setup on the EC2 instance:

1. **Docker Installation**: Install Docker and Docker-Compose on the EC2 instance.
2. **Service Management**: Start and enable Docker service.
3. **Docker Group Setup**: Add `ec2-user` to the Docker group and reset the SSH connection.
4. **Deploy Services**: Copy the `docker-compose.yaml` file to the instance and start the services.

Run the playbook with:
```bash
ansible-playbook -i inventory.ini playbook.yml
```

---

### 🐳 Step 3: Running Docker-Compose Services

The **`docker-compose.yaml`** file defines two services:

#### 1. **MySQL Service**:

- A **MySQL** container that serves as the backend database for WordPress.
- **Docker Volumes**: Ensures data persists using Docker volumes (`db`).
- Configuration:
    ```yaml
    services:
      mysql_database:
        image: mysql
        environment:
          MYSQL_ROOT_PASSWORD: 123
          MYSQL_DATABASE: wp_db
          MYSQL_USER: wael
          MYSQL_PASSWORD: 12345
        volumes:
          - db:/var/lib/mysql
    ```


#### 2. **WordPress Service**:

- The **WordPress** container, serving the website and interacting with the MySQL database.
- Exposes port `8080` for access to the site.
- Configuration:
    ```yaml
    services:
      wordpress:
        image: wordpress
        ports:
          - 8080:80
        environment:
          WORDPRESS_DB_HOST: mysql_database
          WORDPRESS_DB_USER: wael
          WORDPRESS_DB_PASSWORD: 12345
          WORDPRESS_DB_NAME: wp_db
        volumes:
          - wordpress:/var/www/html
    ```

Once Docker and Docker Compose are installed, the **Ansible playbook** copies the `docker-compose.yaml` file and starts the services:
```bash
docker-compose -f docker-compose.yaml up -d
```

Access the WordPress site at:
```
http://<EC2-instance-public-ip>:8080
```

---

## 🔎 Detailed Step-by-Step Guide

### Step 1: Terraform Infrastructure Provisioning

1. Define the infrastructure in Terraform.
2. Run the following Terraform commands to deploy:
    ```bash
    terraform init
    terraform apply
    ```
    
### Step 2: Deploy Docker and Docker Compose with Ansible

1. Add your EC2 instance's public IP to the Ansible inventory (`inventory.ini`).
2. Run the Ansible playbook to deploy Docker and Docker Compose:
    ```bash
    ansible-playbook deploy-docker.yaml
    ```
![100](https://github.com/user-attachments/assets/7c2dfe4b-ed52-4a0a-9590-67a1c0de6d40)

![200](https://github.com/user-attachments/assets/22f7d759-2aee-4456-a197-ad7333d6032e)

### Step 3: Run the WordPress and MySQL Services

1. **Docker Compose File**: The `docker-compose.yaml` file is copied to the EC2 instance.
2. **Start the Services**: Run the services in the background using Docker Compose:
    ```bash
    docker-compose up -d
    ```
3. **Access WordPress**: Go to `http://<EC2-public-ip>:8080` to access the WordPress site.

![300](https://github.com/user-attachments/assets/1474cd56-6cdb-45ad-99b4-16448c506383)

![400](https://github.com/user-attachments/assets/b5cd1fc1-48bc-4171-b088-7432a2cff4c5)

---

## 🎉 Conclusion

This project efficiently automates the setup of a scalable **WordPress** and **MySQL** stack on AWS using **Terraform**, **Ansible**, and **Docker-Compose**. By leveraging **Infrastructure as Code (IaC)** and **configuration management** tools, the process of deploying cloud infrastructure and applications becomes seamless, reproducible, and scalable. 

💡 **Key Learnings**:
- Automating infrastructure deployment with Terraform.
- Using Ansible for remote configuration management.
- Deploying multi-container applications with Docker Compose on AWS.

---
