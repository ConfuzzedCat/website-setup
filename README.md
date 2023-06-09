# Træfik Setup Remote

## Requirements

- [DigitalOcean](https://www.digitalocean.com/) account
- [Domain](https://www.namecheap.com/) name (could be any provider)
- Your domain is pointing to DigitalOcean DNS servers
- Wildcard DNS record for your domain (*.your_domain.com)

## Features

- [Traefik](https://traefik.io/) as a reverse proxy
- [Let's Encrypt](https://letsencrypt.org/) for SSL certificates
- [Traefik Dashboard](https://docs.traefik.io/operations/dashboard/) for monitoring
- [PostgreSQL](https://www.postgresql.org/) for database
- [pgAdmin](https://www.pgadmin.org/) for database management
- [Docker](https://www.docker.com/) for containerization
- [Docker Compose](https://docs.docker.com/compose/) for container orchestration
- [DigitalOcean](https://www.digitalocean.com/) for cloud hosting

## Setup

### 1. Create .env file and add your environment variables

```bash
  PROVIDER=digitalocean
  DO_AUTH_TOKEN=<your_token>
  ACME_STORAGE=/etc/traefik/acme/acme.json
  EMAIL=<your_email>
  TRAFIK_DOMAIN=traefik.<your_domain>
  DASHBOARD_AUTH=<your_dashboard_auth>
  API_DOMAIN=<your_api_domain>
  POSTGRES_USER=<your_postgres_user>
  POSTGRES_PASSWORD=<your_postgres_password>
```

To generate your token, go to [DigitalOcean](https://cloud.digitalocean.com/account/api/tokens) and create a new token.

### 2. Create acme.json file

```bash
  touch ./acme/acme.json
```

```bash
  chmod 600 ./acme/acme.json
```

### 3. How to generate DASHBOARD_AUTH

```bash
  echo $(htpasswd -nb <your_username> <your_password>) | sed -e s/\\$/\\$\\$/g
```

### 4. Run Docker

```bash
  docker-compose up -d
```

### 5. Stop Docker

```bash
  docker-compose down
```

### 6. Access Traefik Dashboard through browser

```bash
  traefik.<your_domain>
```

### 7. Access Your Rest Api

```bash
  <your_domain>/<your_api_path>
```

### 8. Clear DB data installation

(-v) // remove volumes
```bash
 docker-compose down -v 
```

```bash
 sudo  rm -rf ./data
```

