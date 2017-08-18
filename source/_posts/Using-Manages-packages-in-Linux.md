---
title: Using Manages packages in Linux
date: 2017-08-16 23:17:49
tags: System Administration
description: "CS615 Assignment3"
---
<!-- more -->

* Ankai Liang
* 10411998
* link: http://www.cs.stevens.edu/~jschauma/615/s17-hw3.html
# CLI

## Create instances

```
➜  ~ git:(master) ✗ aws ec2 run-instances --image-id ami-0187f76b --count 2 --instance-type t1.micro --key-name keypair3 --security-groups mysg
{
    "OwnerId": "624990436890", 
    "ReservationId": "r-02736e99fd5cddc54", 
    "Groups": [], 
    "Instances": [
        {
            "Monitoring": {
                "State": "disabled"
            }, 
            "PublicDnsName": "", 
            "KernelId": "aki-919dcaf8", 
            "State": {
                "Code": 0, 
                "Name": "pending"
            }, 
            "EbsOptimized": false, 
            "LaunchTime": "2017-02-20T00:28:55.000Z", 
            "PrivateIpAddress": "172.31.19.227", 
            "ProductCodes": [], 
            "VpcId": "vpc-adb325cb", 
            "StateTransitionReason": "", 
            "InstanceId": "i-0276fca1b0be5642b", 
            "ImageId": "ami-0187f76b", 
            "PrivateDnsName": "ip-172-31-19-227.ec2.internal", 
            "KeyName": "keypair3", 
            "SecurityGroups": [
                {
                    "GroupName": "mysg", 
                    "GroupId": "sg-a364e4df"
                }
            ], 
            "ClientToken": "", 
            "SubnetId": "subnet-09dda752", 
            "InstanceType": "t1.micro", 
            "NetworkInterfaces": [
                {
                    "Status": "in-use", 
                    "MacAddress": "0e:de:79:8f:ba:ec", 
                    "SourceDestCheck": true, 
                    "VpcId": "vpc-adb325cb", 
                    "Description": "", 
                    "NetworkInterfaceId": "eni-6d7a58a9", 
                    "PrivateIpAddresses": [
                        {
                            "PrivateDnsName": "ip-172-31-19-227.ec2.internal", 
                            "Primary": true, 
                            "PrivateIpAddress": "172.31.19.227"
                        }
                    ], 
                    "PrivateDnsName": "ip-172-31-19-227.ec2.internal", 
                    "Attachment": {
                        "Status": "attaching", 
                        "DeviceIndex": 0, 
                        "DeleteOnTermination": true, 
                        "AttachmentId": "eni-attach-041ed055", 
                        "AttachTime": "2017-02-20T00:28:55.000Z"
                    }, 
                    "Groups": [
                        {
                            "GroupName": "mysg", 
                            "GroupId": "sg-a364e4df"
                        }
                    ], 
                    "Ipv6Addresses": [], 
                    "SubnetId": "subnet-09dda752", 
                    "OwnerId": "624990436890", 
                    "PrivateIpAddress": "172.31.19.227"
                }
            ], 
            "SourceDestCheck": true, 
            "Placement": {
                "Tenancy": "default", 
                "GroupName": "", 
                "AvailabilityZone": "us-east-1b"
            }, 
            "Hypervisor": "xen", 
            "BlockDeviceMappings": [], 
            "Architecture": "x86_64", 
            "StateReason": {
                "Message": "pending", 
                "Code": "pending"
            }, 
            "RootDeviceName": "/dev/sda", 
            "VirtualizationType": "paravirtual", 
            "RootDeviceType": "ebs", 
            "AmiLaunchIndex": 0
        }, 
        {
            "Monitoring": {
                "State": "disabled"
            }, 
            "PublicDnsName": "", 
            "KernelId": "aki-919dcaf8", 
            "State": {
                "Code": 0, 
                "Name": "pending"
            }, 
            "EbsOptimized": false, 
            "LaunchTime": "2017-02-20T00:28:55.000Z", 
            "PrivateIpAddress": "172.31.22.54", 
            "ProductCodes": [], 
            "VpcId": "vpc-adb325cb", 
            "StateTransitionReason": "", 
            "InstanceId": "i-0300f21d53294d05d", 
            "ImageId": "ami-0187f76b", 
            "PrivateDnsName": "ip-172-31-22-54.ec2.internal", 
            "KeyName": "keypair3", 
            "SecurityGroups": [
                {
                    "GroupName": "mysg", 
                    "GroupId": "sg-a364e4df"
                }
            ], 
            "ClientToken": "", 
            "SubnetId": "subnet-09dda752", 
            "InstanceType": "t1.micro", 
            "NetworkInterfaces": [
                {
                    "Status": "in-use", 
                    "MacAddress": "0e:02:fd:83:77:4c", 
                    "SourceDestCheck": true, 
                    "VpcId": "vpc-adb325cb", 
                    "Description": "", 
                    "NetworkInterfaceId": "eni-6e7a58aa", 
                    "PrivateIpAddresses": [
                        {
                            "PrivateDnsName": "ip-172-31-22-54.ec2.internal", 
                            "Primary": true, 
                            "PrivateIpAddress": "172.31.22.54"
                        }
                    ], 
                    "PrivateDnsName": "ip-172-31-22-54.ec2.internal", 
                    "Attachment": {
                        "Status": "attaching", 
                        "DeviceIndex": 0, 
                        "DeleteOnTermination": true, 
                        "AttachmentId": "eni-attach-051ed054", 
                        "AttachTime": "2017-02-20T00:28:55.000Z"
                    }, 
                    "Groups": [
                        {
                            "GroupName": "mysg", 
                            "GroupId": "sg-a364e4df"
                        }
                    ], 
                    "Ipv6Addresses": [], 
                    "SubnetId": "subnet-09dda752", 
                    "OwnerId": "624990436890", 
                    "PrivateIpAddress": "172.31.22.54"
                }
            ], 
            "SourceDestCheck": true, 
            "Placement": {
                "Tenancy": "default", 
                "GroupName": "", 
                "AvailabilityZone": "us-east-1b"
            }, 
            "Hypervisor": "xen", 
            "BlockDeviceMappings": [], 
            "Architecture": "x86_64", 
            "StateReason": {
                "Message": "pending", 
                "Code": "pending"
            }, 
            "RootDeviceName": "/dev/sda", 
            "VirtualizationType": "paravirtual", 
            "RootDeviceType": "ebs", 
            "AmiLaunchIndex": 1
        }
    ]
}

➜  ~ git:(master) ✗ aws ec2 describe-instances --filters "Name=image-id,Values=ami-0187f76b"
{
    "Reservations": [
        {
            "OwnerId": "624990436890", 
            "ReservationId": "r-02736e99fd5cddc54", 
            "Groups": [], 
            "Instances": [
                {
                    "Monitoring": {
                        "State": "disabled"
                    }, 
                    "PublicDnsName": "ec2-54-226-229-126.compute-1.amazonaws.com", 
                    "RootDeviceType": "ebs", 
                    "State": {
                        "Code": 16, 
                        "Name": "running"
                    }, 
                    "EbsOptimized": false, 
                    "LaunchTime": "2017-02-20T00:28:55.000Z", 
                    "PublicIpAddress": "54.226.229.126", 
                    "PrivateIpAddress": "172.31.19.227", 
                    "ProductCodes": [], 
                    "VpcId": "vpc-adb325cb", 
                    "StateTransitionReason": "", 
                    "InstanceId": "i-0276fca1b0be5642b", 
                    "ImageId": "ami-0187f76b", 
                    "PrivateDnsName": "ip-172-31-19-227.ec2.internal", 
                    "KeyName": "keypair3", 
                    "SecurityGroups": [
                        {
                            "GroupName": "mysg", 
                            "GroupId": "sg-a364e4df"
                        }
                    ], 
                    "ClientToken": "", 
                    "SubnetId": "subnet-09dda752", 
                    "InstanceType": "t1.micro", 
                    "NetworkInterfaces": [
                        {
                            "Status": "in-use", 
                            "MacAddress": "0e:de:79:8f:ba:ec", 
                            "SourceDestCheck": true, 
                            "VpcId": "vpc-adb325cb", 
                            "Description": "", 
                            "Association": {
                                "PublicIp": "54.226.229.126", 
                                "PublicDnsName": "ec2-54-226-229-126.compute-1.amazonaws.com", 
                                "IpOwnerId": "amazon"
                            }, 
                            "NetworkInterfaceId": "eni-6d7a58a9", 
                            "PrivateIpAddresses": [
                                {
                                    "PrivateDnsName": "ip-172-31-19-227.ec2.internal", 
                                    "Association": {
                                        "PublicIp": "54.226.229.126", 
                                        "PublicDnsName": "ec2-54-226-229-126.compute-1.amazonaws.com", 
                                        "IpOwnerId": "amazon"
                                    }, 
                                    "Primary": true, 
                                    "PrivateIpAddress": "172.31.19.227"
                                }
                            ], 
                            "PrivateDnsName": "ip-172-31-19-227.ec2.internal", 
                            "Attachment": {
                                "Status": "attached", 
                                "DeviceIndex": 0, 
                                "DeleteOnTermination": true, 
                                "AttachmentId": "eni-attach-041ed055", 
                                "AttachTime": "2017-02-20T00:28:55.000Z"
                            }, 
                            "Groups": [
                                {
                                    "GroupName": "mysg", 
                                    "GroupId": "sg-a364e4df"
                                }
                            ], 
                            "Ipv6Addresses": [], 
                            "SubnetId": "subnet-09dda752", 
                            "OwnerId": "624990436890", 
                            "PrivateIpAddress": "172.31.19.227"
                        }
                    ], 
                    "SourceDestCheck": true, 
                    "Placement": {
                        "Tenancy": "default", 
                        "GroupName": "", 
                        "AvailabilityZone": "us-east-1b"
                    }, 
                    "Hypervisor": "xen", 
                    "BlockDeviceMappings": [
                        {
                            "DeviceName": "/dev/sda", 
                            "Ebs": {
                                "Status": "attached", 
                                "DeleteOnTermination": true, 
                                "VolumeId": "vol-0e23ef64b32cbbe21", 
                                "AttachTime": "2017-02-20T00:28:56.000Z"
                            }
                        }
                    ], 
                    "Architecture": "x86_64", 
                    "KernelId": "aki-919dcaf8", 
                    "RootDeviceName": "/dev/sda", 
                    "VirtualizationType": "paravirtual", 
                    "AmiLaunchIndex": 0
                }, 
                {
                    "Monitoring": {
                        "State": "disabled"
                    }, 
                    "PublicDnsName": "ec2-52-204-105-92.compute-1.amazonaws.com", 
                    "RootDeviceType": "ebs", 
                    "State": {
                        "Code": 16, 
                        "Name": "running"
                    }, 
                    "EbsOptimized": false, 
                    "LaunchTime": "2017-02-20T00:28:55.000Z", 
                    "PublicIpAddress": "52.204.105.92", 
                    "PrivateIpAddress": "172.31.22.54", 
                    "ProductCodes": [], 
                    "VpcId": "vpc-adb325cb", 
                    "StateTransitionReason": "", 
                    "InstanceId": "i-0300f21d53294d05d", 
                    "ImageId": "ami-0187f76b", 
                    "PrivateDnsName": "ip-172-31-22-54.ec2.internal", 
                    "KeyName": "keypair3", 
                    "SecurityGroups": [
                        {
                            "GroupName": "mysg", 
                            "GroupId": "sg-a364e4df"
                        }
                    ], 
                    "ClientToken": "", 
                    "SubnetId": "subnet-09dda752", 
                    "InstanceType": "t1.micro", 
                    "NetworkInterfaces": [
                        {
                            "Status": "in-use", 
                            "MacAddress": "0e:02:fd:83:77:4c", 
                            "SourceDestCheck": true, 
                            "VpcId": "vpc-adb325cb", 
                            "Description": "", 
                            "Association": {
                                "PublicIp": "52.204.105.92", 
                                "PublicDnsName": "ec2-52-204-105-92.compute-1.amazonaws.com", 
                                "IpOwnerId": "amazon"
                            }, 
                            "NetworkInterfaceId": "eni-6e7a58aa", 
                            "PrivateIpAddresses": [
                                {
                                    "PrivateDnsName": "ip-172-31-22-54.ec2.internal", 
                                    "Association": {
                                        "PublicIp": "52.204.105.92", 
                                        "PublicDnsName": "ec2-52-204-105-92.compute-1.amazonaws.com", 
                                        "IpOwnerId": "amazon"
                                    }, 
                                    "Primary": true, 
                                    "PrivateIpAddress": "172.31.22.54"
                                }
                            ], 
                            "PrivateDnsName": "ip-172-31-22-54.ec2.internal", 
                            "Attachment": {
                                "Status": "attached", 
                                "DeviceIndex": 0, 
                                "DeleteOnTermination": true, 
                                "AttachmentId": "eni-attach-051ed054", 
                                "AttachTime": "2017-02-20T00:28:55.000Z"
                            }, 
                            "Groups": [
                                {
                                    "GroupName": "mysg", 
                                    "GroupId": "sg-a364e4df"
                                }
                            ], 
                            "Ipv6Addresses": [], 
                            "SubnetId": "subnet-09dda752", 
                            "OwnerId": "624990436890", 
                            "PrivateIpAddress": "172.31.22.54"
                        }
                    ], 
                    "SourceDestCheck": true, 
                    "Placement": {
                        "Tenancy": "default", 
                        "GroupName": "", 
                        "AvailabilityZone": "us-east-1b"
                    }, 
                    "Hypervisor": "xen", 
                    "BlockDeviceMappings": [
                        {
                            "DeviceName": "/dev/sda", 
                            "Ebs": {
                                "Status": "attached", 
                                "DeleteOnTermination": true, 
                                "VolumeId": "vol-0ac8f0cc34c1ebc56", 
                                "AttachTime": "2017-02-20T00:28:56.000Z"
                            }
                        }
                    ], 
                    "Architecture": "x86_64", 
                    "KernelId": "aki-919dcaf8", 
                    "RootDeviceName": "/dev/sda", 
                    "VirtualizationType": "paravirtual", 
                    "AmiLaunchIndex": 1
                }
            ]
        }
    ]
}
```

The public DNS of two instances are:
ec2-54-226-229-126.compute-1.amazonaws.com
ec2-52-204-105-92.compute-1.amazonaws.com

## Install nginx by package manager
According to the tutorial of Nginx,(https://www.nginx.com/resources/wiki/start/topics/tutorials/install/)
I should create a file named /etc/yum.repos.d/nginx.repo
First time, I couldn't modify the file in this documents. Use `sudo` to create file.

```
➜  Documents git:(master) ✗ ssh -i p.pem fedora@ec2-54-226-229-126.compute-1.amazonaws.com
[fedora@ip-172-31-19-227 ~]$ cd /etc/yum.repos.d
[fedora@ip-172-31-19-227 yum.repos.d]$ vi nginx.repo
[fedora@ip-172-31-19-227 yum.repos.d]$ cd ..
[fedora@ip-172-31-19-227 etc]$ chmod 777 yum.repos.d
[fedora@ip-172-31-19-227 etc]$ cd yum.repos.d
[fedora@ip-172-31-19-227 yum.repos.d]$ sudo vi nginx.repo
```
nginx.repo's content:

```
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/rhel/6/$basearch/
gpgcheck=0
enabled=1
```

Then I try to use `yum`, but the system told me I should use dnf.

```
[fedora@ip-172-31-19-227 ~]$ yum
Yum command has been deprecated, redirecting to '/usr/bin/dnf '.
See 'man dnf' and 'man yum2dnf' for more information.
To transfer transaction metadata from yum to DNF, run:
'dnf install python-dnf-plugins-extras-migrate && dnf-2 migrate'

You need to give some command
usage: dnf [options] COMMAND

List of Main Commands

autoremove                
check-update              Check for available package upgrades
clean                     Remove cached data
distro-sync               Synchronize installed packages to the latest available versions
downgrade                 downgrade a package
group                     Display, or use, the groups information
help                      Display a helpful usage message
history                   Display, or use, the transaction history
info                      Display details about a package or group of packages
install                   Install a package or packages on your system
list                      List a package or groups of packages
makecache                 Generate the metadata cache
mark                      Mark or unmark installed packages as installed by user.
provides                  Find what package provides the given value
reinstall                 reinstall a package
remove                    Remove a package or packages from your system
repolist                  Display the configured software repositories
repository-packages       Run commands on top of all packages in given repository
search                    Search package details for the given string
updateinfo                Display advisories about packages
upgrade                   Upgrade a package or packages on your system
upgrade-to                Upgrade a package on your system to the specified version

List of Plugin Commands

builddep                  Install build dependencies for package or spec file
config-manager            manage dnf configuration options and repositories
copr                      Interact with Copr repositories.
debuginfo-install         install debuginfo packages
download                  Download package to current directory
needs-restarting          determine updated binaries that need restarting
playground                Interact with Playground repository.
repoquery                 search for packages matching keyword
reposync                  download all packages from remote repo
[fedora@ip-172-31-19-227 ~]$ dnf install nginx
Error: This command has to be run under the root user.
[fedora@ip-172-31-19-227 ~]$ sudo dnf info nginx
Last metadata expiration check performed 0:05:19 ago on Mon Feb 20 07:40:11 2017.
Available Packages
Name        : nginx
Arch        : x86_64
Epoch       : 1
Version     : 1.8.1
Release     : 3.fc23
Size        : 536 k
Repo        : updates
Summary     : A high performance web server and reverse proxy server
URL         : http://nginx.org/
License     : BSD
Description : Nginx is a web server and a reverse proxy server for HTTP, SMTP,
            : POP3 and IMAP protocols, with a strong focus on high concurrency,
            : performance and low memory usage.
[fedora@ip-172-31-19-227 ~]$ sudo dnf install nginx
Last metadata expiration check performed 0:11:33 ago on Mon Feb 20 07:40:11 2017.
Dependencies resolved.
================================================================================
 Package                    Arch      Version                  Repository  Size
================================================================================
Installing:
 aajohan-comfortaa-fonts    noarch    2.004-5.fc23             fedora     151 k
 fontconfig                 x86_64    2.11.94-5.fc23           updates    242 k
 fontpackages-filesystem    noarch    1.44-14.fc23             fedora      15 k
 gd                         x86_64    2.1.1-10.fc23            updates    146 k
 gperftools-libs            x86_64    2.4-5.fc23               fedora     273 k
 jbigkit-libs               x86_64    2.1-4.fc23               fedora      51 k
 libX11                     x86_64    1.6.3-2.fc23             fedora     608 k
 libX11-common              noarch    1.6.3-2.fc23             fedora     166 k
 libXau                     x86_64    1.0.8-5.fc23             fedora      33 k
 libXpm                     x86_64    3.5.11-4.fc23            fedora      54 k
 libjpeg-turbo              x86_64    1.4.1-2.fc23             fedora     147 k
 libtiff                    x86_64    4.0.4-1.fc23             fedora     173 k
 libunwind                  x86_64    1.1-10.fc23              fedora      64 k
 libvpx                     x86_64    1.4.0-6.fc23             updates    618 k
 libxcb                     x86_64    1.11.1-1.fc23            updates    192 k
 libxslt                    x86_64    1.1.28-11.fc23           fedora     246 k
 make                       x86_64    1:4.0-5.1.fc23           fedora     449 k
 nginx                      x86_64    1:1.8.1-3.fc23           updates    536 k
 nginx-filesystem           noarch    1:1.8.1-3.fc23           updates     20 k
 nginx-mimetypes            noarch    2.1.45-1.fc23            fedora      26 k
 openssl                    x86_64    1:1.0.2d-2.fc23          fedora     511 k
 perl                       x86_64    4:5.22.2-355.fc23        updates    6.9 M
 perl-Carp                  noarch    1.38-1.fc23              updates     29 k
 perl-Encode                x86_64    3:2.80-7.fc23            updates    1.5 M
 perl-Exporter              noarch    5.72-347.fc23            fedora      33 k
 perl-File-Path             noarch    2.09-347.fc23            fedora      31 k
 perl-File-Temp             noarch    0.23.04-346.fc23         fedora      61 k
 perl-Getopt-Long           noarch    2.49.1-1.fc23            updates     62 k
 perl-HTTP-Tiny             noarch    0.056-4.fc23             updates     53 k
 perl-MIME-Base64           x86_64    3.15-348.fc23            fedora      29 k
 perl-PathTools             x86_64    3.62-2.fc23              updates     88 k
 perl-Pod-Escapes           noarch    1:1.07-348.fc23          fedora      19 k
 perl-Pod-Perldoc           noarch    3.26-1.fc23              updates     86 k
 perl-Pod-Simple            noarch    1:3.31-1.fc23            fedora     211 k
 perl-Pod-Usage             noarch    4:1.67-3.fc23            fedora      33 k
 perl-Scalar-List-Utils     x86_64    2:1.43-1.fc23            updates     62 k
 perl-Socket                x86_64    3:2.024-1.fc23           updates     56 k
 perl-Storable              x86_64    1:2.53-347.fc23          updates     84 k
 perl-Term-ANSIColor        noarch    4.03-346.fc23            fedora      45 k
 perl-Term-Cap              noarch    1.17-1.fc23              fedora      22 k
 perl-Text-ParseWords       noarch    3.30-346.fc23            fedora      17 k
 perl-Text-Tabs+Wrap        noarch    2013.0523-346.fc23       fedora      23 k
 perl-Time-HiRes            x86_64    1.9728-1.fc23            updates     50 k
 perl-Time-Local            noarch    1:1.250-1.fc23           updates     30 k
 perl-Unicode-Normalize     x86_64    1.24-1.fc23              updates     80 k
 perl-constant              noarch    1.33-347.fc23            fedora      24 k
 perl-libs                  x86_64    4:5.22.2-355.fc23        updates    823 k
 perl-macros                x86_64    4:5.22.2-355.fc23        updates     57 k
 perl-parent                noarch    1:0.234-3.fc23           fedora      18 k
 perl-podlators             noarch    2.5.3-347.fc23           fedora     112 k
 perl-threads               x86_64    1:2.02-2.fc23            fedora      58 k
 perl-threads-shared        x86_64    1.48-346.fc23            fedora      44 k

Transaction Summary
================================================================================
Install  52 Packages

Total download size: 15 M
Installed size: 45 M
Is this ok [y/N]: y
Downloading Packages:
(1/52): libxslt-1.1.28-11.fc23.x86_64.rpm                                767 kB/s | 246 kB     00:00    
(2/52): nginx-1.8.1-3.fc23.x86_64.rpm                                    1.4 MB/s | 536 kB     00:00    
(3/52): gperftools-libs-2.4-5.fc23.x86_64.rpm                            683 kB/s | 273 kB     00:00    
(4/52): nginx-mimetypes-2.1.45-1.fc23.noarch.rpm                         177 kB/s |  26 kB     00:00    
(5/52): perl-Exporter-5.72-347.fc23.noarch.rpm                           230 kB/s |  33 kB     00:00    
(6/52): perl-constant-1.33-347.fc23.noarch.rpm                           228 kB/s |  24 kB     00:00    
(7/52): nginx-filesystem-1.8.1-3.fc23.noarch.rpm                         525 kB/s |  20 kB     00:00    
(8/52): libunwind-1.1-10.fc23.x86_64.rpm                                 369 kB/s |  64 kB     00:00    
(9/52): make-4.0-5.1.fc23.x86_64.rpm                                     1.2 MB/s | 449 kB     00:00    
(10/52): openssl-1.0.2d-2.fc23.x86_64.rpm                                1.2 MB/s | 511 kB     00:00    
(11/52): gd-2.1.1-10.fc23.x86_64.rpm                                     522 kB/s | 146 kB     00:00    
(12/52): libXpm-3.5.11-4.fc23.x86_64.rpm                                 343 kB/s |  54 kB     00:00    
(13/52): libjpeg-turbo-1.4.1-2.fc23.x86_64.rpm                           604 kB/s | 147 kB     00:00    
(14/52): libX11-1.6.3-2.fc23.x86_64.rpm                                  1.7 MB/s | 608 kB     00:00    
(15/52): libtiff-4.0.4-1.fc23.x86_64.rpm                                 655 kB/s | 173 kB     00:00    
(16/52): jbigkit-libs-2.1-4.fc23.x86_64.rpm                              354 kB/s |  51 kB     00:00    
(17/52): libX11-common-1.6.3-2.fc23.noarch.rpm                           746 kB/s | 166 kB     00:00    
(18/52): perl-File-Path-2.09-347.fc23.noarch.rpm                         284 kB/s |  31 kB     00:00    
(19/52): perl-File-Temp-0.23.04-346.fc23.noarch.rpm                      336 kB/s |  61 kB     00:00    
(20/52): perl-Text-Tabs+Wrap-2013.0523-346.fc23.noarch.rpm               219 kB/s |  23 kB     00:00    
(21/52): perl-Pod-Simple-3.31-1.fc23.noarch.rpm                          735 kB/s | 211 kB     00:00    
(22/52): perl-parent-0.234-3.fc23.noarch.rpm                             174 kB/s |  18 kB     00:00    
(23/52): perl-5.22.2-355.fc23.x86_64.rpm                                 9.8 MB/s | 6.9 MB     00:00    
(24/52): perl-threads-2.02-2.fc23.x86_64.rpm                             215 kB/s |  58 kB     00:00    
(25/52): perl-threads-shared-1.48-346.fc23.x86_64.rpm                    185 kB/s |  44 kB     00:00    
(26/52): perl-libs-5.22.2-355.fc23.x86_64.rpm                             12 MB/s | 823 kB     00:00    
(27/52): fontconfig-2.11.94-5.fc23.x86_64.rpm                            2.3 MB/s | 242 kB     00:00    
(28/52): perl-Pod-Escapes-1.07-348.fc23.noarch.rpm                       176 kB/s |  19 kB     00:00    
(29/52): perl-Carp-1.38-1.fc23.noarch.rpm                                859 kB/s |  29 kB     00:00    
(30/52): fontpackages-filesystem-1.44-14.fc23.noarch.rpm                 201 kB/s |  15 kB     00:00    
(31/52): perl-Scalar-List-Utils-1.43-1.fc23.x86_64.rpm                   2.1 MB/s |  62 kB     00:00    
(32/52): libvpx-1.4.0-6.fc23.x86_64.rpm                                  7.2 MB/s | 618 kB     00:00    
(33/52): perl-Getopt-Long-2.49.1-1.fc23.noarch.rpm                       3.4 MB/s |  62 kB     00:00    
(34/52): perl-MIME-Base64-3.15-348.fc23.x86_64.rpm                       270 kB/s |  29 kB     00:00    
(35/52): perl-Encode-2.80-7.fc23.x86_64.rpm                              9.7 MB/s | 1.5 MB     00:00    
(36/52): perl-Pod-Usage-1.67-3.fc23.noarch.rpm                           268 kB/s |  33 kB     00:00    
(37/52): perl-Text-ParseWords-3.30-346.fc23.noarch.rpm                   136 kB/s |  17 kB     00:00    
(38/52): perl-Term-ANSIColor-4.03-346.fc23.noarch.rpm                    318 kB/s |  45 kB     00:00    
(39/52): perl-PathTools-3.62-2.fc23.x86_64.rpm                           3.7 MB/s |  88 kB     00:00    
(40/52): perl-podlators-2.5.3-347.fc23.noarch.rpm                        534 kB/s | 112 kB     00:00    
(41/52): perl-Term-Cap-1.17-1.fc23.noarch.rpm                            202 kB/s |  22 kB     00:00    
(42/52): perl-Socket-2.024-1.fc23.x86_64.rpm                             1.7 MB/s |  56 kB     00:00    
(43/52): libxcb-1.11.1-1.fc23.x86_64.rpm                                 3.0 MB/s | 192 kB     00:00    
(44/52): perl-Storable-2.53-347.fc23.x86_64.rpm                          2.7 MB/s |  84 kB     00:00    
(45/52): perl-Time-HiRes-1.9728-1.fc23.x86_64.rpm                        2.5 MB/s |  50 kB     00:00    
(46/52): perl-Unicode-Normalize-1.24-1.fc23.x86_64.rpm                   4.0 MB/s |  80 kB     00:00    
(47/52): perl-macros-5.22.2-355.fc23.x86_64.rpm                          2.0 MB/s |  57 kB     00:00    
(48/52): perl-Pod-Perldoc-3.26-1.fc23.noarch.rpm                         4.5 MB/s |  86 kB     00:00    
(49/52): perl-HTTP-Tiny-0.056-4.fc23.noarch.rpm                          2.7 MB/s |  53 kB     00:00    
(50/52): perl-Time-Local-1.250-1.fc23.noarch.rpm                         941 kB/s |  30 kB     00:00    
(51/52): libXau-1.0.8-5.fc23.x86_64.rpm                                  211 kB/s |  33 kB     00:00    
(52/52): aajohan-comfortaa-fonts-2.004-5.fc23.noarch.rpm                 616 kB/s | 151 kB     00:00    
---------------------------------------------------------------------------------------------------------
Total                                                                    4.7 MB/s |  15 MB     00:03     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Installing  : perl-libs-4:5.22.2-355.fc23.x86_64                                                  1/52 
  Installing  : fontpackages-filesystem-1.44-14.fc23.noarch                                         2/52 
  Installing  : libjpeg-turbo-1.4.1-2.fc23.x86_64                                                   3/52 
  Installing  : nginx-filesystem-1:1.8.1-3.fc23.noarch                                              4/52 
  Installing  : nginx-mimetypes-2.1.45-1.fc23.noarch                                                5/52 
  Installing  : aajohan-comfortaa-fonts-2.004-5.fc23.noarch                                         6/52 
  Installing  : fontconfig-2.11.94-5.fc23.x86_64                                                    7/52 
  Installing  : perl-macros-4:5.22.2-355.fc23.x86_64                                                8/52 
  Installing  : perl-Time-Local-1:1.250-1.fc23.noarch                                               9/52 
  Installing  : perl-Term-ANSIColor-4.03-346.fc23.noarch                                           10/52 
  Installing  : perl-Term-Cap-1.17-1.fc23.noarch                                                   11/52 
  Installing  : perl-HTTP-Tiny-0.056-4.fc23.noarch                                                 12/52 
  Installing  : perl-MIME-Base64-3.15-348.fc23.x86_64                                              13/52 
  Installing  : perl-podlators-2.5.3-347.fc23.noarch                                               14/52 
  Installing  : perl-Pod-Perldoc-3.26-1.fc23.noarch                                                15/52 
  Installing  : perl-Pod-Escapes-1:1.07-348.fc23.noarch                                            16/52 
  Installing  : perl-Text-ParseWords-3.30-346.fc23.noarch                                          17/52 
  Installing  : perl-Encode-3:2.80-7.fc23.x86_64                                                   18/52 
  Installing  : perl-Pod-Usage-4:1.67-3.fc23.noarch                                                19/52 
  Installing  : perl-Text-Tabs+Wrap-2013.0523-346.fc23.noarch                                      20/52 
  Installing  : perl-parent-1:0.234-3.fc23.noarch                                                  21/52 
  Installing  : perl-constant-1.33-347.fc23.noarch                                                 22/52 
  Installing  : perl-threads-1:2.02-2.fc23.x86_64                                                  23/52 
  Installing  : perl-Carp-1.38-1.fc23.noarch                                                       24/52 
  Installing  : perl-threads-shared-1.48-346.fc23.x86_64                                           25/52 
  Installing  : perl-Scalar-List-Utils-2:1.43-1.fc23.x86_64                                        26/52 
  Installing  : perl-File-Path-2.09-347.fc23.noarch                                                27/52 
  Installing  : perl-File-Temp-0.23.04-346.fc23.noarch                                             28/52 
  Installing  : perl-PathTools-3.62-2.fc23.x86_64                                                  29/52 
  Installing  : perl-Socket-3:2.024-1.fc23.x86_64                                                  30/52 
  Installing  : perl-Storable-1:2.53-347.fc23.x86_64                                               31/52 
  Installing  : perl-Time-HiRes-1.9728-1.fc23.x86_64                                               32/52 
  Installing  : perl-Unicode-Normalize-1.24-1.fc23.x86_64                                          33/52 
  Installing  : perl-Pod-Simple-1:3.31-1.fc23.noarch                                               34/52 
  Installing  : perl-Getopt-Long-2.49.1-1.fc23.noarch                                              35/52 
  Installing  : perl-Exporter-5.72-347.fc23.noarch                                                 36/52 
  Installing  : perl-4:5.22.2-355.fc23.x86_64                                                      37/52 
  Installing  : libXau-1.0.8-5.fc23.x86_64                                                         38/52 
  Installing  : libxcb-1.11.1-1.fc23.x86_64                                                        39/52 
  Installing  : libvpx-1.4.0-6.fc23.x86_64                                                         40/52 
  Installing  : jbigkit-libs-2.1-4.fc23.x86_64                                                     41/52 
  Installing  : libtiff-4.0.4-1.fc23.x86_64                                                        42/52 
  Installing  : libX11-common-1.6.3-2.fc23.noarch                                                  43/52 
  Installing  : libX11-1.6.3-2.fc23.x86_64                                                         44/52 
  Installing  : libXpm-3.5.11-4.fc23.x86_64                                                        45/52 
  Installing  : gd-2.1.1-10.fc23.x86_64                                                            46/52 
  Installing  : make-1:4.0-5.1.fc23.x86_64                                                         47/52 
  Installing  : openssl-1:1.0.2d-2.fc23.x86_64                                                     48/52 
  Installing  : libunwind-1.1-10.fc23.x86_64                                                       49/52 
  Installing  : gperftools-libs-2.4-5.fc23.x86_64                                                  50/52 
  Installing  : libxslt-1.1.28-11.fc23.x86_64                                                      51/52 
  Installing  : nginx-1:1.8.1-3.fc23.x86_64                                                        52/52 
  Verifying   : nginx-1:1.8.1-3.fc23.x86_64                                                         1/52 
  Verifying   : gperftools-libs-2.4-5.fc23.x86_64                                                   2/52 
  Verifying   : libxslt-1.1.28-11.fc23.x86_64                                                       3/52 
  Verifying   : nginx-mimetypes-2.1.45-1.fc23.noarch                                                4/52 
  Verifying   : perl-Exporter-5.72-347.fc23.noarch                                                  5/52 
  Verifying   : perl-constant-1.33-347.fc23.noarch                                                  6/52 
  Verifying   : nginx-filesystem-1:1.8.1-3.fc23.noarch                                              7/52 
  Verifying   : libunwind-1.1-10.fc23.x86_64                                                        8/52 
  Verifying   : openssl-1:1.0.2d-2.fc23.x86_64                                                      9/52 
  Verifying   : make-1:4.0-5.1.fc23.x86_64                                                         10/52 
  Verifying   : gd-2.1.1-10.fc23.x86_64                                                            11/52 
  Verifying   : libX11-1.6.3-2.fc23.x86_64                                                         12/52 
  Verifying   : libXpm-3.5.11-4.fc23.x86_64                                                        13/52 
  Verifying   : libjpeg-turbo-1.4.1-2.fc23.x86_64                                                  14/52 
  Verifying   : libtiff-4.0.4-1.fc23.x86_64                                                        15/52 
  Verifying   : libX11-common-1.6.3-2.fc23.noarch                                                  16/52 
  Verifying   : jbigkit-libs-2.1-4.fc23.x86_64                                                     17/52 
  Verifying   : perl-4:5.22.2-355.fc23.x86_64                                                      18/52 
  Verifying   : perl-File-Path-2.09-347.fc23.noarch                                                19/52 
  Verifying   : perl-File-Temp-0.23.04-346.fc23.noarch                                             20/52 
  Verifying   : perl-Pod-Simple-1:3.31-1.fc23.noarch                                               21/52 
  Verifying   : perl-Text-Tabs+Wrap-2013.0523-346.fc23.noarch                                      22/52 
  Verifying   : perl-parent-1:0.234-3.fc23.noarch                                                  23/52 
  Verifying   : perl-threads-1:2.02-2.fc23.x86_64                                                  24/52 
  Verifying   : perl-threads-shared-1.48-346.fc23.x86_64                                           25/52 
  Verifying   : perl-Pod-Escapes-1:1.07-348.fc23.noarch                                            26/52 
  Verifying   : perl-libs-4:5.22.2-355.fc23.x86_64                                                 27/52 
  Verifying   : fontconfig-2.11.94-5.fc23.x86_64                                                   28/52 
  Verifying   : fontpackages-filesystem-1.44-14.fc23.noarch                                        29/52 
  Verifying   : libvpx-1.4.0-6.fc23.x86_64                                                         30/52 
  Verifying   : perl-Carp-1.38-1.fc23.noarch                                                       31/52 
  Verifying   : perl-Scalar-List-Utils-2:1.43-1.fc23.x86_64                                        32/52 
  Verifying   : perl-Encode-3:2.80-7.fc23.x86_64                                                   33/52 
  Verifying   : perl-MIME-Base64-3.15-348.fc23.x86_64                                              34/52 
  Verifying   : perl-Getopt-Long-2.49.1-1.fc23.noarch                                              35/52 
  Verifying   : perl-Pod-Usage-4:1.67-3.fc23.noarch                                                36/52 
  Verifying   : perl-Text-ParseWords-3.30-346.fc23.noarch                                          37/52 
  Verifying   : perl-podlators-2.5.3-347.fc23.noarch                                               38/52 
  Verifying   : perl-Term-ANSIColor-4.03-346.fc23.noarch                                           39/52 
  Verifying   : perl-Term-Cap-1.17-1.fc23.noarch                                                   40/52 
  Verifying   : perl-PathTools-3.62-2.fc23.x86_64                                                  41/52 
  Verifying   : libxcb-1.11.1-1.fc23.x86_64                                                        42/52 
  Verifying   : libXau-1.0.8-5.fc23.x86_64                                                         43/52 
  Verifying   : perl-Socket-3:2.024-1.fc23.x86_64                                                  44/52 
  Verifying   : perl-Storable-1:2.53-347.fc23.x86_64                                               45/52 
  Verifying   : perl-Time-HiRes-1.9728-1.fc23.x86_64                                               46/52 
  Verifying   : perl-Unicode-Normalize-1.24-1.fc23.x86_64                                          47/52 
  Verifying   : perl-macros-4:5.22.2-355.fc23.x86_64                                               48/52 
  Verifying   : perl-Pod-Perldoc-3.26-1.fc23.noarch                                                49/52 
  Verifying   : perl-HTTP-Tiny-0.056-4.fc23.noarch                                                 50/52 
  Verifying   : perl-Time-Local-1:1.250-1.fc23.noarch                                              51/52 
  Verifying   : aajohan-comfortaa-fonts-2.004-5.fc23.noarch                                        52/52 

Installed:
  aajohan-comfortaa-fonts.noarch 2.004-5.fc23        fontconfig.x86_64 2.11.94-5.fc23                    
  fontpackages-filesystem.noarch 1.44-14.fc23        gd.x86_64 2.1.1-10.fc23                             
  gperftools-libs.x86_64 2.4-5.fc23                  jbigkit-libs.x86_64 2.1-4.fc23                      
  libX11.x86_64 1.6.3-2.fc23                         libX11-common.noarch 1.6.3-2.fc23                   
  libXau.x86_64 1.0.8-5.fc23                         libXpm.x86_64 3.5.11-4.fc23                         
  libjpeg-turbo.x86_64 1.4.1-2.fc23                  libtiff.x86_64 4.0.4-1.fc23                         
  libunwind.x86_64 1.1-10.fc23                       libvpx.x86_64 1.4.0-6.fc23                          
  libxcb.x86_64 1.11.1-1.fc23                        libxslt.x86_64 1.1.28-11.fc23                       
  make.x86_64 1:4.0-5.1.fc23                         nginx.x86_64 1:1.8.1-3.fc23                         
  nginx-filesystem.noarch 1:1.8.1-3.fc23             nginx-mimetypes.noarch 2.1.45-1.fc23                
  openssl.x86_64 1:1.0.2d-2.fc23                     perl.x86_64 4:5.22.2-355.fc23                       
  perl-Carp.noarch 1.38-1.fc23                       perl-Encode.x86_64 3:2.80-7.fc23                    
  perl-Exporter.noarch 5.72-347.fc23                 perl-File-Path.noarch 2.09-347.fc23                 
  perl-File-Temp.noarch 0.23.04-346.fc23             perl-Getopt-Long.noarch 2.49.1-1.fc23               
  perl-HTTP-Tiny.noarch 0.056-4.fc23                 perl-MIME-Base64.x86_64 3.15-348.fc23               
  perl-PathTools.x86_64 3.62-2.fc23                  perl-Pod-Escapes.noarch 1:1.07-348.fc23             
  perl-Pod-Perldoc.noarch 3.26-1.fc23                perl-Pod-Simple.noarch 1:3.31-1.fc23                
  perl-Pod-Usage.noarch 4:1.67-3.fc23                perl-Scalar-List-Utils.x86_64 2:1.43-1.fc23         
  perl-Socket.x86_64 3:2.024-1.fc23                  perl-Storable.x86_64 1:2.53-347.fc23                
  perl-Term-ANSIColor.noarch 4.03-346.fc23           perl-Term-Cap.noarch 1.17-1.fc23                    
  perl-Text-ParseWords.noarch 3.30-346.fc23          perl-Text-Tabs+Wrap.noarch 2013.0523-346.fc23       
  perl-Time-HiRes.x86_64 1.9728-1.fc23               perl-Time-Local.noarch 1:1.250-1.fc23               
  perl-Unicode-Normalize.x86_64 1.24-1.fc23          perl-constant.noarch 1.33-347.fc23                  
  perl-libs.x86_64 4:5.22.2-355.fc23                 perl-macros.x86_64 4:5.22.2-355.fc23                
  perl-parent.noarch 1:0.234-3.fc23                  perl-podlators.noarch 2.5.3-347.fc23                
  perl-threads.x86_64 1:2.02-2.fc23                  perl-threads-shared.x86_64 1.48-346.fc23            

Complete!
[fedora@ip-172-31-19-227 ~]$ which nginx
/usr/sbin/nginx
```

## Binary Packages Q & A
* How many packages were added?
A: 52 packages. (sudo dnf install nginx)
* How many new files were added?
A: I install the packages around the system time 'Mon Feb 20 07:40:11 2017'
I use `find` to count how many new files were added.
```
[fedora@ip-172-31-19-227 dnf]$ date
Mon Feb 20 09:01:50 UTC 2017
[fedora@ip-172-31-19-227 dnf]$ sudo find / -cmin -100 | grep '\/' -c
find: ‘/proc/9625/task/9625/fd/6’: No such file or directory
find: ‘/proc/9625/task/9625/fdinfo/6’: No such file or directory
find: ‘/proc/9625/fd/5’: No such file or directory
find: ‘/proc/9625/fdinfo/5’: No such file or directory
27490
[fedora@ip-172-31-19-227 dnf]$ sudo find / -cmin -70 | grep '\/' -c
find: ‘/proc/9635/task/9635/fd/6’: No such file or directory
find: ‘/proc/9635/task/9635/fdinfo/6’: No such file or directory
find: ‘/proc/9635/fd/5’: No such file or directory
find: ‘/proc/9635/fdinfo/5’: No such file or directory
24766
```
So when install system create around 27490-24766=2724 files
* Are all added packages necessary to run the software?
A: Yes they are. （infer from this sentence 'Dependencies resolved.'）
* Which version of nginx did you end up with?
A: Version     : 1.8.1 (sudo dnf info nginx)
* Which directories did the software get installed into?
A: /usr/sbin/nginx (which nginx)
* How do you know you didn't get any backdoors installed?
A: Check the file 'dnf.cof', I found 'gpgcheck = 1'.
That means every time `dnf` download package from repo, it will run 'GNU Private Guard' checking, and make sure the resource of this package is safe and vaild.

```
[fedora@ip-172-31-19-227 dnf]$ whereis dnf
dnf: /usr/bin/dnf /etc/dnf /usr/share/man/man8/dnf.8.gz
[fedora@ip-172-31-19-227 dnf]$ ls
dnf.conf  plugins  protected.d
[fedora@ip-172-31-19-227 dnf]$ vi dnf.conf
```
```
[main]
gpgcheck=1
installonly_limit=3
clean_requirements_on_remove=true
```


## Build manually from source

SSH to the second instance。
From the tutorial, find the link of stable nginx source. Copy link.


```
➜  Documents git:(master) ✗ ssh -i p.pem fedora@ec2-52-204-105-92.compute-1.amazonaws.com
The authenticity of host 'ec2-52-204-105-92.compute-1.amazonaws.com (52.204.105.92)' can't be established.
ECDSA key fingerprint is SHA256:lzmOqbZO/3jhhD29OeShFz9aqPnzYj0cNbRHNmTk8SE.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'ec2-52-204-105-92.compute-1.amazonaws.com,52.204.105.92' (ECDSA) to the list of known hosts.
[fedora@ip-172-31-22-54 ~]$ mkdir nginx
[fedora@ip-172-31-22-54 ~]$ cd nginx/
[fedora@ip-172-31-22-54 nginx]$ curl -O http://nginx.org/download/nginx-1.9.9.tar.gz
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  867k  100  867k    0     0   924k      0 --:--:-- --:--:-- --:--:--  926k
[fedora@ip-172-31-22-54 nginx]$ tar xvf nginx-1.9.9.tar.gz 
nginx-1.9.9/
nginx-1.9.9/auto/
nginx-1.9.9/conf/
nginx-1.9.9/contrib/
nginx-1.9.9/src/
nginx-1.9.9/configure
nginx-1.9.9/LICENSE
nginx-1.9.9/README
nginx-1.9.9/html/
nginx-1.9.9/man/
nginx-1.9.9/CHANGES.ru
nginx-1.9.9/CHANGES
nginx-1.9.9/man/nginx.8
nginx-1.9.9/html/50x.html
nginx-1.9.9/html/index.html
nginx-1.9.9/src/core/
nginx-1.9.9/src/event/
nginx-1.9.9/src/http/
nginx-1.9.9/src/mail/
nginx-1.9.9/src/misc/
nginx-1.9.9/src/os/
nginx-1.9.9/src/stream/
nginx-1.9.9/src/stream/ngx_stream_handler.c
nginx-1.9.9/src/stream/ngx_stream.c
nginx-1.9.9/src/stream/ngx_stream.h
nginx-1.9.9/src/stream/ngx_stream_limit_conn_module.c
nginx-1.9.9/src/stream/ngx_stream_access_module.c
nginx-1.9.9/src/stream/ngx_stream_core_module.c
nginx-1.9.9/src/stream/ngx_stream_upstream_hash_module.c
nginx-1.9.9/src/stream/ngx_stream_proxy_module.c
nginx-1.9.9/src/stream/ngx_stream_ssl_module.c
nginx-1.9.9/src/stream/ngx_stream_ssl_module.h
nginx-1.9.9/src/stream/ngx_stream_upstream.c
nginx-1.9.9/src/stream/ngx_stream_upstream.h
nginx-1.9.9/src/stream/ngx_stream_upstream_least_conn_module.c
nginx-1.9.9/src/stream/ngx_stream_upstream_round_robin.c
nginx-1.9.9/src/stream/ngx_stream_upstream_round_robin.h
nginx-1.9.9/src/stream/ngx_stream_upstream_zone_module.c
nginx-1.9.9/src/os/unix/
nginx-1.9.9/src/os/unix/ngx_atomic.h
nginx-1.9.9/src/os/unix/ngx_alloc.c
nginx-1.9.9/src/os/unix/ngx_alloc.h
nginx-1.9.9/src/os/unix/ngx_darwin_config.h
nginx-1.9.9/src/os/unix/ngx_channel.c
nginx-1.9.9/src/os/unix/ngx_channel.h
nginx-1.9.9/src/os/unix/ngx_daemon.c
nginx-1.9.9/src/os/unix/ngx_darwin.h
nginx-1.9.9/src/os/unix/ngx_darwin_sendfile_chain.c
nginx-1.9.9/src/os/unix/ngx_darwin_init.c
nginx-1.9.9/src/os/unix/ngx_file_aio_read.c
nginx-1.9.9/src/os/unix/ngx_errno.c
nginx-1.9.9/src/os/unix/ngx_errno.h
nginx-1.9.9/src/os/unix/ngx_freebsd.h
nginx-1.9.9/src/os/unix/ngx_files.c
nginx-1.9.9/src/os/unix/ngx_files.h
nginx-1.9.9/src/os/unix/ngx_gcc_atomic_amd64.h
nginx-1.9.9/src/os/unix/ngx_freebsd_config.h
nginx-1.9.9/src/os/unix/ngx_freebsd_init.c
nginx-1.9.9/src/os/unix/ngx_linux_config.h
nginx-1.9.9/src/os/unix/ngx_linux.h
nginx-1.9.9/src/os/unix/ngx_freebsd_sendfile_chain.c
nginx-1.9.9/src/os/unix/ngx_gcc_atomic_ppc.h
nginx-1.9.9/src/os/unix/ngx_gcc_atomic_sparc64.h
nginx-1.9.9/src/os/unix/ngx_gcc_atomic_x86.h
nginx-1.9.9/src/os/unix/ngx_linux_sendfile_chain.c
nginx-1.9.9/src/os/unix/ngx_linux_aio_read.c
nginx-1.9.9/src/os/unix/ngx_linux_init.c
nginx-1.9.9/src/os/unix/ngx_posix_config.h
nginx-1.9.9/src/os/unix/ngx_os.h
nginx-1.9.9/src/os/unix/ngx_solaris_config.h
nginx-1.9.9/src/os/unix/ngx_posix_init.c
nginx-1.9.9/src/os/unix/ngx_process.c
nginx-1.9.9/src/os/unix/ngx_process.h
nginx-1.9.9/src/os/unix/ngx_process_cycle.c
nginx-1.9.9/src/os/unix/ngx_process_cycle.h
nginx-1.9.9/src/os/unix/ngx_readv_chain.c
nginx-1.9.9/src/os/unix/ngx_recv.c
nginx-1.9.9/src/os/unix/ngx_send.c
nginx-1.9.9/src/os/unix/ngx_setaffinity.c
nginx-1.9.9/src/os/unix/ngx_setaffinity.h
nginx-1.9.9/src/os/unix/ngx_setproctitle.c
nginx-1.9.9/src/os/unix/ngx_setproctitle.h
nginx-1.9.9/src/os/unix/ngx_shmem.c
nginx-1.9.9/src/os/unix/ngx_shmem.h
nginx-1.9.9/src/os/unix/ngx_socket.c
nginx-1.9.9/src/os/unix/ngx_socket.h
nginx-1.9.9/src/os/unix/ngx_solaris.h
nginx-1.9.9/src/os/unix/ngx_sunpro_atomic_sparc64.h
nginx-1.9.9/src/os/unix/ngx_solaris_init.c
nginx-1.9.9/src/os/unix/ngx_sunpro_amd64.il
nginx-1.9.9/src/os/unix/ngx_solaris_sendfilev_chain.c
nginx-1.9.9/src/os/unix/ngx_sunpro_sparc64.il
nginx-1.9.9/src/os/unix/ngx_sunpro_x86.il
nginx-1.9.9/src/os/unix/ngx_thread.h
nginx-1.9.9/src/os/unix/ngx_thread_cond.c
nginx-1.9.9/src/os/unix/ngx_thread_id.c
nginx-1.9.9/src/os/unix/ngx_thread_mutex.c
nginx-1.9.9/src/os/unix/ngx_time.c
nginx-1.9.9/src/os/unix/ngx_time.h
nginx-1.9.9/src/os/unix/ngx_udp_recv.c
nginx-1.9.9/src/os/unix/ngx_user.c
nginx-1.9.9/src/os/unix/ngx_user.h
nginx-1.9.9/src/os/unix/ngx_writev_chain.c
nginx-1.9.9/src/misc/ngx_google_perftools_module.c
nginx-1.9.9/src/misc/ngx_cpp_test_module.cpp
nginx-1.9.9/src/mail/ngx_mail_handler.c
nginx-1.9.9/src/mail/ngx_mail.c
nginx-1.9.9/src/mail/ngx_mail.h
nginx-1.9.9/src/mail/ngx_mail_auth_http_module.c
nginx-1.9.9/src/mail/ngx_mail_core_module.c
nginx-1.9.9/src/mail/ngx_mail_imap_handler.c
nginx-1.9.9/src/mail/ngx_mail_imap_module.c
nginx-1.9.9/src/mail/ngx_mail_imap_module.h
nginx-1.9.9/src/mail/ngx_mail_parse.c
nginx-1.9.9/src/mail/ngx_mail_pop3_handler.c
nginx-1.9.9/src/mail/ngx_mail_pop3_module.c
nginx-1.9.9/src/mail/ngx_mail_pop3_module.h
nginx-1.9.9/src/mail/ngx_mail_proxy_module.c
nginx-1.9.9/src/mail/ngx_mail_smtp_handler.c
nginx-1.9.9/src/mail/ngx_mail_smtp_module.c
nginx-1.9.9/src/mail/ngx_mail_smtp_module.h
nginx-1.9.9/src/mail/ngx_mail_ssl_module.c
nginx-1.9.9/src/mail/ngx_mail_ssl_module.h
nginx-1.9.9/src/http/modules/
nginx-1.9.9/src/http/ngx_http_cache.h
nginx-1.9.9/src/http/ngx_http.c
nginx-1.9.9/src/http/ngx_http.h
nginx-1.9.9/src/http/ngx_http_core_module.c
nginx-1.9.9/src/http/ngx_http_config.h
nginx-1.9.9/src/http/ngx_http_postpone_filter_module.c
nginx-1.9.9/src/http/ngx_http_copy_filter_module.c
nginx-1.9.9/src/http/ngx_http_core_module.h
nginx-1.9.9/src/http/ngx_http_file_cache.c
nginx-1.9.9/src/http/ngx_http_header_filter_module.c
nginx-1.9.9/src/http/ngx_http_parse.c
nginx-1.9.9/src/http/ngx_http_special_response.c
nginx-1.9.9/src/http/ngx_http_request.c
nginx-1.9.9/src/http/ngx_http_request.h
nginx-1.9.9/src/http/ngx_http_request_body.c
nginx-1.9.9/src/http/ngx_http_script.c
nginx-1.9.9/src/http/ngx_http_script.h
nginx-1.9.9/src/http/ngx_http_variables.c
nginx-1.9.9/src/http/ngx_http_upstream.c
nginx-1.9.9/src/http/ngx_http_upstream.h
nginx-1.9.9/src/http/v2/
nginx-1.9.9/src/http/ngx_http_upstream_round_robin.c
nginx-1.9.9/src/http/ngx_http_upstream_round_robin.h
nginx-1.9.9/src/http/ngx_http_variables.h
nginx-1.9.9/src/http/ngx_http_write_filter_module.c
nginx-1.9.9/src/http/v2/ngx_http_v2_module.c
nginx-1.9.9/src/http/v2/ngx_http_v2.c
nginx-1.9.9/src/http/v2/ngx_http_v2.h
nginx-1.9.9/src/http/v2/ngx_http_v2_filter_module.c
nginx-1.9.9/src/http/v2/ngx_http_v2_huff_decode.c
nginx-1.9.9/src/http/v2/ngx_http_v2_huff_encode.c
nginx-1.9.9/src/http/v2/ngx_http_v2_module.h
nginx-1.9.9/src/http/v2/ngx_http_v2_table.c
nginx-1.9.9/src/http/modules/ngx_http_addition_filter_module.c
nginx-1.9.9/src/http/modules/ngx_http_access_module.c
nginx-1.9.9/src/http/modules/ngx_http_charset_filter_module.c
nginx-1.9.9/src/http/modules/ngx_http_auth_basic_module.c
nginx-1.9.9/src/http/modules/ngx_http_auth_request_module.c
nginx-1.9.9/src/http/modules/ngx_http_autoindex_module.c
nginx-1.9.9/src/http/modules/ngx_http_browser_module.c
nginx-1.9.9/src/http/modules/ngx_http_not_modified_filter_module.c
nginx-1.9.9/src/http/modules/ngx_http_chunked_filter_module.c
nginx-1.9.9/src/http/modules/ngx_http_dav_module.c
nginx-1.9.9/src/http/modules/ngx_http_degradation_module.c
nginx-1.9.9/src/http/modules/ngx_http_empty_gif_module.c
nginx-1.9.9/src/http/modules/ngx_http_fastcgi_module.c
nginx-1.9.9/src/http/modules/ngx_http_flv_module.c
nginx-1.9.9/src/http/modules/ngx_http_geo_module.c
nginx-1.9.9/src/http/modules/ngx_http_geoip_module.c
nginx-1.9.9/src/http/modules/ngx_http_gunzip_filter_module.c
nginx-1.9.9/src/http/modules/ngx_http_gzip_filter_module.c
nginx-1.9.9/src/http/modules/ngx_http_gzip_static_module.c
nginx-1.9.9/src/http/modules/ngx_http_headers_filter_module.c
nginx-1.9.9/src/http/modules/ngx_http_image_filter_module.c
nginx-1.9.9/src/http/modules/ngx_http_index_module.c
nginx-1.9.9/src/http/modules/ngx_http_limit_conn_module.c
nginx-1.9.9/src/http/modules/ngx_http_limit_req_module.c
nginx-1.9.9/src/http/modules/ngx_http_log_module.c
nginx-1.9.9/src/http/modules/ngx_http_map_module.c
nginx-1.9.9/src/http/modules/ngx_http_memcached_module.c
nginx-1.9.9/src/http/modules/ngx_http_mp4_module.c
nginx-1.9.9/src/http/modules/ngx_http_random_index_module.c
nginx-1.9.9/src/http/modules/ngx_http_proxy_module.c
nginx-1.9.9/src/http/modules/ngx_http_upstream_ip_hash_module.c
nginx-1.9.9/src/http/modules/ngx_http_range_filter_module.c
nginx-1.9.9/src/http/modules/ngx_http_realip_module.c
nginx-1.9.9/src/http/modules/ngx_http_referer_module.c
nginx-1.9.9/src/http/modules/ngx_http_rewrite_module.c
nginx-1.9.9/src/http/modules/ngx_http_scgi_module.c
nginx-1.9.9/src/http/modules/ngx_http_secure_link_module.c
nginx-1.9.9/src/http/modules/ngx_http_slice_filter_module.c
nginx-1.9.9/src/http/modules/ngx_http_split_clients_module.c
nginx-1.9.9/src/http/modules/perl/
nginx-1.9.9/src/http/modules/ngx_http_ssi_filter_module.c
nginx-1.9.9/src/http/modules/ngx_http_ssi_filter_module.h
nginx-1.9.9/src/http/modules/ngx_http_ssl_module.c
nginx-1.9.9/src/http/modules/ngx_http_ssl_module.h
nginx-1.9.9/src/http/modules/ngx_http_static_module.c
nginx-1.9.9/src/http/modules/ngx_http_stub_status_module.c
nginx-1.9.9/src/http/modules/ngx_http_sub_filter_module.c
nginx-1.9.9/src/http/modules/ngx_http_upstream_hash_module.c
nginx-1.9.9/src/http/modules/ngx_http_xslt_filter_module.c
nginx-1.9.9/src/http/modules/ngx_http_upstream_keepalive_module.c
nginx-1.9.9/src/http/modules/ngx_http_upstream_least_conn_module.c
nginx-1.9.9/src/http/modules/ngx_http_upstream_zone_module.c
nginx-1.9.9/src/http/modules/ngx_http_uwsgi_module.c
nginx-1.9.9/src/http/modules/ngx_http_userid_filter_module.c
nginx-1.9.9/src/http/modules/perl/Makefile.PL
nginx-1.9.9/src/http/modules/perl/nginx.pm
nginx-1.9.9/src/http/modules/perl/nginx.xs
nginx-1.9.9/src/http/modules/perl/typemap
nginx-1.9.9/src/http/modules/perl/ngx_http_perl_module.c
nginx-1.9.9/src/http/modules/perl/ngx_http_perl_module.h
nginx-1.9.9/src/event/modules/
nginx-1.9.9/src/event/ngx_event_accept.c
nginx-1.9.9/src/event/ngx_event.c
nginx-1.9.9/src/event/ngx_event.h
nginx-1.9.9/src/event/ngx_event_openssl_stapling.c
nginx-1.9.9/src/event/ngx_event_connect.c
nginx-1.9.9/src/event/ngx_event_connect.h
nginx-1.9.9/src/event/ngx_event_openssl.c
nginx-1.9.9/src/event/ngx_event_openssl.h
nginx-1.9.9/src/event/ngx_event_pipe.c
nginx-1.9.9/src/event/ngx_event_pipe.h
nginx-1.9.9/src/event/ngx_event_posted.c
nginx-1.9.9/src/event/ngx_event_posted.h
nginx-1.9.9/src/event/ngx_event_timer.c
nginx-1.9.9/src/event/ngx_event_timer.h
nginx-1.9.9/src/event/modules/ngx_win32_select_module.c
nginx-1.9.9/src/event/modules/ngx_devpoll_module.c
nginx-1.9.9/src/event/modules/ngx_epoll_module.c
nginx-1.9.9/src/event/modules/ngx_eventport_module.c
nginx-1.9.9/src/event/modules/ngx_kqueue_module.c
nginx-1.9.9/src/event/modules/ngx_poll_module.c
nginx-1.9.9/src/event/modules/ngx_select_module.c
nginx-1.9.9/src/core/ngx_array.c
nginx-1.9.9/src/core/nginx.c
nginx-1.9.9/src/core/nginx.h
nginx-1.9.9/src/core/ngx_conf_file.c
nginx-1.9.9/src/core/ngx_array.h
nginx-1.9.9/src/core/ngx_buf.c
nginx-1.9.9/src/core/ngx_buf.h
nginx-1.9.9/src/core/ngx_connection.c
nginx-1.9.9/src/core/ngx_conf_file.h
nginx-1.9.9/src/core/ngx_config.h
nginx-1.9.9/src/core/ngx_murmurhash.c
nginx-1.9.9/src/core/ngx_file.c
nginx-1.9.9/src/core/ngx_connection.h
nginx-1.9.9/src/core/ngx_core.h
nginx-1.9.9/src/core/ngx_cpuinfo.c
nginx-1.9.9/src/core/ngx_crc.h
nginx-1.9.9/src/core/ngx_crc32.c
nginx-1.9.9/src/core/ngx_crc32.h
nginx-1.9.9/src/core/ngx_crypt.c
nginx-1.9.9/src/core/ngx_crypt.h
nginx-1.9.9/src/core/ngx_cycle.c
nginx-1.9.9/src/core/ngx_cycle.h
nginx-1.9.9/src/core/ngx_file.h
nginx-1.9.9/src/core/ngx_hash.c
nginx-1.9.9/src/core/ngx_hash.h
nginx-1.9.9/src/core/ngx_inet.c
nginx-1.9.9/src/core/ngx_inet.h
nginx-1.9.9/src/core/ngx_list.c
nginx-1.9.9/src/core/ngx_list.h
nginx-1.9.9/src/core/ngx_log.c
nginx-1.9.9/src/core/ngx_log.h
nginx-1.9.9/src/core/ngx_md5.c
nginx-1.9.9/src/core/ngx_md5.h
nginx-1.9.9/src/core/ngx_open_file_cache.c
nginx-1.9.9/src/core/ngx_murmurhash.h
nginx-1.9.9/src/core/ngx_thread_pool.c
nginx-1.9.9/src/core/ngx_open_file_cache.h
nginx-1.9.9/src/core/ngx_output_chain.c
nginx-1.9.9/src/core/ngx_palloc.c
nginx-1.9.9/src/core/ngx_palloc.h
nginx-1.9.9/src/core/ngx_parse.c
nginx-1.9.9/src/core/ngx_parse.h
nginx-1.9.9/src/core/ngx_parse_time.c
nginx-1.9.9/src/core/ngx_string.c
nginx-1.9.9/src/core/ngx_parse_time.h
nginx-1.9.9/src/core/ngx_proxy_protocol.c
nginx-1.9.9/src/core/ngx_proxy_protocol.h
nginx-1.9.9/src/core/ngx_queue.c
nginx-1.9.9/src/core/ngx_queue.h
nginx-1.9.9/src/core/ngx_radix_tree.c
nginx-1.9.9/src/core/ngx_radix_tree.h
nginx-1.9.9/src/core/ngx_rbtree.c
nginx-1.9.9/src/core/ngx_rbtree.h
nginx-1.9.9/src/core/ngx_regex.c
nginx-1.9.9/src/core/ngx_regex.h
nginx-1.9.9/src/core/ngx_resolver.c
nginx-1.9.9/src/core/ngx_resolver.h
nginx-1.9.9/src/core/ngx_rwlock.c
nginx-1.9.9/src/core/ngx_rwlock.h
nginx-1.9.9/src/core/ngx_sha1.h
nginx-1.9.9/src/core/ngx_shmtx.c
nginx-1.9.9/src/core/ngx_shmtx.h
nginx-1.9.9/src/core/ngx_slab.c
nginx-1.9.9/src/core/ngx_slab.h
nginx-1.9.9/src/core/ngx_spinlock.c
nginx-1.9.9/src/core/ngx_string.h
nginx-1.9.9/src/core/ngx_syslog.c
nginx-1.9.9/src/core/ngx_syslog.h
nginx-1.9.9/src/core/ngx_thread_pool.h
nginx-1.9.9/src/core/ngx_times.c
nginx-1.9.9/src/core/ngx_times.h
nginx-1.9.9/contrib/geo2nginx.pl
nginx-1.9.9/contrib/README
nginx-1.9.9/contrib/unicode2nginx/
nginx-1.9.9/contrib/vim/
nginx-1.9.9/contrib/vim/ftdetect/
nginx-1.9.9/contrib/vim/indent/
nginx-1.9.9/contrib/vim/syntax/
nginx-1.9.9/contrib/vim/syntax/nginx.vim
nginx-1.9.9/contrib/vim/indent/nginx.vim
nginx-1.9.9/contrib/vim/ftdetect/nginx.vim
nginx-1.9.9/contrib/unicode2nginx/koi-utf
nginx-1.9.9/contrib/unicode2nginx/win-utf
nginx-1.9.9/contrib/unicode2nginx/unicode-to-nginx.pl
nginx-1.9.9/conf/fastcgi.conf
nginx-1.9.9/conf/fastcgi_params
nginx-1.9.9/conf/koi-utf
nginx-1.9.9/conf/koi-win
nginx-1.9.9/conf/mime.types
nginx-1.9.9/conf/nginx.conf
nginx-1.9.9/conf/scgi_params
nginx-1.9.9/conf/uwsgi_params
nginx-1.9.9/conf/win-utf
nginx-1.9.9/auto/cc/
nginx-1.9.9/auto/have_headers
nginx-1.9.9/auto/define
nginx-1.9.9/auto/endianness
nginx-1.9.9/auto/feature
nginx-1.9.9/auto/have
nginx-1.9.9/auto/lib/
nginx-1.9.9/auto/os/
nginx-1.9.9/auto/headers
nginx-1.9.9/auto/include
nginx-1.9.9/auto/init
nginx-1.9.9/auto/install
nginx-1.9.9/auto/types/
nginx-1.9.9/auto/make
nginx-1.9.9/auto/modules
nginx-1.9.9/auto/nohave
nginx-1.9.9/auto/options
nginx-1.9.9/auto/sources
nginx-1.9.9/auto/stubs
nginx-1.9.9/auto/summary
nginx-1.9.9/auto/threads
nginx-1.9.9/auto/unix
nginx-1.9.9/auto/types/uintptr_t
nginx-1.9.9/auto/types/sizeof
nginx-1.9.9/auto/types/typedef
nginx-1.9.9/auto/types/value
nginx-1.9.9/auto/os/conf
nginx-1.9.9/auto/os/darwin
nginx-1.9.9/auto/os/freebsd
nginx-1.9.9/auto/os/linux
nginx-1.9.9/auto/os/solaris
nginx-1.9.9/auto/os/win32
nginx-1.9.9/auto/lib/geoip/
nginx-1.9.9/auto/lib/conf
nginx-1.9.9/auto/lib/google-perftools/
nginx-1.9.9/auto/lib/libatomic/
nginx-1.9.9/auto/lib/libgd/
nginx-1.9.9/auto/lib/libxslt/
nginx-1.9.9/auto/lib/md5/
nginx-1.9.9/auto/lib/make
nginx-1.9.9/auto/lib/openssl/
nginx-1.9.9/auto/lib/pcre/
nginx-1.9.9/auto/lib/perl/
nginx-1.9.9/auto/lib/sha1/
nginx-1.9.9/auto/lib/zlib/
nginx-1.9.9/auto/lib/test
nginx-1.9.9/auto/lib/zlib/makefile.bcc
nginx-1.9.9/auto/lib/zlib/conf
nginx-1.9.9/auto/lib/zlib/make
nginx-1.9.9/auto/lib/zlib/makefile.msvc
nginx-1.9.9/auto/lib/zlib/makefile.owc
nginx-1.9.9/auto/lib/sha1/makefile.bcc
nginx-1.9.9/auto/lib/sha1/conf
nginx-1.9.9/auto/lib/sha1/make
nginx-1.9.9/auto/lib/sha1/makefile.msvc
nginx-1.9.9/auto/lib/sha1/makefile.owc
nginx-1.9.9/auto/lib/perl/conf
nginx-1.9.9/auto/lib/perl/make
nginx-1.9.9/auto/lib/pcre/makefile.bcc
nginx-1.9.9/auto/lib/pcre/conf
nginx-1.9.9/auto/lib/pcre/make
nginx-1.9.9/auto/lib/pcre/makefile.msvc
nginx-1.9.9/auto/lib/pcre/makefile.owc
nginx-1.9.9/auto/lib/openssl/makefile.bcc
nginx-1.9.9/auto/lib/openssl/conf
nginx-1.9.9/auto/lib/openssl/make
nginx-1.9.9/auto/lib/openssl/makefile.msvc
nginx-1.9.9/auto/lib/md5/makefile.bcc
nginx-1.9.9/auto/lib/md5/conf
nginx-1.9.9/auto/lib/md5/make
nginx-1.9.9/auto/lib/md5/makefile.msvc
nginx-1.9.9/auto/lib/md5/makefile.owc
nginx-1.9.9/auto/lib/libxslt/conf
nginx-1.9.9/auto/lib/libgd/conf
nginx-1.9.9/auto/lib/libatomic/conf
nginx-1.9.9/auto/lib/libatomic/make
nginx-1.9.9/auto/lib/google-perftools/conf
nginx-1.9.9/auto/lib/geoip/conf
nginx-1.9.9/auto/cc/clang
nginx-1.9.9/auto/cc/acc
nginx-1.9.9/auto/cc/bcc
nginx-1.9.9/auto/cc/ccc
nginx-1.9.9/auto/cc/conf
nginx-1.9.9/auto/cc/gcc
nginx-1.9.9/auto/cc/icc
nginx-1.9.9/auto/cc/msvc
nginx-1.9.9/auto/cc/name
nginx-1.9.9/auto/cc/owc
nginx-1.9.9/auto/cc/sunc
[fedora@ip-172-31-22-54 nginx]$ rm -r nginx-1.9.9.tar.gz 
[fedora@ip-172-31-22-54 nginx]$ ls
nginx-1.9.9
[fedora@ip-172-31-22-54 nginx]$ cd nginx-1.9.9/
[fedora@ip-172-31-22-54 nginx-1.9.9]$ ls | wc -c
75
```
Notice: After extracting the source, there are 75 files added.

```
[fedora@ip-172-31-22-54 nginx-1.9.9]$ ./configure
checking for OS
 + Linux 4.2.3-300.fc23.x86_64 x86_64
checking for C compiler ... not found

./configure: error: C compiler cc is not found
```
System need C compiler.

```
[fedora@ip-172-31-22-54 nginx-1.9.9]$ sudo dnf install gcc
Last metadata expiration check performed 2:54:43 ago on Mon Feb 20 06:50:08 2017.
Dependencies resolved.
=========================================================================================================
 Package                     Arch                Version                      Repository            Size
=========================================================================================================
Installing:
 binutils                    x86_64              2.25-17.fc23                 updates              5.6 M
 cpp                         x86_64              5.3.1-6.fc23                 updates              8.3 M
 gcc                         x86_64              5.3.1-6.fc23                 updates               19 M
 glibc-devel                 x86_64              2.22-3.fc23                  fedora               909 k
 glibc-headers               x86_64              2.22-3.fc23                  fedora               493 k
 isl                         x86_64              0.14-4.fc23                  fedora               490 k
 kernel-headers              x86_64              4.8.13-100.fc23              updates              1.0 M
 libmpc                      x86_64              1.0.2-4.fc23                 fedora                55 k
 mpfr                        x86_64              3.1.3-2.fc23                 updates              214 k
Upgrading:
 libgcc                      x86_64              5.3.1-6.fc23                 updates               92 k
 libgomp                     x86_64              5.3.1-6.fc23                 updates              156 k

Transaction Summary
=========================================================================================================
Install  9 Packages
Upgrade  2 Packages

Total download size: 36 M
Is this ok [y/N]: y
Downloading Packages:
(1/11): cpp-5.3.1-6.fc23.x86_64.rpm                                      9.3 MB/s | 8.3 MB     00:00    
(2/11): libmpc-1.0.2-4.fc23.x86_64.rpm                                    61 kB/s |  55 kB     00:00    
(3/11): mpfr-3.1.3-2.fc23.x86_64.rpm                                     3.2 MB/s | 214 kB     00:00    
(4/11): gcc-5.3.1-6.fc23.x86_64.rpm                                       10 MB/s |  19 MB     00:01    
(5/11): binutils-2.25-17.fc23.x86_64.rpm                                 5.0 MB/s | 5.6 MB     00:01    
(6/11): glibc-devel-2.22-3.fc23.x86_64.rpm                               815 kB/s | 909 kB     00:01    
(7/11): kernel-headers-4.8.13-100.fc23.x86_64.rpm                        7.2 MB/s | 1.0 MB     00:00    
(8/11): libgcc-5.1.1-4.fc23_5.3.1-6.fc23.x86_64.drpm                     481 kB/s |  35 kB     00:00    
(9/11): libgomp-5.3.1-6.fc23.x86_64.rpm                                  2.3 MB/s | 156 kB     00:00    
(10/11): isl-0.14-4.fc23.x86_64.rpm                                      602 kB/s | 490 kB     00:00    
(11/11): glibc-headers-2.22-3.fc23.x86_64.rpm                            654 kB/s | 493 kB     00:00    
[DRPM] libgcc-5.1.1-4.fc23_5.3.1-6.fc23.x86_64.drpm: done                                               
---------------------------------------------------------------------------------------------------------
Total                                                                     11 MB/s |  36 MB     00:03     
Delta RPMs reduced 36.4 MB of updates to 36.4 MB (0.1% saved)
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Installing  : mpfr-3.1.3-2.fc23.x86_64                                                            1/13 
  Installing  : libmpc-1.0.2-4.fc23.x86_64                                                          2/13 
  Installing  : cpp-5.3.1-6.fc23.x86_64                                                             3/13 
  Upgrading   : libgomp-5.3.1-6.fc23.x86_64                                                         4/13 
  Upgrading   : libgcc-5.3.1-6.fc23.x86_64                                                          5/13 
  Installing  : kernel-headers-4.8.13-100.fc23.x86_64                                               6/13 
  Installing  : glibc-headers-2.22-3.fc23.x86_64                                                    7/13 
  Installing  : glibc-devel-2.22-3.fc23.x86_64                                                      8/13 
  Installing  : isl-0.14-4.fc23.x86_64                                                              9/13 
  Installing  : binutils-2.25-17.fc23.x86_64                                                       10/13 
  Installing  : gcc-5.3.1-6.fc23.x86_64                                                            11/13 
  Cleanup     : libgomp-5.1.1-4.fc23.x86_64                                                        12/13 
  Cleanup     : libgcc-5.1.1-4.fc23.x86_64                                                         13/13 
  Verifying   : gcc-5.3.1-6.fc23.x86_64                                                             1/13 
  Verifying   : cpp-5.3.1-6.fc23.x86_64                                                             2/13 
  Verifying   : libmpc-1.0.2-4.fc23.x86_64                                                          3/13 
  Verifying   : mpfr-3.1.3-2.fc23.x86_64                                                            4/13 
  Verifying   : binutils-2.25-17.fc23.x86_64                                                        5/13 
  Verifying   : glibc-devel-2.22-3.fc23.x86_64                                                      6/13 
  Verifying   : isl-0.14-4.fc23.x86_64                                                              7/13 
  Verifying   : glibc-headers-2.22-3.fc23.x86_64                                                    8/13 
  Verifying   : kernel-headers-4.8.13-100.fc23.x86_64                                               9/13 
  Verifying   : libgcc-5.3.1-6.fc23.x86_64                                                         10/13 
  Verifying   : libgomp-5.3.1-6.fc23.x86_64                                                        11/13 
  Verifying   : libgomp-5.1.1-4.fc23.x86_64                                                        12/13 
  Verifying   : libgcc-5.1.1-4.fc23.x86_64                                                         13/13 

Installed:
  binutils.x86_64 2.25-17.fc23            cpp.x86_64 5.3.1-6.fc23            gcc.x86_64 5.3.1-6.fc23   
  glibc-devel.x86_64 2.22-3.fc23          glibc-headers.x86_64 2.22-3.fc23   isl.x86_64 0.14-4.fc23    
  kernel-headers.x86_64 4.8.13-100.fc23   libmpc.x86_64 1.0.2-4.fc23         mpfr.x86_64 3.1.3-2.fc23  

Upgraded:
  libgcc.x86_64 5.3.1-6.fc23                         libgomp.x86_64 5.3.1-6.fc23                        

Complete!

```

```
[fedora@ip-172-31-22-54 nginx-1.9.9]$ ./configure
checking for OS
 + Linux 4.2.3-300.fc23.x86_64 x86_64
checking for C compiler ... found
 + using GNU C compiler
 + gcc version: 5.3.1 20160406 (Red Hat 5.3.1-6) (GCC) 
checking for gcc -pipe switch ... found
checking for gcc builtin atomic operations ... found
checking for C99 variadic macros ... found
checking for gcc variadic macros ... found
checking for unistd.h ... found
checking for inttypes.h ... found
checking for limits.h ... found
checking for sys/filio.h ... not found
checking for sys/param.h ... found
checking for sys/mount.h ... found
checking for sys/statvfs.h ... found
checking for crypt.h ... found
checking for Linux specific features
checking for epoll ... found
checking for EPOLLRDHUP ... found
checking for O_PATH ... found
checking for sendfile() ... found
checking for sendfile64() ... found
checking for sys/prctl.h ... found
checking for prctl(PR_SET_DUMPABLE) ... found
checking for sched_setaffinity() ... found
checking for crypt_r() ... found
checking for sys/vfs.h ... found
checking for nobody group ... found
checking for poll() ... found
checking for /dev/poll ... not found
checking for kqueue ... not found
checking for crypt() ... not found
checking for crypt() in libcrypt ... found
checking for F_READAHEAD ... not found
checking for posix_fadvise() ... found
checking for O_DIRECT ... found
checking for F_NOCACHE ... not found
checking for directio() ... not found
checking for statfs() ... found
checking for statvfs() ... found
checking for dlopen() ... not found
checking for dlopen() in libdl ... found
checking for sched_yield() ... found
checking for SO_SETFIB ... not found
checking for SO_REUSEPORT ... found
checking for SO_ACCEPTFILTER ... not found
checking for TCP_DEFER_ACCEPT ... found
checking for TCP_KEEPIDLE ... found
checking for TCP_FASTOPEN ... found
checking for TCP_INFO ... found
checking for accept4() ... found
checking for eventfd() ... found
checking for int size ... 4 bytes
checking for long size ... 8 bytes
checking for long long size ... 8 bytes
checking for void * size ... 8 bytes
checking for uint64_t ... found
checking for sig_atomic_t ... found
checking for sig_atomic_t size ... 4 bytes
checking for socklen_t ... found
checking for in_addr_t ... found
checking for in_port_t ... found
checking for rlim_t ... found
checking for uintptr_t ... uintptr_t found
checking for system byte ordering ... little endian
checking for size_t size ... 8 bytes
checking for off_t size ... 8 bytes
checking for time_t size ... 8 bytes
checking for setproctitle() ... not found
checking for pread() ... found
checking for pwrite() ... found
checking for pwritev() ... found
checking for sys_nerr ... found
checking for localtime_r() ... found
checking for posix_memalign() ... found
checking for memalign() ... found
checking for mmap(MAP_ANON|MAP_SHARED) ... found
checking for mmap("/dev/zero", MAP_SHARED) ... found
checking for System V shared memory ... found
checking for POSIX semaphores ... not found
checking for POSIX semaphores in libpthread ... found
checking for struct msghdr.msg_control ... found
checking for ioctl(FIONBIO) ... found
checking for struct tm.tm_gmtoff ... found
checking for struct dirent.d_namlen ... not found
checking for struct dirent.d_type ... found
checking for sysconf(_SC_NPROCESSORS_ONLN) ... found
checking for openat(), fstatat() ... found
checking for getaddrinfo() ... found
checking for PCRE library ... not found
checking for PCRE library in /usr/local/ ... not found
checking for PCRE library in /usr/include/pcre/ ... not found
checking for PCRE library in /usr/pkg/ ... not found
checking for PCRE library in /opt/local/ ... not found

./configure: error: the HTTP rewrite module requires the PCRE library.
You can either disable the module by using --without-http_rewrite_module
option, or install the PCRE library into the system, or build the PCRE library
statically from the source with nginx by using --with-pcre=<path> option.
```

System need `make` package

```
[fedora@ip-172-31-22-54 nginx-1.9.9]$ make
-bash: make: command not found
[fedora@ip-172-31-22-54 nginx-1.9.9]$ sudo dnf install make
Last metadata expiration check performed 0:01:37 ago on Mon Feb 20 09:50:49 2017.
Dependencies resolved.
=========================================================================================================
 Package              Arch                   Version                        Repository              Size
=========================================================================================================
Installing:
 make                 x86_64                 1:4.0-5.1.fc23                 fedora                 449 k

Transaction Summary
=========================================================================================================
Install  1 Package

Total download size: 449 k
Installed size: 1.2 M
Is this ok [y/N]: y
Downloading Packages:
make-4.0-5.1.fc23.x86_64.rpm                                             4.7 MB/s | 449 kB     00:00    
---------------------------------------------------------------------------------------------------------
Total                                                                    733 kB/s | 449 kB     00:00     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Installing  : make-1:4.0-5.1.fc23.x86_64                                                           1/1 
  Verifying   : make-1:4.0-5.1.fc23.x86_64                                                           1/1 

Installed:
  make.x86_64 1:4.0-5.1.fc23                                                                             

Complete!
[fedora@ip-172-31-22-54 nginx-1.9.9]$ ./configure --without-http_rewrite_module --without-http_gzip_module
checking for OS
 + Linux 4.2.3-300.fc23.x86_64 x86_64
checking for C compiler ... found
 + using GNU C compiler
 + gcc version: 5.3.1 20160406 (Red Hat 5.3.1-6) (GCC) 
checking for gcc -pipe switch ... found
checking for gcc builtin atomic operations ... found
checking for C99 variadic macros ... found
checking for gcc variadic macros ... found
checking for unistd.h ... found
checking for inttypes.h ... found
checking for limits.h ... found
checking for sys/filio.h ... not found
checking for sys/param.h ... found
checking for sys/mount.h ... found
checking for sys/statvfs.h ... found
checking for crypt.h ... found
checking for Linux specific features
checking for epoll ... found
checking for EPOLLRDHUP ... found
checking for O_PATH ... found
checking for sendfile() ... found
checking for sendfile64() ... found
checking for sys/prctl.h ... found
checking for prctl(PR_SET_DUMPABLE) ... found
checking for sched_setaffinity() ... found
checking for crypt_r() ... found
checking for sys/vfs.h ... found
checking for nobody group ... found
checking for poll() ... found
checking for /dev/poll ... not found
checking for kqueue ... not found
checking for crypt() ... not found
checking for crypt() in libcrypt ... found
checking for F_READAHEAD ... not found
checking for posix_fadvise() ... found
checking for O_DIRECT ... found
checking for F_NOCACHE ... not found
checking for directio() ... not found
checking for statfs() ... found
checking for statvfs() ... found
checking for dlopen() ... not found
checking for dlopen() in libdl ... found
checking for sched_yield() ... found
checking for SO_SETFIB ... not found
checking for SO_REUSEPORT ... found
checking for SO_ACCEPTFILTER ... not found
checking for TCP_DEFER_ACCEPT ... found
checking for TCP_KEEPIDLE ... found
checking for TCP_FASTOPEN ... found
checking for TCP_INFO ... found
checking for accept4() ... found
checking for eventfd() ... found
checking for int size ... 4 bytes
checking for long size ... 8 bytes
checking for long long size ... 8 bytes
checking for void * size ... 8 bytes
checking for uint64_t ... found
checking for sig_atomic_t ... found
checking for sig_atomic_t size ... 4 bytes
checking for socklen_t ... found
checking for in_addr_t ... found
checking for in_port_t ... found
checking for rlim_t ... found
checking for uintptr_t ... uintptr_t found
checking for system byte ordering ... little endian
checking for size_t size ... 8 bytes
checking for off_t size ... 8 bytes
checking for time_t size ... 8 bytes
checking for setproctitle() ... not found
checking for pread() ... found
checking for pwrite() ... found
checking for pwritev() ... found
checking for sys_nerr ... found
checking for localtime_r() ... found
checking for posix_memalign() ... found
checking for memalign() ... found
checking for mmap(MAP_ANON|MAP_SHARED) ... found
checking for mmap("/dev/zero", MAP_SHARED) ... found
checking for System V shared memory ... found
checking for POSIX semaphores ... not found
checking for POSIX semaphores in libpthread ... found
checking for struct msghdr.msg_control ... found
checking for ioctl(FIONBIO) ... found
checking for struct tm.tm_gmtoff ... found
checking for struct dirent.d_namlen ... not found
checking for struct dirent.d_type ... found
checking for sysconf(_SC_NPROCESSORS_ONLN) ... found
checking for openat(), fstatat() ... found
checking for getaddrinfo() ... found
checking for md5 in system md library ... not found
checking for md5 in system md5 library ... not found
checking for md5 in system OpenSSL crypto library ... not found
checking for sha1 in system md library ... not found
checking for sha1 in system OpenSSL crypto library ... not found
creating objs/Makefile

Configuration summary
  + PCRE library is not used
  + OpenSSL library is not used
  + using builtin md5 code
  + sha1 library is not found
  + zlib library is not used

  nginx path prefix: "/usr/local/nginx"
  nginx binary file: "/usr/local/nginx/sbin/nginx"
  nginx configuration prefix: "/usr/local/nginx/conf"
  nginx configuration file: "/usr/local/nginx/conf/nginx.conf"
  nginx pid file: "/usr/local/nginx/logs/nginx.pid"
  nginx error log file: "/usr/local/nginx/logs/error.log"
  nginx http access log file: "/usr/local/nginx/logs/access.log"
  nginx http client request body temporary files: "client_body_temp"
  nginx http proxy temporary files: "proxy_temp"
  nginx http fastcgi temporary files: "fastcgi_temp"
  nginx http uwsgi temporary files: "uwsgi_temp"
  nginx http scgi temporary files: "scgi_temp"

[fedora@ip-172-31-22-54 nginx-1.9.9]$ make
...(omit console print)
[fedora@ip-172-31-22-54 nginx-1.9.9]$ sudo make install
make -f objs/Makefile install
make[1]: Entering directory '/home/fedora/nginx/nginx-1.9.9'
test -d '/usr/local/nginx' || mkdir -p '/usr/local/nginx'
test -d '/usr/local/nginx/sbin' 		|| mkdir -p '/usr/local/nginx/sbin'
test ! -f '/usr/local/nginx/sbin/nginx' 		|| mv '/usr/local/nginx/sbin/nginx' 		'/usr/local/nginx/sbin/nginx.old'
cp objs/nginx '/usr/local/nginx/sbin/nginx'
test -d '/usr/local/nginx/conf' 		|| mkdir -p '/usr/local/nginx/conf'
cp conf/koi-win '/usr/local/nginx/conf'
cp conf/koi-utf '/usr/local/nginx/conf'
cp conf/win-utf '/usr/local/nginx/conf'
test -f '/usr/local/nginx/conf/mime.types' 		|| cp conf/mime.types '/usr/local/nginx/conf'
cp conf/mime.types '/usr/local/nginx/conf/mime.types.default'
test -f '/usr/local/nginx/conf/fastcgi_params' 		|| cp conf/fastcgi_params '/usr/local/nginx/conf'
cp conf/fastcgi_params 		'/usr/local/nginx/conf/fastcgi_params.default'
test -f '/usr/local/nginx/conf/fastcgi.conf' 		|| cp conf/fastcgi.conf '/usr/local/nginx/conf'
cp conf/fastcgi.conf '/usr/local/nginx/conf/fastcgi.conf.default'
test -f '/usr/local/nginx/conf/uwsgi_params' 		|| cp conf/uwsgi_params '/usr/local/nginx/conf'
cp conf/uwsgi_params 		'/usr/local/nginx/conf/uwsgi_params.default'
test -f '/usr/local/nginx/conf/scgi_params' 		|| cp conf/scgi_params '/usr/local/nginx/conf'
cp conf/scgi_params 		'/usr/local/nginx/conf/scgi_params.default'
test -f '/usr/local/nginx/conf/nginx.conf' 		|| cp conf/nginx.conf '/usr/local/nginx/conf/nginx.conf'
cp conf/nginx.conf '/usr/local/nginx/conf/nginx.conf.default'
test -d '/usr/local/nginx/logs' 		|| mkdir -p '/usr/local/nginx/logs'
test -d '/usr/local/nginx/logs' || 		mkdir -p '/usr/local/nginx/logs'
test -d '/usr/local/nginx/html' 		|| cp -R html '/usr/local/nginx'
test -d '/usr/local/nginx/logs' || 		mkdir -p '/usr/local/nginx/logs'
make[1]: Leaving directory '/home/fedora/nginx/nginx-1.9.9'
[fedora@ip-172-31-22-54 nginx-1.9.9]$ 
```

Add /usr/local/nginx to the $PATH.
```
[fedora@ip-172-31-22-54 sbin]$ vi ~/.bashrc
```
add these at the end of file:
export PATH=$PATH:/usr/local/nginx/sbin




### Build manually from source Q&A

* What additional software did you have to install?

- A: gcc, make

* How did you install these pre-requisites? Can you do this without using any package manager at all (i.e. everything from source)?

- A: I use dnf install gcc and make. Maybe I can, but there are too many packages are related. It's a really heavy work. 

* How many new files were added?
* A: Around Mon Feb 20 09:45:08 2017 , added `gcc`.
Use the same way like above.

```
[fedora@ip-172-31-22-54 sbin]$ sudo find / -cmin -50 | grep '\/' -c
find: ‘/proc/16447/task/16447/fd/6’: No such file or directory
find: ‘/proc/16447/task/16447/fdinfo/6’: No such file or directory
find: ‘/proc/16447/fd/5’: No such file or directory
find: ‘/proc/16447/fdinfo/5’: No such file or directory
11154
[fedora@ip-172-31-22-54 sbin]$ sudo find / -cmin -40 | grep '\/' -c
find: ‘/proc/16459/task/16459/fd/6’: No such file or directory
find: ‘/proc/16459/task/16459/fdinfo/6’: No such file or directory
find: ‘/proc/16459/fd/5’: No such file or directory
find: ‘/proc/16459/fdinfo/5’: No such file or directory
8422
```
So there are about 11154-6422+75=2870 new files.

* Did this software use any of the added packages you had installed in the previous step? Why / why not?

- A: Yes, the software command `configure` need C compiler to compile and run.
Then need tool `make` to create Makefile and set file environment.

* Does this version of the software have feature parity with the binary package above? Are there some features enabled in one version that are not enabled in the other?
- A: No. When I use `configure`, the system told me can't run these two modules: 
http_rewrite_module, http_gzip_module.
Because there are not PCRE library and zilb library. The first instance didn't tell me that.

* Which directories did the software get installed into?
* A: /usr/local/nginx. (refer from tutorial)

* How do you know you didn't get any backdoors installed?
If we install manually from source, we only rely on the trust of source.
* A: I can use command `top` and `netstat` to check if there is suspicious progress running or port has been occupied. But it's still not a reliable method.

