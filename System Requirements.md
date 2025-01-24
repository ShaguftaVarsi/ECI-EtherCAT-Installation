## System Requirements

To build ECI images or packages, you need a:

    Target system
    Linux* build system
    USB Flash Drive with a minimum 12 GB capacity (recommend USB 3.1)

### Target System

An industrial PC with an Intel® CPU supporting silicon features such as cache allocation technology (CAT), Intel® Time Coordinated Computing, and onboard Intel® Ethernet Controller to support Time Sensitive Networking (TSN). ECI packages will be installed on the Target System. Internet connectivity is recommended during the initial setup for installing open-source content.

Check your system requirements :  
[Requirements](https://eci.intel.com/docs/3.3/getstarted/requirements.html)


### Linux Build System:

A Linux build system is optional and is used to build ECI from source or privately host an ECI package repository. The requirements of the Linux build system vary depending on the use.

ECI provides ready-to-use packages, referred to as Deb or RPM packages, which you can directly install on to a target from a hosted ECI repository. Alternatively, you may privately host the ECI repository on your own local network.

To privately host the ECI repository, the Linux build system should meet the following requirements:

System Requirements:

        Canonical® Ubuntu® 20.04 (Focal Fossa) or Canonical® Ubuntu® 22.04 (Jammy Jellyfish)
        At least 10 GB of free disk space
        4 CPU Cores
        4 GB RAM

Software Requirements:

    Docker engine (version 19.03.15 or higher).

If your systems satisfy the system requirements, next go to [Getting Access to ECI](https://github.com/ShaguftaVarsi/ECI-EtherCAT-Installation/blob/main/Get%20Access%20to%20ECI.md).
