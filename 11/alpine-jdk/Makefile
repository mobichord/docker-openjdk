JDK ?="13"
JAVA_BUILD ?="27"
JAVA_AGENT ?="0.12.0"
TAG ?="test" 
USER ?="mobichord"
NAME ="openjdk-alpine"

.PHONY:	build	run 
build:
	@echo "build container with using cache $(NAME)"
	docker build -t $(NAME):$(TAG) .


build-nc:
	@echo "build container --no-cache"
	docker build --no-cache -t  $(NAME):$(TAG) . 

build-args:
	@echo "build container with args"
	docker build --build-args JDK=$(JDK) JAVA_BUILD=$(JAVA_BUILD) JAVA_AGENT=$(JAVA_AGENT) -t  $(NAME):$(TAG) . 

run:
	@echo "Running docker container"
	docker run -it --rm  --name $(NAME) $(NAME):$(TAG)

stop:
	@echo "Stop docker container"
	docker stop $(NAME)

clean:
	@echo "Cleaning docker container and image"
	docker rm -f $(NAME)

clean_up:
	@echo "Cleaning docker build containers"
	docker ps -qa | xargs -I ARGS docker rm -f ARGS
	docker images -q -f dangling=true -f label=app=openjdk-alpine | xargs -I ARGS docker rmi -f --no-prune ARGS
