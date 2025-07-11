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

Creat an EC2 instance in AWS, name it anything you want. Go to the AMI, in the search bar type Debian and select the option shown.
![Kibana Screenshot](https://github.com/Alvin-Janton/Visualizing-Threats/blob/main/images/Screenshot%202025-07-04%20165144.png?raw=true)

Scroll down to instance type, hit the drop down and choose t2.xlarge. Scroll down to key pair and click create pair. Choose a name then click rsa and .pem, the file will donwload to your download folder automatically.
![Kibana Screenshot](https://github.com/Alvin-Janton/Visualizing-Threats/blob/main/images/Screenshot%202025-07-04%20165600.png?raw=true)

Scroll down to configure storage and bump it to 128 from 30. Click launch instance, once instance has started click on it then click connect, click SSH Client, then copy the example ssh command and paste it in your downloads folder into your terminal. If your root directory changes, then you were successful.
![Kibana Screenshot](https://github.com/Alvin-Janton/Visualizing-Threats/blob/main/images/Screenshot%202025-07-04%20184807.png?raw=true)

In your terminal run the following commands. These commands will find and install the latest versions of any dependencies on your instance, and install git.
<pre> bash sudo apt update -y 
 sudo apt upgrade -y 
 sudo apt install git  
</pre>

In your terminal run the following command below. This command will clone the tpot repository and give you access to the resources to launch your honeypots.
<pre>
 git clone https://github.com/telekom-security/tpotce.git
</pre>
