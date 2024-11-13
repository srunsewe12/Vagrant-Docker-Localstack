# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Use Docker as the provider
  config.vm.provider "docker" do |d|
    d.image = "ubuntu:20.04"
    d.has_ssh = false
  end

  # Install Docker and Docker Compose inside the container
  config.vm.provision "docker"
  config.vm.provision :docker_compose, yml: "/vagrant/docker-compose.yml", run: "always"

  # Set environment variables
  config.vm.provision "shell", inline: <<-SHELL
    echo "export SECRET_KEY=your_secret_key_here" >> /etc/environment
    echo "export DEFAULT_REGION=us-east-1" >> /etc/environment
    echo "export DJANGO_DEBUG=True" >> /etc/environment
    echo "export OTHER_ENV_VAR=your_value_here" >> /etc/environment
    # Add any other environment variables you need
  SHELL
end

