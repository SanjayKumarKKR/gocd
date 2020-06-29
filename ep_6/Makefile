GIT_TAG := $(shell git rev-parse --short HEAD)

all: build tag push

build:
ifeq ($(OS),Windows_NT)
    del /s *.o *.d *.elf *.map *.log
endif
	docker build .

tag:
	docker tag sanjay:latest 966166518746.dkr.ecr.us-east-1.amazonaws.com/sanjay:latest

push:
	aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 966166518746.dkr.ecr.us-east-1.amazonaws.com


test:
	docker run -d -p 8080:80 --rm --name sanjay
	sleep 2
	curl localhost:8080

test_clean:
	docker rm -f sanjay
