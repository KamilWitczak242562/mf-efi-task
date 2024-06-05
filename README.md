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


## TODO

### Cloud hosting

* Set up the weather service in a free cloud hosting service, e.g. [Azure](https://azure.microsoft.com/en-us/free/), [AWS](https://aws.amazon.com/free/) or [Google Cloud](https://cloud.google.com/free/).
* Enable external access to weather app via HTTP reverse proxy. We suggest creating one compute instance e.g. for AWS one EC2 instance, that will host both weather app and before mentioned proxy. Remember that Weather App should be exposed in a secure way.
* Enable external SSH access and add id_rsa_internship.pub key, which you can find in this repository. We would like to check your work so grant us admin rights on your test system.

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
