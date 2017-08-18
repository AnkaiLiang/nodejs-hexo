---
title: Using the AWS-CLI to set instance
date: 2017-08-16 23:04:16
tags: System Administration
description: "CS615 Assignment2"
---
<!-- more -->
# Using the AWS-CLI to set instance

* CS615
* Ankai Liang
* 10411998
* link: http://www.cs.stevens.edu/~jschauma/615/s17-hw2.html

## Run 1

### Use `script` to log

```
KKs-MacBook-Air:~ kk$ Script -ar timestamps
Script started, output file is timestamps
```
### Create two AWS instances of a given OS (First time I choose OmniOS)
Using the infomation in Assignment1

```
bash-3.2$ aws ec2 run-instances --image-id ami-50ecc847 --count 2 --instance-type t1.micro --key-name keypair3 --security-groups mysg
{
    "OwnerId": "624990436890", 
    "ReservationId": "r-0226656e8c065402b", 
    "Groups": [], 
    "Instances": [
        {
            "Monitoring": {
                "State": "disabled"
            }, 
            "PublicDnsName": "", 
            "KernelId": "aki-b4aa75dd", 
            "State": {
                "Code": 0, 
                "Name": "pending"
            }, 
            "EbsOptimized": false, 
            "LaunchTime": "2017-02-12T21:35:12.000Z", 
            "PrivateIpAddress": "172.31.51.44", 
            "ProductCodes": [], 
            "VpcId": "vpc-adb325cb", 
            "StateTransitionReason": "", 
            "InstanceId": "i-0f177e140a2d45383", 
            "ImageId": "ami-50ecc847", 
            "PrivateDnsName": "ip-172-31-51-44.ec2.internal", 
            "KeyName": "keypair3", 
            "SecurityGroups": [
                {
                    "GroupName": "mysg", 
                    "GroupId": "sg-a364e4df"
                }
            ], 
            "ClientToken": "", 
            "SubnetId": "subnet-8e2c63a3", 
            "InstanceType": "t1.micro", 
            "NetworkInterfaces": [
                {
                    "Status": "in-use", 
                    "MacAddress": "12:4e:f4:9c:4c:1e", 
                    "SourceDestCheck": true, 
                    "VpcId": "vpc-adb325cb", 
                    "Description": "", 
                    "NetworkInterfaceId": "eni-fc54fa0e", 
                    "PrivateIpAddresses": [
                        {
                            "PrivateDnsName": "ip-172-31-51-44.ec2.internal", 
                            "Primary": true, 
                            "PrivateIpAddress": "172.31.51.44"
                        }
                    ], 
                    "PrivateDnsName": "ip-172-31-51-44.ec2.internal", 
                    "Attachment": {
                        "Status": "attaching", 
                        "DeviceIndex": 0, 
                        "DeleteOnTermination": true, 
                        "AttachmentId": "eni-attach-93f26ab9", 
                        "AttachTime": "2017-02-12T21:35:12.000Z"
                    }, 
                    "Groups": [
                        {
                            "GroupName": "mysg", 
                            "GroupId": "sg-a364e4df"
                        }
                    ], 
                    "Ipv6Addresses": [], 
                    "SubnetId": "subnet-8e2c63a3", 
                    "OwnerId": "624990436890", 
                    "PrivateIpAddress": "172.31.51.44"
                }
            ], 
            "SourceDestCheck": true, 
            "Placement": {
                "Tenancy": "default", 
                "GroupName": "", 
                "AvailabilityZone": "us-east-1d"
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
        }, 
        {
            "Monitoring": {
                "State": "disabled"
            }, 
            "PublicDnsName": "", 
            "KernelId": "aki-b4aa75dd", 
            "State": {
                "Code": 0, 
                "Name": "pending"
            }, 
            "EbsOptimized": false, 
            "LaunchTime": "2017-02-12T21:35:12.000Z", 
            "PrivateIpAddress": "172.31.57.85", 
            "ProductCodes": [], 
            "VpcId": "vpc-adb325cb", 
            "StateTransitionReason": "", 
            "InstanceId": "i-0ab15f53de99f4dff", 
            "ImageId": "ami-50ecc847", 
            "PrivateDnsName": "ip-172-31-57-85.ec2.internal", 
            "KeyName": "keypair3", 
            "SecurityGroups": [
                {
                    "GroupName": "mysg", 
                    "GroupId": "sg-a364e4df"
                }
            ], 
            "ClientToken": "", 
            "SubnetId": "subnet-8e2c63a3", 
            "InstanceType": "t1.micro", 
            "NetworkInterfaces": [
                {
                    "Status": "in-use", 
                    "MacAddress": "12:6a:12:1b:97:60", 
                    "SourceDestCheck": true, 
                    "VpcId": "vpc-adb325cb", 
                    "Description": "", 
                    "NetworkInterfaceId": "eni-ff54fa0d", 
                    "PrivateIpAddresses": [
                        {
                            "PrivateDnsName": "ip-172-31-57-85.ec2.internal", 
                            "Primary": true, 
                            "PrivateIpAddress": "172.31.57.85"
                        }
                    ], 
                    "PrivateDnsName": "ip-172-31-57-85.ec2.internal", 
                    "Attachment": {
                        "Status": "attaching", 
                        "DeviceIndex": 0, 
                        "DeleteOnTermination": true, 
                        "AttachmentId": "eni-attach-94f26abe", 
                        "AttachTime": "2017-02-12T21:35:12.000Z"
                    }, 
                    "Groups": [
                        {
                            "GroupName": "mysg", 
                            "GroupId": "sg-a364e4df"
                        }
                    ], 
                    "Ipv6Addresses": [], 
                    "SubnetId": "subnet-8e2c63a3", 
                    "OwnerId": "624990436890", 
                    "PrivateIpAddress": "172.31.57.85"
                }
            ], 
            "SourceDestCheck": true, 
            "Placement": {
                "Tenancy": "default", 
                "GroupName": "", 
                "AvailabilityZone": "us-east-1d"
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
        }
    ]
}
```

### Get the info of my two instances

```
bash-3.2$ aws ec2 describe-instances --filters "Name=image-id,Values=ami-50ecc847"
{
    "Reservations": [
        {
            "OwnerId": "624990436890", 
            "ReservationId": "r-0226656e8c065402b", 
            "Groups": [], 
            "Instances": [
                {
                    "Monitoring": {
                        "State": "disabled"
                    }, 
                    "PublicDnsName": "ec2-54-82-89-190.compute-1.amazonaws.com", 
                    "RootDeviceType": "ebs", 
                    "State": {
                        "Code": 16, 
                        "Name": "running"
                    }, 
                    "EbsOptimized": false, 
                    "LaunchTime": "2017-02-12T22:04:23.000Z", 
                    "PublicIpAddress": "54.82.89.190", 
                    "PrivateIpAddress": "172.31.51.44", 
                    "ProductCodes": [], 
                    "VpcId": "vpc-adb325cb", 
                    "StateTransitionReason": "", 
                    "InstanceId": "i-0f177e140a2d45383", 
                    "ImageId": "ami-50ecc847", 
                    "PrivateDnsName": "ip-172-31-51-44.ec2.internal", 
                    "KeyName": "keypair3", 
                    "SecurityGroups": [
                        {
                            "GroupName": "mysg", 
                            "GroupId": "sg-a364e4df"
                        }
                    ], 
                    "ClientToken": "", 
                    "SubnetId": "subnet-8e2c63a3", 
                    "InstanceType": "t1.micro", 
                    "NetworkInterfaces": [
                        {
                            "Status": "in-use", 
                            "MacAddress": "12:4e:f4:9c:4c:1e", 
                            "SourceDestCheck": true, 
                            "VpcId": "vpc-adb325cb", 
                            "Description": "", 
                            "Association": {
                                "PublicIp": "54.82.89.190", 
                                "PublicDnsName": "ec2-54-82-89-190.compute-1.amazonaws.com", 
                                "IpOwnerId": "amazon"
                            }, 
                            "NetworkInterfaceId": "eni-fc54fa0e", 
                            "PrivateIpAddresses": [
                                {
                                    "PrivateDnsName": "ip-172-31-51-44.ec2.internal", 
                                    "Association": {
                                        "PublicIp": "54.82.89.190", 
                                        "PublicDnsName": "ec2-54-82-89-190.compute-1.amazonaws.com", 
                                        "IpOwnerId": "amazon"
                                    }, 
                                    "Primary": true, 
                                    "PrivateIpAddress": "172.31.51.44"
                                }
                            ], 
                            "PrivateDnsName": "ip-172-31-51-44.ec2.internal", 
                            "Attachment": {
                                "Status": "attached", 
                                "DeviceIndex": 0, 
                                "DeleteOnTermination": true, 
                                "AttachmentId": "eni-attach-93f26ab9", 
                                "AttachTime": "2017-02-12T21:35:12.000Z"
                            }, 
                            "Groups": [
                                {
                                    "GroupName": "mysg", 
                                    "GroupId": "sg-a364e4df"
                                }
                            ], 
                            "Ipv6Addresses": [], 
                            "SubnetId": "subnet-8e2c63a3", 
                            "OwnerId": "624990436890", 
                            "PrivateIpAddress": "172.31.51.44"
                        }
                    ], 
                    "SourceDestCheck": true, 
                    "Placement": {
                        "Tenancy": "default", 
                        "GroupName": "", 
                        "AvailabilityZone": "us-east-1d"
                    }, 
                    "Hypervisor": "xen", 
                    "BlockDeviceMappings": [
                        {
                            "DeviceName": "/dev/sda", 
                            "Ebs": {
                                "Status": "attached", 
                                "DeleteOnTermination": true, 
                                "VolumeId": "vol-05a3a6b06a43fc4b6", 
                                "AttachTime": "2017-02-12T21:35:13.000Z"
                            }
                        }, 
                        {
                            "DeviceName": "/dev/sdf", 
                            "Ebs": {
                                "Status": "attached", 
                                "DeleteOnTermination": false, 
                                "VolumeId": "vol-09a61b9189216583f", 
                                "AttachTime": "2017-02-12T21:49:38.000Z"
                            }
                        }
                    ], 
                    "Architecture": "x86_64", 
                    "KernelId": "aki-b4aa75dd", 
                    "RootDeviceName": "/dev/sda", 
                    "VirtualizationType": "paravirtual", 
                    "AmiLaunchIndex": 1
                }, 
                {
                    "Monitoring": {
                        "State": "disabled"
                    }, 
                    "PublicDnsName": "ec2-52-55-98-238.compute-1.amazonaws.com", 
                    "RootDeviceType": "ebs", 
                    "State": {
                        "Code": 16, 
                        "Name": "running"
                    }, 
                    "EbsOptimized": false, 
                    "LaunchTime": "2017-02-12T21:35:12.000Z", 
                    "PublicIpAddress": "52.55.98.238", 
                    "PrivateIpAddress": "172.31.57.85", 
                    "ProductCodes": [], 
                    "VpcId": "vpc-adb325cb", 
                    "StateTransitionReason": "", 
                    "InstanceId": "i-0ab15f53de99f4dff", 
                    "ImageId": "ami-50ecc847", 
                    "PrivateDnsName": "ip-172-31-57-85.ec2.internal", 
                    "KeyName": "keypair3", 
                    "SecurityGroups": [
                        {
                            "GroupName": "mysg", 
                            "GroupId": "sg-a364e4df"
                        }
                    ], 
                    "ClientToken": "", 
                    "SubnetId": "subnet-8e2c63a3", 
                    "InstanceType": "t1.micro", 
                    "NetworkInterfaces": [
                        {
                            "Status": "in-use", 
                            "MacAddress": "12:6a:12:1b:97:60", 
                            "SourceDestCheck": true, 
                            "VpcId": "vpc-adb325cb", 
                            "Description": "", 
                            "Association": {
                                "PublicIp": "52.55.98.238", 
                                "PublicDnsName": "ec2-52-55-98-238.compute-1.amazonaws.com", 
                                "IpOwnerId": "amazon"
                            }, 
                            "NetworkInterfaceId": "eni-ff54fa0d", 
                            "PrivateIpAddresses": [
                                {
                                    "PrivateDnsName": "ip-172-31-57-85.ec2.internal", 
                                    "Association": {
                                        "PublicIp": "52.55.98.238", 
                                        "PublicDnsName": "ec2-52-55-98-238.compute-1.amazonaws.com", 
                                        "IpOwnerId": "amazon"
                                    }, 
                                    "Primary": true, 
                                    "PrivateIpAddress": "172.31.57.85"
                                }
                            ], 
                            "PrivateDnsName": "ip-172-31-57-85.ec2.internal", 
                            "Attachment": {
                                "Status": "attached", 
                                "DeviceIndex": 0, 
                                "DeleteOnTermination": true, 
                                "AttachmentId": "eni-attach-94f26abe", 
                                "AttachTime": "2017-02-12T21:35:12.000Z"
                            }, 
                            "Groups": [
                                {
                                    "GroupName": "mysg", 
                                    "GroupId": "sg-a364e4df"
                                }
                            ], 
                            "Ipv6Addresses": [], 
                            "SubnetId": "subnet-8e2c63a3", 
                            "OwnerId": "624990436890", 
                            "PrivateIpAddress": "172.31.57.85"
                        }
                    ], 
                    "SourceDestCheck": true, 
                    "Placement": {
                        "Tenancy": "default", 
                        "GroupName": "", 
                        "AvailabilityZone": "us-east-1d"
                    }, 
                    "Hypervisor": "xen", 
                    "BlockDeviceMappings": [
                        {
                            "DeviceName": "/dev/sda", 
                            "Ebs": {
                                "Status": "attached", 
                                "DeleteOnTermination": true, 
                                "VolumeId": "vol-0e47feae707a44536", 
                                "AttachTime": "2017-02-12T21:35:13.000Z"
                            }
                        }
                    ], 
                    "Architecture": "x86_64", 
                    "KernelId": "aki-b4aa75dd", 
                    "RootDeviceName": "/dev/sda", 
                    "VirtualizationType": "paravirtual", 
                    "AmiLaunchIndex": 0
                }
            ]
        }, 
        {
            "OwnerId": "624990436890", 
            "ReservationId": "r-0b0ff317e4b1acab4", 
            "Groups": [], 
            "Instances": [
                {
                    "Monitoring": {
                        "State": "disabled"
                    }, 
                    "PublicDnsName": "", 
                    "KernelId": "aki-b4aa75dd", 
                    "State": {
                        "Code": 48, 
                        "Name": "terminated"
                    }, 
                    "EbsOptimized": false, 
                    "LaunchTime": "2017-02-12T20:13:47.000Z", 
                    "ProductCodes": [], 
                    "StateTransitionReason": "User initiated (2017-02-12 21:33:48 GMT)", 
                    "InstanceId": "i-06d4cb4ecd0874992", 
                    "ImageId": "ami-50ecc847", 
                    "PrivateDnsName": "", 
                    "KeyName": "keypair3", 
                    "SecurityGroups": [], 
                    "ClientToken": "", 
                    "InstanceType": "t1.micro", 
                    "NetworkInterfaces": [], 
                    "Placement": {
                        "Tenancy": "default", 
                        "GroupName": "", 
                        "AvailabilityZone": "us-east-1d"
                    }, 
                    "Hypervisor": "xen", 
                    "BlockDeviceMappings": [], 
                    "Architecture": "x86_64", 
                    "StateReason": {
                        "Message": "Client.UserInitiatedShutdown: User initiated shutdown", 
                        "Code": "Client.UserInitiatedShutdown"
                    }, 
                    "RootDeviceName": "/dev/sda", 
                    "VirtualizationType": "paravirtual", 
                    "RootDeviceType": "ebs", 
                    "AmiLaunchIndex": 1
                }, 
                {
                    "Monitoring": {
                        "State": "disabled"
                    }, 
                    "PublicDnsName": "", 
                    "KernelId": "aki-b4aa75dd", 
                    "State": {
                        "Code": 48, 
                        "Name": "terminated"
                    }, 
                    "EbsOptimized": false, 
                    "LaunchTime": "2017-02-12T20:13:47.000Z", 
                    "ProductCodes": [], 
                    "StateTransitionReason": "User initiated (2017-02-12 21:33:48 GMT)", 
                    "InstanceId": "i-0d371a9afb03cea66", 
                    "ImageId": "ami-50ecc847", 
                    "PrivateDnsName": "", 
                    "KeyName": "keypair3", 
                    "SecurityGroups": [], 
                    "ClientToken": "", 
                    "InstanceType": "t1.micro", 
                    "NetworkInterfaces": [], 
                    "Placement": {
                        "Tenancy": "default", 
                        "GroupName": "", 
                        "AvailabilityZone": "us-east-1d"
                    }, 
                    "Hypervisor": "xen", 
                    "BlockDeviceMappings": [], 
                    "Architecture": "x86_64", 
                    "StateReason": {
                        "Message": "Client.UserInitiatedShutdown: User initiated shutdown", 
                        "Code": "Client.UserInitiatedShutdown"
                    }, 
                    "RootDeviceName": "/dev/sda", 
                    "VirtualizationType": "paravirtual", 
                    "RootDeviceType": "ebs", 
                    "AmiLaunchIndex": 0
                }
            ]
        }
    ]
}

```
### Create a 1GB volume and attach it to one of the instances
According to the above infomation, I knew the instances-id and public DNS of my two running OmniOs instances:

1. i-0ab15f53de99f4dff    ec2-52-55-98-238.compute-1.amazonaws.com
2. i-0f177e140a2d45383    ec2-54-166-108-26.compute-1.amazonaws.com

Because I used to reboot the second instance, the public DNS has changed. It's not a necessary step, I omit that part.

And their "AvailabilityZone" is "us-east-1d"
I create the colume and attach it to the first instance "/dev/sdf".

```
bash-3.2$ aws ec2 create-volume --no-dry-run --size 1 --availability-zone us-east-1d --volume-type gp2 --no-encrypted
{
    "AvailabilityZone": "us-east-1d", 
    "Encrypted": false, 
    "VolumeType": "gp2", 
    "VolumeId": "vol-0a3064debd17cede4", 
    "State": "creating", 
    "Iops": 100, 
    "SnapshotId": "", 
    "CreateTime": "2017-02-13T05:19:24.216Z", 
    "Size": 1
}

bash-3.2$ aws ec2 attach-volume --volume-id vol-0a3064debd17cede4 --instance-id i-0ab15f53de99f4dff --device /dev/sdg
{
    "AttachTime": "2017-02-13T05:20:41.520Z", 
    "InstanceId": "i-0ab15f53de99f4dff", 
    "VolumeId": "vol-0a3064debd17cede4", 
    "State": "attaching", 
    "Device": "/dev/sdg"
}

```

### Create the file system in the volume, mount it to the first instance then create a file.

In this section, I met a lot of troubles to create the file system. After command `format`, I got the DISK device-name is 'c1t2144d0'.
But I cannot run by command `newfs c1t2144d0` or `newfs /devices/xpvd/xdf@2144`. CLI told me "it's not a raw device". After searching lots of blog and tutorial, I knew that newfs parameter 'address' should locate into `/dev/rdsk`. But under the directory `/dev/rdsk`, there isn't file whose name is 'c1t2144d0'. By comparing the example command and the files name in `/dev/rdsk`, I realized that the volume has been divided into slices, and I should use the 'c1t2144d0s0' as the part of parameter.

In the OmniOS, I create a UFS file system. The OmniOS also support ZFS, but the creation of ZFS is more complecate than UFS.
Using the command `newfs`. `newfs` is a friendly front-end command of `mkfs`. It could caculate the properly parameters then transfer to `mkfs` to run. 

```
root@ip-10-152-178-106.ec2.internal:/root# format
Searching for disks...done


AVAILABLE DISK SELECTIONS:
       0. c1t2048d0 <Unknown-Unknown-0001 cyl 4085 alt 2 hd 128 sec 32>
          /xpvd/xdf@2048
       1. c1t2144d0 <Unknown-Unknown-0001 cyl 1024 alt 0 hd 64 sec 32>
          /xpvd/xdf@2144
Specify disk (enter its number): 1
selecting c1t2144d0
[disk formatted, no defect list found]
No Solaris fdisk partition found.


FORMAT MENU:
        disk       - select a disk
        type       - select (define) a disk type
        partition  - select (define) a partition table
        current    - describe the current disk
        format     - format and analyze the disk
        fdisk      - run the fdisk program
        repair     - repair a defective sector
        show       - translate a disk address
        label      - write label to the disk
        analyze    - surface analysis
        defect     - defect list management
        backup     - search for backup labels
        verify     - read and display labels
        save       - save new disk/partition definitions
        volname    - set 8-character volume name
        !<cmd>     - execute <cmd>, then return
        quit
format> quit
root@ip-10-152-178-106.ec2.internal:/root# newfs /dev/rdsk/c1t2144d0s0
newfs: construct a new file system /dev/rdsk/c1t2144d0s0: (y/n)? y
/dev/rdsk/c1t2144d0s0:  2097152 sectors in 1024 cylinders of 64 tracks, 32 sectors
        1024.0MB in 32 cyl groups (32 c/g, 32.00MB/g, 15872 i/g)
super-block backups (for fsck -F ufs -o b=#) at:
 32, 65600, 131168, 196736, 262304, 327872, 393440, 459008, 524576, 590144,
 1442528, 1508096, 1573664, 1639232, 1704800, 1770368, 1835936, 1901504,
 1967072, 2032640
root@ip-10-152-178-106.ec2.internal:/root# fsck /dev/rdsk/c1t2144d0s0
** /dev/rdsk/c1t2144d0s0
** Last Mounted on 
** Phase 1 - Check Blocks and Sizes
** Phase 2 - Check Pathnames
** Phase 3a - Check Connectivity
** Phase 3b - Verify Shadows/ACLs
** Phase 4 - Check Reference Counts
** Phase 5 - Check Cylinder Groups
2 files, 9 used, 984550 free (14 frags, 123067 blocks, 0.0% fragmentation)
root@ip-10-152-178-106.ec2.internal:/root# mkdir /data
root@ip-10-152-178-106.ec2.internal:/root# mount /dev/dsk/c1t2144d0s0 /data
root@ip-10-152-178-106.ec2.internal:/root# mount
/ on syspool/ROOT/omnios-r151020-1 read/write/setuid/devices/dev=1710002 on Thu Jan  1 00:00:00 1970
/devices on /devices read/write/setuid/devices/dev=8340000 on Sun Feb 12 21:36:02 2017
/dev on /dev read/write/setuid/devices/dev=8380000 on Sun Feb 12 21:36:02 2017
/system/contract on ctfs read/write/setuid/devices/dev=8440001 on Sun Feb 12 21:36:03 2017
/proc on proc read/write/setuid/devices/dev=83c0000 on Sun Feb 12 21:36:03 2017
/etc/mnttab on mnttab read/write/setuid/devices/dev=8480001 on Sun Feb 12 21:36:03 2017
/etc/svc/volatile on swap read/write/setuid/devices/xattr/dev=84c0001 on Sun Feb 12 21:36:03 2017
/system/object on objfs read/write/setuid/devices/dev=8500001 on Sun Feb 12 21:36:03 2017
/system/boot on bootfs read/write/setuid/devices/dev=8540001 on Sun Feb 12 21:36:03 2017
/etc/dfs/sharetab on sharefs read/write/setuid/devices/dev=8580001 on Sun Feb 12 21:36:03 2017
/lib/libc.so.1 on /usr/lib/libc/libc_hwcap3.so.1 read/write/setuid/devices/dev=1710002 on Sun Feb 12 21:36:41 2017
/dev/fd on fd read/write/setuid/devices/dev=8680001 on Sun Feb 12 21:36:46 2017
/tmp on swap read/write/setuid/devices/xattr/dev=84c0002 on Sun Feb 12 21:36:47 2017
/var/run on swap read/write/setuid/devices/xattr/dev=84c0003 on Sun Feb 12 21:36:47 2017
/syspool on syspool read/write/setuid/devices/nonbmand/exec/xattr/atime/dev=1710007 on Sun Feb 12 21:36:58 2017
/data on /dev/dsk/c1t2144d0s0 read/write/setuid/devices/intr/largefiles/logging/xattr/onerror=panic/dev=21800c0 on Mon Feb 13 06:10:02 2017
```

Create a file(testfile).

```
root@ip-10-152-178-106.ec2.internal:/# cd /
root@ip-10-152-178-106.ec2.internal:/# sudo chmod 777 data
root@ip-10-152-178-106.ec2.internal:/# cd data
root@ip-10-152-178-106.ec2.internal:/data# vi testfile
```

### Terminate the first OmniOS instace
```
bash-3.2$ aws ec2 terminate-instances --instance-ids i-0ab15f53de99f4dff
{
    "TerminatingInstances": [
        {
            "InstanceId": "i-0ab15f53de99f4dff", 
            "CurrentState": {
                "Code": 32, 
                "Name": "shutting-down"
            }, 
            "PreviousState": {
                "Code": 16, 
                "Name": "running"
            }
        }
    ]
}
```

### Attach the volume to the second instance
The volume id is: vol-0a3064debd17cede4
The second instance id is: i-0f177e140a2d45383
The second instance public DNS is: ec2-54-166-108-26.compute-1.amazonaws.com

Check the state of this volume.
```
bash-3.2$ aws ec2 describe-volumes --filters Name=volume-id,Values=vol-0a3064debd17cede4
{
    "Volumes": [
        {
            "AvailabilityZone": "us-east-1d", 
            "Attachments": [], 
            "Encrypted": false, 
            "VolumeType": "gp2", 
            "VolumeId": "vol-0a3064debd17cede4", 
            "State": "available", 
            "Iops": 100, 
            "SnapshotId": "", 
            "CreateTime": "2017-02-13T05:19:24.216Z", 
            "Size": 1
        }
    ]
}
```

We find that its state is available. 

```
bash-3.2$ aws ec2 attach-volume --volume-id vol-0a3064debd17cede4 --instance-id i-0f177e140a2d45383 --device /dev/sdf
{
    "AttachTime": "2017-02-13T06:26:28.486Z", 
    "InstanceId": "i-0f177e140a2d45383", 
    "VolumeId": "vol-0a3064debd17cede4", 
    "State": "attaching", 
    "Device": "/dev/sdf"
}
```
SSH to the seconde instance, mount the volume and retrieve the file we just created.

```
bash-3.2$ pwd
/Users/kk/Documents
bash-3.2$ ssh -i p.pem root@ec2-54-166-108-26.compute-1.amazonaws.com
Last login: Mon Feb 13 04:59:30 2017 from 98.109.151.68
OmniOS 5.11     omnios-r151020-b5b8c75  November 2016
root@ip-172-31-51-44:/root# format
Searching for disks...done


AVAILABLE DISK SELECTIONS:
       0. c1t2048d0 <Unknown-Unknown-0001 cyl 4085 alt 2 hd 128 sec 32>
          /xpvd/xdf@2048
       1. c1t2128d0 <Unknown-Unknown-0001 cyl 1024 alt 0 hd 64 sec 32>
          /xpvd/xdf@2128
Specify disk (enter its number): 1
selecting c1t2128d0
[disk formatted, no defect list found]
No Solaris fdisk partition found.


FORMAT MENU:
        disk       - select a disk
        type       - select (define) a disk type
        partition  - select (define) a partition table
        current    - describe the current disk
        format     - format and analyze the disk
        fdisk      - run the fdisk program
        repair     - repair a defective sector
        show       - translate a disk address
        label      - write label to the disk
        analyze    - surface analysis
        defect     - defect list management
        backup     - search for backup labels
        verify     - read and display labels
        save       - save new disk/partition definitions
        volname    - set 8-character volume name
        !<cmd>     - execute <cmd>, then return
        quit
format> quit
root@ip-172-31-51-44:/root# fsck /dev/rdsk/c1t2128d0s0
** /dev/rdsk/c1t2128d0s0
** Last Mounted on /data
** Phase 1 - Check Blocks and Sizes
** Phase 2 - Check Pathnames
** Phase 3a - Check Connectivity
** Phase 3b - Verify Shadows/ACLs
** Phase 4 - Check Reference Counts
** Phase 5 - Check Cylinder Groups
3 files, 10 used, 983517 free (13 frags, 122938 blocks, 0.0% fragmentation)
root@ip-172-31-51-44:/root# mkdir /data
root@ip-172-31-51-44:/root# mount /dev/dsk/c1t2128d0s0 /data
root@ip-172-31-51-44:/root# mount
/ on syspool/ROOT/omnios-r151020-1 read/write/setuid/devices/dev=1710002 on Thu Jan  1 00:00:00 1970
/devices on /devices read/write/setuid/devices/dev=8340000 on Mon Feb 13 04:55:17 2017
/dev on /dev read/write/setuid/devices/dev=8380000 on Mon Feb 13 04:55:17 2017
/system/contract on ctfs read/write/setuid/devices/dev=8440001 on Mon Feb 13 04:55:17 2017
/proc on proc read/write/setuid/devices/dev=83c0000 on Mon Feb 13 04:55:17 2017
/etc/mnttab on mnttab read/write/setuid/devices/dev=8480001 on Mon Feb 13 04:55:17 2017
/etc/svc/volatile on swap read/write/setuid/devices/xattr/dev=84c0001 on Mon Feb 13 04:55:17 2017
/system/object on objfs read/write/setuid/devices/dev=8500001 on Mon Feb 13 04:55:17 2017
/system/boot on bootfs read/write/setuid/devices/dev=8540001 on Mon Feb 13 04:55:17 2017
/etc/dfs/sharetab on sharefs read/write/setuid/devices/dev=8580001 on Mon Feb 13 04:55:17 2017
/lib/libc.so.1 on /usr/lib/libc/libc_hwcap3.so.1 read/write/setuid/devices/dev=1710002 on Mon Feb 13 04:55:25 2017
/dev/fd on fd read/write/setuid/devices/dev=8680001 on Mon Feb 13 04:55:26 2017
/tmp on swap read/write/setuid/devices/xattr/dev=84c0002 on Mon Feb 13 04:55:26 2017
/var/run on swap read/write/setuid/devices/xattr/dev=84c0003 on Mon Feb 13 04:55:26 2017
/syspool on syspool read/write/setuid/devices/nonbmand/exec/xattr/atime/dev=1710007 on Mon Feb 13 04:55:31 2017
/data on /dev/dsk/c1t2128d0s0 read/write/setuid/devices/intr/largefiles/logging/xattr/onerror=panic/dev=21800c0 on Mon Feb 13 06:38:28 2017
root@ip-172-31-51-44:/root# cd /data
root@ip-172-31-51-44:/data# ls
lost+found  testfile
```

### Retrieve the file.

Then we use `scp` to retrieve the file.

```
root@ip-172-31-51-44:/data# exit
logout
Connection to ec2-54-166-108-26.compute-1.amazonaws.com closed.
bash-3.2$ pwd
/Users/kk/Documents
bash-3.2$ scp -i p.pem root@ec2-54-166-108-26.compute-1.amazonaws.com:/data/testfile testfile
testfile                                      100%    7     0.2KB/s   00:00    
bash-3.2$ vi testfile
bash-3.2$ exit
exit

Script done, output file is timestamps
```


## Run 2 
### Use `script` to log

```
KKs-MacBook-Air:~ kk$ Script -ar timestamps
Script started, output file is timestamps
```
### Create two AWS instances of a given OS (First time I choose Linux)

```
bash-3.2$ aws ec2 run-instances --image-id ami-0b33d91d --count 1 --instance-type t2.micro --key-name keypair3 --security-groups mysg
{
    "OwnerId": "624990436890", 
    "ReservationId": "r-09603da3f14e5fd5d", 
    "Groups": [], 
    "Instances": [
        {
            "Monitoring": {
                "State": "disabled"
            }, 
            "PublicDnsName": "", 
            "RootDeviceType": "ebs", 
            "State": {
                "Code": 0, 
                "Name": "pending"
            }, 
            "EbsOptimized": false, 
            "LaunchTime": "2017-02-13T00:23:07.000Z", 
            "PrivateIpAddress": "172.31.26.132", 
            "ProductCodes": [], 
            "VpcId": "vpc-adb325cb", 
            "StateTransitionReason": "", 
            "InstanceId": "i-0892e3a2148d40757", 
            "ImageId": "ami-0b33d91d", 
            "PrivateDnsName": "ip-172-31-26-132.ec2.internal", 
            "KeyName": "keypair3", 
            "SecurityGroups": [
                {
                    "GroupName": "mysg", 
                    "GroupId": "sg-a364e4df"
                }
            ], 
            "ClientToken": "", 
            "SubnetId": "subnet-09dda752", 
            "InstanceType": "t2.micro", 
            "NetworkInterfaces": [
                {
                    "Status": "in-use", 
                    "MacAddress": "0e:4e:0d:5f:f1:08", 
                    "SourceDestCheck": true, 
                    "VpcId": "vpc-adb325cb", 
                    "Description": "", 
                    "NetworkInterfaceId": "eni-da07b71e", 
                    "PrivateIpAddresses": [
                        {
                            "PrivateDnsName": "ip-172-31-26-132.ec2.internal", 
                            "Primary": true, 
                            "PrivateIpAddress": "172.31.26.132"
                        }
                    ], 
                    "PrivateDnsName": "ip-172-31-26-132.ec2.internal", 
                    "Attachment": {
                        "Status": "attaching", 
                        "DeviceIndex": 0, 
                        "DeleteOnTermination": true, 
                        "AttachmentId": "eni-attach-98eacfc6", 
                        "AttachTime": "2017-02-13T00:23:07.000Z"
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
                    "PrivateIpAddress": "172.31.26.132"
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
            "RootDeviceName": "/dev/xvda", 
            "VirtualizationType": "hvm", 
            "AmiLaunchIndex": 0
        }
    ]
}
bash-3.2$ aws ec2 run-instances --image-id ami-0b33d91d --count 1 --instance-type t2.micro --key-name keypair3 --security-groups mysg
{
    "OwnerId": "624990436890", 
    "ReservationId": "r-0e5f45ce61018f566", 
    "Groups": [], 
    "Instances": [
        {
            "Monitoring": {
                "State": "disabled"
            }, 
            "PublicDnsName": "", 
            "RootDeviceType": "ebs", 
            "State": {
                "Code": 0, 
                "Name": "pending"
            }, 
            "EbsOptimized": false, 
            "LaunchTime": "2017-02-13T00:24:52.000Z", 
            "PrivateIpAddress": "172.31.25.133", 
            "ProductCodes": [], 
            "VpcId": "vpc-adb325cb", 
            "StateTransitionReason": "", 
            "InstanceId": "i-03c597e94f5bd3809", 
            "ImageId": "ami-0b33d91d", 
            "PrivateDnsName": "ip-172-31-25-133.ec2.internal", 
            "KeyName": "keypair3", 
            "SecurityGroups": [
                {
                    "GroupName": "mysg", 
                    "GroupId": "sg-a364e4df"
                }
            ], 
            "ClientToken": "", 
            "SubnetId": "subnet-09dda752", 
            "InstanceType": "t2.micro", 
            "NetworkInterfaces": [
                {
                    "Status": "in-use", 
                    "MacAddress": "0e:a0:9c:c8:ef:14", 
                    "SourceDestCheck": true, 
                    "VpcId": "vpc-adb325cb", 
                    "Description": "", 
                    "NetworkInterfaceId": "eni-b40ebe70", 
                    "PrivateIpAddresses": [
                        {
                            "PrivateDnsName": "ip-172-31-25-133.ec2.internal", 
                            "Primary": true, 
                            "PrivateIpAddress": "172.31.25.133"
                        }
                    ], 
                    "PrivateDnsName": "ip-172-31-25-133.ec2.internal", 
                    "Attachment": {
                        "Status": "attaching", 
                        "DeviceIndex": 0, 
                        "DeleteOnTermination": true, 
                        "AttachmentId": "eni-attach-6cf6d332", 
                        "AttachTime": "2017-02-13T00:24:52.000Z"
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
                    "PrivateIpAddress": "172.31.25.133"
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
            "RootDeviceName": "/dev/xvda", 
            "VirtualizationType": "hvm", 
            "AmiLaunchIndex": 0
        }
    ]
}
```

### Get the info of my two instances

```
bash-3.2$ aws ec2 describe-instances --filters "Name=image-id,Values=ami-0b33d91d"
{
    "Reservations": [
        {
            "OwnerId": "624990436890", 
            "ReservationId": "r-09603da3f14e5fd5d", 
            "Groups": [], 
            "Instances": [
                {
                    "Monitoring": {
                        "State": "disabled"
                    }, 
                    "PublicDnsName": "ec2-54-242-31-152.compute-1.amazonaws.com", 
                    "State": {
                        "Code": 16, 
                        "Name": "running"
                    }, 
                    "EbsOptimized": false, 
                    "LaunchTime": "2017-02-13T00:23:07.000Z", 
                    "PublicIpAddress": "54.242.31.152", 
                    "PrivateIpAddress": "172.31.26.132", 
                    "ProductCodes": [], 
                    "VpcId": "vpc-adb325cb", 
                    "StateTransitionReason": "", 
                    "InstanceId": "i-0892e3a2148d40757", 
                    "EnaSupport": true, 
                    "ImageId": "ami-0b33d91d", 
                    "PrivateDnsName": "ip-172-31-26-132.ec2.internal", 
                    "KeyName": "keypair3", 
                    "SecurityGroups": [
                        {
                            "GroupName": "mysg", 
                            "GroupId": "sg-a364e4df"
                        }
                    ], 
                    "ClientToken": "", 
                    "SubnetId": "subnet-09dda752", 
                    "InstanceType": "t2.micro", 
                    "NetworkInterfaces": [
                        {
                            "Status": "in-use", 
                            "MacAddress": "0e:4e:0d:5f:f1:08", 
                            "SourceDestCheck": true, 
                            "VpcId": "vpc-adb325cb", 
                            "Description": "", 
                            "Association": {
                                "PublicIp": "54.242.31.152", 
                                "PublicDnsName": "ec2-54-242-31-152.compute-1.amazonaws.com", 
                                "IpOwnerId": "amazon"
                            }, 
                            "NetworkInterfaceId": "eni-da07b71e", 
                            "PrivateIpAddresses": [
                                {
                                    "PrivateDnsName": "ip-172-31-26-132.ec2.internal", 
                                    "Association": {
                                        "PublicIp": "54.242.31.152", 
                                        "PublicDnsName": "ec2-54-242-31-152.compute-1.amazonaws.com", 
                                        "IpOwnerId": "amazon"
                                    }, 
                                    "Primary": true, 
                                    "PrivateIpAddress": "172.31.26.132"
                                }
                            ], 
                            "PrivateDnsName": "ip-172-31-26-132.ec2.internal", 
                            "Attachment": {
                                "Status": "attached", 
                                "DeviceIndex": 0, 
                                "DeleteOnTermination": true, 
                                "AttachmentId": "eni-attach-98eacfc6", 
                                "AttachTime": "2017-02-13T00:23:07.000Z"
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
                            "PrivateIpAddress": "172.31.26.132"
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
                            "DeviceName": "/dev/xvda", 
                            "Ebs": {
                                "Status": "attached", 
                                "DeleteOnTermination": true, 
                                "VolumeId": "vol-02cdf49416a100301", 
                                "AttachTime": "2017-02-13T00:23:08.000Z"
                            }
                        }
                    ], 
                    "Architecture": "x86_64", 
                    "RootDeviceType": "ebs", 
                    "RootDeviceName": "/dev/xvda", 
                    "VirtualizationType": "hvm", 
                    "AmiLaunchIndex": 0
                }
            ]
        }, 
        {
            "OwnerId": "624990436890", 
            "ReservationId": "r-0e5f45ce61018f566", 
            "Groups": [], 
            "Instances": [
                {
                    "Monitoring": {
                        "State": "disabled"
                    }, 
                    "PublicDnsName": "ec2-54-165-167-87.compute-1.amazonaws.com", 
                    "State": {
                        "Code": 16, 
                        "Name": "running"
                    }, 
                    "EbsOptimized": false, 
                    "LaunchTime": "2017-02-13T00:24:52.000Z", 
                    "PublicIpAddress": "54.165.167.87", 
                    "PrivateIpAddress": "172.31.25.133", 
                    "ProductCodes": [], 
                    "VpcId": "vpc-adb325cb", 
                    "StateTransitionReason": "", 
                    "InstanceId": "i-03c597e94f5bd3809", 
                    "EnaSupport": true, 
                    "ImageId": "ami-0b33d91d", 
                    "PrivateDnsName": "ip-172-31-25-133.ec2.internal", 
                    "KeyName": "keypair3", 
                    "SecurityGroups": [
                        {
                            "GroupName": "mysg", 
                            "GroupId": "sg-a364e4df"
                        }
                    ], 
                    "ClientToken": "", 
                    "SubnetId": "subnet-09dda752", 
                    "InstanceType": "t2.micro", 
                    "NetworkInterfaces": [
                        {
                            "Status": "in-use", 
                            "MacAddress": "0e:a0:9c:c8:ef:14", 
                            "SourceDestCheck": true, 
                            "VpcId": "vpc-adb325cb", 
                            "Description": "", 
                            "Association": {
                                "PublicIp": "54.165.167.87", 
                                "PublicDnsName": "ec2-54-165-167-87.compute-1.amazonaws.com", 
                                "IpOwnerId": "amazon"
                            }, 
                            "NetworkInterfaceId": "eni-b40ebe70", 
                            "PrivateIpAddresses": [
                                {
                                    "PrivateDnsName": "ip-172-31-25-133.ec2.internal", 
                                    "Association": {
                                        "PublicIp": "54.165.167.87", 
                                        "PublicDnsName": "ec2-54-165-167-87.compute-1.amazonaws.com", 
                                        "IpOwnerId": "amazon"
                                    }, 
                                    "Primary": true, 
                                    "PrivateIpAddress": "172.31.25.133"
                                }
                            ], 
                            "PrivateDnsName": "ip-172-31-25-133.ec2.internal", 
                            "Attachment": {
                                "Status": "attached", 
                                "DeviceIndex": 0, 
                                "DeleteOnTermination": true, 
                                "AttachmentId": "eni-attach-6cf6d332", 
                                "AttachTime": "2017-02-13T00:24:52.000Z"
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
                            "PrivateIpAddress": "172.31.25.133"
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
                            "DeviceName": "/dev/xvda", 
                            "Ebs": {
                                "Status": "attached", 
                                "DeleteOnTermination": true, 
                                "VolumeId": "vol-07171c3dd90e84036", 
                                "AttachTime": "2017-02-13T00:24:53.000Z"
                            }
                        }
                    ], 
                    "Architecture": "x86_64", 
                    "RootDeviceType": "ebs", 
                    "RootDeviceName": "/dev/xvda", 
                    "VirtualizationType": "hvm", 
                    "AmiLaunchIndex": 0
                }
            ]
        }
    ]
}
```

### Create a 1GB volume and attach it to one of the instances
According to the above infomation, I knew the instance id and public DNS of my two running Linux instances:

i-0892e3a2148d40757    ec2-54-242-31-152.compute-1.amazonaws.com
i-03c597e94f5bd3809    ec2-54-165-167-87.compute-1.amazonaws.com

And their "AvailabilityZone" is "us-east-1d"
I create the colume and attach it to the first instance "/dev/sdf".

```
bash-3.2$ aws ec2 create-volume --no-dry-run --size 1 --availability-zone us-east-1b --volume-type gp2 --no-encrypted
{
    "AvailabilityZone": "us-east-1b", 
    "Encrypted": false, 
    "VolumeType": "gp2", 
    "VolumeId": "vol-020bf1f8883a55593", 
    "State": "creating", 
    "Iops": 100, 
    "SnapshotId": "", 
    "CreateTime": "2017-02-13T00:34:46.510Z", 
    "Size": 1
}



bash-3.2$ aws ec2 attach-volume --volume-id vol-020bf1f8883a55593 --instance-id i-0892e3a2148d40757 --device /dev/sdf
{
    "AttachTime": "2017-02-13T00:35:18.188Z", 
    "InstanceId": "i-0892e3a2148d40757", 
    "VolumeId": "vol-020bf1f8883a55593", 
    "State": "attaching", 
    "Device": "/dev/sdf"
}
```

### Create the new file system on the first linux instance
1. Use lsblk to view available disk devices and their mount points.
2. Determine whether we need to create a file system on the volume. In Linux, use the sudo file -s device command to list special information.
3. Make a new file system by using command mkfs.
4. Check again on step 2.
5. Create a mount point directory for the volume.
6. Mount the volume at the location we just created.

In Linux, I create a exts4 type file system. Using the command `mkfs`, we could use `-t` to point out which type we want to create.

```
bash-3.2$ ssh -i p.pem ec2-user@ec2-54-242-31-152.compute-1.amazonaws.com
The authenticity of host 'ec2-54-242-31-152.compute-1.amazonaws.com (54.242.31.152)' can't be established.
ECDSA key fingerprint is SHA256:KrwlS0mnxQph+wOGxgzmWpOJ9FqL4nhZfBu/kZ0CF5U.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'ec2-54-242-31-152.compute-1.amazonaws.com,54.242.31.152' (ECDSA) to the list of known hosts.

       __|  __|_  )
       _|  (     /   Amazon Linux AMI
      ___|\___|___|

https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/
3 package(s) needed for security, out of 6 available
Run "sudo yum update" to apply all updates.
[ec2-user@ip-172-31-26-132 ~]$ lsblk
NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
xvda    202:0    0   8G  0 disk 
└─xvda1 202:1    0   8G  0 part /
xvdf    202:80   0   1G  0 disk
[ec2-user@ip-172-31-26-132 ~]$ sudo file -s /dev/xvdf
/dev/xvdf: data
[ec2-user@ip-172-31-26-132 ~]$ sudo mkfs -t ext4 /dev/xvdf
mke2fs 1.42.12 (29-Aug-2014)
Creating filesystem with 262144 4k blocks and 65536 inodes
Filesystem UUID: 2fde40f0-e868-4590-b225-eb35a32b15be
Superblock backups stored on blocks: 
	32768, 98304, 163840, 229376

Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (8192 blocks): done
Writing superblocks and filesystem accounting information: done

[ec2-user@ip-172-31-26-132 ~]$ sudo file -s /dev/xvdf
/dev/xvdf: Linux rev 1.0 ext4 filesystem data, UUID=2fde40f0-e868-4590-b225-eb35a32b15be (extents) (large files) (huge files)
[ec2-user@ip-172-31-26-132 ~]$ sudo mkdir data
[ec2-user@ip-172-31-26-132 ~]$ sudo mount /dev/xvdf/ ~/data
[ec2-user@ip-172-31-26-132 ~]$ mount
proc on /proc type proc (rw,relatime)
sysfs on /sys type sysfs (rw,relatime)
devtmpfs on /dev type devtmpfs (rw,relatime,size=498764k,nr_inodes=124691,mode=755)
devpts on /dev/pts type devpts (rw,relatime,gid=5,mode=620,ptmxmode=000)
tmpfs on /dev/shm type tmpfs (rw,relatime)
/dev/xvda1 on / type ext4 (rw,noatime,data=ordered)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw,relatime)
/dev/xvdf on /home/ec2-user/data type ext4 (rw,relatime,data=ordered)
```

Then we create a file ('TestFile') in this volume

```
[ec2-user@ip-172-31-26-132 ~]$ sudo chmod 777 data
[ec2-user@ip-172-31-26-132 ~]$ cd data
[ec2-user@ip-172-31-26-132 data]$ vi TestFile
[ec2-user@ip-172-31-26-132 data]$ ls
lost+found  TestFile
[ec2-user@ip-172-31-26-132 data]$ 
```
### Terminate the first Linux instace

```
[ec2-user@ip-172-31-26-132 data]$ exit
logout
Connection to ec2-54-242-31-152.compute-1.amazonaws.com closed.
bash-3.2$ aws ec2 terminate-instances --instance-ids i-0892e3a2148d40757
{
    "TerminatingInstances": [
        {
            "InstanceId": "i-0892e3a2148d40757", 
            "CurrentState": {
                "Code": 32, 
                "Name": "shutting-down"
            }, 
            "PreviousState": {
                "Code": 16, 
                "Name": "running"
            }
        }
    ]
}
```

### Attach the volume to the second instance
The volume id is: vol-020bf1f8883a55593
The second instance id is:i-03c597e94f5bd3809  
The second instance public DNS is: ec2-54-165-167-87.compute-1.amazonaws.com

Check the state of this volume.
```
bash-3.2$ aws ec2 describe-volumes --filters Name=volume-id,Values=vol-020bf1f8883a55593
{
    "Volumes": [
        {
            "AvailabilityZone": "us-east-1b", 
            "Attachments": [], 
            "Encrypted": false, 
            "VolumeType": "gp2", 
            "VolumeId": "vol-020bf1f8883a55593", 
            "State": "available", 
            "Iops": 100, 
            "SnapshotId": "", 
            "CreateTime": "2017-02-13T00:34:46.510Z", 
            "Size": 1
        }
    ]
}
```

We find that its state is available. Attach it to the second instance.

```
bash-3.2$ aws ec2 attach-volume --volume-id vol-020bf1f8883a55593 --instance-id i-03c597e94f5bd3809 --device /dev/sdf
{
    "AttachTime": "2017-02-13T01:11:02.840Z", 
    "InstanceId": "i-03c597e94f5bd3809", 
    "VolumeId": "vol-020bf1f8883a55593", 
    "State": "attaching", 
    "Device": "/dev/sdf"
}
```
SSH to the seconde instance, mount the volume and retrieve the file we just created.

```
bash-3.2$ pwd
/Users/kk/Documents
bash-3.2$ ssh -i p.pem ec2-user@ec2-54-165-167-87.compute-1.amazonaws.com
The authenticity of host 'ec2-54-165-167-87.compute-1.amazonaws.com (54.165.167.87)' can't be established.
ECDSA key fingerprint is SHA256:GRYNKKQ7WPTdq5jIxx6MA2tl7lCcbpoM58dMOeP6KfQ.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'ec2-54-165-167-87.compute-1.amazonaws.com,54.165.167.87' (ECDSA) to the list of known hosts.

       __|  __|_  )
       _|  (     /   Amazon Linux AMI
      ___|\___|___|

https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/
3 package(s) needed for security, out of 6 available
Run "sudo yum update" to apply all updates.

[ec2-user@ip-172-31-25-133 ~]$ lsblk
NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
xvda    202:0    0   8G  0 disk 
└─xvda1 202:1    0   8G  0 part /
xvdf    202:80   0   1G  0 disk 
[ec2-user@ip-172-31-25-133 ~]$ mkdir data
[ec2-user@ip-172-31-25-133 ~]$ sudo mount /dev/xvdf/ ~/data
[ec2-user@ip-172-31-25-133 ~]$ mount
proc on /proc type proc (rw,relatime)
sysfs on /sys type sysfs (rw,relatime)
devtmpfs on /dev type devtmpfs (rw,relatime,size=498764k,nr_inodes=124691,mode=755)
devpts on /dev/pts type devpts (rw,relatime,gid=5,mode=620,ptmxmode=000)
tmpfs on /dev/shm type tmpfs (rw,relatime)
/dev/xvda1 on / type ext4 (rw,noatime,data=ordered)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw,relatime)
/dev/xvdf on /home/ec2-user/data type ext4 (rw,relatime,data=ordered)
[ec2-user@ip-172-31-25-133 ~]$ sudo chmod 777 data
[ec2-user@ip-172-31-25-133 ~]$ cd data
[ec2-user@ip-172-31-25-133 data]$ ls
lost+found  TestFile
```
Then we use `scp` to retrieve the file.

```
bash-3.2$ scp -i p.pem ec2-user@ec2-54-165-167-87.compute-1.amazonaws.com:~/data/TestFile ~/Documents/Testfile
TestFile                                                                                  100%    7     0.6KB/s   00:00    
bash-3.2$ vi Testfile
bash-3.2$ exit
exit

Script done, output file is timestamps
```

#Run 3
## Test Can I use the same volume / filesystem across different OS instances
The volume id we create in OmniOS: vol-0a3064debd17cede4 

unmount the volume
```
bash-3.2$ cd Documents
bash-3.2$ ssh -i p.pem root@ec2-54-166-108-26.compute-1.amazonaws.com
Last login: Mon Feb 13 06:40:12 2017 from 98.109.151.68
OmniOS 5.11     omnios-r151020-b5b8c75  November 2016
root@ip-172-31-51-44:/root# umount /data
```

Reboot the instance of OmniOS

```
root@ip-172-31-51-44:/root# shutdown -y -i6 -g0

Shutdown started.    February 13, 2017 07:51:33 AM UTC

Changing to init state 6 - please wait
Broadcast Message from root (pts/1) on ip-172-31-51-44 Mon Feb 13 07:51:33...
THE SYSTEM ip-172-31-51-44 IS BEING SHUT DOWN NOW ! ! !
Log off now or risk your files being damaged

showmount: ip-172-31-51-44: RPC: Program not registered
^Croot@ip-172-31-51-44:/root# packet_write_wait: Connection to 54.166.108.26 port 22: Broken pipe
```

Detach it
```
bash-3.2$ aws ec2 detach-volume --volume-id vol-0a3064debd17cede4
{
    "AttachTime": "2017-02-13T06:26:28.000Z", 
    "InstanceId": "i-0f177e140a2d45383", 
    "VolumeId": "vol-0a3064debd17cede4", 
    "State": "detaching", 
    "Device": "/dev/sdf"
}
```
OH! After I detach the volume, the volume immediately was terminated... I would try to create another one with file system in OmniOS.
Wait...I don'n know what happen. The volume state change from `terminated` to `running`. Never mind, keep test. 

Check the state of this volume.
```
bash-3.2$ aws ec2 describe-volumes --filters Name=volume-id,Values=vol-0a3064debd17cede4
{
    "Volumes": [
        {
            "AvailabilityZone": "us-east-1d", 
            "Attachments": [], 
            "Encrypted": false, 
            "VolumeType": "gp2", 
            "VolumeId": "vol-0a3064debd17cede4", 
            "State": "available", 
            "Iops": 100, 
            "SnapshotId": "", 
            "CreateTime": "2017-02-13T05:19:24.216Z", 
            "Size": 1
        }
    ]
}
```

Creat a linux instance in `us-east-1d`
```
bash-3.2$ aws ec2 run-instances --image-id ami-0b33d91d --count 1 --instance-type t2.micro --placement AvailabilityZone=us-east-1d --key-name keypair3 --security-groups mysg
{
    "OwnerId": "624990436890", 
    "ReservationId": "r-0634424c6101c95eb", 
    "Groups": [], 
    "Instances": [
        {
            "Monitoring": {
                "State": "disabled"
            }, 
            "PublicDnsName": "", 
            "RootDeviceType": "ebs", 
            "State": {
                "Code": 0, 
                "Name": "pending"
            }, 
            "EbsOptimized": false, 
            "LaunchTime": "2017-02-13T07:40:04.000Z", 
            "PrivateIpAddress": "172.31.48.166", 
            "ProductCodes": [], 
            "VpcId": "vpc-adb325cb", 
            "StateTransitionReason": "", 
            "InstanceId": "i-0e28b8fb27b75b707", 
            "ImageId": "ami-0b33d91d", 
            "PrivateDnsName": "ip-172-31-48-166.ec2.internal", 
            "KeyName": "keypair3", 
            "SecurityGroups": [
                {
                    "GroupName": "mysg", 
                    "GroupId": "sg-a364e4df"
                }
            ], 
            "ClientToken": "", 
            "SubnetId": "subnet-8e2c63a3", 
            "InstanceType": "t2.micro", 
            "NetworkInterfaces": [
                {
                    "Status": "in-use", 
                    "MacAddress": "12:9b:60:2c:bc:d4", 
                    "SourceDestCheck": true, 
                    "VpcId": "vpc-adb325cb", 
                    "Description": "", 
                    "NetworkInterfaceId": "eni-ffcd790d", 
                    "PrivateIpAddresses": [
                        {
                            "PrivateDnsName": "ip-172-31-48-166.ec2.internal", 
                            "Primary": true, 
                            "PrivateIpAddress": "172.31.48.166"
                        }
                    ], 
                    "PrivateDnsName": "ip-172-31-48-166.ec2.internal", 
                    "Attachment": {
                        "Status": "attaching", 
                        "DeviceIndex": 0, 
                        "DeleteOnTermination": true, 
                        "AttachmentId": "eni-attach-6c650246", 
                        "AttachTime": "2017-02-13T07:40:04.000Z"
                    }, 
                    "Groups": [
                        {
                            "GroupName": "mysg", 
                            "GroupId": "sg-a364e4df"
                        }
                    ], 
                    "Ipv6Addresses": [], 
                    "SubnetId": "subnet-8e2c63a3", 
                    "OwnerId": "624990436890", 
                    "PrivateIpAddress": "172.31.48.166"
                }
            ], 
            "SourceDestCheck": true, 
            "Placement": {
                "Tenancy": "default", 
                "GroupName": "", 
                "AvailabilityZone": "us-east-1d"
            }, 
            "Hypervisor": "xen", 
            "BlockDeviceMappings": [], 
            "Architecture": "x86_64", 
            "StateReason": {
                "Message": "pending", 
                "Code": "pending"
            }, 
            "RootDeviceName": "/dev/xvda", 
            "VirtualizationType": "hvm", 
            "AmiLaunchIndex": 0
        }
    ]
}
```

Get the info of this instance
```
bash-3.2$ aws ec2 describe-instances --filters "Name=instance-id,Values=i-0e28b8fb27b75b707"
{
    "Reservations": [
        {
            "OwnerId": "624990436890", 
            "ReservationId": "r-0634424c6101c95eb", 
            "Groups": [], 
            "Instances": [
                {
                    "Monitoring": {
                        "State": "disabled"
                    }, 
                    "PublicDnsName": "ec2-52-70-181-33.compute-1.amazonaws.com", 
                    "State": {
                        "Code": 16, 
                        "Name": "running"
                    }, 
                    "EbsOptimized": false, 
                    "LaunchTime": "2017-02-13T07:40:04.000Z", 
                    "PublicIpAddress": "52.70.181.33", 
                    "PrivateIpAddress": "172.31.48.166", 
                    "ProductCodes": [], 
                    "VpcId": "vpc-adb325cb", 
                    "StateTransitionReason": "", 
                    "InstanceId": "i-0e28b8fb27b75b707", 
                    "EnaSupport": true, 
                    "ImageId": "ami-0b33d91d", 
                    "PrivateDnsName": "ip-172-31-48-166.ec2.internal", 
                    "KeyName": "keypair3", 
                    "SecurityGroups": [
                        {
                            "GroupName": "mysg", 
                            "GroupId": "sg-a364e4df"
                        }
                    ], 
                    "ClientToken": "", 
                    "SubnetId": "subnet-8e2c63a3", 
                    "InstanceType": "t2.micro", 
                    "NetworkInterfaces": [
                        {
                            "Status": "in-use", 
                            "MacAddress": "12:9b:60:2c:bc:d4", 
                            "SourceDestCheck": true, 
                            "VpcId": "vpc-adb325cb", 
                            "Description": "", 
                            "Association": {
                                "PublicIp": "52.70.181.33", 
                                "PublicDnsName": "ec2-52-70-181-33.compute-1.amazonaws.com", 
                                "IpOwnerId": "amazon"
                            }, 
                            "NetworkInterfaceId": "eni-ffcd790d", 
                            "PrivateIpAddresses": [
                                {
                                    "PrivateDnsName": "ip-172-31-48-166.ec2.internal", 
                                    "Association": {
                                        "PublicIp": "52.70.181.33", 
                                        "PublicDnsName": "ec2-52-70-181-33.compute-1.amazonaws.com", 
                                        "IpOwnerId": "amazon"
                                    }, 
                                    "Primary": true, 
                                    "PrivateIpAddress": "172.31.48.166"
                                }
                            ], 
                            "PrivateDnsName": "ip-172-31-48-166.ec2.internal", 
                            "Attachment": {
                                "Status": "attached", 
                                "DeviceIndex": 0, 
                                "DeleteOnTermination": true, 
                                "AttachmentId": "eni-attach-6c650246", 
                                "AttachTime": "2017-02-13T07:40:04.000Z"
                            }, 
                            "Groups": [
                                {
                                    "GroupName": "mysg", 
                                    "GroupId": "sg-a364e4df"
                                }
                            ], 
                            "Ipv6Addresses": [], 
                            "SubnetId": "subnet-8e2c63a3", 
                            "OwnerId": "624990436890", 
                            "PrivateIpAddress": "172.31.48.166"
                        }
                    ], 
                    "SourceDestCheck": true, 
                    "Placement": {
                        "Tenancy": "default", 
                        "GroupName": "", 
                        "AvailabilityZone": "us-east-1d"
                    }, 
                    "Hypervisor": "xen", 
                    "BlockDeviceMappings": [
                        {
                            "DeviceName": "/dev/xvda", 
                            "Ebs": {
                                "Status": "attached", 
                                "DeleteOnTermination": true, 
                                "VolumeId": "vol-0f29532370cb532b9", 
                                "AttachTime": "2017-02-13T07:40:05.000Z"
                            }
                        }
                    ], 
                    "Architecture": "x86_64", 
                    "RootDeviceType": "ebs", 
                    "RootDeviceName": "/dev/xvda", 
                    "VirtualizationType": "hvm", 
                    "AmiLaunchIndex": 0
                }
            ]
        }
    ]
}
```

### Attach the volume to the instance

We knew: 
The volume id is: vol-0a3064debd17cede4
instance-id = i-0e28b8fb27b75b707  
public DNS = ec2-52-70-181-33.compute-1.amazonaws.com

```
bash-3.2$ aws ec2 attach-volume --volume-id vol-0a3064debd17cede4 --instance-id i-0e28b8fb27b75b707 --device /dev/sdf
{
    "AttachTime": "2017-02-13T07:59:21.710Z", 
    "InstanceId": "i-0e28b8fb27b75b707", 
    "VolumeId": "vol-0a3064debd17cede4", 
    "State": "attaching", 
    "Device": "/dev/sdf"
}
```
SSH to the instance of Linux, mount the volume and check the file.

```
bash-3.2$ pwd
/Users/kk/Documents
bash-3.2$ ssh -i p.pem ec2-user@ec2-52-70-181-33.compute-1.amazonaws.com
The authenticity of host 'ec2-52-70-181-33.compute-1.amazonaws.com (52.70.181.33)' can't be established.
ECDSA key fingerprint is SHA256:055jVmtgghod4qBq0FtRNZxiJrEIclh1fCxkq6x3XQ4.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'ec2-52-70-181-33.compute-1.amazonaws.com,52.70.181.33' (ECDSA) to the list of known hosts.

       __|  __|_  )
       _|  (     /   Amazon Linux AMI
      ___|\___|___|

https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/
3 package(s) needed for security, out of 6 available
Run "sudo yum update" to apply all updates.
[ec2-user@ip-172-31-48-166 ~]$ 
[ec2-user@ip-172-31-48-166 data]$ lsblk
NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
xvda    202:0    0   8G  0 disk 
└─xvda1 202:1    0   8G  0 part /
xvdf    202:80   0   1G  0 disk 
[ec2-user@ip-172-31-48-166 ~]$ sudo mount /dev/xvdf ~/data
mount: /dev/xvdf is write-protected, mounting read-only
[ec2-user@ip-172-31-48-166 ~]$ cd ~/data
[ec2-user@ip-172-31-48-166 data]$ ls
lost+found  testfile
[ec2-user@ip-172-31-48-166 data]$ vi testfile

```
### Conclusion
We can use the same volume / filesystem across different OS instances.
But the volumn was write-protected state, mounting read-only.
I found something in this web:
http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/monitoring-volume-status.html

"When Amazon EBS determines that a volume's data is potentially inconsistent, it disables I/O to the volume from any attached EC2 instances by default. This causes the volume status check to fail, and creates a volume status event that indicates the cause of the failure."

Check the Attribute of autoEnableIO
```
bash-3.2$ aws ec2 describe-volume-attribute --volume-id vol-0a3064debd17cede4 --attribute autoEnableIO
{
    "AutoEnableIO": {
        "Value": false
    }, 
    "VolumeId": "vol-0a3064debd17cede4"
}
```

Active the AutoEnableIO.
```
bash-3.2$ aws ec2 modify-volume-attribute --volume-id vol-0a3064debd17cede4 --auto-enable-io
bash-3.2$ aws ec2 describe-volume-attribute --volume-id vol-0a3064debd17cede4 --attribute autoEnableIO
{
    "AutoEnableIO": {
        "Value": true
    }, 
    "VolumeId": "vol-0a3064debd17cede4"
}
```

But after setting and reboot the instance, mounting still is read-only...
I check the mount
```
[ec2-user@ip-172-31-48-166 data]$ mount | grep xvdf
/dev/xvdf on /home/ec2-user/data type ufs (ro,relatime,ufstype=old,onerror=lock)
```

I think the reason why volume lock is that this ufstype is too old... So this Linux cann't support.
