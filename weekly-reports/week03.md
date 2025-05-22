# Week 3 (May 16 – May 22, 2025)

## What I studied
- Docker installation and basic commands: `run`, `images`, `ps`, `volume`
- Creating and running containers from images (hello-world, ubuntu)
- Writing a custom Dockerfile for a Python echo server
- Building and running Docker containers
- Using `docker-compose` for multi-container setups (Flask + PostgreSQL)
- Reverse proxy with Nginx for Python applications

## What I practiced

### Docker Basics
- Installed Docker on Ubuntu using `sudo apt install docker.io`
- Verified installation and added user to `docker` group
- Ran test container:
  ```bash
  docker run hello-world
  ```
- Launched Ubuntu container and interacted via shell:
  ```bash
  docker run -it ubuntu bash
  ```
- Created a Docker volume and attached it to a container:
  ```bash
  docker volume create my_volume
  docker run -dit --name my_container1 -v my_volume:/app/data ubuntu bash
  ```

### Python Echo Server with Dockerfile
- Wrote a simple TCP echo server in Python using `socket` module
- Created Dockerfile:
  ```Dockerfile
  FROM python:3.11-slim
  WORKDIR /app
  COPY echo_server.py .
  EXPOSE 12345
  CMD ["python", "echo_server.py"]
  ```
- Built and ran the image:
  ```bash
  docker build -t echo-server .
  docker run -d -p 12345:12345 --name echo echo-server
  ```

### Docker Compose: Flask + PostgreSQL
- Installed `docker-compose`
- Created a multi-container app with:
  - Flask web server
  - PostgreSQL database
- Wrote `docker-compose.yml`:
  ```yaml
  version: '3'
  services:
    web:
      build: ./app
      ports:
        - "5000:5000"
    db:
      image: postgres:15
      environment:
        POSTGRES_USER: user
        POSTGRES_PASSWORD: pass
        POSTGRES_DB: mydb
  ```
- Flask app connects to PostgreSQL and responds on `/`
- Verified deployment in browser via `http://<IP>:5000`

### Nginx as Reverse Proxy for Flask App
- Created a project with two services:
  - Flask app responding on port 5000
  - Nginx reverse proxy listening on port 80
- `nginx.conf`:
  ```nginx
  events {}
  http {
      server {
          listen 80;
          location / {
              proxy_pass http://app:5000;
          }
      }
  }
  ```
- Launched both services via `docker-compose up --build`
- Verified proxying worked correctly: Nginx forwarded requests to Flask app

## Problems I solved
- Initially forgot to expose ports in `Dockerfile` and `docker run` — fixed with `EXPOSE` and `-p` flags
- Docker volume not persisting due to wrong mount point — corrected volume path
- Docker Compose `build` failed until I adjusted file structure and context paths
- Nginx config didn’t proxy correctly at first — resolved by using correct container name in `proxy_pass`

## Plans for next week
-Configure Docker volume to persist data between container restarts

-Explore CI/CD pipelines with GitHub Actions or GitLab CI for automated builds
=Finalize the project and document the Docker infrastructure
-Register on a VPS platform (Hetzner, DigitalOcean, or Yandex Cloud) and deploy the server
-Set up SSH keys, sudo access, Fail2Ban, UFW, and Nginx with TLS for basic server security
