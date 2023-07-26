# Docker container for Ansible environment

## Installation

1. VSCode devcontainer

    Just download and include in your project

2. Build docker image

  - build image: `docker build -t ${IMAGE_NAME} .devcontainer`
  - run container: `docker run -d --name ${CONTAINER_NAME} ${IMAGE_NAME}`
  - access to container: `docker exec -it ${CONTAINER_NAME} bash`