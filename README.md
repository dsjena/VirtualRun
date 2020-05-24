# VirtualRun
Collection of Virtual Script

Idea is to create a virtual image which contains all libraries and send to run it in docker based environment. It should be able to run upon call and the size should be small.


# Quick Method:

We need a CentOS env to work for the same and install wget

```
yum install wget
```

Then we can use the wget command to download EPEL repository on the VM.
```
#wget http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
```
The file will be downloaded to the temp folder. So, to install it we will do the following.
```
# cd /tmp
# sudo yum install epel-release-latest-7.noarch.rpm
```
After the installation is done, there should be a success message as following showing on the console.

```
Installed:
    epel-release.noarch 0:7-11
Complete!
```
Now if we head to /etc/yum.repos.d, we will see the following files.

```
CentOS-Base.repo        CentOS-fasttrack.repo       CentOS-Vault.repo
CentOS-CR.repo          CentOS-Media.repo           epel.repo
CentOS-Debuginfo.repo   CentOS-Sources.repo         epel-testing.repo
```
In the CentOS-Base.repo, we need to enable the CentOS Plus repository which is by default disabled. To do so, we simply change the value of enabled to 1 under [centosplus] section.

Then we can proceed to install docker on the VM using yum.
```
# yum install docker
```
We can then start the docker service with the following command.

```
# service docker start
```

Thanks to collaborative project and it is contributor for the (container ecosystem to assemble container-based systems](https://github.com/moby/moby), who have provided a script to create a base CentOS Docker image using yum.

The [script](https://github.com/moby/moby/blob/master/contrib/mkimage-yum.sh) is now available on Moby Project Github repository. A Copy of script also available in this repo. Please not this script it not created by me, it is taken of [moby](https://github.com/moby/moby)

We now need to create a folder called scripts in the root and then create a file called createimage.sh in the folder. This step can be summarized as the following commands.

```
# mkdir scripts
# cd scripts
# vim createimage.sh
```
We then need to copy-and-paste the script from Moby Project to createimage.sh.

After that, we need to make createimage.sh executable with the following command.
```
# chmod +x createimage.sh
```
To run this script now, we need to do as follows, where centos7base is the name of the image file.

```
# ./createimage.sh centos7base
```
It will create a centos7base image and will add to docker. 
