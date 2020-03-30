TAG = 'latest'
UID = $(shell id -u)
GID = $(shell id -g)

create:
	@echo "Creating docker container..."
	docker create \
		--name=sickchill \
		-e PUID=$(UID) \
		-e PGID=$(GID) \
		-e TZ=Europe/Paris \
		-p 8081:8081 \
		-v /nas/docker/sickchill/config:/config \
		-v /nas/media:/tv \
		-v /nas/media/download:/downloads \
		--restart unless-stopped \
		linuxserver/sickchill:$(TAG)

start:
	@echo "Starting container..."
	docker start sickchill

stop:
	@echo "Stopping container..."
	docker stop sickchill

delete:
	@echo "Deleting container..."
	docker rm -f sickchill

update:
	@echo "Updating image..."
	docker pull linuxserver/sickchill:$(TAG)
	docker image prune

restart: stop start

destroy: stop delete

upgrade: stop delete update create start
