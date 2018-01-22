Now that my home server setup has been functional decently, I wanted to work on the following things:

- Better Uptime
- Network Storage
- Node Scheduling

This post covers the various options I'm considering and a glimpse of what comes next. Before I move further ahead, here is a small diagram of my current setup:

Things to note:

- *Sydney* is my Digital Ocean droplet that proxies all connections from the world
- over a OpenVPN tunnel
- which forwards ports 80/22/443 to the VPN client's connections

# Better Uptime

I need to improve the uptime guarantees of the services. Most of the downtimes are due to power-cuts, and some due to configuration issues / bugs (I tend to run latest/beta images). Have to tackle from multiple directions:

1. Setup a better power-backup. (In progress)
2. Set restart-policies on the containers. This is already done, but if the server goes down, this gets useless
3. Have a self-healing system that detects downtimes and brings up pods in other servers

For (3), I'm looking at ways in which I can, for eg run some basic containers on the Digital Ocean droplet instead.

# Network Storage

Unfortunately, a lot of my containers are disk-dependent (databases/media). Which means, they can't really run on a remote server, unless it gets the data as well. Kinda tricky to maintain. I'm already running a samba setup, so this might be helpful to look into somewhere down the line. For a start, I'm going to look at purely stateless services.

# Node Scheduling

If I'm looking to run services across 2 different servers, there must be a service that decides where each container runs. I considered Docker Swarm and Kubernetes, but settled on Kubernetes since we use it at work so this becomes a learning exercise.

The primary data store that Kubernetes uses is `etcd`, and I didn't want to run a single node etcd only to fail the same way again. So a better choice I decided was to run a 3-node etcd cluster using:

- My Home Server (Arch Linux)
- The Digital Ocean Droplet (Ubuntu 16.04 LTS)
- Raspberry Pi (Hypriot OS)

I ran out of devices here. Researched a bit, and settled on Hypriot as the base OS for the Raspberry Pi. The obvious problems are:

- How do you even run this across 3 different operating systems?
- With 2 different CPU architectures!
- Running the etcd cluster on the same infra that it is managing

Gonna be a fun challenge. The general plan is to:

- Run etcd 3 node cluster with 1 node on each of the servers.
- I can potentially run multiple nodes on the same server depending on whether I use the VPN interface or not. Likely a better idea to just run it on 2 interfaces, and then register it as 2 separate nodes?

Then comes the kubernetes installation, but that is later