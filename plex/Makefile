VERSION = 'docker'
TAG = 'latest'

create:
	@echo "Creating docker container..."
	docker create \
		--name plex \
		--net=host \
		-e PUID=$(id -u) \
		-e PGID=$(id -g) \
		-e VERSION=$(VERSION) \
		-v /nas/docker/plex/config:/config \
		-v /nas/medias/movies:/data/movies \
		-v /nas/medias/tvshows:/data/tvshows \
		-v /nas/medias/animes:/data/animes \
		-v /nas/medias/docus:/data/docus \
		--restart unless-stopped \
		linuxserver/plex:$(TAG)

start:
	@echo "Starting container..."
	docker start plex

stop:
	@echo "Stopping container..."
	docker stop plex

delete:
	@echo "Deleting container..."
	docker rm -f plex

upgrade:
	@echo "Updating plex image..."
	docker pull linuxserver/plex:$(TAG)
	docker image prune

restart: stop start

destroy: stop delete

update: stop delete upgrade create start
