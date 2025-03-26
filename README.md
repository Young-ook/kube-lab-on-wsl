# Kubernetes on WSL (Windows Subsystem for Linux)
> [!TIP]
> This is a project shows how to build an Kubernetes Platform in a WSL environment. Of course, the same can be applied in a general Linux environment.

# Workspace
## Install Debian on WSL
Open Settings > Apps > Programs and Features > Turn Windows features on or off dialog and select the *Windows Subsystem for Linux* to enable WSL on your system. You may reboot your system.

![enable-wsl](images/enable-wsl.png)

After you have enabled WSL, you can install linux distribution via Microsoft Store. We will use the latest version of Debian linux for the hands-on lab. Open Microsoft Store app and search *Debian* (Debian 12, Bookworm), and install.

To verify your install, open windows terminal or command terminal and run `wsl -l -v` command to list WSL distributions.

## Kubernetes
Kubernetes, is an open-source platform designed to automate the deployment, scaling, and management of containerized applications. Containers are lightweight, portable units that bundle an application with its dependencies, making them easy to move between environments. Kubernetes ensures these containers run efficiently and reliably across a cluster of machines. This setup allows you to run Kubernetes locally within WSL, providing a seamless development environment. The simplest way is to access the Kubernetes is provided by Docker Desktop.

> [!IMPORTANT]
> WSL2 (WSL Version 2) is required to enable local Kubernetes within WSL. Because WSL1 (WSL Version 1) lacks the necessary kernel features for containerization, specifically namespace and cgroup support.
>
> - WSL1 Limitations: WSL1 acts as a translation layer, mapping Linux kernel calls to the Windows kernel, but it doesn't provide a real Linux kernel. This means it lacks the features needed for containerization, such as namespaces and cgroups, which are fundamental to how containers work.
> - WSL2 Requirement: WSL2, on the other hand, runs a virtual machine with a real Linux kernel, allowing for the necessary kernel features to be present. This is why you need WSL2 to run container technologies.
> You can check your WSL version by running `wsl -l -v` in PowerShell.

### Install Docker Desktop
Download Docker Desktop from the [official website](https://www.docker.com/products/docker-desktop) and install. During installation, ensure the option to **enable WSL integration** is selected.

Once installed, you can verify installation using `wsl -l -v` command on Windows PowerShell:
```
  NAME              STATE           VERSION
* Debian            Running         2
  docker-desktop    Running         2
```

Open Docker Desktop and go to *Settings > Resources > WSL Integration* to verify if the WSL integration is enabled.

### Enable Kubernetes in Docker Desktop
In Docker Desktop, navigate to *Settings > Kubernetes* and check the box for *Enable Kubernetes* and click **Apply & Restart**. Then, wait for Docker Desktop to download the necessary Kubernetes components. The Kubernetes icon will turn green once it's ready.

![wsl-docker-kube-enabled](images/wsl-docker-kube-enabled.png)

To verify Kubernetes installation, open your linux terminal in WSL and run the following commands to verify Kubernetes is running:
```bash
kubectl version --client
kubectl get nodes
```
You should see at least one node listed, confirming your cluster is up and running.

# Clean up

# Additional Resources
- [asdf - The multiple runtime version manager](https://asdf-vm.com/)
