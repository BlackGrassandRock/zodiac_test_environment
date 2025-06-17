# grand-challenge.org

[![Build Status](https://github.com/comic/grand-challenge.org/workflows/CI/badge.svg)](https://github.com/comic/grand-challenge.org/actions?query=workflow%3ACI+branch%3Amain)
[![Documentation](https://img.shields.io/badge/docs-published-success)](https://comic.github.io/grand-challenge.org/)
[![Black Code Style](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/ambv/black)
[![Cite Us with Zenodo](https://zenodo.org/badge/4557968.svg)](https://zenodo.org/badge/latestdoi/4557968)

In the era of Deep Learning, developing robust machine learning solutions to problems in biomedical imaging requires access to large amounts of annotated training data, objective comparisons of state of the art machine learning solutions, and clinical validation using real world data. Grand Challenge can assist Researchers, Data Scientists, and Clinicians in collaborating to develop these solutions by providing:

* Archives: Manage medical imaging data.
* Reader Studies: Train experts and have them annotate medical imaging data.
* Challenges: Gather and objectively assess machine learning solutions.
* Algorithms: Deploy machine learning solutions for clinical validation.

If you would like to start your own website, or contribute to the development of the framework, please see [the docs](https://comic.github.io/grand-challenge.org/).



**Installation and Running the Project on Ubuntu**

The following commands install all necessary libraries and dependencies, set up Docker, and launch the project. This setup is intended to get the project running smoothly on an Ubuntu system.



# Update system and install essential packages
sudo apt update && sudo apt install -y \
    git \
    make \
    python3-pip

# Install Docker and Docker Compose
sudo apt update
sudo apt install -y ca-certificates curl gnupg

sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
  sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) \
  signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Add the current user to the docker group
sudo usermod -aG docker $USER
newgrp docker

# Clone the project repository
git clone https://github.com/BlackGrassandRock/zodiac_test_environment
cd zodiac_test_environment

# Set Docker group ID environment variable
echo "DOCKER_GID=$(getent group docker | cut -d: -f3)" > .env

# Run the project server
make runserver
