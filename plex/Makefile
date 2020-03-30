VERSION = 'docker'
TAG = 'latest'
UID = $(shell id -u)
GID = $(shell id -g)
CLAIM = 'claim-D51WRNjuyC_8tnSSBWPP'

create:
	@echo "Creating docker container..."
	docker create \
		--name plex \
		--net=host \
		-e PUID=$(UID) \
		-e PGID=$(GID) \
		-e VERSION=$(VERSION) \
		-e PLEX_CLAIM=$(CLAIM) \
		-v /nas/docker/plex:/config \
		-v /nas/media/movies:/data/movies \
		-v /nas/media/tvshows:/data/series \
		-v /nas/media/animes:/data/animes \
		-v /nas/media/docus:/data/docus \
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

update:
	@echo "Updating image..."
	docker pull linuxserver/plex:$(TAG)
	docker image prune

restart: stop start

destroy: stop delete

upgrade: stop delete update create start
