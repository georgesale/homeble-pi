# pi
 raspberry pi home network



### make the pi and get into it

1. use the Raspberry Pi OS imager to flash your SD card. Choose 'raspberry pi other' and 'raspberry pi os lite'
2. put a blank file called 'ssh' on the SD card (included in this repo, download above)
3. find the IP address of the Pi - you might need to log into the router to find this.
4. Reserve the IP address of the Pi on the router. You'll find this in DHCP settings somewhere. Note this down!
5. ssh into the pi, using username ubuntu and password ubuntu `ssh pi@ipaddress`
6. `sudo raspi-config` then System Options, Change Password. Esc to exit the config pane. `sudo reboot`
7. ssh back in with the new password, to check it works. then `exit`
8. use [Terminus](terminus.com) and set up the connection (IP address, username, password). Then connect in.

### install docker

1. `curl -fsSL https://get.docker.com -o get-docker.sh`
2. `sudo sh get-docker.sh`
3. `sudo usermod -aG docker pi`
4. `sudo reboot` (this will kick you out)

### update the pi (do this monthly)

1. `sudo apt update`
2. `sudo apt upgrade` and 'y' to the prompt if required. This might take 5-10 minutes.
3. `sudo reboot` (this will kick you out)


### install (or update) AdGuard Home

these are taken from the AdGuard Home instructions [here](https://hub.docker.com/r/adguard/adguardhome), and the deploy command from [here](https://smarthomepursuits.com/deploy-adguard-home-docker-in-ubuntu/)

If updating, run steps 1-4. If creating for the first time, do step 1, skip 2 and 3, then do from 4 onwards.
You should update monthly.

1. `sudo docker pull adguard/adguardhome` will pull the new image (it will say if it's pulled a newer version). If a newer version is pulled, follow the rest of these steps. If it isn't, stop here. If first time install, skip next 2 steps.
2. stop the container with `sudo docker stop adguardhome`
3. remove the container with `sudo docker rm adguardhome`
4. create and start the new container `sudo docker run --name adguardhome -v /srv/config/AdguardHome/workdir:/opt/adguardhome/work -v /srv/config/AdguardHome/confdir:/opt/adguardhome/conf --net=host -p 67:67/udp -p 80:80/tcp -p 443:443/tcp -p 853:853/tcp -p 3000:3000/tcp -d --restart unless-stopped adguard/adguardhome`
5. from another machine, browse to the IP of your Pi, with port 3000 at the end. http://ipaddress:3000/
6. run the setup for AdGuard Home, save the username and password somewhere
7. favourite the address in your browser and save password


### install (or update) Home Assistant

If updating, run steps 1-4. If creating for the first time, do step 1, skip 2 and 3, then do from 4 onwards.
You should update monthly.

1. `sudo docker pull homeassistant/home-assistant` will pull the new image (it will say if it's pulled a newer version). If a newer version is pulled, follow the rest of these steps. If it isn't, stop here.
2. `docker stop home-assistant` will stop the container
3. `docker rm home-assistant` will remove the container
4. create and run the new container with `docker run -d --name="home-assistant" --restart unless-stopped -v /srv/homeautomation/hass-config:/config -v /etc/localtime:/etc/localtime:ro --net=host homeassistant/home-assistant`
5. from another machine, browse to the IP of your Pi, with port 3000 at the end. http://ipaddress:8123/
6. run the setup for Home Assistant, save the username and password somewhere
7. favourite the address in your browser and save password


### docker maintenance (do this monthly, after updating the above containers)

`docker image prune` will clean up all unused images and save space


### docker handy commands

`docker container ls` shows all running containers

