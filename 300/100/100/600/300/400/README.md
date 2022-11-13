# 400 - Installing Portainer on MacOS

Portainer is a graphical user interface that allows you to view and manage your Docker containers. It makes it way easier to interact with Docker and I highly recommend that you install it. The best part is, it can actually be installed on Docker itself!

To install Portainer, we need to first create a Docker Compose YAML file. This file contains all the information needed to create and start the container.

I like to keep all my Docker configuration files in my /opt directory on my Ubuntu server, so this is where we will create our Docker Compose file. First, let’s navigate to the /opt directory

```
cd /opt
```

Then we will use the Nano text editor to create a new file called docker-compose.yaml

```
sudo nano docker-compose.yaml
```

Now copy and paste this configuration information into the Nano text editor. If you want more information about what all these keys do, check out the YouTube video I linked at the top of this post. I go through all these items in more details.

You will see that this will map a directory from /opt/portainer on your Ubuntu machine to /data inside the Portainer container. This is great because it means you can recreate your container at any time and all of the configuration data will be safe and sound on your host computer. I make sure that all of my containers have their configuration data stored in its own folder in the /opt directory so I can easily update configurations and take backups.

```
version: '3.0'

services:
  portainer:
    container_name: portainer
    image: portainer/portainer-ce
    restart: always
    ports:
      - "9000:9000/tcp"
    environment:
      - TZ=Europe/London
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - /opt/portainer:/data
```

Now press CTRL + X to exit Nano and Y to save the file. If you do an ls -l on the /opt directory you should now see the file there.

We can now start Docker using the following command. Make sure you are in the /opt directory when you run this command, as it needs to be run from the same place that you keep your docker-compose.yaml file.

```
docker-compose up -d
```

This will bring up the Docker containers that you have specified in the compose file, and the -d will start them in Detached mode which means they will run in the background.

You should now be able to navigate to the IP address of your Ubuntu Server in a web browser on port 9000

```
http://<IPADDRESS>:9000/
```
  
The first time you load Portainer you will be asked to create a username and password. This will only need to be done the first time you load it up.
  
Now select the LOCAL option, so that you can start managing containers locally on your Ubuntu server, and click Connect.

And you should now see Portainer running! You can select Containers in the left hand navigation menu and see your Portainer container running!

You’ve done it! You’ve got Docker, Docker Compose and Portainer running on your Linux server! You have everything you need to get started with Home Assistant and any other Docker containers that you wish to run!
