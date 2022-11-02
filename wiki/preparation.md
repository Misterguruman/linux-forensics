[< back](../README.md)

# Preparation
- Have a response kit with a complete set of system binaries and forensics tools
    - 32 and 64 bit versions
    - Ideally a live USB

- Hardware
    - Write blockers
    - Media
    - Forensic laptop
        - At least 8GB Ram
        - 64-bit Linux installation
        - Wired networking available
        - Ideally with USB 3.0 ports
    


- Physical place for documentation

# Installing tools
- SIFT (deprecated)  
```bash 
wget --quiet -O - https://raw.github.com/sans-dfir/sift-bootstrap/master/bootstrap.sh | sudo bash -s -- -i
```

> Since SIFT is no longer a supported tool. There is a script made available by Dr Phil Postra that will install the tools on your current Ubuntu instance. You can find that [here](../scripts/install-dfir.sh) 


- Creating a forensics toolkit usb
    - partition a usb with 2 partitions, 1 FAT32 parition, and one ext4 partition. You will want to install linux on the FAT32 partition, and copy your /bin and /sbin directories to the second partition using the commands below
        - Best practice is to have a USB 2.0 and USB 3.0 variant in case of compatibility issues with older systems

```bash
# We will use -rp to copy recursively and also copy the permissions of your binaries
cp -rp /bin /your-usb-directory

cp -rp /sbin /your-usb-directory
```