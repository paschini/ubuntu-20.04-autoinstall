# Ubuntu Focal Fossa 20.04 Live Server autoinstall
Creates an iso file to boot an unattended installation of ubuntu live server 20.04

This repo provides a very basic example and then a more complete example on how to configure and create an image file that can be used to boot and autoinstall an Ubuntu 20.04 Live Server VM. Note that the previous method (preseeding using d-i configs) has been deprecated.

The full documentation for the autoinstall can be found [here](https://ubuntu.com/server/docs/install/autoinstall-reference).

### BaseExample
We use the new method found [here](https://ubuntu.com/server/docs/install/autoinstall-quickstart) to boot and autoinstall from a base image by feeding configuration from a user-data file to it. Once the installation is an image disk containing a freshly installed and never yet run Ubuntu Live Server that can be booted and used with the username and password specified in the user-data.




