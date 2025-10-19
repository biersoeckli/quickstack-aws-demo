# QuickStack AWS Deployment

## Installation Guide

To deploy QuickStack on AWS, navigate to the EC2 dashboard and launch a new instance using the latest Ubuntu AMI. 
![EC2 Launch Instance](./images/setup_1.png "EC2 Launch Instance")

1) Select an instance type with at least 2 CPU Cores and 4GB of RAM for optimal performance.
![EC2 Instance Type](./images/setup_2.png "EC2 Instance Type")

2) Be sure to configure at least 30 GB of storage to accommodate QuickStack's requirements.
![EC2 Storage Setup](./images/setup_3.png "EC2 Storage Setup")

3) To setup and use QuickStack, make sure the following ports are open in your security group:
- TCP 22 (SSH)
- TCP 80 (HTTP)
- TCP 443 (HTTPS)
- TCP 30000 (QuickStack Web Interface)
![EC2 Security Group Setup](./images/setup_4.png "EC2 Security Group Setup")

4) If not already done, create a key pair to access your instance via SSH.

5) Connect to your instance using SSH.
   1) Use the web-based SSH client in the AWS EC2 dashboard (easy)
   ![EC2 Connect](./images/setup_5.png "EC2 Connect")
   2) Using your terminal or an SSH Client like PuTTY (Windows) or Termius (macOS) to connect to your instance.

Once your EC2 instance is running and you are connected, follow the installation instructions provided in the QuickStack documentation: https://quickstack.dev/docs/getting-started/installation

## Deployment example
After you completed the setup, try to deploy the following example applications:
- https://github.com/biersoeckli/dummy-node-app
  - Requires only an empty App
  - Domain has to point to port 3000 of the dummy-node-app

- https://github.com/biersoeckli/modern-beer-app
  - Requires a Postgres DB instance and an empty App
  - Domain has to point to port 3000 of the modern-beer-app
  - Requires env variable `DATABASE_URL` with the connection string to the Postgres DB
    - **Example:** `DATABASE_URL=postgresql://postgresuser:postgrespassword@hostname:5432/modernbeer`
  - After the first start of the application, you need to initialize the database by accessing the following URL in your browser: `http://<your-domain>/init-db`

To deploy these applications, follow the steps in the QuickStack documentation: https://quickstack.dev/docs/managing-apps/from-git-source

## Adding Domains
To access your deployed applications you need to add domains in QuickStack. To add custom domains to your QuickStack deployment, you have two options:
1. Configure your own Domain so that it points to the public IP of your QuickStack instance.
2. Use a *traefik.me* domain. To use a traefik.me domain, you need to add the prefix with the IP of your QuickStack instance. 
   1. For example: wordpress-*13-60-233-171*.traefik.me if your QuickStack instance has the IP 13.60.233.171 (only works with HTTP, not HTTPS).