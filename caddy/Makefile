all : test docs
.PHONY : all
test:
	@echo "Hello Yubico"

docs:
	@echo "Author:Prangya Parmita Kar"
	@echo "This is to build caddy server using a ubuntu base image"
	@echo "make clean:  To clean all images and containers"
	@echo "make build:  To build the caddy from source and it creates the docker image"
	@echo "make run:  To run the caddy and print Hello world!"
	@echo "This compile with https://blog.golang.org/go1.14 "

build:
	@echo "Creating docker build"
	docker images
	docker build -t prangya-caddy-image:1.0 . -f Dockerfile --no-cache
	#docker build -t pammi:1.0 . -f Dockerfile --no-cache

run:
	@echo "Creating docker container"
	docker ps -a
	docker run -it --name prangya-caddy-web -p 8080:8080 prangya-caddy-image:1.0
	#to run caddy on detach mode use docker run -d -it --name prangya-caddy-web -p 8080:8080 prangya-caddy-image:1.0

clean:
	@echo "Cleaning docker images and process"
	@echo "Cleaning docker images"
	docker rmi -f $$(docker images -q) || true
	@echo "Cleaning docker running processes"
	docker rm -f $$(docker ps -a -q) || true
