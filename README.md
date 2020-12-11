# plexserver
Raspberry Pi Plex Server for Home Sharing Files.


All credit goes to Ash at howchoo, as it was the tutorial I followed along with. I'll include a link and the directions below.

Link: https://howchoo.com/pi/how-to-turn-your-raspberry-pi-into-a-media-server-using-plex

1: Install and update Raspbian

In order to set up our media server, we'll need the latest version of Raspbian installed. Visit our guide here on how to update Raspbian.

How to Update Your Raspberry PiHow to Update Your Raspberry Pi
Make sure your Pi is fresh.

2: Install the HTTPS transport package

We'll need to install the HTTPS transport package for our media server to work. This can be done via command line terminal. For more information on how to log in using a terminal, visit our guide on how to access a Raspberry Pi using SSH.

How to Connect to a Raspberry Pi Remotely via SSHHow to Connect to a Raspberry Pi Remotely via SSH
The preferred (and most common) method of connecting to your Pi to run commands.
Once you've logged into your Raspberry Pi, it's time to initiate the package install. Run the following command to start the process.

sudo apt-get install apt-transport-https

3: Add the dev2day repository

The program we're using to create our media server is called Plex. You can learn more about Plex on the official Plex website. To get our hands on it, we'll need to download the dev2day repository. First up, we'll need to get a key. Run the following command to set it up.

wget -O - https://dev2day.de/pms/dev2day-pms.gpg.key | sudo apt-key add -
Once you have the key, run the following command to add the repository to the list of package sources.

echo "deb https://dev2day.de/pms/ jessie main" | sudo tee /etc/apt/sources.list.d/pms.list

4: Install the Plex server

Now it's time for the meat of our media server sandwich—the Plex server files. To install this component, run the following command.

sudo apt-get install -t jessie plexmediaserver

5: Set the Plex server permissions

In order to use our media server, we need to adjust the permission settings. To do this, we need to modify a line of text from a specific file. Run the following command to open the file.

sudo nano /etc/default/plexmediaserver.prev
Your screen will fill with several lines of text. Scroll through them until you find the following line.

PLEX_MEDIA_SERVER_USER=plex
Replace the word "plex" with "pi". The full string will look like this.

PLEX_MEDIA_SERVER_USER=pi
Press Ctrl + X to close the file. You will be prompted to save the changes, to do so press Y followed by Enter.

Restart the media server using the following command.

sudo service plexmediaserver restart

6: Define a static IP address

To help us reach our new media server, we'll be defining a static IP address. To find your current IP address, run the following command.

hostname -i
To set this IP address as static, add it to the cmdline.txt file. To open this file, run the following command.

sudo nano /boot/cmdline.txt
At the bottom of this file, add an extra line of text for the IP address. It should look like the following, where x.x.x.x represents your desired static IP address.

IP=x.x.x.x
Use Ctrl+X to close the file. You will need to press Y to save the changes and Enter to return to the terminal screen.

Restart your Raspberry Pi.

7: Connect media files to the Raspberry Pi
First, attach your files to the Raspberry Pi. This can be accomplished using things like thumb drives, hard drives, or SD cards.

Once your media is accessible, open a browser window. Enter the static IP address from before. Include the suffix :32400/web/. It should look like the following string:

x.x.x.x:32400/web/

Plex will guide you through setting up for the first time. You'll notice the option to add a library. This tells the Raspberry Pi where our media files are located. Follow the prompts to add your media library.

8: Test the media server

Let's test out our new setup. Your media server should be accessible using Plex from any device on the same network. Just open Plex and look for your Raspberry Pi server in the list.

Congratulations! Your new media server is set up and ready to go.
