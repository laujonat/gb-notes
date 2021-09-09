---
description: This tutorial covers how to install Docker on an Ubuntu 20.04 machine.
---

# Docker

Docker is an open-source containerization platform that allows you to quickly build, test, and deploy applications as portable containers that can run virtually anywhere. A container represents a runtime for a single application and includes everything the software needs to run.

Docker is an integral part of modern software development and DevOps continuous integration and deployment pipelines.

This tutorial covers how to install Docker on an Ubuntu 20.04 machine.

### Installing Docker on Ubuntu 20.04 <a id="installing-docker-on-ubuntu-2004"></a>

Installing Docker on Ubuntu is fairly straightforward. We’ll enable the Docker repository, import the repository GPG key, and install the package.

First, update the packages index and install the dependencies necessary to [add a new HTTPS repository](https://linuxize.com/post/how-to-add-apt-repository-in-ubuntu/) :

```text
sudo apt updatesudo apt install apt-transport-https ca-certificates curl gnupg-agent software-properties-commonCopyCopy
```

Import the repository’s GPG key using the following [`curl`](https://linuxize.com/post/curl-command-examples/) command:

```text
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -Copy
```

Add the Docker APT repository to your system:

```text
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"Copy
```

Now that the Docker repository is enabled, you can install any Docker version that is available in the repositories.

1. To install the latest version of Docker, run the commands below. If you want to install a specific Docker version, skip this step and go to the next one.

   ```text
   sudo apt updatesudo apt install docker-ce docker-ce-cli containerd.ioCopyCopy
   ```

2. To install a specific version, first list all the available versions in the Docker repository:

   ```text
   sudo apt updateapt list -a docker-ceCopyCopy
   ```

   The available Docker versions are printed in the second column. At the time of writing this article, there is only one Docker version \(`5:19.03.9~3-0~ubuntu-focal`\) available in the official Docker repositories.

   ```text
   docker-ce/focal 5:19.03.9~3-0~ubuntu-focal amd64Copy
   ```

   Install a specific version by adding `=<VERSION>` after the package name:

   ```text
   sudo apt install docker-ce=<VERSION> docker-ce-cli=<VERSION> containerd.ioCopy
   ```

Once the installation is completed, the Docker service will start automatically. You can verify it by typing:

```text
sudo systemctl status dockerCopy
```

The output will look something like this:

```text
● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     Active: active (running) since Thu 2020-05-21 14:47:34 UTC; 42s ago
...Copy
```

When a new version of Docker is released, you can update the packages using the standard `sudo apt update && sudo apt upgrade` procedure.

If you want to prevent the Docker package from being updated, mark it as held back:

```text
sudo apt-mark hold docker-ceCopy
```

### Executing Docker Commands as a Non-Root User <a id="executing-docker-commands-as-a-non-root-user"></a>

By default, only root and [user with sudo privileges](https://linuxize.com/post/how-to-create-a-sudo-user-on-ubuntu/) can execute Docker commands.

To execute Docker commands as non-root user you’ll need to add your user to the docker group that is created during the installation of the Docker CE package. To do that, type in:

```text
sudo usermod -aG docker $USERCopy
```

`$USER` is an [environment variable](https://linuxize.com/post/how-to-set-and-list-environment-variables-in-linux/) that holds your username.

Log out and log back in so that the group membership is refreshed.

### Verifying the Installation <a id="verifying-the-installation"></a>

To verify that Docker has been successfully installed and that you can execute the `docker` command without prepending [`sudo`](https://linuxize.com/post/sudo-command-in-linux/) , we’ll [run](https://linuxize.com/post/docker-run-command/) a test container:

```text
docker container run hello-worldCopy
```

The command will download the test image, if not found locally, run it in a container, print a “Hello from Docker” message, and exit. The output should look like the following:

![Docker Hello World](https://linuxize.com/post/how-to-install-and-use-docker-on-ubuntu-20-04/docker-hello-world_hu0e93396502d67b4a7c43a5ce3cac5c2c_75442_768x0_resize_q75_lanczos.jpg?ezimgfmt=ng:webp/ngcb90)

The container will stop after printing the message because it does not have a long-running process.

By default, Docker pulls images from the Docker Hub. It is a cloud-based registry service which among other functionalities, stores the Docker images in public or private repositories.

### Uninstalling Docker <a id="uninstalling-docker"></a>

Before uninstalling Docker it is a good idea to [remove all containers, images, volumes, and networks](https://linuxize.com/post/how-to-remove-docker-images-containers-volumes-and-networks/) .

Run the following commands to stop all running containers and remove all docker objects:

```text
docker container stop $(docker container ls -aq)docker system prune -a --volumesCopyCopy
```

You can now uninstall Docker as any other package installed with `apt`:

```text
sudo apt purge docker-cesudo apt autoremoveCopyCopy
```

### Conclusion <a id="conclusion"></a>

We’ve shown you how to install Docker on Ubuntu 20.04 machine. To learn more about Docker, check out the official [Docker documentation](https://docs.docker.com/) .

If you have any questions, please leave a comment below.  




