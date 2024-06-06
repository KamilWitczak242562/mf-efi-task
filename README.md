# Weatherapp

## Docker

This step consists of a backend and frontend application containerized using Docker and orchestrated using Docker Compose.

## Prerequisites

- Docker

## Setup Instructions

### Step 1: Clone the repository

```sh
git clone https://github.com/KamilWitczak242562/mf-efi-task.git
cd mf-efi-task
```

---

### Step 2: Create a Configuration File

In the root directory of the project, create a file named `config.env` with the following content:

```plaintext
APPID=YOUR_API_KEY
```

This file is essential for configuring the backend service to fetch weather data correctly.
You can get yourself an API key in the [openweathermap](https://openweathermap.org/).

### Step 3: Build and run the application using Docker Compose

Run the following command to build and start the application:

```sh
docker compose -f docker-compose.yaml up
```

### Step 4: Access the application

- Backend service will be available at `http://localhost:9000/api/weather`.
- Frontend service will be available at `http://localhost:8000`.

## Alternative: Running Backend and Frontend Separately

### Running Backend

1. Navigate to the `backend` directory:

    ```sh
    cd backend
    ```

2. Build and run the backend container:

    ```sh
    docker build --build-arg APPID=$(grep APPID ../config.env | cut -d '=' -f2) -t weatherapp_backend .
    docker run --rm -i -p 9000:9000 --name weatherapp_backend -t weatherapp_backend
    ```

### Running Frontend

1. Navigate to the `frontend` directory:

    ```sh
    cd frontend
    ```

2. Build and run the frontend container:

    ```sh
    docker build -t weatherapp_frontend .
    docker run --rm -i -p 8000:8000 --name weatherapp_frontend -t weatherapp_frontend
    ```

### Access the application

- Backend service will be available at `http://localhost:9000/api/weather`.
- Frontend service will be available at `http://localhost:8000`.

## Cloud Hosting on Azure

### Step 1: Set Up an Azure Virtual Machine

1. **Create a Virtual Machine**:
   - Go to the [Azure Portal](https://portal.azure.com/).
   - Navigate to "Create a resource" > "Compute" > "Virtual Machine".
   - Configure the VM (e.g., Ubuntu Server) and ensure it has a public IP.

2. **Open Ports**:
   - Go to "Networking" and add inbound port rules for ports 80, 8000, and 9000 to allow HTTP traffic.

### Step 2: Install Docker and Docker Compose on the VM

1. **SSH into your VM**:
   ```sh
   ssh -i /path/to/your/private/key azureuser@your_vm_public_ip
   ```

2. **Install Docker and Docker Compose**:
   ```sh
   sudo apt-get update
   sudo apt-get install -y docker.io
   sudo systemctl start docker
   sudo systemctl enable docker
   sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   sudo chmod +x /usr/local/bin/docker-compose
   ```

### Step 3: Deploy the Application

1. **Clone the Repository and Create Configuration File**:
   ```sh
   git clone https://github.com/KamilWitczak242562/mf-efi-task.git
   cd mf-efi-task
   echo "APPID=YOUR_API_KEY" > config.env
   ```

2. **Run Docker Compose**:
   ```sh
   sudo docker-compose up -d
   ```

### Step 4: Set Up Azure Application Gateway

1. **Create an Application Gateway** in the Azure Portal.
2. **Configure Backend Pools** to include your virtual machine.
3. **Create Listeners** for HTTP traffic.
4. **Configure Routing Rules** to route traffic to the appropriate backend pools.

### Step 5: Enable External SSH Access and Add Public Key

1. **Add SSH Public Key** to the VM's authorized keys file:
   - On your local machine, copy the contents of `id_rsa_internship.pub`.
   - On the VM, open the authorized keys file:
     ```sh
     nano ~/.ssh/authorized_keys
     ```
   - Paste the contents of `id_rsa_internship.pub` into this file and save it.

2. **Set Permissions**:
   ```sh
   chmod 700 ~/.ssh
   chmod 600 ~/.ssh/authorized_keys
   ```

3. **Ensure the SSH Port is Open** in the VM's networking settings.

### Access the Application
The application is deployed on Azure and accessible at http://20.215.97.163/.



## TODO

### Ansible

* Write [Ansible](http://docs.ansible.com/ansible/intro.html) playbooks for installing [docker](https://www.docker.com/) and the app itself. These playbooks should work both for local and cloud environment.

#### Terraform

* Write [Terraform](https://www.terraform.io/) configuration files to set up infrastructure required to run the app in the cloud provider of your choice.

### Documentation

* Remember to update the README

* Use descriptive names and add comments in the code when necessary

### ProTips

* The app must be ready to deploy and work flawlessly.

* Detailed instructions to run the app should be included in your forked version because a customer would expect detailed instructions also.

* Extra points for making sure the app could be deployed with as few manual steps as possible.

* Feel free to add would-be-nice-to-haves in the app / infra setup that you didn't have time to complete as possible further improvements in README.
