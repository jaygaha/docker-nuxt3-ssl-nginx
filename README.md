# Nuxt 3 with Nginx and SSL Docker Container

This Docker container runs a Nuxt 3 application with an Nginx server and SSL encryption.
It is based on the official Nuxt 3 Docker image and the official Nginx Docker image

Look at the [Nuxt 3 documentation](https://nuxt.com/docs/getting-started/introduction) to learn more.

## Setup

### Installation

Use the package manager [git](https://git-scm.com/downloads) to install docker boilerplate.

```bash
$ git clone https://github.com/jaygaha/docker-nuxt3-ssl-nginx.git
```

Copy `.env` variable:

```bash
$ cp .env.example .env
```

**Adjust the environment variable according to your preference.**

For the local development, adjust as:

```bash
NODE_ENV=development
DOCKER_FILE=./.docker/node/Dockerfile.dev
NGINX_CONFIG=./.docker/nginx/default.dev.conf
```

### Update SSL

For development, create self-signed certificates:

```bash
$ mkdir -p .docker/nginx/certs/dev
$ openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout .docker/nginx/certs/dev/server.key -out .docker/nginx/certs/dev/server.crt -subj "/CN=localhost"

```

For production, use Certbot to obtain Let's Encrypt certificates:

```bash
$ mkdir -p .docker/nginx/certs/prod
$ docker run -it --rm --name certbot -v "$(pwd)/.docker/nginx/certs/prod:/etc/letsencrypt" -v "$(pwd)/.docker/nginx/www:/var/www" certbot/certbot certonly --webroot -w /var/www -d yourdomain.com

```

**Replace `yourdomain.com` with your real domain name.**

Make sure to install the dependencies:

```bash
npm install
```

## Run Docker Container

Build the Docker container using the following command:

```bash
$ docker compose build
$ docker compose up -d
```

Check the browser:

Start the development server on `http://localhost:8000`

That's it! You have successfully set up a Dockerized Nuxt 3 application with an Nginx server and SSL certificates using Let's Encrypt.

Check out the [Nuxt 3 deployment documentation](https://nuxt.com/docs/getting-started/deployment) for more information.
