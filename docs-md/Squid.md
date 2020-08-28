# Squid
## Summary
Squid is a caching and forwarding HTTP web proxy. It has a wide variety of uses, including speeding up a web server by caching repeated requests, caching web, DNS and other computer network lookups for a group of people sharing network resources, and aiding security by filtering traffic.
## Install - Debian
### 1. Update & Install

        sudo apt update 
        sudo apt upgrade -y 
        sudo apt install squid
### 2. Edit config

    sudo vi /etc/squid/squid.conf

    1. Type /http_access and hit enter
    2. Hit 'n' until you find 'http_access allow !Safe_ports' 
    3. Add a line just below that one:

            http_access allow Safe_ports
            
    4. Do the same to search to 'Safe_ports' in vim. This is where you can specify what ports you want to allow traffic through in squid. 

### 3. Restart squid to apply changes

        sudo systemctl restart squid
