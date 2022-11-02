# Initial Investigation - Was there a security incident?

## First steps 
- Open a case file
    - Take note of: 
        - who is calling 
        - when they called 
        - what their reason for calling was 
        - any relavent recent events involving the machine
        - What is the general purpose of this device? (Web Server, user endpoint, etc)
        - Where did you purchase this device and when?

    - Consider taking photos of the system when you acquire it

- Now you are ready to start your inital investigation to see if there was an incident
    - Start by mounting your [forensics toolkit usb](./preparation.md) 
        - Run your known-good shell from your usb on the system
        - Set path to point to your directories 
        - Reset LD_LIBRARY_PATH
        - [terminal example](#mounting-your-usb)

    - Data preservation:
        - Don't install anything on the subject system
        - Don't create new files on the system
        - Minimize memory footprint
        - Achieve this with two possible solutions
            - Netcat (best option)
            - Storing to USB 

    - Using netcat 

# Setting up your binaries example/commands

```bash
# Mount your binary partition to the system
mkdir /mnt/directory-name
mount /dev/your-drive-uid /mnt/directory-name

# Change directory to your mounted binaries
cd /mnt/directory-name

# Execute your known-good shell
exec bin/bash

# Update your PATH to include your bin and sbin directories
export PATH=/mnt/directory-name/bin:/mnt/directory-name/sbin

# Update your library path with your x86/x64 libraries 
export LD_LIBRARY_PATH=/mnt/directory-name/lib:/mnt/directory-name/lib64

```