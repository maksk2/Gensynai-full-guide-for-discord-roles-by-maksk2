# Gensynai-full-guide-for-discord-roles-by-maksk2
We'll figure out how to get the roles of "the swarm" and "blockassist"


# Vast.ai 
Open the command prompt (CMD) and enter the following command:
```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com "
```
Press Enter several times, leaving the default path and password until a message about the successful creation of the key appears.

<img width="1139" height="644" alt="image" src="https://github.com/user-attachments/assets/4dcf511d-ede6-487e-b95b-be4e55243d03" />

After generating the keys, pay attention to the path indicated in the output — the key pair was saved there.

Follow this path and you will see two files.:

- id_rsa — private key (we don't show it to anyone)
- id_rsa.pub — public key

Open the id_rsa.pub file using Notepad, copy the entire text — it will be useful for you to add the key to the server.

<img width="978" height="617" alt="image" src="https://github.com/user-attachments/assets/f6fafa9c-79fa-4092-aa59-f212aa8dafb8" />

register using the link https://cloud.vast.ai

Go to the SSH Keys tab on the platform and click +New 

We paste the previously copied public key from the id_rsa.pub file there and save it.

<img width="1910" height="765" alt="image" src="https://github.com/user-attachments/assets/907cd40f-b96e-44cb-9933-21f5dd205771" />
<img width="1919" height="798" alt="image" src="https://github.com/user-attachments/assets/646638fc-078f-49c9-a782-da28702d71a2" />
Go to the machine search tab and click RENT next to the appropriate server. we need a server with cuda 12.8 and higher
<img width="1722" height="736" alt="image" src="https://github.com/user-attachments/assets/741e8159-71b4-4980-ae86-3dd0045a8b28" />

Next, go to the Instances tab — your rented server will be displayed here. We are waiting for the installation to complete — it usually takes a few minutes.
<img width="1225" height="528" alt="image" src="https://github.com/user-attachments/assets/f7747b1b-8645-4592-a683-e59a08734623" />
<img width="1147" height="456" alt="image" src="https://github.com/user-attachments/assets/a7c39865-38aa-4e4b-a2e4-754384c78a3c" />
<img width="1255" height="696" alt="image" src="https://github.com/user-attachments/assets/7302c29a-d048-479d-a170-25eb22f72e18" />

Go to MobaXterm, create a new SSH session. Enter the IP, port, and username. https://mobaxterm.mobatek.net/

At the bottom, turn on the Use private key option, follow the path where the second file from the key pair is located — id_rsa, specify it as the private key for connection and click ok.

<img width="929" height="631" alt="image" src="https://github.com/user-attachments/assets/88c2032d-bee3-4d01-9588-8a677c2fad10" />
<img width="957" height="547" alt="image" src="https://github.com/user-attachments/assets/c409206b-0d48-46c3-a920-12c7b2987ff6" />
After that, you successfully connect to the server, and the remote access console opens.
<img width="1609" height="884" alt="image" src="https://github.com/user-attachments/assets/827eb476-1052-41b9-8660-c7a5968aaedb" />


# Gensyn RL-Swarm Node  (Linux VPS)
Installation of all necessary components:
```bash
#  System update
sudo apt update && sudo apt upgrade -y && \
sudo apt purge -y nodejs npm libnode* nodejs-doc && \
sudo rm -rf /usr/{lib,local/lib}/node_modules /usr/{bin,local/bin}/{node,npm} && \
sudo apt clean && sudo apt update && \
sudo apt install -y curl wget git build-essential python3 python3-pip python3-venv python3.10-dev screen && \
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash - && \
sudo apt install -y nodejs && \
sudo npm install -g yarn@1.22.22 esbuild next && \
pip install --upgrade jinja2 && \
node -v && npm -v && yarn -v
rade jinja2```


# IF YOU HAVE A GPU!!!

# Installing CUDA Toolkit 12.4
wget https://developer.download.nvidia.com/compute/cuda/12.4.1/local_installers/cuda-repo-ubuntu2204-12-4-local_12.4.1-550.54.15-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2204-12-4-local_12.4.1-550.54.15-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2204-12-4-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt update
sudo apt install -y cuda-toolkit-12-4

# Exporting CUDA environment variables
echo 'export CUDA_HOME=/usr/local/cuda' >> ~/.bashrc
echo 'export PATH=$CUDA_HOME/bin:$PATH' >> ~/.bashrc
echo 'export LD_LIBRARY_PATH=$CUDA_HOME/lib64:$LD_LIBRARY_PATH' >> ~/.bashrc
source ~/.bashrc
```

# Downloading the node:

```bash
git clone https://github.com/VaniaHilkovets/GensynFix.git && cd GensynFix && chmod +x run_rl_swarm.sh
```

# Launching in screen:
```bash
screen -S gensyn

./run_rl_swarm.sh
```
<img width="1621" height="740" alt="image" src="https://github.com/user-attachments/assets/cfa11a34-b638-4d48-a222-651532da5661" />

# Open a new terminal tab without closing the old one:
```bash
ssh -o StrictHostKeyChecking=no -R 80:localhost:3000 nokey@localhost.run
```
<img width="1080" height="248" alt="image" src="https://github.com/user-attachments/assets/f7461317-2fb9-4049-8215-1135af6ae348" />

Log in via Google/Email

<img width="1076" height="769" alt="image" src="https://github.com/user-attachments/assets/cea834a0-622c-434f-96a4-86dec7cfc3ed" />

After successful login, we return to the SSH terminal.
 When will the question appear:

 Would you like to push models you train in the RL swarm to the Hugging Face Hub? [y/N]

— answer N and press Enter.

After that, the installation and testing of the node will automatically continue.
 Information will appear in the console, including the name of your node (highlighted in green).

 <img width="1503" height="945" alt="image" src="https://github.com/user-attachments/assets/a03ddfaf-a917-41dc-a736-353de2f61e20" />

 # After completion, you will be able to find your node in the shared dashboard at:
  https://dashboard.gensyn.ai/ 

Exit screen (RL-Swarm remains in the background):
```bash
Ctrl + A, then D
```
Log in to screen again:
```bash
screen -r gensyn
```
# mistakes:
<img width="490" height="198" alt="image" src="https://github.com/user-attachments/assets/1f295f3e-8ac7-431c-8350-927275ba7013" />

Decision:
```bash
ln -s /usr/bin/python3 /usr/bin/python
```
<img width="1049" height="810" alt="image" src="https://github.com/user-attachments/assets/9ba32668-d138-4c85-8dea-0e1bb7bf6f74" />

Decision:
```bash
pip install -U trl
```

# You can now take on the role of THE SWARM in Discord.
To get it, follow these steps:

1. Go to Telegram to @BotFather, create any bot and save its token.
2. Go to https://dashboard.gensyn.ai /, log in via email and save the account address (it will be on the top right).
3. Go to Telegram to @myidbot and find out your ID.
4. Go to Discord in the #swarm-link channel, enter the /link-telegram command and copy the generated command with the code.
5. On any server, run the command:
   
```bash
wget -O tg_role.sh https://raw.githubusercontent.com/VaniaHilkovets/GensynFix/main/tg_role.sh && chmod +x tg_role.sh && ./tg_role.sh
```

6. Wait for the installation and enter the requested data one at a time (bot token, address from dashboard, your ID).
7. Go to your created bot, click /start and paste the command with the code from Discord.

<img width="357" height="81" alt="image" src="https://github.com/user-attachments/assets/5b045b47-dca1-487c-beed-6a45a993bfe7" />

# Getting the blockassist role
go to the website https://octa.space?ref=r0Leqpsrmfp and we replenish the balance by 1 dollar

<img width="1772" height="943" alt="image" src="https://github.com/user-attachments/assets/bbdfb9d5-50d8-4da0-af01-590cf165e028" />
we search for gensyn in the search and select "Gensyn AI Block Assist"

<img width="1628" height="742" alt="image" src="https://github.com/user-attachments/assets/97d249a1-c96a-4bfe-883c-68216629df80" />

Look for nodes with min 16GB of RAM and 6+ core CPU. Most modern GPU's are supported ranging from RTX 3060, Ada4000, RTX 4070, RTX 5070 etc.


IMPORTANT: Look for nodes which have CUDA 12.8 and newer installed. Use the filter on the left hand side.

<img width="800" height="438" alt="image" src="https://github.com/user-attachments/assets/a3f29436-1c3c-44a6-9d94-28b5ac0c5bde" />

Select a suitable node and click "Configure" in the top right hand corner.

<img width="800" height="613" alt="image" src="https://github.com/user-attachments/assets/2e478f6c-2e48-4d51-8318-1f096f60a24c" />

we register on the website https://huggingface.co and go to settings

<img width="1899" height="849" alt="image" src="https://github.com/user-attachments/assets/7b8b3cba-c495-4f1b-b775-a0a1a17c9ff5" />

select acces token and click create a new token

<img width="1920" height="862" alt="image" src="https://github.com/user-attachments/assets/16be1d31-f2eb-411b-a643-0d5495f52289" />

On the configuration page, paste your HuggingFace token in the HF_TOKEN field and leave the remaining settings to default.

<img width="800" height="563" alt="image" src="https://github.com/user-attachments/assets/0b7e6e22-4b10-4326-a62c-ae49e73fb597" />

Click the "Deploy" button in the top right hand corner.

Initially you will see this status.

<img width="800" height="142" alt="image" src="https://github.com/user-attachments/assets/ea8eedc1-0a9a-4375-927b-0d7f5ac709aa" />

Wait until it changes to "Service configured"

<img width="800" height="110" alt="image" src="https://github.com/user-attachments/assets/6e54abf7-0112-484d-b33d-82289f9488b0" />

Then click on the session. This will show a pop-up. Click on the link under "HTTP Services"

<img width="800" height="261" alt="image" src="https://github.com/user-attachments/assets/63360964-c42b-43b1-8b0f-597290221c16" />

You will be presented with a desktop. There you will see a "Gensyn AI Block Assist" icon. Double click to load it.

<img width="800" height="408" alt="image" src="https://github.com/user-attachments/assets/0fb4b328-1bef-40fe-bf55-4dc27ec8c9b1" />

This will load up a console window, wait until it loads a Gensyn login window.

<img width="800" height="493" alt="image" src="https://github.com/user-attachments/assets/844c4d49-e0e0-48d9-9bb6-8726eb27da73" />

After the process is completed you will need to sign-in to the Gensyn Testnet:

<img width="800" height="450" alt="image" src="https://github.com/user-attachments/assets/ee59f7c8-951c-44f5-9644-67dcaadf56c3" />

After you've signed in, Minecraft will load.

Be patient, it can take up to 5 minutes for Minecraft to load.

<img width="800" height="474" alt="image" src="https://github.com/user-attachments/assets/5afdfd46-2037-483f-abc5-d0d56776292b" />

Once Minecraft has loaded, in the terminal, press the ENTER key to load up AI.
After playing the game you have to go back to the terminal and press enter 2-3 times.
Finally, when you start a new game for the interaction to be fully immersive and work, you will need to enter full screen.
To do that, hover over the small gray semicircle and click on it to expand the main panel.

<img width="800" height="474" alt="image" src="https://github.com/user-attachments/assets/4db112f3-a767-4ca3-b3c4-2645ab5ae588" />

Click this icon to enter full screen

<img width="800" height="433" alt="image" src="https://github.com/user-attachments/assets/3f952038-3791-4f16-9717-99b9f5016a7f" />

# taking over the Block role
in the Swarm branch in the discord, we write 
```bash
/block-verify
```
<img width="285" height="79" alt="image" src="https://github.com/user-attachments/assets/2f0324ff-9611-4a23-9cda-c809f289692c" />

We will need to fill in 2 fields

<img width="473" height="410" alt="image" src="https://github.com/user-attachments/assets/4481fd6e-c378-4e3f-b45f-54486a1a96ce" />

• 1 these are the records of our model, you can find it in our profile 

<img width="1901" height="854" alt="image" src="https://github.com/user-attachments/assets/dac3957b-db33-4b55-b92a-6eda239aa2e4" />
<img width="1283" height="47" alt="image" src="https://github.com/user-attachments/assets/882b063a-1375-4ed6-b6d2-0090f24e5b74" />


• 2 this is our unique Hugging face token, we insert it

Congratulations, you got these roles.

<img width="324" height="88" alt="image" src="https://github.com/user-attachments/assets/e51d9144-c48f-4c57-b14f-17b2ea7705e1" />







































