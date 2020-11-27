# Name of the docker image
IMAGE :=cfs
# Container name is the current git hash
NAME := $(shell git rev-parse --short HEAD)

.PHONY: clean

build:
	$(info Make: Building image "$(IMAGE)".)
	@docker build -t $(IMAGE) -f Dockerfile .

run:
	$(info Make: Starting container "$(NAME)".)
	@docker run --name=$(IMAGE)-$(NAME) -d $(IMAGE)

run-bash:
	$(info Make: Starting container "$(NAME)" with bash.)
	@docker run -it --name=$(IMAGE)-$(NAME) $(IMAGE) /bin/bash

run-display:
	$(info Make: Starting container "$(NAME)" with display support and bash.)
	@docker run -it -e DISPLAY=$(DISPLAY) -v /tmp/.X11-unix:/tmp/.X11-unix --sysctl fs.mqueue.msg_max=256 --name=$(IMAGE)-$(NAME) $(IMAGE)

bash:
	$(info Make: Starting a bash session for container "$(NAME)".)
	@docker exec -it $(IMAGE)-$(NAME) /bin/bash

stop:
	$(info Make: Stopping container "$(NAME)".)
	@docker stop $(IMAGE)-$(NAME)

restart:
	$(info Make: Restarting container "$(NAME)".)
	@docker restart $(IMAGE)-$(NAME)

rm: stop
	$(info Make: Deleting container "$(NAME)".)
	@docker rm $(IMAGE)-$(NAME)

rmi: stop
	$(info Make: Deleting image "$(IMAGE)".)
	@docker images -a | grep "cfs" | awk '{print $3}' | xargs docker rmi

prune: 
	$(info Make: Deleting dangling images.)
	@docker system prune
