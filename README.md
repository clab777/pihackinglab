# A tiny hacking lab!
I needed something small and quiet, easy to move around and travel with... and the Raspberry Pi 5 fits the bill.  This is a walkthrough on how to build your own tiny hacking lab.

Video is here:  https://www.youtube.com/@gerardobrien

### Requirements
- Raspberry Pi 5 (im using 16gb version in the video, but 8gb version should work)
- Raspberry Pi OS Lite 64-bit
- Cockpit
- Docker
- Portainer
- Kali in the browser (container)
- Obsidian (container)
- Metasplotable2 (container)

*******

## Part 1 - Build Pi OS on your SD Card

You need to build your SD Card with Raspberry Pi OS Lite (64-bit).  It's very easy to do, just follow the video instructions.

You need the Raspberry Pi Imager tool, which can be downloaded from: https://www.raspberrypi.com/software/

![Raspberry Pi Imager](https://github.com/gerardobrien/pihackinglab/blob/main/images/rasp-pi-lite-64-bit.png)

*******

## Part 2 - Updates & Cockpit install

SSH to your Pi and run updates

```
sudo apt update
```

Then do the upgrades
```
sudo apt upgrade
```

Then install Cockpit 
```
sudo apt install cockpit
```

Once this is done, test access to Cockpit by accessing it in the browser:

https://YOUR-PI-IP=ADDRESS:9090

Log into Cockpit using the username and password for your Pi.

![Cockpit](https://github.com/gerardobrien/pihackinglab/blob/main/images/cockpit.png)


*******

## Part 3 - Install Docker & Portainer

Install Docker

```
curl -sSL https://get.docker.com | sh
```

Adding local user to the docker group
```
sudo usermod -aG docker $USER
```

Pull the latest Portainer image
```
docker pull portainer/portainer-ce:latest
```

Build the Portainer Container
```
sudo docker run -d -p 9000:9000 --name=portainer_app --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

Once this is done, access Portainer in the browser:

https://YOUR-PI-IP=ADDRESS:9000

![Portainer](https://github.com/gerardobrien/pihackinglab/blob/main/images/portainer.png)







