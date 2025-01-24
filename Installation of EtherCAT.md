# Installation of EtherCAT

## Target System

Follow the steps to install packages and EtherCAT on target system:

1. Before using the ECI repository, update the APT packages list:

        $ sudo apt update

2. ECI provides Deb packages named `customizations-*` which add a GRUB menu entry for ECI and prepares the system to be deterministic. Install these packages using the `eci-customizations` meta-package:

        $ sudo apt install -y eci-customizations

3. ECI provides a firmware package which backports updates from upstream to bring better hardware support to the current distribution. Install this package:

        $ sudo apt-get reinstall '(firmware-linux-nonfree|linux-firmware$)'

4. Next, install the ECI real-time Linux kernel.

        $ sudo apt install -y linux-intel-rt

5. Reboot the target system.

        $ sudo reboot

6. [Verify your build]().

7. Install the eci-realtime meta-package, perform the following command:

        $ sudo apt install eci-realtime

### IgH EtherCAT Master Stack

The [EtherCAT master stack](https://eci.intel.com/docs/3.3/components/ethercat.html#ethercat) by IgH is used for open source projects for automation of systems such as Robot Operating System (ROS) and Linux* CNC. Applications of an open source–based EtherCAT master system reduces cost and makes application program development flexible.

8. Install EtherCAT from meta-package

        $ sudo apt install eci-softplc-fieldbus

- EtherCAT Initialization Script

The EtherCAT master `init` script is installed in `/etc/init.d/ethercat`.

- EtherCAT Sysconfig File

The init script uses a mandatory sysconfig file installed in `/etc/sysconfig/ethercat`. The sysconfig file contains the configuration variables needed to operate one or more masters. The documentation is within the file and also included here.

We have to fill the fields as per our requirements.

Open the file by the following command:

    $ sudo nano /etc/sysconfig/ethercat

![image](https://github.com/user-attachments/assets/56ff204b-d93d-4357-a770-111ddafa0f20)

Do the following:
1. Set REBIND_NICS. Use `lspci` to query net devices. One of the devices might be specified as an **EtherCAT** network interface.

2. Fill the MAC address for MASTER0_DEVICE. Get the MAC address of the Network Interface Controllers (NICs) selected for EtherCAT. We will use eno3.

![image](https://github.com/user-attachments/assets/66ba47ba-c4f9-4b71-91c9-01d3e3c422b6)

3. Use `lshw` command to get all the required field values of eno3.

       $ lshw -class network

4. Modify DEVICE_MODULES:

Option 1: Intel Corporation I210 GbE controller EtherCAT driver (High performance)

    DEVICE_MODULES="igb"

Option 2: Intel Corporation I225 GbE controller EtherCAT driver (High performance)

    DEVICE_MODULES="igc"

Option 3: Intel® Core™ 12th S-Series [Alder Lake] and 11th Gen P-Series and U-Series [Tiger Lake] Intel® Atom™ x6000 Series [Elkhart Lake] GbE controller EtherCAT driver (High performance)

    DEVICE_MODULES="dwmac_intel"

Fallback: Generic driver as EtherCAT driver (Low performance)

    DEVICE_MODULES="generic"


At this moment your EtherCAT setup is done. You change update and reboot the target system.

### Start Master as Service

After the init script and the sysconfig file are ready to configure, and are placed in the right location, the EtherCAT master can be inserted as a service. You can use the init script to manually start and stop the EtherCAT master. Execute the init script with one of the following parameters:

![image](https://github.com/user-attachments/assets/ebad6634-ea29-4b70-90ad-9f89e3f42f7f)

### EtherCAT Sanity Checks

Sanity Check #1: EtherCAT Master Start

1. Start EtherCAT Master:
    
       $ sudo /etc/init.d/ethercat start

![image](https://github.com/user-attachments/assets/2b40effe-02a6-4cb7-a100-f1697c12894b)

2. Check Master information:

        $ ethercat master
   
Expected Output:

![image](https://github.com/user-attachments/assets/ceb42cab-46c7-4590-b89b-cc840521bc62)

3. Check EtherCAT slaves :

        $ ethercat slaves

Expected output:

![image](https://github.com/user-attachments/assets/7009c054-cf86-4723-a14d-1138fc74998e)




The Installation is completed! 

Hope this helps!! 👍


