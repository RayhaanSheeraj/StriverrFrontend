---
layout: base
title: AWS Deployment Plan
search_exclude: true
permalink: /Striver/deployment
author: Hithin, Nikith, Rayhaan, Pradyun, Neil, Kush, Zaiddf
---

## AWS Deployment Process for Backend/Database

### Prerequisites

1. **AWS Account**: Obtain access to an active AWS account.
2. **IAM User**: Create an Identity and Access Management (IAM) user with the required permissions.
3. **AWS CLI**: Install and configure the AWS Command Line Interface (CLI) on your local machine. Follow the [AWS CLI installation guide](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html).

### Test Server

Ensure your frontend-to-backend test server is fully functional locally. If it does not work in the local environment, it will not work in deployment.

### Subdomain Setup

Configure a DNS endpoint through AWS Route 53:

```yaml
Server: https://Striverr2025nighthawkcodingsociety.com/
Domain: nighthawkcodingsociety.com
Subdomain: Striverr2025
```

### Port Configuration

**Backend:**

1. **main.py:** Ensure the server runs on the designated port (8503).

```python
if __name__ == "__main__":
    app.run(debug=True, host="0.0.0.0", port=8503)
```

2. **Dockerfile:** Configure to run the server as a virtual machine.

```dockerfile
FROM docker.io/python:3.11
WORKDIR /
RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y python3 python3-pip git
COPY . /
RUN pip install --no-cache-dir -r requirements.txt
RUN pip install gunicorn
ENV GUNICORN_CMD_ARGS="--workers=1 --bind=0.0.0.0:8085"
EXPOSE 8503
ENV FLASK_ENV=production
CMD [ "gunicorn", "main:app" ]
```

3. **docker-compose.yml:** Define Docker services.

```yaml
version: '3'
services:
    web:
        image: flask2025
        build: .
        env_file:
            - .env
        ports:
            - "8503:8503"
        volumes:
            - ./instance:/instance
        restart: unless-stopped
```

4. **nginx Configuration:** Set up as a reverse proxy.

```nginx
server {
    listen 80;
    listen [::]:80;
    server_name Striverr2025.nighthawkcodingsociety.com;

    location / {
        proxy_pass http://localhost:8503;
        if ($request_method = OPTIONS) {
            add_header "Access-Control-Allow-Credentials" "true" always;
            add_header "Access-Control-Allow-Origin" "https://nighthawkcoders.github.io" always;
            add_header "Access-Control-Allow-Methods" "GET, POST, PUT, DELETE, OPTIONS, HEAD" always;
            add_header "Access-Control-Allow-MaxAge" 600 always;
            add_header "Access-Control-Allow-Headers" "Authorization, Origin, X-Origin, X-Requested-With, Content-Type, Accept" always;
            return 204;
        }
    }
}
```

### Frontend Configuration

Update to match domain and port settings:

```javascript
export var pythonURI;
if (location.hostname === "localhost" || location.hostname === "127.0.0.1") {
    pythonURI = "http://localhost:8503";
} else {
    pythonURI = "https://Striverr2025.nighthawkcodingsociety.com";
}
```

### Accessing AWS EC2

1. Log into AWS Console and access the EC2 Dashboard.
2. Launch an EC2 instance.
3. Alternatively, use Cockpit for server management.

### Application Setup

1. Ensure port 8503 is open:

```bash
docker ps
```

2. Use `docker-compose up` locally to build and test:

```bash
docker-compose up
```

### Server Setup

1. Clone the backend repository:

```bash
git clone https://github.com/illuminati1618/prism_backend.git
cd prism_backend
docker-compose up -d --build
curl localhost:8503
```

2. **Route 53 DNS:** Configure subdomain routing.

3. **Nginx Setup:**

```bash
cd /etc/nginx/sites-available
sudo nano prism
cd /etc/nginx/sites-enabled
sudo ln -s /etc/nginx/sites-available/prism /etc/nginx/sites-enabled
sudo nginx -t
sudo systemctl restart nginx
```

4. **Certbot Configuration:**

```bash
sudo certbot --nginx
```

### Deployment Updates

1. Pull changes:

```bash
cd ~/Striverr_2025
docker-compose down
git pull
docker-compose up -d --build
```

2. Troubleshoot with:

```bash
curl localhost:8503
docker-compose ps
docker ps
```