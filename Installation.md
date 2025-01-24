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





