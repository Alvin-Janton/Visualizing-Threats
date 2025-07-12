# Troubleshooting Guide for Visualizing Threats

## 1. T-Pot Web Interface Not Loading

### ✅ Check EC2 Security Group
- Ensure ports `64295` (SSH) and `64297` (Kibana) are open to your IP.
- Review inbound rules in the Security Group settings.

### ✅ Check Public IPv4 and URL Format
- Use the public IP from EC2 with `:64297` appended. Example:  
  `https://your-public-ip:64297`

### ✅ Bypass SSL Warning
- On browser warning page, click **Advanced** → **Proceed to site**.

### ✅ Check docker containers
- Docker containers like Kibana, ElasticSearch, and nginx may have failed to deploy.
 Run the command below to see what docker containers are running, look for any failed, or starting.
<pre>
  sudo docker ps -a
</pre>

If you see any failed or starting containers run
<pre>
  sudo docker logs <container-name>
</pre>

If you get an error, or get no output the container likely hasn't started, run the command below to start the container
<pre>
  sudo docker restart <container-name> 
    or
  Sudo docker-compose -d <container-name>
</pre>

If containers aren't launching as expected, check for configuration issues. This will validate your YAML config and highlight formatting or reference issues.
<pre>
  sudo docker-compose config
</pre>

Once you verify that ElasticSearch, Kibana, and nginx are working run the command below to make sure there are no port conflicts on port 25
<pre>
  sudo ss -tuln | grep :<25>
</pre>

If you see anything except what is shown in the image below, shut the application down, and restart docker.
![Kibana Screenshot](https://github.com/Alvin-Janton/Visualizing-Threats/blob/main/images/Screenshot%202025-07-12%20155452.png?raw=true)

Run the following commands to restart all docker containers
<pre>
  sudo docker-compose down
  sudo docker-compose up
</pre>



If everything is working, then run this command in your terminal to see if nginx is listening on port 64297
<pre>
  sudo ss -tuln | grep :64297
</pre>

If you see the output below then nginx is up and working and you can go to your EC2 public IPv4 address.
![Kibana Screenshot](https://github.com/Alvin-Janton/Visualizing-Threats/blob/main/images/Screenshot%202025-07-12%20155414.png?raw=true)

## 2. Can't Log In to Kibana

### ✅ Use Incognito mode
- Sometimes session cookies cause looping, use an incognito tab to refresh.

### ✅ Ensure NGINX Password File Exists & Is Mapped
Run the following command in your terminal
<pre>
  sudo ls -l /opt/tpot/nginx/conf/nginxpasswd
</pre>

If the file does not exist, recreate it using the following command. This will prompt you to enter and confirm a password.
<pre>
  sudo htpasswd -c /opt/tpot/nginx/conf/nginxpasswd <yourUsername>
</pre>

### ✅ Confirm Docker Volume Mapping
Check that your docker-compose.yml file includes this line under the NGINX service.
<pre>
  - /opt/tpot/nginx/conf/nginxpasswd:/etc/nginx/nginxpasswd:ro
</pre>

If you're unsure how to check you docker-compose.yml, run the following command
<pre>
  cat docker-compose.yml
</pre>

### ✅ Ensure NGINX Configuration Uses the Right Password File
Log into the container, to leave just type exit into the terminal.
<pre>
  sudo docker exec -it nginx /bin/sh
</pre>

Use the following command
<pre>
  grep auth_basic_user_file /etc/nginx/conf.d/*.conf
</pre>

Look for the string of text below, if it's missing or misconfigured then you won't be able to login.
<pre>
  auth_basic_user_file /etc/nginx/nginxpasswd
</pre>

### ✅Check Logs for Errors
Inspect the NGINX logs
<pre>
  sudo docker logs nginx
</pre>
Look for errors like "No such file or directory", "Permission denied", or "Invalid user"

If everything is working correctly restart nginx and try to login.

### 3. If all else fails
If nothing you've done so far works, try pasting this prompt into an AI
<pre>
  I'm working on a cybersecurity project where I deployed T-Pot (a multi-honeypot platform) on an AWS EC2 instance running Debian. I followed a guide that involved cloning the tpotce repo, installing with ./install.sh -s -t h -u <username> -p <password>, and accessing Kibana via port 64297. I'm trying to troubleshoot an issue but not sure how to proceed.

Here's what's going wrong:

[Briefly describe your current issue — e.g., “Kibana is stuck in a login loop,” “NGINX won’t start,” “port conflict preventing access,” “I can’t find the nginxpasswd file,” etc.]

Additional context:

I’ve already [list any commands you've run or changes you've made].

I’m using Docker and Docker Compose as part of the T-Pot setup.

Can you walk me through what might be causing this and how to fix it?
</pre>
Fill in the blanks and make sure to do every step before querying the AI again.
