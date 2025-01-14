# Installing the Lustre client<a name="install-lustre-client"></a>

To mount your Amazon FSx for Lustre file system from a Linux instance, first install the open\-source Lustre client\. Amazon FSx for Lustre version 2\.10 and version 2\.12 both support access from the 2\.10 versions of the Lustre client\. Then, depending on your operating system version, use one of the following procedures\.

If your compute instance isn't running the Linux kernel specified in the installation instructions, and you can't change the kernel, you can build your own Lustre client\. For more information, see [Compiling Lustre](http://wiki.lustre.org/Compiling_Lustre) on the Lustre Wiki\.

## Amazon Linux 2 and Amazon Linux<a name="lustre-client-amazon-linux"></a>

### To install the Lustre client on Amazon Linux 2<a name="install-lustre-client-amazon-linux-2"></a>

1. Open a terminal on your client\.

1. Determine which kernel is currently running on your compute instance by running the following command\.

   ```
   uname -r
   ```

1. Do one of the following:
   + If the command returns `4.14.104-95.84.amzn2.x86_64` for x86\-based EC2 instances, or `4.14.181-142.260.amzn2.aarch64` or higher for AWS Graviton1\- or Graviton2\-powered EC2 instances, download and install the Lustre client with the following command\.

     ```
     sudo amazon-linux-extras install -y lustre2.10
     ```
   +  If the command returns a result less than `4.14.104-95.84.amzn2.x86_64` for x86\-based EC2 instances, or less than `4.14.181-142.260.amzn2.aarch64` for AWS Graviton1\- or Graviton2\-powered EC2 instances, update the kernel and reboot your Amazon EC2 instance by running the following command\. 

     ```
     sudo yum -y update kernel && sudo reboot
     ```

     Confirm that the kernel has been updated using the uname \-r command\. Then download and install the Lustre client as described previously\.

### To install the Lustre client on Amazon Linux<a name="install-lustre-client-amazon-linux"></a>

1. Open a terminal on your client\.

1. Determine which kernel is currently running on your compute instance by running the following command\. The Lustre client requires Amazon Linux kernel `4.14, version 104` or higher\. 

   ```
   uname -r
   ```

1. Do one of the following:
   + If the command returns `4.14.104-78.84.amzn1.x86_64` or a higher version of 4\.14, download and install the Lustre client using the following command\.

     ```
     sudo yum install -y lustre-client
     ```
   +  If the command returns a result less than `4.14.104-78.84.amzn1.x86_64`, update the kernel and reboot your Amazon EC2 instance by running the following command\. 

     ```
     sudo yum -y update kernel && sudo reboot
     ```

     Confirm that the kernel has been updated using the uname \-r command\. Then download and install the Lustre client as described previously\.

## CentOS and Red Hat<a name="lustre-client-rhel"></a>

### To install the Lustre client on CentOS and Red Hat 7\.5 or 7\.6<a name="install-lustre-client-amazon-centos-7.5"></a>

1. Open a terminal on your client\.

1. Determine which kernel is currently running on the compute instance with the following command\.

   ```
   uname -r
   ```

1. Do one of the following:
   + If the instance is running kernel version `3.10.0-862.*`, download and install the Lustre 2\.10\.5 client with the following commands\. The client comes in two packages to download and install\.

     ```
     sudo yum -y install https://downloads.whamcloud.com/public/lustre/lustre-2.10.5/el7/client/RPMS/x86_64/kmod-lustre-client-2.10.5-1.el7.x86_64.rpm
     sudo yum -y install https://downloads.whamcloud.com/public/lustre/lustre-2.10.5/el7/client/RPMS/x86_64/lustre-client-2.10.5-1.el7.x86_64.rpm
     ```
   + If the instance is running kernel version `3.10.0-957.*`, download and install the Lustre 2\.10\.8 client with the following commands\. The client comes in two packages to download and install\.

     ```
     sudo yum -y install https://downloads.whamcloud.com/public/lustre/lustre-2.10.8/el7/client/RPMS/x86_64/kmod-lustre-client-2.10.8-1.el7.x86_64.rpm
     sudo yum -y install https://downloads.whamcloud.com/public/lustre/lustre-2.10.8/el7/client/RPMS/x86_64/lustre-client-2.10.8-1.el7.x86_64.rpm
     ```
   + If the instance is running kernel `3.10.0-1062.*` or greater, see [To install the Lustre client on CentOS and Red Hat 7\.7, 7\.8, or 7\.9 \(x86\_64 instances\)](#install-lustre-client-Centos-7) for instructions on how to install the Lustre client from the Amazon FSx yum package repository\.

**Note**  
You might need to reboot your compute instance for the client to finish installing\.

### To install the Lustre client on CentOS and Red Hat 7\.7, 7\.8, or 7\.9 \(x86\_64 instances\)<a name="install-lustre-client-Centos-7"></a>

You can install and update Lustre client packages that are compatible with Red Hat Enterprise Linux \(RHEL\) and CentOS from the Amazon FSx Lustre client yum package repository\. These packages are signed to help ensure they have not been tampered with before or during download\. The repository installation fails if you don't install the corresponding public key on your system\.

**To add the Amazon FSx Lustre client yum package repository**

1. Open a terminal on your client\.

1. Install the Amazon FSx rpm public key using the following command\.

   ```
   curl https://fsx-lustre-client-repo-public-keys.s3.amazonaws.com/fsx-rpm-public-key.asc -o /tmp/fsx-rpm-public-key.asc
   ```

1. Import the key using the following command\.

   ```
   sudo rpm --import /tmp/fsx-rpm-public-key.asc
   ```

1. Add the repository and update the package manager using the following command\.

   ```
   sudo curl https://fsx-lustre-client-repo.s3.amazonaws.com/el/7/fsx-lustre-client.repo -o /etc/yum.repos.d/aws-fsx.repo
   ```

**To configure the Amazon FSx Lustre client yum repository**

The Amazon FSx Lustre client yum package repository is configured by default to install the Lustre client that is compatible with the kernel version that initially shipped with the latest supported CentOS and RHEL 7 release\. To install a Lustre client that is compatible with the kernel version you are using, you can edit the repository configuration file\. 

This section describes how to determine which kernel you are running, whether you need to edit the repository configuration, and how to edit the configuration file\.

1. Determine which kernel is currently running on your compute instance by using the following command\.

   ```
   uname -r
   ```

1. Do one of the following:
   + If the command returns `3.10.0-1160*`, you don't need to modify the repository configuration\. Continue to the **To install the Lustre client** procedure\.
   +  If the command returns `3.10.0-1127*`, you must edit the repository configuration so that it points to the Lustre client for the CentOS and RHEL 7\.8 release\.
   +  If the command returns `3.10.0-1062*`, you must edit the repository configuration so that it points to the Lustre client for the CentOS and RHEL 7\.7 release\.

1. Edit the repository configuration file to point to a specific version of RHEL using the following command\.

   ```
   sudo sed -i 's#7#specific_RHEL_version#' /etc/yum.repos.d/aws-fsx.repo
   ```

   To point to release 7\.8, substitute `specific_RHEL_version` with `7.8` in the command\.

   ```
   sudo sed -i 's#7#7.8#' /etc/yum.repos.d/aws-fsx.repo
   ```

   To point to release 7\.7, substitute `specific_RHEL_version` with `7.7` in the command\.

   ```
   sudo sed -i 's#7#7.7#' /etc/yum.repos.d/aws-fsx.repo
   ```

1. Use the following command to clear the yum cache\.

   ```
   sudo yum clean all
   ```

**To install the Lustre client**
+ Install the Lustre client packages from the repository using the following command\.

  ```
  sudo yum install -y kmod-lustre-client lustre-client
  ```

#### Additional information \(CentOS and Red Hat 7\.7 and newer\)<a name="lustre-client-Centos-7-additional-info"></a>

The commands preceding install the two packages that are necessary for mounting and interacting with your Amazon FSx file system\. The repository includes additional Lustre packages, such as a package containing the source code and packages containing tests, and you can optionally install them\. To list all available packages in the repository, use the following command\. 

```
yum --disablerepo="*" --enablerepo="aws-fsx" list available
```

To download the source rpm containing a tarball of the upstream source code and the set of patches that we've applied, use the following command\.

```
 sudo yumdownloader --source kmod-lustre-client
```

When you run yum update, a more recent version of the module is installed if available, and the existing version is replaced\. To prevent the currently installed version from being removed on update, add a line like the following to your `/etc/yum.conf` file\.

```
installonlypkgs=kernel, kernel-big‐mem, kernel-enterprise, kernel-smp,
              kernel-debug, kernel-unsupported, kernel-source, kernel-devel, kernel-PAE,
              kernel-PAE-debug, kmod-lustre-client
```

 This list includes the default install only packages, specified in the `yum.conf` man page, and the `kmod-lustre-client` package\.

### To install the Lustre client on CentOS 7\.8 or 7\.9 \(Arm\-based AWS Graviton\-powered instances\)<a name="install-lustre-client-Centos-7-arm"></a>

You can install and update Lustre client packages from the Amazon FSx Lustre client yum package repository that are compatible with CentOS 7 for Arm\-based AWS Graviton1\- and Graviton2\-powered EC2 instances\. These packages are signed to help ensure they have not been tampered with before or during download\. The repository installation fails if you don't install the corresponding public key on your system\.

**To add the Amazon FSx Lustre client yum package repository**

1. Open a terminal on your client\.

1. Install the Amazon FSx rpm public key using the following command\.

   ```
   curl https://fsx-lustre-client-repo-public-keys.s3.amazonaws.com/fsx-rpm-public-key.asc -o /tmp/fsx-rpm-public-key.asc
   ```

1. Import the key using the following command\.

   ```
   sudo rpm --import /tmp/fsx-rpm-public-key.asc
   ```

1. Add the repository and update the package manager using the following command\.

   ```
   sudo curl https://fsx-lustre-client-repo.s3.amazonaws.com/centos/7/fsx-lustre-client.repo -o /etc/yum.repos.d/aws-fsx.repo
   ```

**To configure the Amazon FSx Lustre client yum repository**

The Amazon FSx Lustre client yum package repository is configured by default to install the Lustre client that is compatible with the kernel version that initially shipped with the latest supported CentOS 7 release\. To install a Lustre client that is compatible with the kernel version you are using, you can edit the repository configuration file\. 

This section describes how to determine which kernel you are running, whether you need to edit the repository configuration, and how to edit the configuration file\.

1. Determine which kernel is currently running on your compute instance by using the following command\.

   ```
   uname -r
   ```

1. Do one of the following:
   + If the command returns `4.18.0-193*`, you don't need to modify the repository configuration\. Continue to the **To install the Lustre client** procedure\.
   +  If the command returns `4.18.0-147*`, you must edit the repository configuration so that it points to the Lustre client for the CentOS 7\.8 release\.

1. Edit the repository configuration file to point to the CentOS 7\.8 release using the following command\.

   ```
   sudo sed -i 's#7#7.8#' /etc/yum.repos.d/aws-fsx.repo
   ```

1. Use the following command to clear the yum cache\.

   ```
   sudo yum clean all
   ```

**To install the Lustre client**
+ Install the packages from the repository using the following command\.

  ```
  sudo yum install -y kmod-lustre-client lustre-client
  ```

#### Additional information \(CentOS 7\.8 or 7\.9 for Arm\-based AWS Graviton\-powered EC2 instances\)<a name="lustre-client-Centos-7-arm-additional-info"></a>

The commands preceding install the two packages that are necessary for mounting and interacting with your Amazon FSx file system\. The repository includes additional Lustre packages, such as a package containing the source code and packages containing tests, and you can optionally install them\. To list all available packages in the repository, use the following command\. 

```
yum --disablerepo="*" --enablerepo="aws-fsx" list available
```

To download the source rpm, containing a tarball of the upstream source code and the set of patches that we've applied, use the following command\.

```
 sudo yumdownloader --source kmod-lustre-client
```

When you run yum update, a more recent version of the module is installed if available, and the existing version is replaced\. To prevent the currently installed version from being removed on update, add a line like the following to your `/etc/yum.conf` file\.

```
installonlypkgs=kernel, kernel-big‐mem, kernel-enterprise, kernel-smp,
              kernel-debug, kernel-unsupported, kernel-source, kernel-devel, kernel-PAE,
              kernel-PAE-debug, kmod-lustre-client
```

 This list includes the default install only packages, specified in the `yum.conf` man page, and the `kmod-lustre-client` package\.

### To install the Lustre client on CentOS and Red Hat 8\.2 and newer<a name="install-lustre-client-RH8.2"></a>

You can install and update Lustre client packages that are compatible with Red Hat Enterprise Linux \(RHEL\) and CentOS from the Amazon FSx Lustre client yum package repository\. These packages are signed to help ensure that they have not been tampered with before or during download\. The repository installation fails if you don't install the corresponding public key on your system\.

**To add the Amazon FSx Lustre client yum package repository**

1. Open a terminal on your client\.

1. Install the Amazon FSx rpm public key by using the following command\.

   ```
   curl https://fsx-lustre-client-repo-public-keys.s3.amazonaws.com/fsx-rpm-public-key.asc -o /tmp/fsx-rpm-public-key.asc
   ```

1. Import the key by using the following command\.

   ```
   sudo rpm --import /tmp/fsx-rpm-public-key.asc
   ```

1. Add the repository and update the package manager using the following command\.

   ```
   sudo curl https://fsx-lustre-client-repo.s3.amazonaws.com/el/8/fsx-lustre-client.repo -o /etc/yum.repos.d/aws-fsx.repo
   ```

**To configure the Amazon FSx Lustre client yum repository**

The Amazon FSx Lustre client yum package repository is configured by default to install the Lustre client that is compatible with the kernel version that initially shipped with the latest supported CentOS and RHEL 8 release\. To install a Lustre client that is compatible with the kernel version you are using, you can edit the repository configuration file\.

This section describes how to determine which kernel you are running, whether you need to edit the repository configuration, and how to edit the configuration file\.

1. Determine which kernel is currently running on your compute instance by using the following command\.

   ```
   uname -r
   ```

1. Do one of the following:
   + If the command returns `4.18.0-348*`, you don't need to modify the repository configuration\. Continue to the **To install the Lustre client** procedure\.
   +  If the command returns `4.18.0-305*`, you must edit the repository configuration so that it points to the Lustre client for the CentOS and RHEL 8\.4 release\.
   +  If the command returns `4.18.0-240*`, you must edit the repository configuration so that it points to the Lustre client for the CentOS and RHEL 8\.3 release\.
   +  If the command returns `4.18.0-193*`, you must edit the repository configuration so that it points to the Lustre client for the CentOS and RHEL 8\.2 release\.

1. Edit the repository configuration file to point to a specific version of RHEL using the following command\.

   ```
   sudo sed -i 's#8#specific_RHEL_version#' /etc/yum.repos.d/aws-fsx.repo
   ```

   For example, to point to release 8\.4, substitute `specific_RHEL_version` with `8.4` in the command\.

   ```
   sudo sed -i 's#8#8.4#' /etc/yum.repos.d/aws-fsx.repo
   ```

1. Use the following command to clear the yum cache\.

   ```
   sudo yum clean all
   ```

**To install the Lustre client**
+ Install the packages from the repository using the following command\.

  ```
  sudo yum install -y kmod-lustre-client lustre-client
  ```

#### Additional information \(CentOS and Red Hat 8\.2 and newer\)<a name="lustre-client-RH8.2-additional-info"></a>

The commands preceding install the two packages that are necessary for mounting and interacting with your Amazon FSx file system\. The repository includes additional Lustre packages, such as a package containing the source code and packages containing tests, and you can optionally install them\. To list all available packages in the repository, use the following command\. 

```
yum --disablerepo="*" --enablerepo="aws-fsx" list available
```

To download the source rpm, containing a tarball of the upstream source code and the set of patches that we've applied, use the following command\.

```
 sudo yumdownloader --source kmod-lustre-client
```

When you run yum update, a more recent version of the module is installed if available and the existing version is replaced\. To prevent the currently installed version from being removed on update, add a line like the following to your `/etc/yum.conf` file\.

```
installonlypkgs=kernel, kernel-PAE, installonlypkg(kernel), installonlypkg(kernel-module), 
              installonlypkg(vm), multiversion(kernel), kmod-lustre-client
```

 This list includes the default install only packages, specified in the `yum.conf` man page, and the `kmod-lustre-client` package\.

## Ubuntu<a name="lustre-client-ubuntu"></a>

### To install the Lustre client on Ubuntu 16\.04<a name="install-lustre-client-Ubuntu-16"></a>

You can get Lustre packages from the Ubuntu 16\.04 Amazon FSx repository\. To validate that the contents of the repository have not been tampered with before or during download, a GNU Privacy Guard \(GPG\) signature is applied to the metadata of the repository\. Installing the repository fails unless you have the correct public GPG key installed on your system\. 

1. Open a terminal on your client\.

1. Follow these steps to add the Amazon FSx Ubuntu repository:

   1. If you have not previously registered an Amazon FSx Ubuntu repository on your client instance, download and install the public key\. Use the following command\.

      ```
      wget -O - https://fsx-lustre-client-repo-public-keys.s3.amazonaws.com/fsx-ubuntu-public-key.asc | sudo apt-key add -
      ```

   1. Add the Amazon FSx package repository to your local package manager\. Use the following command\.

      ```
      sudo bash -c 'echo "deb https://fsx-lustre-client-repo.s3.amazonaws.com/ubuntu xenial main" > /etc/apt/sources.list.d/fsxlustreclientrepo.list && apt-get update'
      ```

1. Determine which kernel is currently running on your client instance, and update as needed\. The Lustre client on Ubuntu 16\.04 requires kernel `4.4.0-1092-aws` or later\.

   1. Run the following command to determine which kernel is running\. 

      ```
      uname -r
      ```

   1. Run the following command to update to the latest Ubuntu kernel and Lustre version and then reboot\.

      ```
      sudo apt install -y linux-aws lustre-client-modules-aws && sudo reboot
      ```

      If your kernel version is greater than `4.4.0-1092-aws` and you don’t want to update to the latest kernel version, you can install Lustre for the current kernel with the following command\.

      ```
      sudo apt install -y lustre-client-modules-$(uname -r)
      ```

      The two Lustre packages that are necessary for mounting and interacting with your Amazon FSx for Lustre file system are installed\. You can optionally install additional related packages, such as a package containing the source code and packages containing tests that are included in the repository\.

   1. List all available packages in the repository by using the following command\.

      ```
      sudo apt-cache search ^lustre
      ```

   1. \(Optional\) If you want your system upgrade to also always upgrade Lustre client modules, make sure that the `lustre-client-modules-aws` package is installed using the following command\.

      ```
      sudo apt install -y lustre-client-modules-aws
      ```

**Note**  
If you get a `Module Not Found error`, do the following:  
Downgrade your kernel to the latest supported version\. List all available versions of the lustre\-client\-modules package and install the corresponding kernel\. To do this, use the following command\.  

```
sudo apt-cache search lustre-client-modules
```
For example, if the latest version that is included in the repository is `lustre-client-modules-4.4.0-1092-aws`, do the following:  
Install the kernel this package was built for\. Use the following commands\.  

   ```
   sudo apt-get install -y linux-image-4.4.0-1092-aws
   ```

   ```
   sudo sed -i 's/GRUB_DEFAULT=.\+/GRUB\_DEFAULT="Advanced options for Ubuntu>Ubuntu, with Linux 4.4.0-1099-aws"/' /etc/default/grub
   ```

   ```
   sudo update-grub
   ```
Reboot your instance using the following command\.  

   ```
   sudo reboot
   ```
Install the Lustre client using the following command\.  

   ```
   sudo apt-get install -y lustre-client-modules-$(uname -r)
   ```

### To install the Lustre client on Ubuntu 18\.04<a name="install-lustre-client-Ubuntu-18"></a>

You can get Lustre packages from the Ubuntu 18\.04 Amazon FSx repository\. To validate that the contents of the repository have not been tampered with before or during download, a GNU Privacy Guard \(GPG\) signature is applied to the metadata of the repository\. Installing the repository fails unless you have the correct public GPG key installed on your system\. 

1. Open a terminal on your client\.

1. Follow these steps to add the Amazon FSx Ubuntu repository:

   1. If you have not previously registered an Amazon FSx Ubuntu repository on your client instance, download and install the required public key\. Use the following command\.

      ```
      wget -O - https://fsx-lustre-client-repo-public-keys.s3.amazonaws.com/fsx-ubuntu-public-key.asc | sudo apt-key add -
      ```

   1. Add the Amazon FSx package repository to your local package manager using the following command\.

      ```
      sudo bash -c 'echo "deb https://fsx-lustre-client-repo.s3.amazonaws.com/ubuntu bionic main" > /etc/apt/sources.list.d/fsxlustreclientrepo.list && apt-get update'
      ```

1. Determine which kernel is currently running on your client instance, and update as needed\. The Lustre client on Ubuntu 18\.04 requires kernel `4.15.0-1054-aws` or later for x86\-based EC2 instances and kernel `5.3.0-1023-aws` or later for Arm\-based EC2 instances powered by AWS Graviton2 processors\. 

   1. Run the following command to determine which kernel is running\.

      ```
      uname -r
      ```

   1. Run the following command to update to the latest Ubuntu kernel and Lustre version and then reboot\.

      ```
      sudo apt install -y linux-aws lustre-client-modules-aws && sudo reboot
      ```

       If your kernel version is greater than `4.15.0-1054-aws` for x86\-based EC2 instances, or greater than `5.3.0-1023-aws` for Graviton2\-based EC2 instances, and you don’t want to update to the latest kernel version, you can install Lustre for the current kernel with the following command\. 

      ```
      sudo apt install -y lustre-client-modules-$(uname -r)
      ```

      The two Lustre packages that are necessary for mounting and interacting with your FSx for Lustre file system are installed\. You can optionally install additional related packages, such as a package containing the source code and packages containing tests that are included in the repository\.

   1. List all available packages in the repository by using the following command\. 

      ```
      sudo apt-cache search ^lustre
      ```

   1. \(Optional\) If you want your system upgrade to also always upgrade Lustre client modules, make sure that the `lustre-client-modules-aws` package is installed using the following command\.

      ```
      sudo apt install -y lustre-client-modules-aws
      ```

**Note**  
If you get a `Module Not Found error`, do the following:  
Downgrade your kernel to the latest supported version\. List all available versions of the `lustre-client-modules` package and install the corresponding kernel\. To do this, use the following command\.  

```
sudo apt-cache search lustre-client-modules
```
For example, if the latest version that is included in the repository is `lustre-client-modules-4.15.0-1054-aws`, do the following:  
Install the kernel this package was built for using the following commands\.  

   ```
   sudo apt-get install -y linux-image-4.15.0-1054-aws
   ```

   ```
   sudo sed -i 's/GRUB_DEFAULT=.\+/GRUB\_DEFAULT="Advanced options for Ubuntu>Ubuntu, with Linux 4.15.0-1054-aws"/' /etc/default/grub
   ```

   ```
   sudo update-grub
   ```
Reboot your instance using the following command\.  

   ```
   sudo reboot
   ```
Install the Lustre client using the following command\.  

   ```
   sudo apt-get install -y lustre-client-modules-$(uname -r)
   ```

### To install the Lustre client on Ubuntu 20\.04<a name="install-lustre-client-Ubuntu-20"></a>

You can get Lustre packages from the Ubuntu 20\.04 Amazon FSx repository\. To validate that the contents of the repository have not been tampered with before or during download, a GNU Privacy Guard \(GPG\) signature is applied to the metadata of the repository\. Installing the repository fails unless you have the correct public GPG key installed on your system\. 

1. Open a terminal on your client\.

1. Follow these steps to add the Amazon FSx Ubuntu repository:

   1. If you have not previously registered an Amazon FSx Ubuntu repository on your client instance, download and install the required public key\. Use the following command\.

      ```
      wget -O - https://fsx-lustre-client-repo-public-keys.s3.amazonaws.com/fsx-ubuntu-public-key.asc | sudo apt-key add -
      ```

   1. Add the Amazon FSx package repository to your local package manager using the following command\.

      ```
      sudo bash -c 'echo "deb https://fsx-lustre-client-repo.s3.amazonaws.com/ubuntu focal main" > /etc/apt/sources.list.d/fsxlustreclientrepo.list && apt-get update'
      ```

1. Determine which kernel is currently running on your client instance, and update as needed\. The Lustre client on Ubuntu 20\.04 requires kernel `5.4.0-1011-aws` or later for x86\-based EC2 instances and kernel `5.4.0-1015-aws` or later for Arm\-based EC2 instances powered by AWS Graviton2 processors\. 

   1. Run the following command to determine which kernel is running\.

      ```
      uname -r
      ```

   1. Run the following command to update to the latest Ubuntu kernel and Lustre version and then reboot\.

      ```
      sudo apt install -y linux-aws lustre-client-modules-aws && sudo reboot
      ```

       If your kernel version is greater than `5.4.0-1011-aws` for x86\-based EC2 instances, or greater than `5.4.0-1015-aws` for Graviton2\-based EC2 instances, and you don’t want to update to the latest kernel version, you can install Lustre for the current kernel with the following command\. 

      ```
      sudo apt install -y lustre-client-modules-$(uname -r)
      ```

      The two Lustre packages that are necessary for mounting and interacting with your FSx for Lustre file system are installed\. You can optionally install additional related packages such as a package containing the source code and packages containing tests that are included in the repository\.

   1. List all available packages in the repository by using the following command\. 

      ```
      sudo apt-cache search ^lustre
      ```

   1. \(Optional\) If you want your system upgrade to also always upgrade Lustre client modules, make sure that the `lustre-client-modules-aws` package is installed using the following command\.

      ```
      sudo apt install -y lustre-client-modules-aws
      ```

**Note**  
If you get a `Module Not Found error`, do the following:  
Downgrade your kernel to the latest supported version\. List all available versions of the lustre\-client\-modules package and install the corresponding kernel\. To do this, use the following command\.  

```
sudo apt-cache search lustre-client-modules
```
For example, if the latest version that is included in the repository is `lustre-client-modules-5.4.0-1011-aws`, do the following:  
Install the kernel that this package was built for using the following commands\.  

   ```
   sudo apt-get install -y linux-image-5.4.0-1011-aws
   ```

   ```
   sudo sed -i 's/GRUB_DEFAULT=.\+/GRUB\_DEFAULT="Advanced options for Ubuntu>Ubuntu, with Linux 5.4.0-1011-aws"/' /etc/default/grub
   ```

   ```
   sudo update-grub
   ```
Reboot your instance using the following command\.  

   ```
   sudo reboot
   ```
Install the Lustre client using the following command\.  

   ```
   sudo apt-get install -y lustre-client-modules-$(uname -r)
   ```

## SUSE Linux<a name="lustre-client-suse"></a>

### To install the Lustre client on SUSE Linux 12 SP3, SP4, or SP5<a name="install-lustre-client-SUSE-Linux"></a>

**To install the Lustre client on SUSE Linux 12 SP3**

1. Open a terminal on your client\.

1. Install the Amazon FSx rpm public key by using the following command\.

   ```
   sudo wget https://fsx-lustre-client-repo-public-keys.s3.amazonaws.com/fsx-sles-public-key.asc
   ```

1. Import the key by using the following command\.

   ```
   sudo rpm --import fsx-sles-public-key.asc
   ```

1. Add the repository for the Lustre client using the following command\.

   ```
   sudo wget https://fsx-lustre-client-repo.s3.amazonaws.com/suse/sles-12/SLES-12/fsx-lustre-client.repo
   ```

1. Download and install the Lustre client with the following commands\.

   ```
   sudo zypper ar --gpgcheck-strict fsx-lustre-client.repo
   sudo sed -i 's#SLES-12#SP3#' /etc/zypp/repos.d/aws-fsx.repo
   sudo zypper refresh
   sudo zypper in lustre-client
   ```

**To install the Lustre client on SUSE Linux 12 SP4**

1. Open a terminal on your client\.

1. Install the Amazon FSx rpm public key by using the following command\.

   ```
   sudo wget https://fsx-lustre-client-repo-public-keys.s3.amazonaws.com/fsx-sles-public-key.asc
   ```

1. Import the key by using the following command\.

   ```
   sudo rpm --import fsx-sles-public-key.asc
   ```

1. Add the repository for the Lustre client using the following command\.

   ```
   sudo wget https://fsx-lustre-client-repo.s3.amazonaws.com/suse/sles-12/SLES-12/fsx-lustre-client.repo
   ```

1. Do one of the following:
   + If you installed SP4 directly, download and install the Lustre client with the following commands\.

     ```
     sudo zypper ar --gpgcheck-strict fsx-lustre-client.repo
     sudo sed -i 's#SLES-12#SP4#' /etc/zypp/repos.d/aws-fsx.repo
     sudo zypper refresh
     sudo zypper in lustre-client
     ```
   + If you migrated from SP3 to SP4 and previously added the Amazon FSx repository for SP3, download and install the Lustre client with the following commands\.

     ```
     sudo zypper ar --gpgcheck-strict fsx-lustre-client.repo
     sudo sed -i 's#SP3#SP4#' /etc/zypp/repos.d/aws-fsx.repo
     sudo zypper ref
     sudo zypper up --force-resolution lustre-client-kmp-default
     ```

**To install the Lustre client on SUSE Linux 12 SP5**

1. Open a terminal on your client\.

1. Install the Amazon FSx rpm public key by using the following command\.

   ```
   sudo wget https://fsx-lustre-client-repo-public-keys.s3.amazonaws.com/fsx-sles-public-key.asc
   ```

1. Import the key by using the following command\.

   ```
   sudo rpm --import fsx-sles-public-key.asc
   ```

1. Add the repository for the Lustre client using the following command\.

   ```
   sudo wget https://fsx-lustre-client-repo.s3.amazonaws.com/suse/sles-12/SLES-12/fsx-lustre-client.repo
   ```

1. Do one of the following:
   + If you installed SP5 directly, download and install the Lustre client with the following commands\.

     ```
     sudo zypper ar --gpgcheck-strict fsx-lustre-client.repo
     sudo zypper refresh
     sudo zypper in lustre-client
     ```
   + If you migrated from SP4 to SP5 and previously added the Amazon FSx repository for SP4, download and install the Lustre client with the following commands\.

     ```
     sudo sed -i 's#SP4#SLES-12' /etc/zypp/repos.d/aws-fsx.repo
     sudo zypper ref
     sudo zypper up --force-resolution lustre-client-kmp-default
     ```

**Note**  
You might need to reboot your compute instance for the client to finish installing\.