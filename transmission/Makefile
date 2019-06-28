TAG = 'latest'

create:
	@echo "Creating docker container..."
	docker create \
		--name transmission \
		--net=host \
		-e PUID=$(id -u) \
		-e PGID=$(id -g) \
		-e TZ=Europe/Paris \
		-e TRANSMISSION_WEB_HOME=/combustion-release/ \
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

upgrade:
	@echo "Updating plex image..."
	docker pull linuxserver/transmission:$(TAG)
	docker image prune

restart: stop start

destroy: stop delete

update: stop delete upgrade create start
