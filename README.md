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

### install pihole

1. `curl -sSL https://install.pi-hole.net | bash` and follow the instructions

### update the pi and pihole app (do this monthly)

1. `sudo apt update`
2. `sudo apt upgrade` and 'y' to the prompt if required. This might take 5-10 minutes.
3. `pihole -up` 
3. `sudo reboot` (this will kick you out) 