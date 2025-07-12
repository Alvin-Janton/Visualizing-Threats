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
- Docker containers like Kibana, ElasticSearch, and nginx may have failed to deply.
- Run the command below to see what docker containers are running, look for any failed, or starting.
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
  Sudo docker-compse -d <container-name>
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


## 2. Can't Log In to Kibana

### ✅ Recheck Install Command
- Confirm correct username/password were passed in the install command:
```bash
./install.sh -s -t h -u yourUsername -p yourPassword

