# TailscaleOnOCIforMinecraftProxyServer for Ubuntu
How to use Tailscale as a Proxy Server on OCI (Oracle Cloud Infrastructure) for Minecraft 

For this tutorial, I'm assuming you already have a self-hosted Minecraft server set up

Used for Self-Hosted Community servers that you don't wanna hand your IP address out

# Setup Oracle Cloud Server
1. [Go to Oracle's Cloud Infrastructure website](https://www.oracle.com/cloud/)
   and create an account
2. Go over to Instances and create one
3. AMD 1 core 1 gb of ram worked fine for this
4. MAKE SURE TO CHOOSE UBUNTU 22.04 AS THE IMAGE 

   # SSH
     [How to SSH](https://docs.oracle.com/en/cloud/cloud-at-customer/occ-get-started/log-vm-using-ssh.html)

# Setting up Tailscale 
  Go to [Tailscale's Website](https://tailscale.com/) and create an account

  # Tailscale Server Install 
  
   When you get to Tailscale's Quick Install, Skip the instructions
   <img width="936" height="747" alt="image" src="https://github.com/user-attachments/assets/1c2ecc0d-60ea-4d20-91a6-f504e214b609" />


  Click add device and add a linux server

  
   <img width="458" height="254" alt="image" src="https://github.com/user-attachments/assets/1f4c6d3d-7a91-4fc0-b3da-9d70a6988c8f" />



   Make sure the setting look like this and click generate install script
   <img width="650" height="1051" alt="image" src="https://github.com/user-attachments/assets/82cd555e-4173-4f17-ad11-a22e51ad34a4" />


  Once you get the generated install script, throw that into your linux terminal and let it install

  # Tailscale Local PC install
   [Install Tailscale on your local PC](https://tailscale.com/download) and login

   Once installed go to CMD and ping the name of your VM

   ex. ping oracle-proxy

   On your taskbar right-click on Tailscale

   
   <img width="483" height="317" alt="image" src="https://github.com/user-attachments/assets/d171587d-d91f-4522-9828-f2b4633951c3" />

   Go click on Exit Nodes and connect to your server

   <img width="495" height="193" alt="image" src="https://github.com/user-attachments/assets/574afc01-0867-4d4b-8850-f07b996f8883" />

   After connecting, go ping any server you want

   ex. ping 1.1.1.1

   WOOO GODO JOB IF EVERYTHING WENT WELL YOU NOW HAVE YOUR OWN VPN


