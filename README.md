# synology-nginx-proxy-manager-compose-file
docker-compose file for synology npm

Synology Nginx proxy manager docker compose file (tested on Synology DSM 7.2)
based on excellent post from https://www.wundertech.net/nginx-proxy-manager-synology-nas-setup-instructions/

1. if you want to use npm (nginx proxy manager), you need to forward ports on your router:
- router port 80 goes to synology lan ip and port 8085
- router port 443     -->              4443 

2. your router must be able to ping docker ip ranges
- docker ip ranges are usually : 172.1x.xxx.xxx
in this compose file, I use 3 networks : 172.17.0.0/24 for mariadb sql, 192.168.1.198 for npm host in macvlan network,  and 192.168.10.0/24 for npm bridge
- if your router does not ping your synology docker networks, you can use ip routes as below
 fyi my router is on LAN IP: 192.168.1.1
- target: the docker network you want to route
- gateway: your synology local IP address
 IP routes to add:
 e.g.   target              Gateway          metric    table
      172.17.0.0/16      192.168.1.xx          0        main
      172.18.0.0/16      192.168.1.xx          0        main
      172.19.0.0/16      192.168.1.xx          0        main
      192.168.10.0/16    192.168.1.xx          0        main

3. npm usage: you can add a proxy host : e.g. test.yourdomain.com which forwards to destination on lan docker network : 172.17.0.1 
   (172.17.0.1 is the gateway for the docker subnet 172.17.0.0/16) and port: xxxx (the port you choosed to expose from your docker component) 



