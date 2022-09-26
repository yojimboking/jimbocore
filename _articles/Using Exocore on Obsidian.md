---
published: true
topic: Computers
subtitle:
date: 2021-01-27
tags: exocore remilia computers web
---

# Using Exocore on Obsidian
Obsidian can be used as an alternative to VSCode Foam for managing your exocore, with live syncing to Github for automated publishing. 

It also has a powerful mobile application that can be used if you keep your Exocore synced on a cloud drive such as Google Drive or iCloud (on iOS).

If you're setting up your exocore for the first, first follow [[Exocore Installation Instructions|steps 1 and 2 here]] and then come back.

## 1. Clone your repo and set to ssh
First, download [Github Desktop](https://desktop.github.com/) if you don't already have it.

Open the program and follow the instructions to sign in to your Github account then click `Current Repository` at the top left, then `Add > Clone Repository...`

Now enter `git@github.com:yourusername/reponame.git` replacing your github username and repo name, e.g. `git@github.com:remiliacorp/exocore.git`, and where you want to store your exocore (if you want to edit on mobile this will need to be on a cloud drive like iCloud, see [[Using Exocore on Obsidian#4 Optional Sync with Mobile|Step 4: Sync with Mobile]])

![[Screen Shot 2022-09-19 at 7.06.31 PM.png]]

### Change repo to ssh
If you've already cloned your repo before, you'll need to make sure it's set to ssh, not https.

Navigate to the repo on Github Desktop, then click `Repository > Repository Settings` in the menu bar. 

If the `Primary remote repository (origin)` begins with `git@github.com:` you're on ssh already and don't need to do anything. If it begins with `https://github.com/` simply replace that excerpt with `git@github.com:`.

eg `https://github.com/remiliacorp/exocore.git` becomes `git@github.com:remiliacorp/exocore.git`
![[Screen Shot 2022-09-19 at 7.04.29 PM.png]]

## 2. Setup SSH with Github
If you don't already have an SSH Key, you'll need to make one to add to Github. If you do move directly to [[Using Exocore on Obsidian#2c Add SSH Public Key to your Github|Step 2c]]. If you're not sure, you can run `ls -al ~/.ssh` in Terminal to check, if you see `id_rsa` and `id_rsa.pub` you can continue to [[Using Exocore on Obsidian#2c Add SSH Public Key to your Github|Step 2c]].

### 2a. Generate SSH Key

1. Open Terminal on OSX or Linux ([Git Bash](https://gitforwindows.org/) on Windows).

2. Paste the text below, substituting in your GitHub email address:
`ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

This creates a new SSH key, using the provided email as a label.   
 `> Generating public/private algorithm key pair.`

3. When you're prompted to "Enter a file in which to save the key," press Enter. This accepts the default file location.
`Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]`

4. At the prompt, type a password that you'll remember. 

`Enter passphrase (empty for no passphrase): [Type a passphrase]`
`Enter same passphrase again: [Type passphrase again]` 

### 2b. Add SSH Private Key to the ssh-agent

1. Ensure the ssh-agent is running.
`$ eval "$(ssh-agent -s)
`Agent pid 59566`

2. Add your SSH private key to the ssh-agent.
`ssh-add ~/.ssh/id_rsa`

### 2c. Add SSH Public Key to your Github

1. Copy your SSH public key to your clipboard.

`pbcopy < ~/.ssh/id_rsa.pub`

2. Login on Github and click your profile photo, then click **Settings**.
![[Pasted image 20220905145243.png]]

3.  In the "Access" section of the sidebar, click  **SSH and GPG keys**.
4. Click **New SSH key** or **Add SSH key**.
![[Pasted image 20220905145302.png]]

5. Give it a Title. Under Key type select: Authentication.
6. Past the key into the "Key" field and click add ssh key
![[Pasted image 20220905145417.png]]


## 3. Install and Setup Obsidian

[Download Obisidian](https://obsidian.md/) on your PC.

Select Open a Folder as a Vault and select where you saved your exocore. Click `Trust authors and enable plugins`. 

By default, changes are saved 10 minutes after no files have been edited to prevent publishing while you're making corrections.

You can adjust this setting by clicking the gear icon in the bottom right, then scrolling down to the bottom of the sidebar and selecting `Obsidian Git`:

- `Vault backup interval (minutes)` - how frequently you want to changes to be saved automatically. Set to 10 minutes by default

Also relevant if you plan to be editing on mobile is  `Auto pull interval (minutes)`, how frequently you want to sync with any changes to the exocore from another source. 10 minutes is reasonable, you can set this lower if you're frequently moving back and forth from phone to PC. Make sure to set the Vault backup interval lower too if so.

Remember that you still control what is actually publicly published on the public site with the `published: true/false` tag at the top of each file.


## 4. Optional: Sync with Mobile

Obsidian has a good [mobile app](https://obsidian.md/mobile) if you want to do mobile editing, but you'll either need to store your Exocore on a cloud service such as iCloud or Google Drive to get the files on your phone, or pay $10/mon for [Obsidian Sync](https://obsidian.md/sync). The exocore is entirely text so it is very lightweight, the standard cloud drive 5-15GB free tiers all have more than enough to storage unless you're hosting many PDFs or large files.

You'll need to download their respective apps to point Obsidian to them on your local drive on both PC and mobile. For example, with Google Drive, you just download [Drive for Desktop](https://www.google.com/intl/en_in/drive/download/) and [Drive for Android](https://play.google.com/store/apps/details?id=com.google.android.apps.docs&hl=en_US&gl=US)  and login and your files will be accessible on the Obsidian apps.

Warning: For iOS, you will *need* to use iCloud storage, Apple doesn't support other cloud storage solutions. If you're familiar with git workflows, you can also [sync with Git using Working Copy or iSH](https://forum.obsidian.md/t/mobile-setting-up-ios-git-based-syncing-with-mobile-app-using-working-copy/16499) as an alternative to iCloud.

## Next Steps


---

## Appendix

The Obsidian config file has been preconfigured, but for reference, I've documented all the steps to recreate the same workspace.

### Set Attachments Folder location

You'll want to set the attachments folder to point to `/assets/img`. Goto the `Settings` by clicking the gear icon at the bottom left, then in `Files & Links`, change `Default location for new attachments` from `Vault folder` to `in the folder specified below` and then set `Attachments folder path` to `/assets/img`.

![[Screen Shot 2022-09-18 at 4.31.03 PM.png]]

###  Detect all files extensions

Settings > Files & Links > Detect all file extensions

### Set Daily Notes location
In `Settings > Daily Notes` set the `New File Location` to `_daily`, and set the template file location to `exocore/_templates/_daily`

### Install Templater

Go to "Settings" -> "Community plugins" -> "Browse", search for "[Obsidian Git](obsidian://show-plugin?id=obsidian-git). Click `Install` then click `Enable`.

Next click `Options` and make the following settings change:
- Set `Template folder location` to `other/_templates`
- Toggle `Trigger Templater on new file creation` to on

Then down where it says `Folder Templates` add `_articles`, `_journal` and `_notes` with the corresponding file in the templates folder. Note, you'll ignore `_daily` as it is already done by the core Obsidian Daily Notes plugin.

### Filename Heading Sync

An additional plugin I would recommend is "Filename Heading Sync". This will automatically rename a file to the first H1 level header that appears.

Go to "Settings" -> "Community plugins" -> "Browse", search for "[Filename Heading Sync](https://github.com/dvcrn/obsidian-filename-heading-sync). Install it then click enable. You will need to go into options and disable `Use File Open Hook` to avoid a conflict with Templater.

`Ignore Regex Rule` has been set to include `exocore/.*|index|readme|Gemfile|site/.*|assets/.*|exocore/.*|images/.*|library/.*|pages/.*` to avoid renaming exocore files.

### Set Theme

You can quickly find themes in `Settings > Appearance > Themes > Manage`. The default exocore theme has been set to Obsidian Gruvbox.

### Setup Obsidian Git to Publish your Exocore

Go to "Settings" -> "Community plugins" -> "Browse", search for "[Obsidian Git](obsidian://show-plugin?id=obsidian-git). Click `Install` then click `Enable`.

Next click `Options` and make the following settings change:

- `Vault backup interval (minutes)` - how frequently you want to changes to be published automatically. I recommend 720 minutes, four times a day.
- `Do auto backup every X minutes after last change` - Turn this on so it only publishes files that haven't been edited for that period of time.
- `Auto pull interval (minutes)` - how frequently you want to sync with any changes to the exocore. This is necessary if you are working on it from multiple systems or your mobile device. 10 minutes is reasonable, you can set this lower if you quickly move from phone to PC.

Everything else can be set to default. 

If you want to manually publish changes instead of automatically, you can leave these settings off and do the following commands in the Command Pallet (cmd + P):
- Obsidian Git Commit All Changes
- Obsidian Git Push

---
## Appendix: Setting up Exocore as a VS Code Workspace on your Machine
A modified VS Code Workspace also exists, but doesn't have an automatic git workflow working as of now.

1. Download [Visual Studio Code](https://code.visualstudio.com/Download)
2. Download the forked repo to your computer by navigating to your github account's exocore repo, then selectiong `Code > Download Zip`
3. Open your newly forked repository in VS Code with File > Open, and navigating to the downloaded folder
4. Accept the prompts to trust the folder, and install the recommended extensions. Your Exocore is now ready to be edited locally on VS Code.

While you're working in VS Code, your work will be automatically saved. However, to publish the data to Github so that it propagates onto the web, you'll need to setup a git commit workflow.

If you're already familiar with git, it's the standard commit process that can be done on your terminal. If you're new to git and Github, the easiest process is [using GitHub Desktop](https://joshuadull.github.io/GitHub-Desktop/02-getting-started/index.html).

You can also [customize Visual Studio Code heavily to your preference](https://www.jamesqquick.com/blog/5-ways-to-customize-vs-code), including easily changing color themes.