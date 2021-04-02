# Install Spinnaker on Ubuntu 20 LTS

### setup & configure Spinnaker on single Ubuntu VM

* `making sure the machine has the 4 cores and 16GB`

### Step1: Install Halyard

> **Halyard is a command-line administration tool that manages the lifecycle of your Spinnaker deployment, including writing & validating your deployment’s configuration, deploying each of Spinnaker’s microservices, and updating the deployment.**

> **All production-capable deployments of Spinnaker require Halyard in order to install, configure, and update Spinnaker. Though it’s possible to install Spinnaker without Halyard, it is not recommend by official Spinnaker, and if you get stuck they will just going ask you to use Halyard.**

> `it is recommended to install Halyard on a machine with at least 12GB of RAM.`

> **Halyard requires Java 11 to be installed**
```
Install JAVA

	sudo add-apt-repository ppa:openjdk-r/ppa
	sudo apt-get update
	sudo apt-get install -y openjdk-11-jdk

```

> **Get the latest version of Halyard**
```
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


### Step2: Deploy Spinnaker and Connect to the UI

> **List the available versions**
```
note: run as devops user ## su - devops

hal version list
```
> **set the version you want to deploy"
```
note: run as devops user ## su - devops

VERSION=1.24.4
hal config version edit --version $VERSION
```

> **configure storage**
```
Spinnaker requires an external storage provider for persisting your Application settings and configured Pipelines. Because these data are sensitive and can be costly to lose, it is recommend you use a hosted storage solution you are confident in

Currently, Halyard only allows you to use the Redis instance that Halyard provisions/installs on your behalf, you don’t need to preconfigure anything to get this storage source working

hal config storage edit --type redis

```
[Supported storage solutions](https://spinnaker.io/setup/install/storage/)

> **Deploy spinnaker**

* Halyard installs Spinnaker in its most locked-down form, on a local deployment Spinnaker binds to localhost intentionally by default. because Your Spinnaker instance has the ability to deploy and destroy a lot of infrastructure in whatever accounts it manages, and opening it to the public is not a good idea without authentication enabled.

* we can open Gate and Deck for external access. To do this for a Local environment, we need to hook into the custom service settings feature of Halyard.

* We'll have to specify the 0.0.0.0 host in both gate.yml and deck.yml in our default Halyard deployment

```
note: run as devops user   ## su - devops

mkdir -p /home/devops/.hal/default/service-settings

echo "host: 0.0.0.0" | tee \
    ~/.hal/default/service-settings/gate.yml \
    ~/.hal/default/service-settings/deck.yml

## run below command to deploy Spinnaker

note: run as root user

sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common
hal deploy apply
```
> **Connect to the Spinnaker UI**
```
navigating to the instance’s public IP address on port 9000 in your browser.

http://publicip:9000/
```
