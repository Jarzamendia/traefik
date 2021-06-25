# Traefik 2 - Docker Swarm

docker network create -d overlay proxy_net

docker stack deploy -c .\traefik.yaml traefik

docker stack deploy -c .\api.yaml api

docker stack deploy -c .\nginx.yaml nginx