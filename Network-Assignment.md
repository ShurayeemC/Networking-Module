# Setup Guide for Hosting NGINX with a Custom Domain

This guide walks through the process of setting up an EC2 instance running NGINX and linking it to a custom domain purchased via Cloudflare or AWS Route53.

---

## 1. Buy a Domain

### Using Cloudflare:
1. Create an account at [Cloudflare](https://www.cloudflare.com).
2. Go to the "Registrar" section to register a domain.

### Using AWS Route53:
1. Log in to the [AWS Management Console](https://aws.amazon.com/).
2. Navigate to Route53 and follow the steps to purchase a domain.

---

## 2. Launch an EC2 Instance

1. Log in to the [AWS Management Console](https://aws.amazon.com/).
2. Navigate to **EC2** under "Compute" and click **Launch Instance**.
3. Configure your instance:
   - **Choose an AMI**: Select a Linux-based AMI (e.g., Amazon Linux 2 or Ubuntu).
   - **Choose an instance type**: Start with "t2.micro" for simplicity.
   - **Instance details**: Ensure the instance has a public IP enabled.
   - **Storage and tags**: Add storage and tags (optional).
   - **Security group**:
     - Allow **HTTP (port 80)** and **SSH (port 22)**.
4. Launch the instance and download the private key file (`.pem`) for SSH access.

---

## 3. Install NGINX

1. SSH into your EC2 instance using the private key:
   ```bash
   ssh -i your-key.pem ec2-user@your-ec2-public-ip
   ```
2. Update the instance and install NGINX:
   
   **For Amazon Linux**:
   ```bash
   sudo yum update -y
   sudo yum install nginx -y
   ```
   
   **For Ubuntu**:
   ```bash
   sudo apt update
   sudo apt install nginx -y
   ```
3. Start and enable NGINX to serve webpages:
   ```bash
   sudo systemctl start nginx
   sudo systemctl enable nginx
   ```
4. Verify NGINX is running by accessing your EC2's public IP in a browser:
   ```
   http://<your-ec2-public-ip>
   ```

---

## 4. Configure DNS on Cloudflare

1. Add your domain to Cloudflare:
   - Go to the "Domains" section and add your purchased domain.
   - Update your domain’s nameservers to the ones provided by Cloudflare.

2. Create an **A Record**:
   - Navigate to the DNS settings in Cloudflare.
   - Add an **A record**:
     - **Name**: Use "nginx" (for `nginx.yourdomain.com`) or leave blank for the root domain.
     - **IPv4 Address**: Enter the public IP of your EC2 instance.
   - Save the record.

3. Wait for DNS propagation (this may take a few minutes to a couple of hours).

---

## 5. Test Your Setup

1. Open your browser and visit your domain:
   - For example: `http://nginx.yourdomain.com`.
2. You should see the default NGINX welcome page.

---

### Troubleshooting
If you cannot access the NGINX page:
- Check your EC2 security group to ensure HTTP (port 80) is allowed.
- Verify that the DNS propagation is complete using tools like [What's My DNS](https://www.whatsmydns.net/).
- Ensure NGINX is running on your EC2 instance:
  ```bash
  sudo systemctl status nginx
