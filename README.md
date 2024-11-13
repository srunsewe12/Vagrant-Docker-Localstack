# Local AWS-Integrated Development Environment

This repository provides a template for setting up a local development environment that emulates AWS services using Vagrant, Docker Compose, and Localstack. It's designed to help developers work independently on their feature branches without the need for shared staging environments.

## **Prerequisites**

Before you begin, ensure you have the following tools installed on your machine:

- **Vagrant**: [Download Vagrant](https://www.vagrantup.com/downloads)
- **Docker and Docker Compose**: [Download Docker](https://www.docker.com/products/docker-desktop)
- **Vagrant Docker Compose Plugin**: Install with the following command:

```
vagrant plugin install vagrant-docker-compose
```

**Getting Started**

**Clone the Repository**

```
git clone (https://github.com/srunsewe12/Vagrant-Docker-Localstack.git)
cd Vagrant-Docker-Localstack
```

**Bring Up the Environment**

```
vagrant up --provider=docker
```

This command will:

- Use Vagrant to provision the environment with Docker as the provider.
- Install Docker and Docker Compose inside the container.
- Run docker-compose.yml to start all the services.

Note: The first time you run this command, it may take several minutes to download all the necessary Docker images.

**Accessing the Application**
- The Django application should be accessible at ```http://localhost:8000.```
- Other services are exposed on their respective ports as defined in the docker-compose.yml file.

**Stopping and Destroying the Environment**

**Stop the environment:**

```
vagrant halt
```

**Destroy the environment:**

```
vagrant destroy
```


**Services Included**

**Django Application** (app),
**Celery Workers** (celery and celery_scheduler),
**PostgreSQL Database** (db),
**Redis Cache** (redis),
**Kafka and Zookeeper** (kafka and zookeeper),
**Localstack** (localstack): Emulates AWS services locally,
**Trino** (trino): SQL query engine for distributed data

**Configuration**

**Environment Variables**
Environment variables are set in the Vagrantfile and passed to the Docker containers. You should replace placeholder values with your actual configuration.

**Example:**

In Vagrantfile:

```echo "export SECRET_KEY=your_actual_secret_key" >> /etc/environment```

As a more secure alternative, you can create a .env file in the project root with your environment variables:


```
SECRET_KEY=your_actual_secret_key
DEFAULT_REGION=us-east-1
DJANGO_DEBUG=True
OTHER_ENV_VAR=your_value_here
```

Then, modify the docker-compose.yml to use the .env file:

```
env_file:
  - .env
```

**Dockerfile**
Make sure you have a Dockerfile in your project root that defines how to build your application image. This repo assumes you have one.

**Customizing the Setup**
Feel free to modify the services, environment variables, and configurations to suit your project's needs.

- To add new services, update the docker-compose.yml file.
- To modify environment variables, adjust them in the Vagrantfile or use a .env file.
- To change service configurations, update individual service settings.

**Troubleshooting**
1. Service Not Starting: Check the logs for any service by running:

```
docker-compose logs [service_name]
```

2. Port Conflicts: Double-check that the ports exposed in docker-compose.yml are not already used on your host machine.

3. Database Connection Issues: Verify that the environment variables for database credentials are correctly set.

**Contributing**
Contributions are welcome! Please fork the repository and submit a pull request with your changes.

**License**
This project is licensed under the MIT License - see the LICENSE file for details.

Note: This setup is intended for local development and testing purposes only. Please don't use this configuration for production environments.

