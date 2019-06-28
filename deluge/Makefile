create:
	@echo "Creating docker container..."
	docker create --name deluge --net=host -e PUID=$(id -u) -e PGID=$(id -g) -e TZ="Europe/Paris" -v /nas/downloads/torrents:/downloads -v /nas/docker/deluge/config:/config lsioarmhf/deluge

start:
	@echo "Starting container..."
	docker start deluge

stop:
	@echo "Stopping container..."
	docker stop deluge

delete:
	@echo "Deleting container..."
	docker container rm -f deluge

destroy: stop delete
