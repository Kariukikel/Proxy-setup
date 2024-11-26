# Proxy-setup
#!/bin/bash

# Update and install dependencies
sudo apt update && sudo apt upgrade -y
sudo apt install -y squid

# Backup original config
sudo cp /etc/squid/squid.conf /etc/squid/squid.conf.bak

# Configure Squid for basic proxy usage
echo "
http_port 3128
acl allowed_ips src 0.0.0.0/0
http_access allow allowed_ips
" | sudo tee /etc/squid/squid.conf

# Restart Squid
sudo systemctl restart squid

echo "Squid proxy installed and running on port 3128"
