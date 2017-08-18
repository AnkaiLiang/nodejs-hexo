---
title: Install and Configure AWS Tools
date: 2017-05-19 03:32:39
tags: System Administration
description: "CS615 Assignment1"
---
<!-- more -->
* Ankai Liang
* CWID:10411998
* Environment: Mac OS 


### Install AWS Tool
```
➜  bin git:(master) sudo pip install awscli --ignore-installed six
```
### AWS Command Line Configuration

```
➜  bin git:(master) aws configure
AWS Access Key ID [None]: ***
AWS Secret Access Key [None]: ***
Default region name [None]: ***
Default output format [None]: ***
```

### Creating a Key Pair and setting the chomod mod

```
➜  Documents git:(master) ✗ aws ec2 create-key-pair --key-name keypair3 --query 'KeyMaterial' --output text > p.pem
➜  Documents git:(master) ✗ chmod 400 p.pem 
➜  Documents git:(master) ✗ aws ec2 create-security-group --group-name mysg --description "My security group" 
{
    "GroupId": "sg-a364e4df"
}
```

### Adding Rules to Your Security Group
```
➜  Documents git:(master) ✗ aws ec2 authorize-security-group-ingress --group-name mysg --protocol tcp --port 22 --cidr 0.0.0.0/0 
```

## CentOS

### Find images id (get ami-50ecc847)
```
➜  Documents git:(master) ✗ aws ec2 describe-images --filters 'Name=name, Values=OmniOS r151020*' 
{
    "Images": [
        {
            "VirtualizationType": "paravirtual", 
            "Name": "OmniOS r151020 Stable 20161102", 
            "Hypervisor": "xen", 
            "ImageId": "ami-50ecc847", 
            "RootDeviceType": "ebs", 
            "State": "available", 
            "BlockDeviceMappings": [
                {
                    "DeviceName": "/dev/sda", 
                    "Ebs": {
                        "DeleteOnTermination": true, 
                        "SnapshotId": "snap-48c359d7", 
                        "VolumeSize": 8, 
                        "VolumeType": "gp2", 
                        "Encrypted": false
                    }
                }
            ], 
            "Architecture": "x86_64", 
            "ImageLocation": "182711560792/OmniOS r151020 Stable 20161102", 
            "KernelId": "aki-b4aa75dd", 
            "OwnerId": "182711560792", 
            "RootDeviceName": "/dev/sda", 
            "CreationDate": "2016-11-02T19:38:56.000Z", 
            "Public": true, 
            "ImageType": "machine", 
            "Description": "OmniOS r151020 Stable created 20161102"
        }
    ]
}

```
### Run a instance
```
➜  Documents git:(master) ✗ aws ec2 run-instances --image-id ami-50ecc847 --count 1 --instance-type t1.micro --key-name keypair3 --security-groups mysg
{
    "OwnerId": "624990436890", 
    "ReservationId": "r-01c81ac895aa8c726", 
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
            "LaunchTime": "2017-01-30T02:24:36.000Z", 
            "PrivateIpAddress": "172.31.15.139", 
            "ProductCodes": [], 
            "VpcId": "vpc-adb325cb", 
            "StateTransitionReason": "", 
            "InstanceId": "i-054b740b8e10e8438", 
            "ImageId": "ami-50ecc847", 
            "PrivateDnsName": "ip-172-31-15-139.ec2.internal", 
            "KeyName": "keypair3", 
            "SecurityGroups": [
                {
                    "GroupName": "mysg", 
                    "GroupId": "sg-a364e4df"
                }
            ], 
            "ClientToken": "", 
            "SubnetId": "subnet-6e82bf27", 
            "InstanceType": "t1.micro", 
            "NetworkInterfaces": [
                {
                    "Status": "in-use", 
                    "MacAddress": "0a:16:eb:98:f7:d4", 
                    "SourceDestCheck": true, 
                    "VpcId": "vpc-adb325cb", 
                    "Description": "", 
                    "NetworkInterfaceId": "eni-2533a1c4", 
                    "PrivateIpAddresses": [
                        {
                            "PrivateDnsName": "ip-172-31-15-139.ec2.internal", 
                            "Primary": true, 
                            "PrivateIpAddress": "172.31.15.139"
                        }
                    ], 
                    "PrivateDnsName": "ip-172-31-15-139.ec2.internal", 
                    "Attachment": {
                        "Status": "attaching", 
                        "DeviceIndex": 0, 
                        "DeleteOnTermination": true, 
                        "AttachmentId": "eni-attach-6cd9522f", 
                        "AttachTime": "2017-01-30T02:24:36.000Z"
                    }, 
                    "Groups": [
                        {
                            "GroupName": "mysg", 
                            "GroupId": "sg-a364e4df"
                        }
                    ], 
                    "Ipv6Addresses": [], 
                    "SubnetId": "subnet-6e82bf27", 
                    "OwnerId": "624990436890", 
                    "PrivateIpAddress": "172.31.15.139"
                }
            ], 
            "SourceDestCheck": true, 
            "Placement": {
                "Tenancy": "default", 
                "GroupName": "", 
                "AvailabilityZone": "us-east-1a"
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

### Create a Tag for my Instance
From above: "InstanceId": "i-054b740b8e10e8438"
```
➜  Documents git:(master) ✗ aws ec2 create-tags --resources i-054b740b8e10e8438 --tags Key=Name,Value=MyInstance
```

### Get the info of my Instance
```
➜  Documents git:(master) ✗ aws ec2 describe-instances --filters "Name=instance-id,Values=i-054b740b8e10e8438"
{
    "Reservations": [
        {
            "OwnerId": "624990436890", 
            "ReservationId": "r-01c81ac895aa8c726", 
            "Groups": [], 
            "Instances": [
                {
                    "Monitoring": {
                        "State": "disabled"
                    }, 
                    "PublicDnsName": "ec2-54-89-190-118.compute-1.amazonaws.com", 
                    "RootDeviceType": "ebs", 
                    "State": {
                        "Code": 16, 
                        "Name": "running"
                    }, 
                    "EbsOptimized": false, 
                    "LaunchTime": "2017-01-30T02:24:36.000Z", 
                    "PublicIpAddress": "54.89.190.118", 
                    "PrivateIpAddress": "172.31.15.139", 
                    "ProductCodes": [], 
                    "VpcId": "vpc-adb325cb", 
                    "StateTransitionReason": "", 
                    "InstanceId": "i-054b740b8e10e8438", 
                    "ImageId": "ami-50ecc847", 
                    "PrivateDnsName": "ip-172-31-15-139.ec2.internal", 
                    "KeyName": "keypair3", 
                    "SecurityGroups": [
                        {
                            "GroupName": "mysg", 
                            "GroupId": "sg-a364e4df"
                        }
                    ], 
                    "ClientToken": "", 
                    "SubnetId": "subnet-6e82bf27", 
                    "InstanceType": "t1.micro", 
                    "NetworkInterfaces": [
                        {
                            "Status": "in-use", 
                            "MacAddress": "0a:16:eb:98:f7:d4", 
                            "SourceDestCheck": true, 
                            "VpcId": "vpc-adb325cb", 
                            "Description": "", 
                            "Association": {
                                "PublicIp": "54.89.190.118", 
                                "PublicDnsName": "ec2-54-89-190-118.compute-1.amazonaws.com", 
                                "IpOwnerId": "amazon"
                            }, 
                            "NetworkInterfaceId": "eni-2533a1c4", 
                            "PrivateIpAddresses": [
                                {
                                    "PrivateDnsName": "ip-172-31-15-139.ec2.internal", 
                                    "Association": {
                                        "PublicIp": "54.89.190.118", 
                                        "PublicDnsName": "ec2-54-89-190-118.compute-1.amazonaws.com", 
                                        "IpOwnerId": "amazon"
                                    }, 
                                    "Primary": true, 
                                    "PrivateIpAddress": "172.31.15.139"
                                }
                            ], 
                            "PrivateDnsName": "ip-172-31-15-139.ec2.internal", 
                            "Attachment": {
                                "Status": "attached", 
                                "DeviceIndex": 0, 
                                "DeleteOnTermination": true, 
                                "AttachmentId": "eni-attach-6cd9522f", 
                                "AttachTime": "2017-01-30T02:24:36.000Z"
                            }, 
                            "Groups": [
                                {
                                    "GroupName": "mysg", 
                                    "GroupId": "sg-a364e4df"
                                }
                            ], 
                            "Ipv6Addresses": [], 
                            "SubnetId": "subnet-6e82bf27", 
                            "OwnerId": "624990436890", 
                            "PrivateIpAddress": "172.31.15.139"
                        }
                    ], 
                    "SourceDestCheck": true, 
                    "Placement": {
                        "Tenancy": "default", 
                        "GroupName": "", 
                        "AvailabilityZone": "us-east-1a"
                    }, 
                    "Hypervisor": "xen", 
                    "BlockDeviceMappings": [
                        {
                            "DeviceName": "/dev/sda", 
                            "Ebs": {
                                "Status": "attached", 
                                "DeleteOnTermination": true, 
                                "VolumeId": "vol-0582ffa74b5a1b765", 
                                "AttachTime": "2017-01-30T02:24:37.000Z"
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
        }
    ]
}
```
### SSH to Instance and Check the info
From above:
"PublicDnsName": "ec2-54-89-190-118.compute-1.amazonaws.com"

```
➜  Documents git:(master) ✗ ssh -i p.pem root@ec2-54-89-190-118.compute-1.amazonaws.com
Last login: Mon Jan 30 02:52:26 2017 from 100.1.162.250
OmniOS 5.11     omnios-r151020-b5b8c75  November 2016
root@ip-10-152-178-106.ec2.internal:/root# uname -a
SunOS ip-10-152-178-106.ec2.internal 5.11 omnios-r151020-b5b8c75 i86pc i386 i86xpv
root@ip-10-152-178-106.ec2.internal:/root# whoami
root
root@ip-10-152-178-106.ec2.internal:/root# date
January 30, 2017 03:23:12 AM 
root@ip-10-152-178-106.ec2.internal:/root# w
03:23:18    up 57 min(s),  2 users,  load average: 0.00, 0.00, 0.00
User     tty      login@         idle    JCPU    PCPU what
root     pts/1    02:52:27         30       0       0 -bash
root     pts/2    03:22:13          0       0       0 w
root@ip-10-152-178-106.ec2.internal:/root# ifconfig -a
lo0: flags=2001000849<UP,LOOPBACK,RUNNING,MULTICAST,IPv4,VIRTUAL> mtu 8232 index 1
        inet 127.0.0.1 netmask ff000000 
xnf0: flags=1004843<UP,BROADCAST,RUNNING,MULTICAST,DHCP,IPv4> mtu 1500 index 2
        inet 172.31.15.139 netmask fffff000 broadcast 172.31.15.255
        ether a:16:eb:98:f7:d4 
lo0: flags=2002000849<UP,LOOPBACK,RUNNING,MULTICAST,IPv6,VIRTUAL> mtu 8252 index 1
        inet6 ::1/128 
xnf0: flags=20002000840<RUNNING,MULTICAST,IPv6> mtu 1500 index 2
        inet6 ::/0 
        ether a:16:eb:98:f7:d4 
root@ip-10-152-178-106.ec2.internal:/root# netstat -na

UDP: IPv4
   Local Address        Remote Address      State
-------------------- -------------------- ----------
      *.68                                Idle
      *.546                               Idle
172.31.15.139.68                          Idle
      *.111                               Idle
      *.*                                 Unbound
      *.50058                             Idle
      *.111                               Idle
      *.*                                 Unbound
      *.45332                             Idle
      *.*                                 Unbound

UDP: IPv6
   Local Address                     Remote Address                   State      If
--------------------------------- --------------------------------- ---------- -----
      *.546                                                         Idle       
      *.111                                                         Idle       
      *.*                                                           Unbound    
      *.50058                                                       Idle       
      *.*                                                           Unbound    

TCP: IPv4
   Local Address        Remote Address    Swind Send-Q Rwind Recv-Q    State
-------------------- -------------------- ----- ------ ----- ------ -----------
127.0.0.1.4999             *.*                0      0 128000      0 LISTEN
      *.111                *.*                0      0 128000      0 LISTEN
      *.*                  *.*                0      0 128000      0 IDLE
      *.111                *.*                0      0 128000      0 LISTEN
      *.*                  *.*                0      0 128000      0 IDLE
      *.56771              *.*                0      0 128000      0 LISTEN
      *.36196              *.*                0      0 128000      0 LISTEN
      *.22                 *.*                0      0 128000      0 LISTEN
172.31.15.139.22     100.1.162.250.59344  130976      0 128872      0 ESTABLISHED
172.31.15.139.22     98.109.151.68.59431  131072     35 128872      0 ESTABLISHED

TCP: IPv6
   Local Address                     Remote Address                 Swind Send-Q Rwind Recv-Q   State      If
--------------------------------- --------------------------------- ----- ------ ----- ------ ----------- -----
      *.111                             *.*                             0      0 128000      0 LISTEN      
      *.*                               *.*                             0      0 128000      0 IDLE        
      *.36196                           *.*                             0      0 128000      0 LISTEN      
      *.22                              *.*                             0      0 128000      0 LISTEN      

Active UNIX domain sockets
Address  Type          Vnode     Conn  Local Addr      Remote Addr
ffffff00a8af4020 dgram      ffffff00a8c77600 0000000 /var/run/in.ndpd_mib                
ffffff00a8af43d0 stream-ord ffffff00a8c77800 0000000 /var/run/in.ndpd_ipadm                
ffffff00a8af4780 stream-ord ffffff00a8bad040 0000000 /var/run/.inetd.uds                
ffffff00a8af4b30 stream-ord 0000000 0000000 /var/run/hald/dbus-PSIt9xbdm8                
ffffff00a8ac4018 stream-ord 0000000 0000000 /var/run/dbus/system_bus_socket                
ffffff00a8ac43c8 stream-ord 0000000 ffffff00a873c680                /var/run/dbus/system_bus_socket 
ffffff00a8ac4778 stream-ord 0000000 ffffff00a8a35280                /var/run/hald/dbus-PSIt9xbdm8 
ffffff00a8ac4b28 stream-ord 0000000 0000000 /var/run/hald/dbus-PSIt9xbdm8                
ffffff00a8a8e010 stream-ord 0000000 ffffff00a8a35280                /var/run/hald/dbus-PSIt9xbdm8 
ffffff00a8a8e3c0 stream-ord 0000000 0000000 /var/run/hald/dbus-s4jHYz6LbO                
ffffff00a8a8e770 stream-ord 0000000 ffffff00a8a32400                /var/run/hald/dbus-s4jHYz6LbO 
ffffff00a8a8eb20 stream-ord ffffff00a8a32400 0000000 /var/run/hald/dbus-s4jHYz6LbO                
ffffff00a7c4e008 stream-ord 0000000 0000000                               
ffffff00a7c4e3b8 stream-ord 0000000 0000000                               
ffffff00a7c4e768 stream-ord ffffff00a8a35280 0000000 /var/run/hald/dbus-PSIt9xbdm8                
ffffff00a7c4eb18 stream-ord ffffff00a873c680 0000000 /var/run/dbus/system_bus_socket
```
### Display the partition table, currently mounted filesystems, disk space
```
root@ip-10-152-178-106.ec2.internal:/root# format -M
Searching for disks...
No request sense for command inquiry
Inquiry failed

Inquiry failed - Inappropriate ioctl for device
done


AVAILABLE DISK SELECTIONS:
       0. c1t2048d0 <Unknown-Unknown-0001 cyl 4085 alt 2 hd 128 sec 32>
          /xpvd/xdf@2048
Specify disk (enter its number): 0
selecting c1t2048d0
[disk formatted, no defect list found]
             Total disk size is 4096 cylinders
             Cylinder size is 4096 (512 byte) blocks

                                               Cylinders
      Partition   Status    Type          Start   End   Length    %
      =========   ======    ============  =====   ===   ======   ===
          1                 DOS-BIG           0     7       8      0
          2                 Solaris2          8  4095    4088    100



SELECT ONE OF THE FOLLOWING:
   1. Create a partition
   2. Specify the active partition
   3. Delete a partition
   4. Change between Solaris and Solaris2 Partition IDs
   5. Edit/View extended partitions
   6. Exit (update disk configuration and exit)
   7. Cancel (exit without updating disk configuration)
Enter Selection: 7
```

```
root@ip-10-152-178-106.ec2.internal:/root# mount
/ on syspool/ROOT/omnios-r151020-1 read/write/setuid/devices/dev=1710002 on Thu Jan  1 00:00:00 1970
/devices on /devices read/write/setuid/devices/dev=8340000 on Mon Jan 30 02:26:31 2017
/dev on /dev read/write/setuid/devices/dev=8380000 on Mon Jan 30 02:26:31 2017
/system/contract on ctfs read/write/setuid/devices/dev=8440001 on Mon Jan 30 02:26:32 2017
/proc on proc read/write/setuid/devices/dev=83c0000 on Mon Jan 30 02:26:32 2017
/etc/mnttab on mnttab read/write/setuid/devices/dev=8480001 on Mon Jan 30 02:26:32 2017
/etc/svc/volatile on swap read/write/setuid/devices/xattr/dev=84c0001 on Mon Jan 30 02:26:32 2017
/system/object on objfs read/write/setuid/devices/dev=8500001 on Mon Jan 30 02:26:32 2017
/system/boot on bootfs read/write/setuid/devices/dev=8540001 on Mon Jan 30 02:26:32 2017
/etc/dfs/sharetab on sharefs read/write/setuid/devices/dev=8580001 on Mon Jan 30 02:26:32 2017
/lib/libc.so.1 on /usr/lib/libc/libc_hwcap3.so.1 read/write/setuid/devices/dev=1710002 on Mon Jan 30 02:27:04 2017
/dev/fd on fd read/write/setuid/devices/dev=8680001 on Mon Jan 30 02:27:09 2017
/tmp on swap read/write/setuid/devices/xattr/dev=84c0002 on Mon Jan 30 02:27:09 2017
/var/run on swap read/write/setuid/devices/xattr/dev=84c0003 on Mon Jan 30 02:27:09 2017
/syspool on syspool read/write/setuid/devices/nonbmand/exec/xattr/atime/dev=1710007 on Mon Jan 30 02:27:15 2017
```

```
root@ip-10-152-178-106.ec2.internal:/root# df -h
Filesystem             Size   Used  Available Capacity  Mounted on
syspool/ROOT/omnios-r151020-1
                       7.7G   864M       6.3G    12%    /
/devices                 0K     0K         0K     0%    /devices
/dev                     0K     0K         0K     0%    /dev
ctfs                     0K     0K         0K     0%    /system/contract
proc                     0K     0K         0K     0%    /proc
mnttab                   0K     0K         0K     0%    /etc/mnttab
swap                   261M   292K       261M     1%    /etc/svc/volatile
objfs                    0K     0K         0K     0%    /system/object
bootfs                   0K     0K         0K     0%    /system/boot
sharefs                  0K     0K         0K     0%    /etc/dfs/sharetab
/usr/lib/libc/libc_hwcap3.so.1
                       7.2G   864M       6.3G    12%    /lib/libc.so.1
fd                       0K     0K         0K     0%    /dev/fd
swap                   261M     0K       261M     0%    /tmp
swap                   261M    32K       261M     1%    /var/run
syspool                7.7G    30K       6.3G     1%    /syspool
```
## Ubuntu
### Images Select
Amazon Linux AMI 2016.09.1 (HVM), SSD Volume Type - ami-0b33d91d
### Run a instance
```
➜  bin git:(master) ✗ aws ec2 run-instances --image-id ami-0b33d91d --count 1 --instance-type t2.micro --key-name keypair3 --security-groups mysg
{
    "OwnerId": "624990436890", 
    "ReservationId": "r-081d903479e0a8659", 
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
            "LaunchTime": "2017-01-30T04:40:43.000Z", 
            "PrivateIpAddress": "172.31.25.111", 
            "ProductCodes": [], 
            "VpcId": "vpc-adb325cb", 
            "StateTransitionReason": "", 
            "InstanceId": "i-0f34e210bdf46cf93", 
            "ImageId": "ami-0b33d91d", 
            "PrivateDnsName": "ip-172-31-25-111.ec2.internal", 
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
                    "MacAddress": "0e:7e:53:40:0a:26", 
                    "SourceDestCheck": true, 
                    "VpcId": "vpc-adb325cb", 
                    "Description": "", 
                    "NetworkInterfaceId": "eni-274dd2e2", 
                    "PrivateIpAddresses": [
                        {
                            "PrivateDnsName": "ip-172-31-25-111.ec2.internal", 
                            "Primary": true, 
                            "PrivateIpAddress": "172.31.25.111"
                        }
                    ], 
                    "PrivateDnsName": "ip-172-31-25-111.ec2.internal", 
                    "Attachment": {
                        "Status": "attaching", 
                        "DeviceIndex": 0, 
                        "DeleteOnTermination": true, 
                        "AttachmentId": "eni-attach-7eccda21", 
                        "AttachTime": "2017-01-30T04:40:43.000Z"
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
                    "PrivateIpAddress": "172.31.25.111"
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

### Get the info of my Instance
From above: "InstanceId": "i-0f34e210bdf46cf93"

```
➜  bin git:(master) ✗ aws ec2 describe-instances --filters "Name=instance-id,Values=i-0f34e210bdf46cf93"
{
    "Reservations": [
        {
            "OwnerId": "624990436890", 
            "ReservationId": "r-081d903479e0a8659", 
            "Groups": [], 
            "Instances": [
                {
                    "Monitoring": {
                        "State": "disabled"
                    }, 
                    "PublicDnsName": "ec2-52-207-16-176.compute-1.amazonaws.com", 
                    "State": {
                        "Code": 16, 
                        "Name": "running"
                    }, 
                    "EbsOptimized": false, 
                    "LaunchTime": "2017-01-30T04:40:43.000Z", 
                    "PublicIpAddress": "52.207.16.176", 
                    "PrivateIpAddress": "172.31.25.111", 
                    "ProductCodes": [], 
                    "VpcId": "vpc-adb325cb", 
                    "StateTransitionReason": "", 
                    "InstanceId": "i-0f34e210bdf46cf93", 
                    "EnaSupport": true, 
                    "ImageId": "ami-0b33d91d", 
                    "PrivateDnsName": "ip-172-31-25-111.ec2.internal", 
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
                            "MacAddress": "0e:7e:53:40:0a:26", 
                            "SourceDestCheck": true, 
                            "VpcId": "vpc-adb325cb", 
                            "Description": "", 
                            "Association": {
                                "PublicIp": "52.207.16.176", 
                                "PublicDnsName": "ec2-52-207-16-176.compute-1.amazonaws.com", 
                                "IpOwnerId": "amazon"
                            }, 
                            "NetworkInterfaceId": "eni-274dd2e2", 
                            "PrivateIpAddresses": [
                                {
                                    "PrivateDnsName": "ip-172-31-25-111.ec2.internal", 
                                    "Association": {
                                        "PublicIp": "52.207.16.176", 
                                        "PublicDnsName": "ec2-52-207-16-176.compute-1.amazonaws.com", 
                                        "IpOwnerId": "amazon"
                                    }, 
                                    "Primary": true, 
                                    "PrivateIpAddress": "172.31.25.111"
                                }
                            ], 
                            "PrivateDnsName": "ip-172-31-25-111.ec2.internal", 
                            "Attachment": {
                                "Status": "attached", 
                                "DeviceIndex": 0, 
                                "DeleteOnTermination": true, 
                                "AttachmentId": "eni-attach-7eccda21", 
                                "AttachTime": "2017-01-30T04:40:43.000Z"
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
                            "PrivateIpAddress": "172.31.25.111"
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
                                "VolumeId": "vol-049fb7df3a019542f", 
                                "AttachTime": "2017-01-30T04:40:44.000Z"
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
### SSH to Instance and Check the info
From above:
"PublicDnsName": "ec2-52-207-16-176.compute-1.amazonaws.com"

```
➜  Documents git:(master) ✗ ssh -i p.pem ec2-user@ec2-52-207-16-176.compute-1.amazonaws.com

       __|  __|_  )
       _|  (     /   Amazon Linux AMI
      ___|\___|___|

https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/
[ec2-user@ip-172-31-25-111 ~]$ uname -a
Linux ip-172-31-25-111 4.4.41-36.55.amzn1.x86_64 #1 SMP Wed Jan 18 01:03:26 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux
[ec2-user@ip-172-31-25-111 ~]$ whoami
ec2-user
[ec2-user@ip-172-31-25-111 ~]$ date
Mon Jan 30 05:49:27 UTC 2017
[ec2-user@ip-172-31-25-111 ~]$ w
 05:49:28 up  1:08,  1 user,  load average: 0.00, 0.00, 0.00
USER     TTY      FROM              LOGIN@   IDLE   JCPU   PCPU WHAT
ec2-user pts/0    pool-98-109-151- 05:42    0.00s  0.00s  0.00s w
[ec2-user@ip-172-31-25-111 ~]$ ifconfig -a
eth0      Link encap:Ethernet  HWaddr 0E:7E:53:40:0A:26  
          inet addr:172.31.25.111  Bcast:172.31.31.255  Mask:255.255.240.0
          inet6 addr: fe80::c7e:53ff:fe40:a26/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:9001  Metric:1
          RX packets:4425 errors:0 dropped:0 overruns:0 frame:0
          TX packets:2918 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:4922228 (4.6 MiB)  TX bytes:218230 (213.1 KiB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:2 errors:0 dropped:0 overruns:0 frame:0
          TX packets:2 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1 
          RX bytes:140 (140.0 b)  TX bytes:140 (140.0 b)

[ec2-user@ip-172-31-25-111 ~]$ netstat -na
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address               Foreign Address             State      
tcp        0      0 127.0.0.1:25                0.0.0.0:*                   LISTEN      
tcp        0      0 0.0.0.0:111                 0.0.0.0:*                   LISTEN      
tcp        0      0 0.0.0.0:52816               0.0.0.0:*                   LISTEN      
tcp        0      0 0.0.0.0:22                  0.0.0.0:*                   LISTEN      
tcp        0    252 172.31.25.111:22            98.109.151.68:49300         ESTABLISHED 
tcp        0      0 :::50557                    :::*                        LISTEN      
tcp        0      0 :::111                      :::*                        LISTEN      
tcp        0      0 :::22                       :::*                        LISTEN      
udp        0      0 0.0.0.0:33305               0.0.0.0:*                               
udp        0      0 0.0.0.0:68                  0.0.0.0:*                               
udp        0      0 0.0.0.0:111                 0.0.0.0:*                               
udp        0      0 172.31.25.111:123           0.0.0.0:*                               
udp        0      0 127.0.0.1:123               0.0.0.0:*                               
udp        0      0 0.0.0.0:123                 0.0.0.0:*                               
udp        0      0 0.0.0.0:694                 0.0.0.0:*                               
udp        0      0 127.0.0.1:717               0.0.0.0:*                               
udp        0      0 fe80::c7e:53ff:fe40:a26:546 :::*                                    
udp        0      0 :::111                      :::*                                    
udp        0      0 :::694                      :::*                                    
udp        0      0 :::52689                    :::*                                    
Active UNIX domain sockets (servers and established)
Proto RefCnt Flags       Type       State         I-Node Path
unix  2      [ ACC ]     STREAM     LISTENING     8060   @/com/ubuntu/upstart
unix  2      [ ACC ]     SEQPACKET  LISTENING     8322   @/org/kernel/udev/udevd
unix  11     [ ]         DGRAM                    9389   /dev/log
unix  2      [ ACC ]     STREAM     LISTENING     9844   /var/run/rpcbind.sock
unix  2      [ ACC ]     STREAM     LISTENING     10017  /var/run/dbus/system_bus_socket
unix  2      [ ]         DGRAM                    11085  
unix  2      [ ]         DGRAM                    10973  
unix  3      [ ]         STREAM     CONNECTED     10025  
unix  3      [ ]         DGRAM                    8330   
unix  3      [ ]         STREAM     CONNECTED     11661  
unix  3      [ ]         DGRAM                    8331   
unix  2      [ ]         DGRAM                    11656  
unix  3      [ ]         STREAM     CONNECTED     11660  
unix  3      [ ]         STREAM     CONNECTED     10026  /var/run/dbus/system_bus_socket
unix  2      [ ]         DGRAM                    10150  
unix  2      [ ]         DGRAM                    10608  
unix  2      [ ]         DGRAM                    9920   
unix  2      [ ]         DGRAM                    10506  
unix  3      [ ]         STREAM     CONNECTED     10020  
unix  2      [ ]         DGRAM                    10587  
unix  2      [ ]         DGRAM                    10629  
unix  3      [ ]         STREAM     CONNECTED     10021 
```

### Display the partition table, currently mounted filesystems, disk space

```
[ec2-user@ip-172-31-25-111 ~]$ sudo su
[root@ip-172-31-25-111 ec2-user]# fdisk -l
WARNING: fdisk GPT support is currently new, and therefore in an experimental phase. Use at your own discretion.

Disk /dev/xvda: 8589 MB, 8589934592 bytes, 16777216 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk label type: gpt


#         Start          End    Size  Type            Name
 1         4096     16777182      8G  Linux filesyste Linux
128         2048         4095      1M  BIOS boot parti BIOS Boot Partition
[root@ip-172-31-25-111 ec2-user]# 
[root@ip-172-31-25-111 ec2-user]# df -h
Filesystem      Size  Used Avail Use% Mounted on
devtmpfs        488M   56K  488M   1% /dev
tmpfs           498M     0  498M   0% /dev/shm
/dev/xvda1      7.8G  984M  6.7G  13% /
[root@ip-172-31-25-111 ec2-user]# mount
proc on /proc type proc (rw,relatime)
sysfs on /sys type sysfs (rw,relatime)
devtmpfs on /dev type devtmpfs (rw,relatime,size=498764k,nr_inodes=124691,mode=755)
devpts on /dev/pts type devpts (rw,relatime,gid=5,mode=620,ptmxmode=000)
tmpfs on /dev/shm type tmpfs (rw,relatime)
/dev/xvda1 on / type ext4 (rw,noatime,data=ordered)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw,relatime)
```
## The Difference of Two Instance

1. The SSH access user names.
2. The orders which are used to view the disk info.
3. Instance type.