# raspberryPiAnsible
By implementing the use of Ansible I am able to create multiple picture frames and configs at once across multiple devices.

Requirements:
1. Ansible
2. Raspberry PI (2 or greater)
3. If RPI2 is chosen a wifi dongel will be required
4. Power supply
5. Rasbian OS
6. rclone
7. feh
8. Ethernet Cable


Perform the step up of your Rasbian OS, enable SSH and ensure you have access to the computers.

Clone this repository:
`git clone https://github.com/BrandWest/raspberryPiAnsible.git`

Update packages, upgrade system, and Install Ansible Core on your host machine:
`sudo apt-get update && sudo apt-get upgrade -y && sudo apt-get install ansible-core`

Modify the files/hosts config to match your remote rasberry pi's IP addresses and ansible_user='name'.

Modify the yaml files to be the location of the users and directories within your system. 


Run the Ansible Playbooks

`ansible-playbook -i hosts updates.yaml`

Create the rclone config files on each device by:
1. Open terminal on the remote machine
2. `rclone config`
3. new remote (n)
3.a) give the repo a name
4. storage (13 for goolge drive)
5. Client ID (enter)
6. Client Secret (enter)
7. Scope: (1)
8. If working on headless or SSH (n) otherwise (y)
9. Shared Drive (n)
10. This okay? (y)

Modify the sync.sh file to align with the rclone
rclone sync -v <drive>:<location of photos> <file save location>

Run the remaining playbooks

`ansible-playbook -i hosts rclone_config.yaml no_blanking.yaml slideshow.yaml`

Optional:
You may want to disable the screen saver on the raspberry PI's this is done through the main screen: Preferences -> Screensaver -> disable screen saver 

Reboot the machine
