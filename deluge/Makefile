TAG = latest
UID = $(shell id -u)
GID = $(shell id -g)

create:
	@echo "Creating docker container..."
	docker create \
		--name deluge \
		--net=host \
		-e PUID=$(UID) \
		-e PGID=$(GID) \
		-e TZ=Europe/Paris \
		-v /nas/docker/deluge/config:/config \
		-v /nas/media/downloads:/downloads \
		--restart unless-stopped \
		linuxserver/deluge:$(TAG)

start:
	@echo "Starting container..."
	docker start deluge

stop:
	@echo "Stopping container..."
	docker stop deluge

delete:
	@echo "Deleting container..."
	docker rm -f deluge

update:
	@echo "Updating image..."
	docker pull linuxserver/deluge:$(TAG)
	docker image prune

restart: stop start

destroy: stop delete

upgrade: stop delete update create start
