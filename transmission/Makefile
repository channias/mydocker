TAG = 'latest'
UID = $(shell id -u)
GID = $(shell id -g)

create:
	@echo "Creating docker container..."
	docker create \
		--name transmission \
		--net=host \
		-e PUID=$(UID) \
		-e PGID=$(GID) \
		-e TZ=Europe/Paris \
		-e TRANSMISSION_WEB_HOME=/transmission-web-control/ \
		-p 9091:9091 \
		-p 51413:51413 \
		-p 51413:51413/udp \
		-v /nas/docker/transmission/config:/config \
		-v /nas/downloads/torrents:/downloads \
		-v /nas/downloads/torrents/watch:/watch \
		--restart unless-stopped \
		linuxserver/transmission:$(TAG)

start:
	@echo "Starting container..."
	docker start transmission

stop:
	@echo "Stopping container..."
	docker stop transmission

delete:
	@echo "Deleting container..."
	docker rm -f transmission

update:
	@echo "Updating plex image..."
	docker pull linuxserver/transmission:$(TAG)
	docker image prune

restart: stop start

destroy: stop delete

upgrade: stop delete update create start
