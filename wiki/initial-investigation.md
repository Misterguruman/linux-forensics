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
        - Start your netcat listener on your forensics laptop


## Setting up your binaries example/commands

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

## Using netcat for exfiltration example/commands
### On your forensics laptop
```bash
# Start a nc listener on port 9999, could be any unused port, and pipe the output to out.txt, could be any file name
nc -l 9999 > out.txt

# The above command will terminate each time you pipe to your listener, we're going to keep it alive with the -k argument
nc -k -l 9999 > out.txt

# To send whole files, for example, if we thought bin/bash was compromised
# In a separate terminal, if you're keeping your other listener running
# Make sure to use a separate unused port if you are running both listeners at the same time
nc -l 4444 > bash.suspect
```

### On the subject machine
> For the sake of syntax/argument accuracy, we'll say our forensics laptop is on the ip 192.168.56.1

> Also that we are listening on port 9999
```bash
# Start by grabbing the date for timezone/time skew information, pipe to your forensics laptop nc listener from above
date | nc 192.168.56.1 9999

# Now we'll grab the basic system information of the subject machine
uname | nc 192.168.56.1 9999

# To send whole files from the subject machine, like in the listener example above, use a command similar to this
# We'll send the suspected compromised bash file to the listener above
nc 192.168.56.1 4444 < /bin/bash
```

