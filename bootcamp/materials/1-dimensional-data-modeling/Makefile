include example.env

.PHONY: up
up:
	@if [ ! -f .env ]; then \
		echo "WARNING: .env file does not exist! 'example.env' copied to '.env'. Please update the configurations in the .env file running this target."; \
		cp example.env .env; \
        exit 1; \
	fi
	# docker compose up -d;
	podman compose up -d;

.PHONY: down
down:
	podman compose down -v
	@if [[ "$(podman ps -q -f name=${DOCKER_CONTAINER})" ]]; then \
		echo "Terminating running container..."; \
		podman rm ${DOCKER_CONTAINER}; \
	fi

.PHONY: restart
restart:
	podman compose down -v; \
	sleep 5; \
	podman compose up -d;

.PHONY: logs
logs:
	podman logs ${DOCKER_CONTAINER}


.PHONY: inspect
inspect:
	podman inspect ${DOCKER_CONTAINER} | grep "Source"


.PHONY: ip
ip:
	@if [[ "$$(podman ps -q -f name=${DOCKER_CONTAINER})" ]]; then \
		echo "Container ${DOCKER_CONTAINER} running! Forwarding connections from $$(podman port ${DOCKER_CONTAINER})"; \
	else \
		echo "Container not running. Please start the container and try again."; \
	fi
