# Initial Investigation - Was there a security incident?

## First steps 
- Open a case file
    - Note 
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


# Setting up your binaries example/commands

```bash
# Mount your binary partition to the system
mkdir /mnt/directory-name
mount /dev/your-drive-uid /mnt/directory-name
```