# Instruction for the Base Example
This was extract directly from the Quickstart in Ubuntu's [website](https://ubuntu.com/server/docs/install/autoinstall-quickstart).
---
Don't forget: you will be running this in a Desktop Ubuntu.
QEMU will try to open a window, and the process will fail if it can't.
It can be done inside a desktop VM, but you need to RDP or VNC into it, because it won't work over SSH.
When running this is a VM, you will need to enable nested virtualization on it, otherwise kvm won't work.
You may get a warning from QEMU if using an AMD VM, but that is OK.

The crypted password in this user-data file is ubuntu.
To make your own, you can use:
```` 
echo -n yourpasswd | makepasswd --crypt-md5 --clearfrom -
````

### Steps
Make sure you have the starting image to work with:
```` 
cd ~/Downloads
wget http://releases.ubuntu.com/20.04/ubuntu-20.04-live-server-amd64.iso
```` 

Mount the ISO:
```` 
sudo mount -r ~/Downloads/ubuntu-20.04-live-server-amd64.iso /mnt
```` 

Edit the autoinstall config, change, add to it, the config is yours:
```` 
cd www
nano user-data
```` 

Serve the cloud-init config over http:
```` 
python3 -m http.server 3003
```` 

Create a target disk:
```` 
truncate -s 10G image.img
```` 

Run the install!
```` 
kvm -no-reboot -m 1024 \
    -drive file=image.img,format=raw,cache=none,if=virtio \
    -cdrom ~/Downloads/ubuntu-20.04-live-server-amd64.iso \
    -kernel /mnt/casper/vmlinuz \
    -initrd /mnt/casper/initrd \
    -append 'autoinstall ds=nocloud-net;s=http://_gateway:3003/'
```` 

At this point you already have the disk image (image.img) ready to use.

Test boot the installed system:
````
kvm -no-reboot -m 1024 \
    -drive file=image.img,format=raw,cache=none,if=virtio
````