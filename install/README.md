# Install Spinnaker on Ubuntu 20 LTS

### setup & configure Spinnaker on single Ubuntu VM

* `making sure the machine has the 4 cores and 16GB`

### Step1: Install Halyard

> **Halyard is a command-line administration tool that manages the lifecycle of your Spinnaker deployment, including writing & validating your deployment’s configuration, deploying each of Spinnaker’s microservices, and updating the deployment.**

> **All production-capable deployments of Spinnaker require Halyard in order to install, configure, and update Spinnaker. Though it’s possible to install Spinnaker without Halyard, it is not recommend by official Spinnaker, and if you get stuck they will just going ask you to use Halyard.**

> `it is recommended to install Halyard on a machine with at least 12GB of RAM.`

> **Halyard requires Java 11 to be installed**

```
Get the latest version of Halyard

For Debian/Ubuntu:

cd /tmp ; curl -O https://raw.githubusercontent.com/spinnaker/halyard/master/install/debian/InstallHalyard.sh
```
```
Install it:

sudo bash /tmp/InstallHalyard.sh

If you’re prompted for any information, default answers are usually suitable.
```
```
Check whether Halyard was installed properly

hal -v
```

> [More Information can be found here](https://spinnaker.io/setup/install/halyard/#install-on-debianubuntu-and-macos)






  2)
















#### A machine on which to install Halyard

* This can be a local machine or VM (Ubuntu 14.04/16.04, Debian, or macOS), or it can be a Docker container. Make sure it has at least 12GB of memory.

* A Kubernetes cluster on which to install Spinnaker itself

#### it is recommend at least 4 cores and 16GB of RAM available in the cluster.

#### `we can also install Spinnaker on a single local machine, making sure the machine has the 4 cores and 16GB`
