# Networking Assignment v2

## Build a HA Web Setup with SSL and Reverse Proxy

Deploy a web setup using multiple backend servers, a reverse proxy (NGINX), and secure the setup with an SSL certificate.

---

## Requirements

### Domain & DNS Setup
- Buy a domain (if you don’t have one already) via Cloudflare, Route53, or Azure DNS (for Azure users).
- Create two subdomains:
  - `app.yourdomain.com` → Points to a load balancer.
  - `status.yourdomain.com` → Points to a separate status page.

### Infrastructure Setup
- Deploy two VM instances in AWS/Azure running a simple web app (can be an NGINX page with different content on each).
- Deploy a third VM running NGINX as a reverse proxy & load balancer.
- Configure NGINX on the reverse proxy to distribute traffic between the two backend VMs.

### SSL Configuration
- Use Let’s Encrypt or any other SSL mechanism to secure `app.yourdomain.com` with HTTPS.
- Enforce redirect from HTTP to HTTPS.

### Status Page & Health Checks
- Deploy a simple status page (`status.yourdomain.com`) showing:
  - The health of both backend servers (use `curl` or a simple script to check).
  - The current active backend server.

### Bonus Challenge (Optional)
- Make the reverse proxy highly available by deploying it with a floating IP or setting up a second reverse proxy in case of failure.

---

## Expected Outcomes
- Understand how to configure a reverse proxy and load balancer.
- Learn how to implement SSL and secure a website.
- Practice health checks and monitoring.
- Gain exposure to designing a resilient cloud infrastructure.

---

## Bonus: Terraform Implementation
To go ahead of the curve, implement the entire setup using Terraform for infrastructure as code (IaC).
