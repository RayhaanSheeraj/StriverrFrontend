### ✅ **AWS Deployment Checklist**

#### **1. Prerequisites**
- [ ] Access an active **AWS account**.
- [ ] Create an **IAM user** with necessary permissions.
- [ ] Install and configure the **AWS CLI**. [AWS CLI Installation Guide](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html).

#### **2. Local Testing**
- [ ] Verify that the **frontend-backend test server** works locally without issues.

#### **3. Subdomain Configuration**
- [ ] Set up a **DNS endpoint** in **AWS Route 53**:
  - **Server:** `https://Striverr2025.nighthawkcodingsociety.com/`
  - **Domain:** `nighthawkcodingsociety.com`
  - **Subdomain:** `Striverr2025`

#### **4. Backend Port Settings**
- [ ] **main.py:** Confirm the server listens on **port 8503**:
  ```python
  if __name__ == "__main__":
      app.run(debug=True, host="0.0.0.0", port=8503)
  ```
- [ ] **Dockerfile:** Ensure it’s configured to run the server:
  - Install dependencies.
  - Expose **port 8503**.
  - Set `FLASK_ENV` to production.
- [ ] **docker-compose.yml:** Define services:
  - Map **port 8503** correctly.
  - Ensure environment variables are set.
- [ ] **Nginx Configuration:** Set up reverse proxy:
  - Listen on **port 80** (do NOT change to 8503).
  - Proxy traffic to **localhost:8503**.

#### **5. Frontend Integration**
- [ ] Update frontend code to detect environment and route requests:
  ```javascript
  export var pythonURI;
  if (location.hostname === "localhost" || location.hostname === "127.0.0.1") {
      pythonURI = "http://localhost:8503";
  } else {
      pythonURI = "https://Striverr2025.nighthawkcodingsociety.com";
  }
  ```

#### **6. Launching an EC2 Instance**
- [ ] Log into **AWS Console** → Go to **EC2 Dashboard**.
- [ ] Launch a new **EC2 instance**.
- [ ] (Optional) Use **Cockpit** for managing the server.

#### **7. Application Deployment**
- [ ] Ensure **port 8503** is open and accessible:
  ```bash
  docker ps
  ```
- [ ] Build and test the Docker container **locally**:
  ```bash
  docker-compose up
  ```

#### **8. Server Configuration**
- [ ] Clone the backend repository to the EC2 instance:
  ```bash
  git clone https://github.com/RayhaanSheeraj/StriverrBackend.git
  cd StriverrBackend
  docker-compose up -d --build
  curl localhost:8503
  ```
- [ ] Configure **Route 53 DNS** for the subdomain.
- [ ] Set up **Nginx**:
  ```bash
  cd /etc/nginx/sites-available
  sudo nano prism
  cd /etc/nginx/sites-enabled
  sudo ln -s /etc/nginx/sites-available/prism /etc/nginx/sites-enabled
  sudo nginx -t
  sudo systemctl restart nginx
  ```
- [ ] Secure the server with **Certbot (SSL)**:
  ```bash
  sudo certbot --nginx
  ```

#### **9. Updating the Deployment**
- [ ] Pull the latest changes from the repository:
  ```bash
  cd ~/Striverr_2025
  docker-compose down
  git pull
  docker-compose up -d --build
  ```
- [ ] Troubleshoot if needed:
  ```bash
  curl localhost:8503
  docker-compose ps
  docker ps
  ```