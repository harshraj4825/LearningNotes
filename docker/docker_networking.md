# Docker Networking
Docker networking allows containers to communicate with each other and with external systems. The key concepts include:

###### Types of Networks in Docker
| Network Type    | Description |
|---------|-----|
| bridge (default)   | Creates an isolated network where containers can communicate. Best for single-host setups.  |
| host     | Shares the host's network namespace (no isolation). Used when you need performance.  |
| none | No networking (fully isolated container).  |
| overlay | Used in Swarm mode for multi-host container communication.  |
| macvlan | Assigns a MAC address to the container, allowing it to appear as a physical device.  |

### Bridge Networking (Default)
By default, containers in a bridge network can communicate using container names.  
Create a Network  
`docker network create my_bridge`  
Run Containers in the Custom Network  
`docker run -dit --name container1 --network my_bridge alpine sh`  
`docker run -dit --name container2 --network my_bridge alpine sh`  
Test Communication  
`docker exec -it container1 ping container2`  
Since both are in the same network, they can resolve names automatically.  
### Host Networking (Direct Access)  
This makes the container use the host’s IP stack, meaning there is no network isolation.  
`docker run --rm --network host nginx`  
 ### Connecting Multiple Containers (Docker Compose)
 If you have a multi-container setup (e.g., database + app), use Docker Compose.  
 Example  `docker-compose.yml`  
```yaml
version: "3"
services:
  app:
    image: nginx
    networks:
      - my_network
  db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: root
    networks:
      - my_network

networks:
  my_network:
    driver: bridge
```
### Overlay Network (Multi-Host Communication) 
If you're running Docker Swarm, you can create an overlay network:
`docker network create -d overlay my_overlay`  
Deploy services that can communicate across different nodes in the Swarm.  

### Macvlan Networking (Assign Real IPs)
This lets a container act like a real device on the LAN:  
`docker network create -d macvlan --subnet=192.168.1.0/24 --gateway=192.168.1.1 -o parent=eth0 my_macvlan`  
`docker run --rm --network my_macvlan alpine ip a`  

###### Debugging Networking Issues
Check Available Networks  
    `docker network ls`  
Inspect a Network  
    `docker network inspect bridge`  
Check active connections  
`docker exec -it container1 netstat -tulnp`  
Test DNS resolution inside a container  
`docker exec -it container1 nslookup google.com`  
