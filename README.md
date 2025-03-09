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

## Step 1 - Build Pi OS on your SD Card

You need to build your SD Card with Raspberry Pi OS Lite (64-bit).  It's very easy to do, just follow the video instructions.

You need the Raspberry Pi Imager tool, which can be downloaded from: https://www.raspberrypi.com/software/

![Raspberry Pi Imager](https://github.com/gerardobrien/pihackinglab/blob/main/images/rasp-pi-lite-64-bit.png)

*******

## Step 2 - Updates & Cockpit install

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

## Step 3 - Install Docker & Portainer

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

*******

## Step 4 - Portainer Network Changes

Usually when I build a number of containers, I like them to have IP Addresses on my host network.  This way I can access everything on their own individual IP Address.

Following the video instructions, create the two additional networks you need.

Yours will be different but I'm using 10.96.17.0/24 for my lab network, my gateway is 10.96.17.254.  I'm also using this range of addresses for my containers, 10.96.17.128/27.

![Portainer](https://github.com/gerardobrien/pihackinglab/blob/main/images/portainer.png)

*******

## Step 5 - Container Builds

Follow the video steps to build the following containers:

![Portainer](https://github.com/gerardobrien/pihackinglab/blob/main/images/portainer.png)

| Architecture | Container | URL |
| ------------ | ----------- | --- |
| Arm64   | Kali Linux | https://docs.linuxserver.io/images/docker-kali-linux/ |
| Amd64   | Metasploitable2 | https://hub.docker.com/r/ocholoko888/metasploitable2-arm64 |
| Amd64   | Obsidian | https://docs.linuxserver.io/images/docker-obsidian/ |



## Step 6 - TryHackMe & HackTheBox VPN's

Install OpenVPN on the Kali Container

```
sudo apt install openvpn
```

Log into TryHackMe & HackTheBox and download the VPN configiration file.

Then switch directory to the Downloads folder

```
cd Downloads
```

Activate VPN's

```
sudo openvpn NAME-OF-VPN-CONFIG-FILE
```


