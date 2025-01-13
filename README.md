# Roadmap.sh-007
Blue-Green Deployment with Traefik Routing Priority

## Requirements:
```Docker``` and ```docker-compose```

### Get started
```
git clone https://github.com/jammie-jelly/Roadmap.sh-007.git
```
```
cd Roadmap.sh-007
```

### Deploy blue-green service
```docker compose up -d```

### Confirm traefik and both green & blue services are running
```
docker compose ps
NAME                          IMAGE          COMMAND                  SERVICE   CREATED         STATUS         PORTS
blue-green-deploy-blue-1      nginx:alpine   "/docker-entrypoint.…"   blue      6 seconds ago   Up 5 seconds   80/tcp
blue-green-deploy-green-1     nginx:alpine   "/docker-entrypoint.…"   green     6 seconds ago   Up 5 seconds   80/tcp
blue-green-deploy-traefik-1   traefik:v3     "/entrypoint.sh --pr…"   traefik   6 seconds ago   Up 5 seconds   0.0.0.0:80->80/tcp, :::80->80/tcp
```

On your browser go to ```http://localhost/``` and you will see the ```blue``` deployment.

# Gist of the solution
```traefik.http.routers.$color.priority=$int```

Whatever service has the ```highest priority``` gets selected. This also means if one service goes down the other one will be picked up automatically thanks to Traefik's loadbalancer.


Part of this challenge: https://roadmap.sh/projects/blue-green-deployment
