# Installation of ECI

This section explains the procedure to build ECI custom images from source or to rebuild all or any the ECI Deb packages.  
Before setting up the Linux build system, make sure that:

- The Linux build system meets the recommended [system requirements]().  
- [Docker](https://docs.docker.com/engine/install/ubuntu/)  (version 19.03.15 or higher) is installed and the user is part of the docker group. For information on installing and configuring Docker, refer to the following:

### Install Docker

To install the latest version, run:

    $ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

Verify that the installation is successful by running the hello-world image:

    $ sudo service docker start
    $ sudo docker run hello-world

> [!NOTE]
> Manage Docker as a non-root user:   

Create the docker group.

     $ sudo groupadd docker

Add your user to the docker group.

      $ sudo usermod -aG docker $USER

## Linux Build System

1. Download the [ECI Release Archive](), if not already done.
2. Copy the `eci-release.tar.gz` archive from the ECI release archive (`release-eci_#.#.zip`) to the Linux build system. Make sure that there are no spaces in the directory path. For example, copy the archive to `~/Desktop`. The `eci-release.tar.gz` archive is located in the ECI release archive within the `Edge-Controls-for-Industrial` directory as follows:

       └── Edge-Controls-for-Industrial
          ├── Codesys_Example_Applications.zip
          ├── Dockerfiles.tar.gz
          └── eci-release.tar.gz

3. Extract the archive. In Canonical® Ubuntu®, right-click the archive and select **Extract Here**.  

![image](https://github.com/user-attachments/assets/73231c01-0544-40ac-82e4-7064facba32c)  

The directory contents should be similar to the following:  

![image](https://github.com/user-attachments/assets/57cb807f-e1a0-4901-8138-f5f992e53ddd)  

4. Navigate to the extracted eci-release directory.
5. Open a terminal to the eci-release directory. In Canonical® Ubuntu®, right-click anywhere in the directory explorer and select **Open in Terminal**.
6. At the terminal prompt, run the provided setup script without any parameters:

        $ ./setup.sh

![image](https://github.com/user-attachments/assets/beda9e62-c782-4753-92f2-3c9ca234a33c)  

7. If you are running the script for the first time, the script will prompt whether you want to check for missing dependencies: `Would you like to verify that all dependencies are met? [Y/n]`. Press **Enter** to check the build system for missing dependencies.


![image](https://github.com/user-attachments/assets/2b153bf7-4bce-4421-a7e3-7ab387161fc8)  

The script will display the build dependencies, if any. When prompted, press the **Enter** or **Y** key to install any missing dependencies.

The script will notify the issues, if any. The following are some of the common issues. Click the links for resolutions:

- [Ensure Docker Engine is installed and running](https://eci.intel.com/docs/3.3/getstarted/notifications_setup.html#ensure-docker-engine-is-installed-and-running)
- [Current user is not part of the Docker Group](https://eci.intel.com/docs/3.3/getstarted/notifications_setup.html#current-user-not-part-of-docker-group)
- [Docker Daemon cannot reach the registry](https://eci.intel.com/docs/3.3/getstarted/notifications_setup.html#docker-daemon-cannot-reach-registry)
- [Filename length test failed](https://eci.intel.com/docs/3.3/getstarted/notifications_setup.html#filename-length-test-failed)

The script will then prepare a container image. This container image will be used whenever you build ECI images or Deb packages.


![image](https://github.com/user-attachments/assets/d7e974dc-aa4b-4695-be50-e0299f68f689)  

After the dependencies are installed and prepared, you will see a confirmation message that the dependency check is complete.

![image](https://github.com/user-attachments/assets/5fb31863-8b5d-4d9d-b7c5-615042b1955c)  

At this point, the setup script will exit.

>[!TIP]
> Continue the following steps in the same terminal.

### Build ECI Targets

1. Rerun the setup script without any parameters:

       $ ./setup.sh

2. A menu will display the available ECI targets. Select an ECI target to build.

![image](https://github.com/user-attachments/assets/f9424a90-9aa0-482d-bc5f-92fda3ef2811)

3. The next step is to build a target. Click a target link from the list for to start building the target:  
In our case it is Ubuntu Nobel-Numbat. Select `core-nobel`.
The setup script will begin configuring the assets needed to build the target image. Depending on the state of the build environment, a few notifications may occur.  


![image](https://github.com/user-attachments/assets/5a0fed1b-39d2-4857-bcb1-4081b65a66e8)  

If the setup script is not building the target for the first time, the script will prompt: `Build directory <target> already exists. Do you want to clean the cached build? [y/N]`.  
Common [Errors](https://eci.intel.com/docs/3.3/getstarted/building/notifications_build.html).

After setting up the build target, the script will prompt: `Do you want to run an automated build? [Y/n].`  
To perform an automated build, press **y** at the prompt.  

![image](https://github.com/user-attachments/assets/df176957-3d93-4bca-b1b1-d0ea7f2b3a38)

The build typically takes a long time. A Linux build system with the recommended specifications might take about 30 minutes to an hour to complete. A Linux build system with the minimum specifications might take over two hours to complete. Refer to Linux build system for the recommended specifications.  


![image](https://github.com/user-attachments/assets/6720475c-4139-4d64-ae15-9d82b44d6eb4)

After the build completes, next create a bootable USB flash drive to install the `core-noble` image.  
## Create Bootable USB  
>[!TIP]
> Continue the following steps in the same terminal.

Do the following to create a bootable USB, which you will later use to build and install the ECI image:  
1. Insert a USB drive with at least 12 GB capacity into the Linux build system.
2. At the terminal prompt, run the `create_bootable_usb.sh` script:

        $ ./create_bootable_usb.sh

If the message “_Please run as root_” appears, run the script again with sudo:

        $ sudo ./create_bootable_usb.sh

![image](https://github.com/user-attachments/assets/9bff454b-20af-4edf-a855-024b0666caf8)  

3. The script will display a list of available ECI images. Enter an image name from the list. In this example, `core-bookworm` was entered.

![image](https://github.com/user-attachments/assets/d0c5733b-1079-425f-aee7-3cea9646ecf6)  

4. The script will display a list of available removable mass storage devices.
Enter the name of a device from the displayed list. In this example, the device name displayed is `sda`.

![image](https://github.com/user-attachments/assets/806a78e6-6405-449b-8e86-044919eb3bca)

When the warning, `Warning: All data will be erased on <device> Proceed? [y/N]` is displayed, enter **y** to proceed. The target ECI image will be written to the removable mass storage device.  

5. After the script completes, you will have a bootable USB drive that can install the target ECI image. You may eject the USB drive from the Linux build system. You will use this USB drive to boot and install the image.

![image](https://github.com/user-attachments/assets/733f53b2-7b0e-4dd2-8c2a-1719a81b5165)  

## Target System

### Configure Target System BIOS

To achieve real-time determinism and utilize available Intel silicon features, certain BIOS settings need to be configured. 

1. Boot the target system and access the BIOS (typically pressing the `delete` or `F2` keys while booting will open the BIOS menu).
2. Select Restore Defaults or Load Defaults and then select Save Changes and Reset. As the target system is booting, access the BIOS again (as per Step 1).
3. Modify the BIOS configuration by visiting the [Configure Target System BIOS](https://eci.intel.com/docs/3.3/getstarted/installation/install_generic.html#configure-target-system-bios).


### Boot and Install Image

To boot and install the image, insert the bootable USB drive created earlier into the target system, and do the following:

1. Power on the target system and access the BIOS.
2. In the BIOS menu, boot the USB as the 1st Boot Option.
3. The target system will boot from the USB drive. A boot menu will appear with a few options. Choose the install option.

![image](https://github.com/user-attachments/assets/b3ca4177-4206-453e-ad69-6ad1458edbfc)  

4. The target system will begin the installation process. During the installation, you will be prompted to: `Please select an install target or press n to exit`. Enter an available install target (make sure that the target is correct). For example, enter sdb.
5. If you see the prompt: `/dev/sdb# contains a ext4 file system … Proceed anyway? (y,N)` , press **y** to continue.
6. After the installation is complete, remove the USB drive and press **Enter**, on the keyboard, to reboot the target system.
7. Let the target system boot completely. Select `boot` from the GRUB menu (this option will automatically be selected after 5 seconds).

![image](https://github.com/user-attachments/assets/8ee9597f-fa02-420b-841e-7af26b3b0899)

8. A login prompt will eventually appear. Login with user `root` and password `root`.  

## Setup ECI Repository

This option is recommended for new users of ECI. This will setup the public ECI repository from which ECI packages can be readily installed onto a target system.

1. After registering on Intel® Edge Software Hub, access the download page on the [ECI portal](https://www.intel.com/content/www/us/en/developer/topic-technology/edge-5g/edge-solutions/controls-for-industrial.html). Sign in to your account if needed.
3. After signing in, you should see the Edge Controls for Industrial page with options to get ECI. You can setup the ECI Repository.
4. Click the “Review License Agreement” button to review and accept the license agreement.
5. Select ECI APT repository link. Then, select Ubuntu ##.# LTS as the Target System OS. After selecting the Version and Target System OS, you will see a box with a link. This link provides instructions for setting up the ECI repository.
6. Copy the link and paste it on your web browser. A page titled Setup ECI APT/DNF Repository will appear. Complete the steps on that page.

![image](https://github.com/user-attachments/assets/1aba861b-3efc-4bee-8003-ee4b55b9f9ef)

Now you’re ready to install [EtherCAT package](https://github.com/ShaguftaVarsi/ECI-EtherCAT-Installation/blob/main/Installation%20of%20EtherCAT.md).
















