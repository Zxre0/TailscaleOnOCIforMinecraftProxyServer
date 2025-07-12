# TailscaleOnOCIforMinecraftProxyServer for Ubuntu
How to use Tailscale as a Proxy Server on OCI (Oracle Cloud Infrastructure) for Minecraft 

For this tutorial, I'm assuming you already have a self-hosted Minecraft server set up

Used for Self-Hosted Community servers that you don't wanna hand your IP address out

# Setup Oracle Cloud Server
1. [Go to Oracle's Cloud Infrastructure website](https://www.oracle.com/cloud/)
   and create an account
2. Go over to Instances and create one
3. AMD 1 core 1 gb of ram worked fine for this (if you can get a ampere based thats even better because you can host ur entire server on it)
4. MAKE SURE IT SAYS ALWAYS FREE ELIGIBLE SO ITS FREE TO HOST
5. MAKE SURE TO CHOOSE UBUNTU 22.04 AS THE IMAGE 

 # SSH
   [How to SSH](https://docs.oracle.com/en/cloud/cloud-at-customer/occ-get-started/log-vm-using-ssh.html)

 # Port Forwarding
   On the VM you just made, click on the instance, scroll down and click on the VCN

   <img width="2490" height="1071" alt="image" src="https://github.com/user-attachments/assets/26db0b49-6e3c-4925-b48e-d289ce984b8f" />

   Then go over to the security tab and make an 3 ingress rule
   

   port fowarding using these ports and options (the voice chat port is optional it's if you are using voice chat)

   
   <img width="2052" height="176" alt="image" src="https://github.com/user-attachments/assets/91fc52b5-e24f-42f5-bde2-028e33f29a28" />

   
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

   Once it shows up in machines, click "disable key expiry"

   <img width="1804" height="581" alt="image" src="https://github.com/user-attachments/assets/964635d1-6668-4607-aee8-bd97a0d4444c" />



   while you are still on the dashboard click the 3 dots again and click "edit route settings"
   
   <img width="1772" height="643" alt="image" src="https://github.com/user-attachments/assets/f33fbde7-4b28-451b-96fd-3d5cc6a12e8c" />

   click "use as exit node"

   <img width="623" height="587" alt="image" src="https://github.com/user-attachments/assets/739254ba-39a1-41ad-b70e-d931716f3c7d" />

   
   # IP Forwarding
   Do sudo nano /etc/sysctl.conf and it will bring up sysctl.conf in a text editor and uncomment (remove the #) from "net.ipv4.ip_forward=1"

   <img width="2539" height="1351" alt="image" src="https://github.com/user-attachments/assets/32c9aa3d-87fb-40ca-9c97-134630e259c1" />


   now run tailscale status and their should be no more warning about exit nodes
   
  # Accept Routes
      sudo tailscale up --accept-routes --advertise-exit-node
   run this command if you get a error about accept routes


   ### MAKE SURE TO RESTART THE VM AFTER ALL OF THIS
      




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


 # Minecraft Setup

   ### YOU CAN SKIP THIS STEP IF YOU WANT PEOPLE TO DOWNLOAD TAILSCALE TO JOIN

   Instead of using Nginx or Velocity we are going to use iptables which comes with linux

   first connect to your own vpn then run tailscale ip -4 write that ip down somewhere 

   after that run this command on your server
   
      sudo iptables -t nat -A PREROUTING -p tcp --dport 25565 -j DNAT --to-destination YOUR_TAILSCALE_LOCAL_PC_IP_ADDRESS:25565
      sudo iptables -t nat -A POSTROUTING -p tcp -d YOUR_TAILSCALE_LOCAL_PC_IP_ADDRESS --dport 25565 -j MASQUERADE

   now people that dont have the vpn installed can now play on your minecraft server

   # Voice Chat (Plasmo Voice,Simple Voice Chat)

   Coming Soon

