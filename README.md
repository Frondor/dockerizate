# Final stack

  - Nginx (SSL)
  - Static website (Nuxt) at `example.com`
  - SPA (Vue) at `app.example.com`
  - Restful API (nodejs) at `api.example.com`
  - MySQL database (mariadb)
  - Redis
  - Elasticsearch (probably)

# Scripts `.sh`

  - start [--front|--back]  (clone submodules)
  - test
  - deploy

## Useful commands

#### Compose for development
`docker-compose up -d`

#### Restart a single service
docker-compose restart nginx

#### Compose for production
`docker-compose -f docker-compose.yml -f docker-compose.production.yml up -d`

#### Open shell with api container as context
docker-compose run --rm api sh

#### Remove unused images: docker image ls
docker image prune