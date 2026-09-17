# homelab-k3s-thing
This repo contains single cluster k3s homelab configs for Raspberry Pi 5.


## Why it exists
1. Because I want to learn how
2. I want to be able to recreate my server from scratch
3. ~~I hate myself~~

This is "second" iteration of my homelab. Last version was powered by Docker and Portainer. I got tired of fiddling with Portainer's WebUI and wanted to make a challenge for myself. My repository represents my learning experience in DevOps practices and Kubernetes in particular

## Technologies used
1. k3s (lightweight enough to be managed on a single Pi 5 node, yet similar enough to usual k8s)
2. ArgoCD (Declarative GitOps tool for continuous delivery)
3. MetalLB (Unlike ServiceLB, provides actual VIP for load balancing)
4. Traefik (Uses less resources than nginx which is handy for Pi 5's limited memory)
5. PiHole (DNS sinkhole with adblocking capabilities, also used for local DNS records)
6. Ansible (IaC suite that I currently use for quick setup of my server)

## What was done already
1. Every app is configured with values.yaml (if helmchart exists for it), any and all updates are managed with git as truth source and ArgoCD
2. Simple and janky ansible playbook to create initial configs for server (installing k3s, mounting external HDD)
3. Server structure is managed by "app of apps" used by ArgoCD to synchronize apps
4. Any and all passwords are either required on first login or handled by sealed-secrets
5. App ingress is managed by traefik and PiHole local DNS records

## What neends to be done
1. Reworking Ansible playbook to more uniform structure.
1. 1. Currently it requires SSH password every time and using SSH key would be much safer and more convenient.
1. 2. My  external HDD had media in it already so I didn't bother to create appropriate media folders (Series, Movies, etc.). This needs to be done for reproducability.
2. Adding more infrastructure. This provides more functionality for the server and great learning experience for me.
2. 1. Graphana + Prometheus for monitoring server load, pod health, metrics, etc.
2. 2. Cloudflare Tunnel for zero trust access to my services from anywhere. As of now, it's all local. My Docker config included Wireguard tunnel, however, this option gets less and less reliable in terms of accessibility. 
3. Adding qbittorrent to get any new media to my server. Currently, I rely on media that is already on my HDD.
4. Adding more nodes to my cluster when I'm ready to move on
