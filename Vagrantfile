# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Use Debian Bookworm as the base OS
  config.vm.box = "debian/bookworm64"

  # Port forwarding to access Flask app from host machine
  config.vm.network "forwarded_port", guest: 5000, host: 8080

  # Provisioning script to install Flask and dependencies
  config.vm.provision "shell", inline: <<-SHELL
    # Update packages and install required software
    sudo apt update
    sudo apt install -y git nano vim python-is-python3 python3-venv python3-pip curl

    # Set up a Python virtual environment
    python3 -m venv /home/vagrant/flask_venv
    source /home/vagrant/flask_venv/bin/activate

    # Install Flask
    pip install Flask
  SHELL

  # Upload the Flask app from host to VM
  config.vm.provision "file", source: "hello.py", destination: "/home/vagrant/hello.py"
end
