help:
	@cat Makefile

DATA?="${HOME}/Data"
GPU?=0
DOCKER_FILE=Dockerfile
DOCKER=GPU=$(GPU) nvidia-docker
BACKEND=tensorflow
TEST=tests/
SRC=$(shell dirname `pwd`)/tensorflow/src


build:
	docker build -t tf -f $(DOCKER_FILE) .
bash: build
	$(DOCKER) run -it -v $(SRC):/code -v $(DATA):/data --env KERAS_BACKEND=$(BACKEND) tf bash

ipython: build
	$(DOCKER) run -it -v $(SRC):/code -v $(DATA):/data --env KERAS_BACKEND=$(BACKEND) tf ipython

notebook: build
	$(DOCKER) run -it -v $(SRC):/code -v $(DATA):/data --net=host --env KERAS_BACKEND=$(BACKEND) tf

test: build
	$(DOCKER) run -it -v $(SRC):/code -v $(DATA):/data --env KERAS_BACKEND=$(BACKEND) tf py.test $(TEST)
