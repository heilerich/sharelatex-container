# sharelatex-container
docker container configuration for sharelatex host with nginx proxy and automatic letencrypt https

Intended for use with RancherOS

## Installation
1. Change host settings according to your needs in `cloud-config.yml`
2. Boot RancherOS from ISO
3. Do `ros install -c cloud-config.yml -d /dev/sdX` to install RancherOS
4. Change sharelatex settings in `sharelatex-compose.yml` and put in `/var/lib/rancher/conf`
5. `ros service enable /var/lib/rancher/conf/sharelatex-compose.yml`
6. Put `custom_proxy_settings.conf` in /home/rancher/sharelatex_nginx/conf to increase file upload size
7. `ros service up mongo redis nginx-proxy letsencrypt-nginx-proxy-companion sharelatex`
8. Execute `docker exec sharelatex tlmgr install scheme-full` to install additional latex packages.

You might need to update tlmgr for the last step. Use `docker exec -it sharelatex /bin/bash` to get 
a shell and follow the instructions on the tlmgr homepage to update.

That's it. You should have a fully operational sharelatex instance.
