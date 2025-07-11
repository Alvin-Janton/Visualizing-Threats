# Visualizing Threats

## Objective

This project focused on deploying the T-Pot honeypot platform on an AWS EC2 instance to simulate and visualize cyber threats using Kibana. The primary goal was to set up a fully functional honeypot environment that could collect malicious activity data and present it in a readable/viewable format through Kibana dashboards. This setup provides insight into real-world attack patterns and is a valuable learning experience in monitoring, threat detection, and log analysis.

### Skills Learned

- Deploying honeypot environments using the T-Pot framework.
- Visualizing threat data using Kibana.
- Working with containerized services using Docker.
- Managing cloud-based deployments via AWS EC2.
- Troubleshooting common issues with container networking, service dependencies, and authentication.
- Interpreting security logs and recognizing common threat signatures
 

### Tools Used

- T-Pot: Honeypot framework bundling multiple honeypots with centralized logging.
- Docker & Docker Compose: For orchestrating containerized honeypots and services.
- Kibana: To visualize attack logs and trends.
- AWS EC2: Cloud infrastructure used for deployment and testing
- Linux utilities (ss, htpasswd, journalctl, etc.): For diagnostics and configuration

## Steps

Creat an EC2 instance in AWS, name it anything you want. Go to the AMI in the search bar type Debian and select the option shown.
