## ❓ Help
### How to Create A deployed site
#### **1. Prerequisites**
✅ Access an active **AWS account**.

✅ Create an **IAM user** with necessary permissions.

#### **2. Local Testing**
✅ Verify that the **frontend-backend test server** works locally without issues.

#### **3. Subdomain Configuration**
✅ Set up a **DNS endpoint** in **AWS Route 53**:
  - **Server:** `https://striver.stu.nighthawkcodingsociety.com/`
  - **Domain:** `nighthawkcodingsociety.com`
  - **Subdomain:** `striver.stu`

#### **4. Backend Port Settings**
✅ **main.py:** Confirm the server listens on **port 8503**:
  ```python
  if __name__ == "__main__":
      app.run(debug=True, host="0.0.0.0", port=8503)
  ```
✅ **Dockerfile:** Ensure it’s configured to run the server:
  - Install dependencies.
  - Expose **port 8503**.
  - Set `FLASK_ENV` to deployed.

✅ **docker-compose.yml:** Define services:
  - Map **port 8503** correctly.
  - Ensure environment variables are set.

✅ **Nginx Configuration:** Set up reverse proxy:
  - Listen on **port 80** (do NOT change to 8503).
  - Proxy traffic to **localhost:8503**.

#### **5. Frontend Integration**
✅ Update frontend code to detect environment and route requests:
  ```javascript
  export var pythonURI;
  if (location.hostname === "localhost" || location.hostname === "127.0.0.1") {
      pythonURI = "http://localhost:8503";
  } else {
      pythonURI = "https://striver.stu.nighthawkcodingsociety.com";
  }
  ```

#### **6. Launching an EC2 Instance**
✅ Log into **AWS Console** → Go to **EC2 Dashboard**. To login to the deployment server on AWS EC2 you will use cockpit backdoor. https://cockpit.stu.nighthawkcodingsociety.com/

✅ Launch a new **EC2 instance**.

#### **7. Application Deployment**
✅ Ensure **port 8503** is open and accessible:
  ```bash
  docker ps
  ```
✅ Build the Docker container:
  ```bash
  docker-compose build
  docker-compose up -d
  ```

#### **8. Server Configuration**
✅ Clone the backend repository to the EC2 instance:
  ```bash
  git clone https://github.com/RayhaanSheeraj/StriverrBackend.git  striverr_backend
  cd striverr_backend
  curl localhost:8503
  ```
✅ Configure **Route 53 DNS** for the subdomain.

✅ Set up **Nginx**:
  ```bash
  cd /etc/nginx/sites-available
  sudo nano striverr.nginx_file  striverr.stu
  cd /etc/nginx/sites-enabled
  sudo ln -s /etc/nginx/sites-available/striverr.stu /etc/nginx/sites-enabled
  sudo nginx -t
  sudo systemctl restart nginx
  ```
Use the
  ```bash
  cat striverr.stu
  ```
to check that the contents of the nginx file are correctly copied into striverr.stu in sites-available.

✅ Secure the server with **Certbot (SSL)**:
  ```bash
  sudo certbot --nginx
  ```

#### **9. Updating the Deployment**
✅ Pull the latest changes from the repository:
  ```bash
  cd ~/striverr_backend
  docker-compose down
  git pull
  docker-compose build
  docker-compose up -d
  sudo cp -f striverr.nginx_file /etc/nginx/sites-available/striverr.stu
  ```
✅ Troubleshoot if needed:
  ```bash
  curl localhost:8503
  docker ps
  ```