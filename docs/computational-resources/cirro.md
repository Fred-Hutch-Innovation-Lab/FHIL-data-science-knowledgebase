---
title: Cirro
parent: Computational resources
---

# Transferring Instrument Data to Cirro

## Method 1: GUI based transfers

Cirro uses AWS Storage Gateways — devices that enable data transfer from on- premises storage systems to cloud-based storage services — to migrate data from instruments to Cirro.

### Step 1: Connect to the Storage Gateway

The first step in transferring data to Cirro involves establishing a connection to a Storage Gateway. This process mirrors the procedure for connecting to any other network drive.

* **On Windows**:
  * Open File Explorer.
  * Paste the following path into the address bar:
    `\\sgw-4540b72c.fhcrc.org\FHIL`
  * Press Enter on your keyboard.
* **On Mac**:
  * Open Finder.
  * Use Command+K to open the Connect to Server dialog.
  * Paste the following path into the server address field:
    `smb://sgw-4540b72c.fhcrc.org/FHIL/`
  * Click the “Connect” button.
* **On Linux**:
  * Open File Manager.
  * Click Other Locations in the sidebar, then click Connect to Server.
  * Paste the following path into the server address field:
  `smb://fhcrc.org;<USERNAME>@sgw-4540b72c.fhcrc.org/FHIL/`
  * Click the “Connect” button.
  
**Note**: If you are working from an office computer logged in under your own individual account, you should be able to auto-connect using your own credentials.
Members of the _IRC_FHIL_grp security group will have access to this share.

### Step 2: Ensure That a Service Connection Has Been Established

Check the SR Data Tool’s Projects page to make sure that a service connection has been established for the lab or research group you are delivering data to.

If the project is visible on the SR Data Tool’s Projects page, proceed to step 3. 

If the project is not visible on the SR Data Tool’s Projects page:
  * Email `support@cirro.bio` to request service connection setup for the lab or research group.
  * Once you’ve been notified that the service connection is established, proceed to step 3.
    
### Step 3: Create a New Folder for the Dataset

Each new dataset should live in a location that conforms to one of the following folder structures:

`Storage Gateway > FHIL > Lab > Username > Dataset Name`
-or-
`Storage Gateway > FHIL > Lab > Dataset Name`

* On the Storage Gateway, select the folder associated with the requesting user’s lab or research group:
  * *Example*: `\\sgw-4540b72c.fhcrc.org\FHIL\Elz Lab\`
* Optional: Select the folder associated with the requesting user’s Hutch ID or username, or create the folder if it does not yet exist:
  * *Example*: `\\sgw-4540b72c.fhcrc.org\FHIL\Elz Lab\aelz\`
* Within the user’s folder (or within the lab folder if not saving to individual user folders), create a folder for the experiment –
this will be the dataset name:
  * *Example*: `\\sgw-4540b72c.fhcrc.org\FHIL\Elz Lab\aelz\Descriptive Dataset Name\`

**Note**:
Saving data to subfolders labeled by username is optional, but one of the useful features associated with this step is that datasets stored in these subfolders will be tagged with the username. When users log in and look for their data, they can quickly filter for it by using these tags.

### Step 4: Transfer the Raw Data from the Instrument to Cirro

Drag and drop all the instrument data files as a group into the newly created folder on the Storage Gateway.
Use the SR Data Tool’s Datasets page to view the status of the transfer to Cirro. 
Once the data successfully transfers, it will be visible in the Cirro web interface (https://cirro.bio) and available for viewing, download, and analysis.
If a transfer has failed, click on it to view more information or to restart the transfer. 

## Method 2: Command line interface using FH servers

This method takes advantage of FH's high-performance compute resources for faster, more reliable data transfers.

### Step 1: log into FH HPC "rhino"

**On Windows**:
*Todo*
    
**On Mac**:
* Open a terminal
* type `ssh <username>@rhino`, where `<username>` is your Fred Hutch user ID, e.g. `aelz@rhino`
   * You can specify a rhino login node in the form `rhino01`, `rhino02`, or `rhino03` if you are trying to check a screen sesion (see Step 3) 
* Enter your FH password (the terminal may not show that you're typing)

### Step 2: load Cirro module

On the command line, enter `module load cirro`. This will load the most recent version of cirro installed on the server. If you need to find other versions for any reason, you can run `module spider cirro` to see all available versions.

### Step 3 (optional, for large uploads): connect to a screen session

To avoid broken pipes if your computer loses connection to the server, you can open a screen session. This will ensure your command will continue running even if you are not actively logged in.

To do so, run `screen` on the command line. This will give some license info which you can hit space or return to close.

From there, run your commands as normal. If you later need to reconnect to a screen session to check the progress of your upload or resume an interrupted interactive session, you can run `screen -r`. If you have more than one
screen session running, you will be shown a list of active sessions. You can copy the ID of the relevant session and run `screen -r <session_ID>` to connect. Note that you will need to be connected to the same server node that
the screen was originally launched from. If you ran screen/cirro from a login node, you will need to be on the same one (01, 02, or 03). See the login details in Step 1.

To exit the screen session after completing a command, simply enter `exit`.

### Step 4: Run the interactive cirro upload prompt

Have the path to your files of interest ready. Note that file paths on the server may be different than mounted paths on Mac. There will be no 'Volumes' prefix. If your data is stored in the fast drive, the path may look something like
`/fh/fast/_IRC/FHIL/grp/NextSeq_SteamPlant/<Seq_run>`

Run `cirro upload -i` and follow the interactive prompts. The steps should be self explanatory, and you can navagate options with arrow keys and the enter key. Leave the connection open (or use a screen session, see Step 3) and wait
for all uploads to finish. You should see the message `[Cirro CLI] File content validated by MD5` once your uploads are completed.

If this is your first time using the interactive prompts, you will have some additional tasks for first time setup and login. These will be cached for future runs. 
* Specify the fred hutch server `fredhutch.cirro.bio`
* Save your login info
* Select the `MD5 (default)` file validation method
* Copy the URL to your browser
* Login with FH credentials

# Troubleshooting

For more help, email `support@cirro.bio.`
