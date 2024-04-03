---
title: tcpdump(1) DNS
date: 2017-08-16 23:27:53
tags: System Administration
description: "CS615 Assignment4"
---

<!-- more -->

# Description
* link: http://www.cs.stevens.edu/~jschauma/615/s17-hw4.html

## Objective

The objective of this assignment is for you to learn how to use tcpdump to observe and analyze network traffic. This reinforces lessons from our lecture on networking and prepares you for our lecture on the DNS.

In order to be able to observe DNS traffic flowing between your host and the DNS root servers as well as other DNS servers, you will need to set up and configure a simple caching name server, aka a resolver.

Note: you must use tcpdump. Graphical helper applications such as "wireshark" or similar tools are explicitly prohibited. You need to be able to read the flat text tcpdump output yourself and not rely on other tools to highlight things for you.

## OS Instances

The exercises below can be done on any OS instance you like. You will need at least two OS instances, one for the DNS server and one for the "client". Make sure that the firewall rules between the server and client allow for all the required traffic.

### DNS server setup

Set up a caching only DNS server (a ``resolver'') on your OS instance. You may consult any online documentation available, such as this document or any others you prefer. You may use bind or any other DNS server software you like. The only restriction is that in the end your host must be able to function as a caching DNS server.

Set up your client host to use your newly created DNS server for host lookups.

tcpdump exercises

Use the tcpdump utility to monitor the network traffic using the following scenarios:

on the DNS server, run the following commands:
$ telnet www.yahoo.com 80
GET / HTTP/1.1
Host: www.yahoo.com
							
Track down the packets in your tcpdump referring to the DNS query from your DNS server to one of the root servers, then to the various DNS servers before the DNS information is returned to your server by one of Yahoo's authoritative DNS servers.
Identify the 3-way handshake that initiates the connection from your DNS server to port 80 on Yahoo's webserver, the packets that are being sent back and forth and finally the closing of the connection.


on your client host, run the following commands:
$ telnet www.tumblr.com 80
GET / HTTP/1.0
							
On your client: Track down the packets in your tcpdump referring to the DNS query from your client host to your DNS server.
On your DNS server: Track down the packets in your tcpdump referring to the DNS query from your DNS server to one of the root servers, then to the various DNS servers before the DNS information is returned to your server by one of Tumblr's authoritative DNS servers.


on the DNS server, perform a reverse host lookup (PTR) for a record not yet in your DNS server's cache; track down in your tcpdump all relevant DNS queries required to retrieve the result. Clearly identify which name servers you are communicating with and who operates them.

-----------------
# Content


## Set up a caching name server

I read some tutorials and decide to set uo my name server in Red Hats OS.
tutorals:
http://www.tecmint.com/install-configure-cache-only-dns-server-in-rhel-centos-7/
http://www.tldp.org/HOWTO/DNS-HOWTO-3.html



## Create a instance of Red Hat.

```bash
➜  ~ git:(master) ✗ aws ec2 run-instances --image-id ami-b63769a1 --count 1 --instance-type t2.micro --key-name keypair3 --security-groups mysg
{
    "OwnerId": "624990436890", 
    "ReservationId": "r-003997252666b66c6", 
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
            "LaunchTime": "2017-03-18T22:23:48.000Z", 
            "PrivateIpAddress": "172.31.30.115", 
            "ProductCodes": [], 
            "VpcId": "vpc-adb325cb", 
            "StateTransitionReason": "", 
            "InstanceId": "i-0c7d5c4b3a4726bd7", 
            "ImageId": "ami-b63769a1", 
            "PrivateDnsName": "ip-172-31-30-115.ec2.internal", 
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
                    "MacAddress": "0e:db:b6:0f:70:54", 
                    "SourceDestCheck": true, 
                    "VpcId": "vpc-adb325cb", 
                    "Description": "", 
                    "NetworkInterfaceId": "eni-423bf184", 
                    "PrivateIpAddresses": [
                        {
                            "PrivateDnsName": "ip-172-31-30-115.ec2.internal", 
                            "Primary": true, 
                            "PrivateIpAddress": "172.31.30.115"
                        }
                    ], 
                    "PrivateDnsName": "ip-172-31-30-115.ec2.internal", 
                    "Attachment": {
                        "Status": "attaching", 
                        "DeviceIndex": 0, 
                        "DeleteOnTermination": true, 
                        "AttachmentId": "eni-attach-dcda6e8c", 
                        "AttachTime": "2017-03-18T22:23:48.000Z"
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
                    "PrivateIpAddress": "172.31.30.115"
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
            "RootDeviceName": "/dev/sda1", 
            "VirtualizationType": "hvm", 
            "AmiLaunchIndex": 0
        }
    ]
}

➜  ~ git:(master) ✗ aws ec2 describe-instances --filters "Name=image-id,Values=ami-b63769a1"
{
    "Reservations": [
        {
            "OwnerId": "624990436890", 
            "ReservationId": "r-003997252666b66c6", 
            "Groups": [], 
            "Instances": [
                {
                    "Monitoring": {
                        "State": "disabled"
                    }, 
                    "PublicDnsName": "ec2-54-91-19-43.compute-1.amazonaws.com", 
                    "State": {
                        "Code": 16, 
                        "Name": "running"
                    }, 
                    "EbsOptimized": false, 
                    "LaunchTime": "2017-03-18T22:23:48.000Z", 
                    "PublicIpAddress": "54.91.19.43", 
                    "PrivateIpAddress": "172.31.30.115", 
                    "ProductCodes": [], 
                    "VpcId": "vpc-adb325cb", 
                    "StateTransitionReason": "", 
                    "InstanceId": "i-0c7d5c4b3a4726bd7", 
                    "ImageId": "ami-b63769a1", 
                    "PrivateDnsName": "ip-172-31-30-115.ec2.internal", 
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
                            "MacAddress": "0e:db:b6:0f:70:54", 
                            "SourceDestCheck": true, 
                            "VpcId": "vpc-adb325cb", 
                            "Description": "", 
                            "Association": {
                                "PublicIp": "54.91.19.43", 
                                "PublicDnsName": "ec2-54-91-19-43.compute-1.amazonaws.com", 
                                "IpOwnerId": "amazon"
                            }, 
                            "NetworkInterfaceId": "eni-423bf184", 
                            "PrivateIpAddresses": [
                                {
                                    "PrivateDnsName": "ip-172-31-30-115.ec2.internal", 
                                    "Association": {
                                        "PublicIp": "54.91.19.43", 
                                        "PublicDnsName": "ec2-54-91-19-43.compute-1.amazonaws.com", 
                                        "IpOwnerId": "amazon"
                                    }, 
                                    "Primary": true, 
                                    "PrivateIpAddress": "172.31.30.115"
                                }
                            ], 
                            "PrivateDnsName": "ip-172-31-30-115.ec2.internal", 
                            "Attachment": {
                                "Status": "attached", 
                                "DeviceIndex": 0, 
                                "DeleteOnTermination": true, 
                                "AttachmentId": "eni-attach-dcda6e8c", 
                                "AttachTime": "2017-03-18T22:23:48.000Z"
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
                            "PrivateIpAddress": "172.31.30.115"
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
                            "DeviceName": "/dev/sda1", 
                            "Ebs": {
                                "Status": "attached", 
                                "DeleteOnTermination": true, 
                                "VolumeId": "vol-0e34a21597e2a21f6", 
                                "AttachTime": "2017-03-18T22:23:49.000Z"
                            }
                        }
                    ], 
                    "Architecture": "x86_64", 
                    "RootDeviceType": "ebs", 
                    "RootDeviceName": "/dev/sda1", 
                    "VirtualizationType": "hvm", 
                    "AmiLaunchIndex": 0
                }
            ]
        }
    ]
}
```

## Install package `bind`, `bind-utils` and `caching-nameserver`. 
Public DNS: ec2-54-91-19-43.compute-1.amazonaws.com

```bash
➜  Documents git:(master) ✗ ssh -i p.pem ec2-user@ec2-54-91-19-43.compute-1.amazonaws.com
[ec2-user@ip-172-31-30-115 ~]$ 
[ec2-user@ip-172-31-30-115 ~]$ yum install bind
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
Repo rhui-REGION-client-config-server-7 forced skip_if_unavailable=True due to: /etc/pki/rhui/cdn.redhat.com-chain.crt
Repo rhui-REGION-client-config-server-7 forced skip_if_unavailable=True due to: /etc/pki/rhui/product/rhui-client-config-server-7.crt
Repo rhui-REGION-client-config-server-7 forced skip_if_unavailable=True due to: /etc/pki/rhui/rhui-client-config-server-7.key
Repo rhui-REGION-rhel-server-releases forced skip_if_unavailable=True due to: /etc/pki/rhui/cdn.redhat.com-chain.crt
Repo rhui-REGION-rhel-server-releases forced skip_if_unavailable=True due to: /etc/pki/rhui/product/content-rhel7.crt
Repo rhui-REGION-rhel-server-releases forced skip_if_unavailable=True due to: /etc/pki/rhui/content-rhel7.key
Repo rhui-REGION-rhel-server-rh-common forced skip_if_unavailable=True due to: /etc/pki/rhui/cdn.redhat.com-chain.crt
Repo rhui-REGION-rhel-server-rh-common forced skip_if_unavailable=True due to: /etc/pki/rhui/product/content-rhel7.crt
Repo rhui-REGION-rhel-server-rh-common forced skip_if_unavailable=True due to: /etc/pki/rhui/content-rhel7.key
You need to be root to perform this command.
[ec2-user@ip-172-31-30-115 ~]$ sudo yum install bind
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
rhui-REGION-client-config-server-7                       | 2.9 kB     00:00     
rhui-REGION-rhel-server-releases                         | 3.5 kB     00:00     
rhui-REGION-rhel-server-rh-common                        | 3.8 kB     00:00     
(1/7): rhui-REGION-client-config-server-7/x86_64/primary_d | 5.5 kB   00:00     
(2/7): rhui-REGION-rhel-server-rh-common/7Server/x86_64/gr |  104 B   00:00     
(3/7): rhui-REGION-rhel-server-releases/7Server/x86_64/gro | 701 kB   00:00     
(4/7): rhui-REGION-rhel-server-releases/7Server/x86_64/upd | 1.8 MB   00:00     
(5/7): rhui-REGION-rhel-server-rh-common/7Server/x86_64/up |  30 kB   00:00     
(6/7): rhui-REGION-rhel-server-rh-common/7Server/x86_64/pr | 112 kB   00:00     
(7/7): rhui-REGION-rhel-server-releases/7Server/x86_64/pri |  34 MB   00:01     
Resolving Dependencies
--> Running transaction check
---> Package bind.x86_64 32:9.9.4-38.el7_3.2 will be installed
--> Processing Dependency: bind-libs = 32:9.9.4-38.el7_3.2 for package: 32:bind-9.9.4-38.el7_3.2.x86_64
--> Processing Dependency: libbind9.so.90()(64bit) for package: 32:bind-9.9.4-38.el7_3.2.x86_64
--> Processing Dependency: libdns.so.100()(64bit) for package: 32:bind-9.9.4-38.el7_3.2.x86_64
--> Processing Dependency: libisc.so.95()(64bit) for package: 32:bind-9.9.4-38.el7_3.2.x86_64
--> Processing Dependency: libisccc.so.90()(64bit) for package: 32:bind-9.9.4-38.el7_3.2.x86_64
--> Processing Dependency: libisccfg.so.90()(64bit) for package: 32:bind-9.9.4-38.el7_3.2.x86_64
--> Processing Dependency: liblwres.so.90()(64bit) for package: 32:bind-9.9.4-38.el7_3.2.x86_64
--> Running transaction check
---> Package bind-libs.x86_64 32:9.9.4-38.el7_3.2 will be installed
--> Processing Dependency: bind-license = 32:9.9.4-38.el7_3.2 for package: 32:bind-libs-9.9.4-38.el7_3.2.x86_64
--> Running transaction check
---> Package bind-license.noarch 32:9.9.4-37.el7 will be updated
--> Processing Dependency: bind-license = 32:9.9.4-37.el7 for package: 32:bind-libs-lite-9.9.4-37.el7.x86_64
---> Package bind-license.noarch 32:9.9.4-38.el7_3.2 will be an update
--> Running transaction check
---> Package bind-libs-lite.x86_64 32:9.9.4-37.el7 will be updated
---> Package bind-libs-lite.x86_64 32:9.9.4-38.el7_3.2 will be an update
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package      Arch   Version             Repository                        Size
================================================================================
Installing:
 bind         x86_64 32:9.9.4-38.el7_3.2 rhui-REGION-rhel-server-releases 1.8 M
Installing for dependencies:
 bind-libs    x86_64 32:9.9.4-38.el7_3.2 rhui-REGION-rhel-server-releases 1.0 M
Updating for dependencies:
 bind-libs-lite
              x86_64 32:9.9.4-38.el7_3.2 rhui-REGION-rhel-server-releases 730 k
 bind-license noarch 32:9.9.4-38.el7_3.2 rhui-REGION-rhel-server-releases  83 k

Transaction Summary
================================================================================
Install  1 Package  (+1 Dependent package)
Upgrade             ( 2 Dependent packages)

Total download size: 3.6 M
Is this ok [y/d/N]: y
Downloading packages:
Delta RPMs disabled because /usr/bin/applydeltarpm not installed.
(1/4): bind-libs-9.9.4-38.el7_3.2.x86_64.rpm               | 1.0 MB   00:00     
(2/4): bind-9.9.4-38.el7_3.2.x86_64.rpm                    | 1.8 MB   00:00     
(3/4): bind-libs-lite-9.9.4-38.el7_3.2.x86_64.rpm          | 730 kB   00:00     
(4/4): bind-license-9.9.4-38.el7_3.2.noarch.rpm            |  83 kB   00:00     
--------------------------------------------------------------------------------
Total                                              7.4 MB/s | 3.6 MB  00:00     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Updating   : 32:bind-license-9.9.4-38.el7_3.2.noarch                      1/6 
  Installing : 32:bind-libs-9.9.4-38.el7_3.2.x86_64                         2/6 
  Installing : 32:bind-9.9.4-38.el7_3.2.x86_64                              3/6 
  Updating   : 32:bind-libs-lite-9.9.4-38.el7_3.2.x86_64                    4/6 
  Cleanup    : 32:bind-libs-lite-9.9.4-37.el7.x86_64                        5/6 
  Cleanup    : 32:bind-license-9.9.4-37.el7.noarch                          6/6 
  Verifying  : 32:bind-9.9.4-38.el7_3.2.x86_64                              1/6 
  Verifying  : 32:bind-libs-lite-9.9.4-38.el7_3.2.x86_64                    2/6 
  Verifying  : 32:bind-libs-9.9.4-38.el7_3.2.x86_64                         3/6 
  Verifying  : 32:bind-license-9.9.4-38.el7_3.2.noarch                      4/6 
  Verifying  : 32:bind-libs-lite-9.9.4-37.el7.x86_64                        5/6 
  Verifying  : 32:bind-license-9.9.4-37.el7.noarch                          6/6 

Installed:
  bind.x86_64 32:9.9.4-38.el7_3.2                                               

Dependency Installed:
  bind-libs.x86_64 32:9.9.4-38.el7_3.2                                          

Dependency Updated:
  bind-libs-lite.x86_64 32:9.9.4-38.el7_3.2                                     
  bind-license.noarch 32:9.9.4-38.el7_3.2                                       

Complete!
[ec2-user@ip-172-31-30-115 ~]$ sudo yum install bind-utils
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
Resolving Dependencies
--> Running transaction check
---> Package bind-utils.x86_64 32:9.9.4-38.el7_3.2 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package    Arch   Version               Repository                        Size
================================================================================
Installing:
 bind-utils x86_64 32:9.9.4-38.el7_3.2   rhui-REGION-rhel-server-releases 202 k

Transaction Summary
================================================================================
Install  1 Package

Total download size: 202 k
Installed size: 434 k
Is this ok [y/d/N]: y
Downloading packages:
bind-utils-9.9.4-38.el7_3.2.x86_64.rpm                     | 202 kB   00:00     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : 32:bind-utils-9.9.4-38.el7_3.2.x86_64                        1/1 
  Verifying  : 32:bind-utils-9.9.4-38.el7_3.2.x86_64                        1/1 

Installed:
  bind-utils.x86_64 32:9.9.4-38.el7_3.2                                         

Complete!
[ec2-user@ip-172-31-30-115 ~]$ sudo yum install caching-nameserver
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
Package 32:bind-9.9.4-38.el7_3.2.x86_64 already installed and latest version
Nothing to do
```

## Modify the file '/etc/named.conf'
Then I look the file `/etc/named.conf`:
This file has limit of permission. I use root as user.

```bash
[ec2-user@ip-172-31-30-115 var]$ sudo su
[root@ip-172-31-30-115 etc]# vi named.conf 
```

Modify:

```bash
//
// named.conf
//
// Provided by Red Hat bind package to configure the ISC BIND named(8) DNS
// server as a caching only nameserver (as a localhost DNS resolver only).
//
// See /usr/share/doc/bind*/sample/ for example named configuration files.
//
// See the BIND Administrator's Reference Manual (ARM) for details about the
// configuration located in /usr/share/doc/bind-{version}/Bv9ARM.html

options {
        listen-on port 53 { 127.0.0.1; any; };
        listen-on-v6 port 53 { ::1; };
        directory       "/var/named";
        dump-file       "/var/named/data/cache_dump.db";
        statistics-file "/var/named/data/named_stats.txt";
        memstatistics-file "/var/named/data/named_mem_stats.txt";
        allow-query     { localhost; any; };
        allow-query-cache { localhost; any; };

        /*
         - If you are building an AUTHORITATIVE DNS server, do NOT enable recursion.
         - If you are building a RECURSIVE (caching) DNS server, you need to enable recursion.
         - If your recursive DNS server has a public IP address, you MUST enable access
           control to limit queries to your legitimate users. Failing to do so will
           cause your server to become part of large scale DNS amplification
           attacks. Implementing BCP38 within your network would greatly
           reduce such attack surface
        */
        recursion yes;

        dnssec-enable yes;
        dnssec-validation yes;

        /* Path to ISC DLV key */
        bindkeys-file "/etc/named.iscdlv.key";

        managed-keys-directory "/var/named/dynamic";

        pid-file "/run/named/named.pid";
        session-keyfile "/run/named/session.key";
};

logging {
        channel default_debug {
                file "data/named.run";
                severity dynamic;
        };
};

zone "." IN {
        type hint;
        file "named.ca";
};


include "/etc/named.rfc1912.zones";
include "/etc/named.root.key";
```

## Look the file 'named.ca':

```bash
[root@ip-172-31-30-115 etc]# vi /var/named/named.ca
```

```bash
; <<>> DiG 9.9.2-P1-RedHat-9.9.2-6.P1.fc18 <<>> +bufsize=1200 +norec @a.root-servers.net
; (2 servers found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 25828
;; flags: qr aa; QUERY: 1, ANSWER: 13, AUTHORITY: 0, ADDITIONAL: 23

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;.                              IN      NS

;; ANSWER SECTION:
.                       518400  IN      NS      a.root-servers.net.
.                       518400  IN      NS      b.root-servers.net.
.                       518400  IN      NS      c.root-servers.net.
.                       518400  IN      NS      d.root-servers.net.
.                       518400  IN      NS      e.root-servers.net.
.                       518400  IN      NS      f.root-servers.net.
.                       518400  IN      NS      g.root-servers.net.
.                       518400  IN      NS      h.root-servers.net.
.                       518400  IN      NS      i.root-servers.net.
.                       518400  IN      NS      j.root-servers.net.
.                       518400  IN      NS      k.root-servers.net.
.                       518400  IN      NS      l.root-servers.net.
.                       518400  IN      NS      m.root-servers.net.

;; ADDITIONAL SECTION:
a.root-servers.net.     3600000 IN      A       198.41.0.4
a.root-servers.net.     3600000 IN      AAAA    2001:503:ba3e::2:30
b.root-servers.net.     3600000 IN      A       192.228.79.201
c.root-servers.net.     3600000 IN      A       192.33.4.12
d.root-servers.net.     3600000 IN      A       199.7.91.13
d.root-servers.net.     3600000 IN      AAAA    2001:500:2d::d
e.root-servers.net.     3600000 IN      A       192.203.230.10
f.root-servers.net.     3600000 IN      A       192.5.5.241
f.root-servers.net.     3600000 IN      AAAA    2001:500:2f::f
g.root-servers.net.     3600000 IN      A       192.112.36.4
h.root-servers.net.     3600000 IN      A       128.63.2.53
h.root-servers.net.     3600000 IN      AAAA    2001:500:1::803f:235
i.root-servers.net.     3600000 IN      A       192.36.148.17
i.root-servers.net.     3600000 IN      AAAA    2001:7fe::53
j.root-servers.net.     3600000 IN      A       192.58.128.30
j.root-servers.net.     3600000 IN      AAAA    2001:503:c27::2:30
k.root-servers.net.     3600000 IN      A       193.0.14.129
k.root-servers.net.     3600000 IN      AAAA    2001:7fd::1
l.root-servers.net.     3600000 IN      A       199.7.83.42
l.root-servers.net.     3600000 IN      AAAA    2001:500:3::42
m.root-servers.net.     3600000 IN      A       202.12.27.33
m.root-servers.net.     3600000 IN      AAAA    2001:dc3::35

;; Query time: 78 msec
;; SERVER: 198.41.0.4#53(198.41.0.4)
;; WHEN: Mon Jan 28 15:33:31 2013
;; MSG SIZE  rcvd: 699
```


## Modify the file 'etc/resolv.conf':

The `nameserver' line specifies the address of nameserver.
The `search` set the searching order of client request:
If a client tries to look up foo, then foo.subdomain.your-domain.edu is tried first, then foo.your-domain.edu, and finally foo. You may not want to put in too many domains in the search line, as it takes time to search them all.

```bash
# Generated by NetworkManager
search subdomain.your-domain.edu your-domain.edu
nameserver 127.0.0.1
```

## Deploy the Cache-only DNS server within chroot environment

```bash
# yum install bind-chroot -y
# systemctl restart named
# ln -s /etc/named.conf /var/named/chroot/etc/named.conf
```

## Start the named server
```bash
[root@ip-172-31-30-115 network-scripts]# systemctl restart named
[root@ip-172-31-30-115 network-scripts]# systemctl enable named
[root@ip-172-31-30-115 network-scripts]# systemctl status named
● named.service - Berkeley Internet Name Domain (DNS)
   Loaded: loaded (/usr/lib/systemd/system/named.service; enabled; vendor preset: disabled)
   Active: active (running) since Sun 2017-03-19 01:09:45 EDT; 10s ago
 Main PID: 17623 (named)
   CGroup: /system.slice/named.service
           └─17623 /usr/sbin/named -u named

Mar 19 01:09:45 ip-172-31-30-115.ec2.internal named[17623]: command channel listening on ::1#953
Mar 19 01:09:45 ip-172-31-30-115.ec2.internal named[17623]: managed-keys-zone: loaded serial 2
Mar 19 01:09:45 ip-172-31-30-115.ec2.internal systemd[1]: Started Berkeley Internet Name Domain (DNS).
Mar 19 01:09:45 ip-172-31-30-115.ec2.internal named[17623]: zone 0.in-addr.arpa/IN: loaded serial 0
Mar 19 01:09:45 ip-172-31-30-115.ec2.internal named[17623]: zone 1.0.0.127.in-addr.arpa/IN: loaded serial 0
Mar 19 01:09:45 ip-172-31-30-115.ec2.internal named[17623]: zone 1.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0....ial 0
Mar 19 01:09:45 ip-172-31-30-115.ec2.internal named[17623]: zone localhost/IN: loaded serial 0
Mar 19 01:09:45 ip-172-31-30-115.ec2.internal named[17623]: zone localhost.localdomain/IN: loaded serial 0
Mar 19 01:09:45 ip-172-31-30-115.ec2.internal named[17623]: all zones loaded
Mar 19 01:09:45 ip-172-31-30-115.ec2.internal named[17623]: running
Hint: Some lines were ellipsized, use -l to show in full.
```

## Configured the client

### Create an instance as our client

```bash
➜  ~ git:(master) ✗ aws ec2 run-instances --image-id ami-b63769a1 --count 1 --instance-type t2.micro --key-name keypair3 --security-groups mysg
{
    "OwnerId": "624990436890", 
    "ReservationId": "r-07677d6d1f894a149", 
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
            "LaunchTime": "2017-03-19T04:29:59.000Z", 
            "PrivateIpAddress": "172.31.23.114", 
            "ProductCodes": [], 
            "VpcId": "vpc-adb325cb", 
            "StateTransitionReason": "", 
            "InstanceId": "i-077fb91e833447d9b", 
            "ImageId": "ami-b63769a1", 
            "PrivateDnsName": "ip-172-31-23-114.ec2.internal", 
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
                    "MacAddress": "0e:b4:86:cf:b2:78", 
                    "SourceDestCheck": true, 
                    "VpcId": "vpc-adb325cb", 
                    "Description": "", 
                    "NetworkInterfaceId": "eni-00f324c6", 
                    "PrivateIpAddresses": [
                        {
                            "PrivateDnsName": "ip-172-31-23-114.ec2.internal", 
                            "Primary": true, 
                            "PrivateIpAddress": "172.31.23.114"
                        }
                    ], 
                    "PrivateDnsName": "ip-172-31-23-114.ec2.internal", 
                    "Attachment": {
                        "Status": "attaching", 
                        "DeviceIndex": 0, 
                        "DeleteOnTermination": true, 
                        "AttachmentId": "eni-attach-cb5aed9b", 
                        "AttachTime": "2017-03-19T04:29:59.000Z"
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
                    "PrivateIpAddress": "172.31.23.114"
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
            "RootDeviceName": "/dev/sda1", 
            "VirtualizationType": "hvm", 
            "AmiLaunchIndex": 0
        }
    ]
}

➜  ~ git:(master) ✗ aws ec2 describe-instances --filters "Name=instance-id,Values=i-077fb91e833447d9b"
{
    "Reservations": [
        {
            "OwnerId": "624990436890", 
            "ReservationId": "r-07677d6d1f894a149", 
            "Groups": [], 
            "Instances": [
                {
                    "Monitoring": {
                        "State": "disabled"
                    }, 
                    "PublicDnsName": "ec2-54-242-90-155.compute-1.amazonaws.com", 
                    "State": {
                        "Code": 16, 
                        "Name": "running"
                    }, 
                    "EbsOptimized": false, 
                    "LaunchTime": "2017-03-19T04:29:59.000Z", 
                    "PublicIpAddress": "54.242.90.155", 
                    "PrivateIpAddress": "172.31.23.114", 
                    "ProductCodes": [], 
                    "VpcId": "vpc-adb325cb", 
                    "StateTransitionReason": "", 
                    "InstanceId": "i-077fb91e833447d9b", 
                    "ImageId": "ami-b63769a1", 
                    "PrivateDnsName": "ip-172-31-23-114.ec2.internal", 
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
                            "MacAddress": "0e:b4:86:cf:b2:78", 
                            "SourceDestCheck": true, 
                            "VpcId": "vpc-adb325cb", 
                            "Description": "", 
                            "Association": {
                                "PublicIp": "54.242.90.155", 
                                "PublicDnsName": "ec2-54-242-90-155.compute-1.amazonaws.com", 
                                "IpOwnerId": "amazon"
                            }, 
                            "NetworkInterfaceId": "eni-00f324c6", 
                            "PrivateIpAddresses": [
                                {
                                    "PrivateDnsName": "ip-172-31-23-114.ec2.internal", 
                                    "Association": {
                                        "PublicIp": "54.242.90.155", 
                                        "PublicDnsName": "ec2-54-242-90-155.compute-1.amazonaws.com", 
                                        "IpOwnerId": "amazon"
                                    }, 
                                    "Primary": true, 
                                    "PrivateIpAddress": "172.31.23.114"
                                }
                            ], 
                            "PrivateDnsName": "ip-172-31-23-114.ec2.internal", 
                            "Attachment": {
                                "Status": "attached", 
                                "DeviceIndex": 0, 
                                "DeleteOnTermination": true, 
                                "AttachmentId": "eni-attach-cb5aed9b", 
                                "AttachTime": "2017-03-19T04:29:59.000Z"
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
                            "PrivateIpAddress": "172.31.23.114"
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
                            "DeviceName": "/dev/sda1", 
                            "Ebs": {
                                "Status": "attached", 
                                "DeleteOnTermination": true, 
                                "VolumeId": "vol-033fa93cda37a3621", 
                                "AttachTime": "2017-03-19T04:30:00.000Z"
                            }
                        }
                    ], 
                    "Architecture": "x86_64", 
                    "RootDeviceType": "ebs", 
                    "RootDeviceName": "/dev/sda1", 
                    "VirtualizationType": "hvm", 
                    "AmiLaunchIndex": 0
                }
            ]
        }
    ]
}
```


According to the above, our named server "PublicIpAddress" is "54.91.19.43".
Clinet Public Dns is "ec2-54-242-90-155.compute-1.amazonaws.com".

SSH to the client and change to 'root' user.

```bash
➜  Documents git:(master) ✗ ssh -i p.pem ec2-user@ec2-54-242-90-155.compute-1.amazonaws.com
The authenticity of host 'ec2-54-242-90-155.compute-1.amazonaws.com (54.242.90.155)' can't be established.
ECDSA key fingerprint is SHA256:RjBCp8++iMcmgBP9LgmWNnBwz+/+gaFJmyooX7fFmnc.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'ec2-54-242-90-155.compute-1.amazonaws.com,54.242.90.155' (ECDSA) to the list of known hosts.
[ec2-user@ip-172-31-23-114 ~]$ sudo su
[root@ip-172-31-23-114 ec2-user]# 
```
Edit /etc/sysconfig/network-scripts/ifcfg-lo (add 'DNS=54.91.19.43' in the end):

```
DEVICE=lo
IPADDR=127.0.0.1
NETMASK=255.0.0.0
NETWORK=127.0.0.0
# If you're having problems with gated making 127.0.0.0/8 a martian,
# you can change this to something else (255.255.255.255, for example)
BROADCAST=127.255.255.255
ONBOOT=yes
NAME=loopback
DNS=54.91.19.43
```
Edit /etc/resolv.conf:

```bash
[ec2-user@ip-172-31-23-114 ~]$ vi /etc/resolv.conf

nameserver 54.91.19.43
```

First, I find I can't visit my name server. After a few mins, I realized that I didn't set inbound of my ec2 security group to allow UDP request. Then I added rule of inbound to allow ALL UDP from my client ip in this security group.


## tcpdump exercises
### First scenario

#### Install telnet and tcpdump

```bash
[root@ip-172-31-30-115 ec2-user]# yum install tcpdump
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
rhui-REGION-client-config-server-7                       | 2.9 kB     00:00     
rhui-REGION-rhel-server-releases                         | 3.5 kB     00:00     
rhui-REGION-rhel-server-rh-common                        | 3.8 kB     00:00     
Resolving Dependencies
--> Running transaction check
---> Package tcpdump.x86_64 14:4.5.1-3.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package   Arch     Version            Repository                          Size
================================================================================
Installing:
 tcpdump   x86_64   14:4.5.1-3.el7     rhui-REGION-rhel-server-releases   388 k

Transaction Summary
================================================================================
Install  1 Package

Total download size: 388 k
Installed size: 931 k
Is this ok [y/d/N]: y
Downloading packages:
tcpdump-4.5.1-3.el7.x86_64.rpm                             | 388 kB   00:00     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : 14:tcpdump-4.5.1-3.el7.x86_64                                1/1 
  Verifying  : 14:tcpdump-4.5.1-3.el7.x86_64                                1/1 

Installed:
  tcpdump.x86_64 14:4.5.1-3.el7                                                 

Complete!

[root@ip-172-31-30-115 ec2-user]# yum install telnet
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
Resolving Dependencies
--> Running transaction check
---> Package telnet.x86_64 1:0.17-60.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package   Arch      Version          Repository                           Size
================================================================================
Installing:
 telnet    x86_64    1:0.17-60.el7    rhui-REGION-rhel-server-releases     63 k

Transaction Summary
================================================================================
Install  1 Package

Total download size: 63 k
Installed size: 113 k
Is this ok [y/d/N]: y
Downloading packages:
telnet-0.17-60.el7.x86_64.rpm                              |  63 kB   00:00     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : 1:telnet-0.17-60.el7.x86_64                                  1/1 
  Verifying  : 1:telnet-0.17-60.el7.x86_64                                  1/1 

Installed:
  telnet.x86_64 1:0.17-60.el7                                                   

Complete!
```

### Set tcpdump to record package information

```bash
[root@ip-172-31-30-115 ec2-user]# tcpdump -w tcpdump.out port not 22 &
[1] 19985
[root@ip-172-31-30-115 ec2-user]# tcpdump: listening on eth0, link-type EN10MB (Ethernet), capture size 65535 bytes
arp -d -a
gateway (172.31.16.1) at 0e:8a:cb:2d:0b:70 [ether] on eth0
[root@ip-172-31-30-115 ec2-user]# telnet www.yahoo.com 80
Trying 98.139.180.149...
Connected to www.yahoo.com.
Escape character is '^]'.
GET / HTTP/1.1
Host: www.yahoo.com

HTTP/1.1 301 Redirect
Date: Mon, 20 Mar 2017 01:42:51 GMT
Via: https/1.1 ir4.fp.bf1.yahoo.com (ApacheTrafficServer)
Server: ATS
Location: https://www.yahoo.com/
Content-Type: text/html
Content-Language: en
Cache-Control: no-store, no-cache
Connection: keep-alive
Content-Length: 304

<HTML>
<HEAD>
<TITLE>Document Has Moved</TITLE>
</HEAD>

<BODY BGCOLOR="white" FGCOLOR="black">
<H1>Document Has Moved</H1>
<HR>

<FONT FACE="Helvetica,Arial"><B>
Description: The document you requested has moved to a new location.  The new location is "https://www.yahoo.com/".
</B></FONT>
<HR>
</BODY>

<!DOCTYPE html>
<html lang="en-us">
  <head>
    <meta http-equiv="content-type" content="text/html; charset=UTF-8">
    <meta charset="utf-8">
    <title>Yahoo</title>
    <meta name="viewport" content="width=device-width,initial-scale=1,minimal-ui">
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
    <style>
      html {
          height: 100%;
      }
      body {
          background: #fafafc url(https://s.yimg.com/nn/img/sad-panda-201402200631.png) 50% 50%;
          background-size: cover;
          height: 100%;
          text-align: center;
          font: 300 18px "helvetica neue", helvetica, verdana, tahoma, arial, sans-serif;
          margin: 0;
      }
      table {
          height: 100%;
          width: 100%;
          table-layout: fixed;
          border-collapse: collapse;
          border-spacing: 0;
          border: none;
      }
      h1 {
          font-size: 42px;
          font-weight: 400;
          color: #400090;
      }
      p {
          color: #1A1A1A;
      }
      #message-1 {
          font-weight: bold;
          margin: 0;
      }
      #message-2 {
          display: inline-block;
          *display: inline;
          zoom: 1;
          max-width: 17em;
          _width: 17em;
      }
      </style>
      <script>
      </script>
  </head>
  <body>
  <!-- status code : 400 -->
  <!-- Bad Request: - -->
  <!-- host machine: ir4.fp.bf1.yahoo.com -->
  <!-- timestamp: 1489974172.000 -->
  <!-- url: /-->
  <script type="text/javascript">
    function buildUrl(url, parameters){
      var qs = [];
      for(var key in parameters) {
        var value = parameters[key];
        qs.push(encodeURIComponent(key) + "=" + encodeURIComponent(value));
      }
      url = url + "?" + qs.join('&');
      return url;
    }

    function addEvent( obj, type, fn ) {
      if ( obj.attachEvent ) {
        obj['e'+type+fn] = fn;
        obj[type+fn] = function(){obj['e'+type+fn]( window.event );}
        obj.attachEvent( 'on'+type, obj[type+fn] );
      } else
        obj.addEventListener( type, fn, false );
    }

    function generateBRBMarkup(site) {
      params.source = 'brb';
      generateBeaconMarkup(params);
      var englishHeader = 'Will be right back...';
      var englishMessage1 = 'Thank you for your patience.';
      var englishMessage2 = 'Our engineers are working quickly to resolve the issue.';
      var defaultLogoStyle = '';
      var siteDataMap = {
        'att.yahoo.com': {
          logo: 'https://s1.yimg.com/rz/d/att_en-US_f_p_bestfit_2x.png',
          logoAlt: 'AT&T',
          logoStyle: defaultLogoStyle,
          header: englishHeader,
          message1: englishMessage1,
          message2: englishMessage2
        },
        'espanol.att.yahoo.com': {
          logo: 'https://s1.yimg.com/rz/d/att_es-US_f_p_bestfit_2x.png',
          logoAlt: 'AT&T En Vivo',
          logoStyle: 'max-width:310px;',
          header: 'Volvemos enseguida…',
          message1: 'Gracias por tu paciencia.',
          message2: 'Nuestros ingenieros están trabajando rápidamente para resolver el problema.'
        },
        'default': {
          logo: 'https://s.yimg.com/nn/img/yahoo-logo-201402200629.png',
          logoAlt: 'Yahoo Logo',
          logoStyle: defaultLogoStyle,
          header: englishHeader,
          message1: englishMessage1,
          message2: englishMessage2
        }
      };

      var siteDetails = siteDataMap['default'];
      switch (site) {
        case 'espanol.att.yahoo.com':
        case 'att.yahoo.com':
          siteDetails = siteDataMap[site];
          break;
        default:
          siteDetails = siteDataMap['default'];
          break;
      }

      document.write('<table><tbody><tr><td>');
      document.write('<div id="content">');
      document.write('<img src="' + siteDetails['logo'] + '" alt="' + siteDetails['logoAlt'] + '" style="' + siteDetails['logoStyle'] + '">');
      document.write('<h1 style="margin-top:20px;">' + siteDetails['header'] + '</h1>');
      document.write('<p id="message-1">' + siteDetails['message1'] + '</p>');
      document.write('<p id="message-2">' + siteDetails['message2'] + '</p>');
      document.write('</div>');
      document.write('</td></tr></tbody></table>');
    }

    function generateIframeMarkup(iframeUrl, params) {
      params.source = 'brbiframe';
      generateBeaconMarkup(params);
      document.write('<iframe src="' + iframeUrl + '" style="width:100%;height:100%;border:none;" >');
    }

    function generateBeaconMarkup(params) {
        document.write('<img src="' + buildUrl('//geo.yahoo.com/b', params) + '" style="display:none;" width="0px" height="0px"/>');
        var beacon = new Image();
        beacon.src = buildUrl('//bcn.fp.yahoo.com/p', params);
    }

    var hostname = window.location.hostname;
    var device = '-';
    var ynet = ('-' === '1');
    var brbHost = 'brb.yahoo.com';
    var brbProto = 'https://';
    var brbIframePath = '/iframe.php';
    var brbParams = {
      protocol: window.location.protocol,
      host: hostname,
      path: window.location.pathname,
      device: device
    };
    var iframeUrl = buildUrl(brbProto + brbHost + brbIframePath, brbParams);
    var iframeDisabled = !true;
    var time = new Date().getTime();
    var params = {
        s: '1197757129',
        t: time,
        err_url: document.URL,
        err: '400',
        test: '-',
        ats_host: 'ir4.fp.bf1.yahoo.com',
        rid: '-',
        message: 'Bad Request: -'
    };

    if(ynet) {
        document.write('<div style="height: 5px; background-color: red;"></div>');
    }
    if (hostname.match('att.yahoo.com') || iframeDisabled) {
      generateBRBMarkup(hostname, params);
    } else {
      generateIframeMarkup(iframeUrl, params);
    }

    addEvent(window, "message", function(event) {
      if (event.origin !== (brbProto + brbHost)) {
        return;
      }

      if (event && event.data && event.data.url) {
        window.location.replace(event.data.url);
      }
    });
  </script>
  <noscript>
  <table>
    <tbody>
      <tr>
        <td>
          <div id="englishContent">
            <h1 style="margin-top:20px;">Will be right back...</h1>
            <p id="message-1">Thank you for your patience.</p>
            <p id="message-2">Our engineers are working quickly to resolve the issue.</p>
          </div>
        </td>
      </tr>
    </tbody>
  </table>
  </noscript>
  </body>
</html>
Connection closed by foreign host.
[root@ip-172-31-30-115 ec2-user]# kill %1
[root@ip-172-31-30-115 ec2-user]# 26 packets captured
26 packets received by filter
0 packets dropped by kernel

[1]+  Done                    tcpdump -w tcpdump.out port not 22
```

### Track down the packets in your tcpdump referring to the DNS query from your DNS server to one of the root servers, then to the various DNS servers before the DNS information is returned to your server by one of Yahoo's authoritative DNS servers.

```bash
[root@ip-172-31-30-115 ec2-user]# tcpdump -t -n -r tcpdump.out udp port 53
reading from file tcpdump.out, link-type EN10MB (Ethernet)
IP 172.31.30.115.18721 > 68.142.255.16.domain: 45641% [1au] A? www.yahoo.com. (42)
IP 172.31.30.115.53735 > 68.142.255.16.domain: 9034% [1au] AAAA? www.yahoo.com. (42)
IP 68.142.255.16.domain > 172.31.30.115.18721: 45641*- 1/4/3 CNAME fd-fp3.wg1.b.yahoo.com. (187)
IP 68.142.255.16.domain > 172.31.30.115.53735: 9034*- 1/4/3 CNAME fd-fp3.wg1.b.yahoo.com. (187)
IP 172.31.30.115.17127 > 68.180.130.15.domain: 64011% [1au] A? fd-fp3.wg1.b.yahoo.com. (51)
IP 172.31.30.115.48161 > 68.180.130.15.domain: 52861% [1au] AAAA? fd-fp3.wg1.b.yahoo.com. (51)
IP 68.180.130.15.domain > 172.31.30.115.17127: 64011*- 2/0/1 A 98.139.180.149, A 98.139.183.24 (83)
IP 68.180.130.15.domain > 172.31.30.115.48161: 52861*- 1/0/1 AAAA 2001:4998:58:c02::a9 (79)
```

### Identify the 3-way handshake that initiates the connection from your DNS server to port 80 on Yahoo's webserver, the packets that are being sent back and forth and finally the closing of the connection.

```bash
[root@ip-172-31-30-115 ec2-user]# tcpdump -n -r tcpdump.out tcp port 80
reading from file tcpdump.out, link-type EN10MB (Ethernet)
21:42:35.282439 IP 172.31.30.115.54256 > 98.139.180.149.http: Flags [S], seq 854216136, win 26883, options [mss 8961,sackOK,TS val 97995307 ecr 0,nop,wscale 7], length 0
21:42:35.299558 IP 98.139.180.149.http > 172.31.30.115.54256: Flags [S.], seq 225539872, ack 854216137, win 8192, options [mss 1460,nop,nop,sackOK,nop,wscale 8], length 0
21:42:35.299596 IP 172.31.30.115.54256 > 98.139.180.149.http: Flags [.], ack 1, win 211, length 0
21:42:41.537040 IP 172.31.30.115.54256 > 98.139.180.149.http: Flags [P.], seq 1:17, ack 1, win 211, length 16
21:42:41.555263 IP 98.139.180.149.http > 172.31.30.115.54256: Flags [.], ack 17, win 58, length 0
21:42:50.064128 IP 172.31.30.115.54256 > 98.139.180.149.http: Flags [P.], seq 17:38, ack 1, win 211, length 21
21:42:50.082376 IP 98.139.180.149.http > 172.31.30.115.54256: Flags [.], ack 38, win 58, length 0
21:42:51.033280 IP 172.31.30.115.54256 > 98.139.180.149.http: Flags [P.], seq 38:40, ack 1, win 211, length 2
21:42:51.051567 IP 98.139.180.149.http > 172.31.30.115.54256: Flags [.], ack 40, win 58, length 0
21:42:51.053313 IP 98.139.180.149.http > 172.31.30.115.54256: Flags [P.], seq 1:600, ack 40, win 58, length 599
21:42:51.053331 IP 172.31.30.115.54256 > 98.139.180.149.http: Flags [.], ack 600, win 220, length 0
21:42:52.502208 IP 172.31.30.115.54256 > 98.139.180.149.http: Flags [P.], seq 40:42, ack 600, win 220, length 2
21:42:52.521318 IP 98.139.180.149.http > 172.31.30.115.54256: Flags [.], seq 600:3520, ack 42, win 58, length 2920
21:42:52.521346 IP 172.31.30.115.54256 > 98.139.180.149.http: Flags [.], ack 3520, win 266, length 0
21:42:52.539662 IP 98.139.180.149.http > 172.31.30.115.54256: Flags [FP.], seq 3520:7066, ack 42, win 58, length 3546
21:42:52.539691 IP 172.31.30.115.54256 > 98.139.180.149.http: Flags [.], ack 7067, win 321, length 0
21:42:52.539912 IP 172.31.30.115.54256 > 98.139.180.149.http: Flags [F.], seq 42, ack 7067, win 321, length 0
21:42:52.558114 IP 98.139.180.149.http > 172.31.30.115.54256: Flags [.], ack 43, win 58, length 0
```


This is the 3-way handshake that initiates the connection from your DNS server to port 80 on Yahoo's webserver：
```bash
21:42:35.282439 IP 172.31.30.115.54256 > 98.139.180.149.http: Flags [S], seq 854216136, win 26883, options [mss 8961,sackOK,TS val 97995307 ecr 0,nop,wscale 7], length 0
21:42:35.299558 IP 98.139.180.149.http > 172.31.30.115.54256: Flags [S.], seq 225539872, ack 854216137, win 8192, options [mss 1460,nop,nop,sackOK,nop,wscale 8], length 0
21:42:35.299596 IP 172.31.30.115.54256 > 98.139.180.149.http: Flags [.], ack 1, win 211, length 0
```

The packets that are being sent back :
```bash
21:42:41.537040 IP 172.31.30.115.54256 > 98.139.180.149.http: Flags [P.], seq 1:17, ack 1, win 211, length 16
21:42:41.555263 IP 98.139.180.149.http > 172.31.30.115.54256: Flags [.], ack 17, win 58, length 0
21:42:50.064128 IP 172.31.30.115.54256 > 98.139.180.149.http: Flags [P.], seq 17:38, ack 1, win 211, length 21
21:42:50.082376 IP 98.139.180.149.http > 172.31.30.115.54256: Flags [.], ack 38, win 58, length 0
21:42:51.033280 IP 172.31.30.115.54256 > 98.139.180.149.http: Flags [P.], seq 38:40, ack 1, win 211, length 2
21:42:51.051567 IP 98.139.180.149.http > 172.31.30.115.54256: Flags [.], ack 40, win 58, length 0
```

and forth:
```bash
21:42:51.053313 IP 98.139.180.149.http > 172.31.30.115.54256: Flags [P.], seq 1:600, ack 40, win 58, length 599
21:42:51.053331 IP 172.31.30.115.54256 > 98.139.180.149.http: Flags [.], ack 600, win 220, length 0
21:42:52.502208 IP 172.31.30.115.54256 > 98.139.180.149.http: Flags [P.], seq 40:42, ack 600, win 220, length 2
21:42:52.521318 IP 98.139.180.149.http > 172.31.30.115.54256: Flags [.], seq 600:3520, ack 42, win 58, length 2920
21:42:52.521346 IP 172.31.30.115.54256 > 98.139.180.149.http: Flags [.], ack 3520, win 266, length 0
```

and finally the closing of the connection:
```bash
21:42:52.539662 IP 98.139.180.149.http > 172.31.30.115.54256: Flags [FP.], seq 3520:7066, ack 42, win 58, length 3546
21:42:52.539691 IP 172.31.30.115.54256 > 98.139.180.149.http: Flags [.], ack 7067, win 321, length 0
21:42:52.539912 IP 172.31.30.115.54256 > 98.139.180.149.http: Flags [F.], seq 42, ack 7067, win 321, length 0
21:42:52.558114 IP 98.139.180.149.http > 172.31.30.115.54256: Flags [.], ack 43, win 58, length 0
```

## Second scenarios

### Install tcpdump and telnet on client (the same step as first scenarios.)

### Set tcpdump to listen

On server:
```bash
[root@ip-172-31-30-115 ~]# tcpdump -w tcpdump.out port not 22 &
[1] 19713
[root@ip-172-31-30-115 ~]# tcpdump: listening on eth0, link-type EN10MB (Ethernet), capture size 65535 bytes
arp -d -a
gateway (172.31.16.1) at 0e:8a:cb:2d:0b:70 [ether] on eth0
```

On client:
```bash
[root@ip-172-31-23-114 ~]# tcpdump -w tcpdump.out port not 22 &
[1] 18272
[root@ip-172-31-23-114 ~]# tcpdump: listening on eth0, link-type EN10MB (Ethernet), capture size 65535 bytes
arp -d -a
gateway (172.31.16.1) at 0e:8a:cb:2d:0b:70 [ether] on eth0
```
### Run telnet

```bash
[root@ip-172-31-23-114 ~]# telnet www.tumblr.com 80
Trying 69.147.82.57...
Connected to www.tumblr.com.
Escape character is '^]'.
GET / HTTP/1.0

HTTP/1.0 400 Host Header Required
Date: Sun, 19 Mar 2017 23:38:52 GMT
Via: http/1.1 e4.ycpi.nya.yahoo.com (ApacheTrafficServer [c s f ])
Server: ATS
Cache-Control: no-store
Content-Type: text/html
Content-Language: en
Content-Length: 2810

<!DOCTYPE html>
<html lang="en-us"><head>
<meta http-equiv="content-type" content="text/html; charset=UTF-8">
    <meta charset="utf-8">
    <title>Yahoo</title>
    <meta name="viewport" content="width=device-width,initial-scale=1,minimal-ui">
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
    <style>
html {
    height: 100%;
}
body {
    background: #fafafc url(https://s.yimg.com/nn/img/sad-panda-201402200631.png) 50% 50%;
    background-size: cover;
    height: 100%;
    text-align: center;
    font: 300 18px "helvetica neue", helvetica, verdana, tahoma, arial, sans-serif;
}
table {
    height: 100%;
    width: 100%;
    table-layout: fixed;
    border-collapse: collapse;
    border-spacing: 0;
    border: none;
}
h1 {
    font-size: 42px;
    font-weight: 400;
    color: #400090;
}
p {
    color: #1A1A1A;
}
#message-1 {
    font-weight: bold;
    margin: 0;
}
#message-2 {
    display: inline-block;
    *display: inline;
    zoom: 1;
    max-width: 17em;
    _width: 17em;
}
#spanishContent {
    display: none;
}
    </style>
<script>
  document.write('<img src="//geo.yahoo.com/b?s=1197757129&t='+new Date().getTime()+'&err_url='+encodeURIComponent(document.URL)+'&err=400&test='+encodeURIComponent('-')+'" width="0px" height="0px"/>');
</script>
</head>
<body>
<!-- status code : 400 -->
<!-- Host Header Required -->
<!-- host machine: e4.ycpi.nya.yahoo.com -->
<!-- timestamp: 1489966732.000 -->
<!-- url: http:///-->
<table>
<tbody><tr>
    <td>
    <div id="englishContent">
        <script type="text/javascript">
        if (window.location.hostname=='att.yahoo.com'){
            document.write('<img src="https://s1.yimg.com/rz/d/att_en-US_f_p_bestfit_2x.png" alt="AT&T">');
        }else{
            document.write('<img src="https://s.yimg.com/nn/img/yahoo-logo-201402200629.png" alt="Yahoo Logo">');
        }    
        </script> 
        <h1 style="margin-top:20px;">Will be right back...</h1>
        <p id="message-1">Thank you for your patience.</p>
        <p id="message-2">Our engineers are working quickly to resolve the issue.</p>
    </div>
    <div id="spanishContent"> 
        <img src="https://s1.yimg.com/rz/d/att_es-US_f_p_bestfit_2x.png" alt="AT&T En Vivo" style="max-width:310px">
        <h1 style="margin-top:20px;">Volvemos enseguida…</h1>
        <p id="message-1">Gracias por tu paciencia.</p>
        <p id="message-2">Nuestros ingenieros están trabajando rápidamente para resolver el problema.</p>
    </div>
    <script type="text/javascript">
    if (window.location.hostname=='espanol.att.yahoo.com'){
        document.getElementById('englishContent').style.display = 'none';
        document.getElementById('spanishContent').style.display = 'block';
    }   
    </script>
    </td>
</tr>
</tbody></table>


</body></html>
Connection closed by foreign host.
[root@ip-172-31-23-114 ~]# kill %1
[root@ip-172-31-23-114 ~]# 33 packets captured
33 packets received by filter
0 packets dropped by kernel

[1]+  Done                    tcpdump -w tcpdump.out port not 22
```
### Track down the packets in tcpdump referring to the DNS query from your client host to DNS server.

On client:
```bash
[root@ip-172-31-23-114 ~]# tcpdump -t -n -r tcpdump.out udp port 53
reading from file tcpdump.out, link-type EN10MB (Ethernet)
IP 172.31.23.114.50439 > 54.91.19.43.domain: 57805+ PTR? 1.16.31.172.in-addr.arpa. (42)
IP 54.91.19.43.domain > 172.31.23.114.50439: 57805 NXDomain* 0/1/0 (77)
IP 172.31.23.114.60063 > 54.91.19.43.domain: 42152+ PTR? 218.24.13.126.in-addr.arpa. (44)
IP 54.91.19.43.domain > 172.31.23.114.60063: 42152 1/2/0 PTR softbank126013024218.bbtec.net. (128)
IP 172.31.23.114.48371 > 54.91.19.43.domain: 58570+ A? softbank126013024218.bbtec.net. (48)
IP 54.91.19.43.domain > 172.31.23.114.48371: 58570 1/2/2 A 126.13.24.218 (136)
IP 172.31.23.114.40529 > 54.91.19.43.domain: 30948+ A? softbank126013024218.bbtec.net. (48)
IP 172.31.23.114.40529 > 54.91.19.43.domain: 36622+ AAAA? softbank126013024218.bbtec.net. (48)
IP 54.91.19.43.domain > 172.31.23.114.40529: 30948 1/2/2 A 126.13.24.218 (136)
IP 54.91.19.43.domain > 172.31.23.114.40529: 36622 0/1/0 (94)
IP 172.31.23.114.32918 > 54.91.19.43.domain: 35896+ A? www.tumblr.com. (32)
IP 172.31.23.114.32918 > 54.91.19.43.domain: 2913+ AAAA? www.tumblr.com. (32)
IP 54.91.19.43.domain > 172.31.23.114.32918: 35896 5/4/2 CNAME e2p-v4.gycs.b.yahoodns.net., A 69.147.82.57, A 69.147.92.13, A 69.147.82.56, A 69.147.92.14 (257)
IP 54.91.19.43.domain > 172.31.23.114.32918: 2913 1/1/0 CNAME e2p-v4.gycs.b.yahoodns.net. (139)
```

### Track down the packets in your tcpdump referring to the DNS query from your DNS server to one of the root servers, then to the various DNS servers before the DNS information is returned to your server by one of Tumblr's authoritative DNS servers.

On server:

```bash
[root@ip-172-31-30-115 ~]# kill %1
[root@ip-172-31-30-115 ~]# 124 packets captured
124 packets received by filter
0 packets dropped by kernel

[1]+  Done                    tcpdump -w tcpdump.out port not 22
[root@ip-172-31-30-115 ~]# tcpdump -t -n -r tcpdump.out udp port 53
reading from file tcpdump.out, link-type EN10MB (Ethernet)
IP 54.242.90.155.50439 > 172.31.30.115.domain: 57805+ PTR? 1.16.31.172.in-addr.arpa. (42)
IP 172.31.30.115.domain > 54.242.90.155.50439: 57805 NXDomain* 0/1/0 (77)
IP 54.242.90.155.60063 > 172.31.30.115.domain: 42152+ PTR? 218.24.13.126.in-addr.arpa. (44)
IP 172.31.30.115.12672 > 193.0.9.1.domain: 25355% [1au] PTR? 218.24.13.126.in-addr.arpa. (55)
IP 193.0.9.1.domain > 172.31.30.115.12672: 25355- 0/7/1 (377)
IP 172.31.30.115.9590 > 202.12.28.131.domain: 893% [1au] PTR? 218.24.13.126.in-addr.arpa. (55)
IP 172.31.30.115.16018 > 192.12.94.30.domain: 4896% [1au] A? ns001.bbtec.net. (44)
IP 172.31.30.115.28464 > 192.12.94.30.domain: 35378% [1au] AAAA? ns001.bbtec.net. (44)
IP 172.31.30.115.39371 > 192.12.94.30.domain: 28698% [1au] A? ns002.bbtec.net. (44)
IP 172.31.30.115.64953 > 192.12.94.30.domain: 61674% [1au] AAAA? ns002.bbtec.net. (44)
IP 192.12.94.30.domain > 172.31.30.115.16018: 4896- 0/6/3 (601)
IP 192.12.94.30.domain > 172.31.30.115.28464: 35378- 0/6/3 (601)
IP 192.12.94.30.domain > 172.31.30.115.39371: 28698- 0/6/3 (601)
IP 172.31.30.115.64318 > 218.176.253.105.domain: 44419% [1au] A? ns001.bbtec.net. (44)
IP 192.12.94.30.domain > 172.31.30.115.64953: 61674- 0/6/3 (601)
IP 172.31.30.115.64670 > 218.176.253.105.domain: 43269% [1au] AAAA? ns001.bbtec.net. (44)
IP 172.31.30.115.15986 > 218.176.253.105.domain: 49175% [1au] A? ns002.bbtec.net. (44)
IP 172.31.30.115.12481 > 218.176.253.105.domain: 30143% [1au] AAAA? ns002.bbtec.net. (44)
IP 202.12.28.131.domain > 172.31.30.115.9590: 893- 0/2/1 (104)
IP 218.176.253.105.domain > 172.31.30.115.64670: 43269*- 0/1/1 (90)
IP 218.176.253.105.domain > 172.31.30.115.12481: 30143*- 0/1/1 (90)
IP 218.176.253.105.domain > 172.31.30.115.15986: 49175*- 1/2/3 A 218.176.253.104 (132)
IP 172.31.30.115.12796 > 218.176.253.104.domain: 1893% [1au] PTR? 218.24.13.126.in-addr.arpa. (55)
IP 218.176.253.105.domain > 172.31.30.115.64318: 44419*- 1/2/3 A 218.176.253.72 (132)
IP 218.176.253.104.domain > 172.31.30.115.12796: 1893*- 1/2/1 PTR softbank126013024218.bbtec.net. (139)
IP 172.31.30.115.15402 > 200.10.60.53.domain: 35634% [1au] DS? 126.in-addr.arpa. (45)
IP 200.10.60.53.domain > 172.31.30.115.15402: 35634*- 0/4/1 (501)
IP 172.31.30.115.29985 > 199.212.0.73.domain: 54806% [1au] DNSKEY? in-addr.arpa. (41)
IP 199.212.0.73.domain > 172.31.30.115.29985: 54806*- 5/0/1 DNSKEY, DNSKEY, DNSKEY, RRSIG, RRSIG (1344)
IP 172.31.30.115.domain > 54.242.90.155.60063: 42152 1/2/0 PTR softbank126013024218.bbtec.net. (128)
IP 54.242.90.155.48371 > 172.31.30.115.domain: 58570+ A? softbank126013024218.bbtec.net. (48)
IP 172.31.30.115.23886 > 218.176.253.73.domain: 64646% [1au] A? softbank126013024218.bbtec.net. (59)
IP 218.176.253.73.domain > 172.31.30.115.23886: 64646*- 1/2/3 A 126.13.24.218 (147)
IP 172.31.30.115.28358 > 192.54.112.30.domain: 41306% [1au] DS? bbtec.net. (38)
IP 192.54.112.30.domain > 172.31.30.115.28358: 41306*- 0/6/1 (759)
IP 172.31.30.115.domain > 54.242.90.155.48371: 58570 1/2/2 A 126.13.24.218 (136)
IP 54.242.90.155.40529 > 172.31.30.115.domain: 30948+ A? softbank126013024218.bbtec.net. (48)
IP 54.242.90.155.40529 > 172.31.30.115.domain: 36622+ AAAA? softbank126013024218.bbtec.net. (48)
IP 172.31.30.115.domain > 54.242.90.155.40529: 30948 1/2/2 A 126.13.24.218 (136)
IP 172.31.30.115.61458 > 218.176.253.73.domain: 11958% [1au] AAAA? softbank126013024218.bbtec.net. (59)
IP 218.176.253.73.domain > 172.31.30.115.61458: 11958*- 0/1/1 (105)
IP 172.31.30.115.domain > 54.242.90.155.40529: 36622 0/1/0 (94)
IP 54.242.90.155.32918 > 172.31.30.115.domain: 35896+ A? www.tumblr.com. (32)
IP 54.242.90.155.32918 > 172.31.30.115.domain: 2913+ AAAA? www.tumblr.com. (32)
IP 172.31.30.115.50312 > 192.5.6.30.domain: 15102% [1au] A? www.tumblr.com. (43)
IP 172.31.30.115.55078 > 192.5.6.30.domain: 24281% [1au] AAAA? www.tumblr.com. (43)
IP 192.5.6.30.domain > 172.31.30.115.50312: 15102- 0/14/15 (1000)
IP 192.5.6.30.domain > 172.31.30.115.55078: 24281- 0/14/15 (1000)
IP 172.31.30.115.54183 > 68.142.255.16.domain: 27760% [1au] A? www.tumblr.com. (43)
IP 172.31.30.115.42766 > 68.142.255.16.domain: 50340% [1au] AAAA? www.tumblr.com. (43)
IP 172.31.30.115.20720 > 192.12.94.30.domain: 56843% [1au] A? ns1.p03.dynect.net. (47)
IP 172.31.30.115.31015 > 192.12.94.30.domain: 59860% [1au] AAAA? ns1.p03.dynect.net. (47)
IP 172.31.30.115.44619 > 192.12.94.30.domain: 48475% [1au] A? ns2.p03.dynect.net. (47)
IP 172.31.30.115.29788 > 192.12.94.30.domain: 9652% [1au] AAAA? ns2.p03.dynect.net. (47)
IP 172.31.30.115.57147 > 192.12.94.30.domain: 62071% [1au] A? ns3.p03.dynect.net. (47)
IP 172.31.30.115.28255 > 192.12.94.30.domain: 63541% [1au] AAAA? ns3.p03.dynect.net. (47)
IP 172.31.30.115.8489 > 192.12.94.30.domain: 48551% [1au] A? ns4.p03.dynect.net. (47)
IP 172.31.30.115.55613 > 192.12.94.30.domain: 31935% [1au] AAAA? ns4.p03.dynect.net. (47)
IP 68.142.255.16.domain > 172.31.30.115.54183: 27760*- 1/4/3 CNAME e2p-v4.gycs.b.yahoodns.net. (204)
IP 68.142.255.16.domain > 172.31.30.115.42766: 50340*- 1/4/3 CNAME e2p-v4.gycs.b.yahoodns.net. (204)
IP 192.12.94.30.domain > 172.31.30.115.20720: 56843- 0/11/13 (933)
IP 192.12.94.30.domain > 172.31.30.115.31015: 59860- 0/11/13 (933)
IP 192.12.94.30.domain > 172.31.30.115.44619: 48475- 0/11/13 (933)
IP 192.12.94.30.domain > 172.31.30.115.29788: 9652- 0/11/13 (933)
IP 192.12.94.30.domain > 172.31.30.115.57147: 62071- 0/11/13 (933)
IP 192.12.94.30.domain > 172.31.30.115.28255: 63541- 0/11/13 (933)
IP 192.12.94.30.domain > 172.31.30.115.8489: 48551- 0/11/13 (933)
IP 192.12.94.30.domain > 172.31.30.115.55613: 31935- 0/11/13 (933)
IP 172.31.30.115.59179 > 204.13.250.136.domain: 32061% [1au] A? ns2.p03.dynect.net. (47)
IP 172.31.30.115.10967 > 204.13.250.136.domain: 15199% [1au] AAAA? ns2.p03.dynect.net. (47)
IP 172.31.30.115.12591 > 204.13.250.136.domain: 46251% [1au] A? ns3.p03.dynect.net. (47)
IP 172.31.30.115.23689 > 204.13.250.136.domain: 49237% [1au] AAAA? ns3.p03.dynect.net. (47)
IP 172.31.30.115.20181 > 204.13.250.136.domain: 23229% [1au] A? ns4.p03.dynect.net. (47)
IP 172.31.30.115.56792 > 204.13.250.136.domain: 59367% [1au] AAAA? ns4.p03.dynect.net. (47)
IP 172.31.30.115.29332 > 192.33.14.30.domain: 41065% [1au] DS? tumblr.com. (39)
IP 172.31.30.115.60180 > 204.13.250.136.domain: 12063% [1au] A? ns1.p03.dynect.net. (47)
IP 172.31.30.115.59836 > 204.13.250.136.domain: 47624% [1au] AAAA? ns1.p03.dynect.net. (47)
IP 204.13.250.136.domain > 172.31.30.115.12591: 46251*- 1/7/1 A 208.78.71.3 (212)
IP 204.13.250.136.domain > 172.31.30.115.10967: 15199*- 0/1/1 (131)
IP 204.13.250.136.domain > 172.31.30.115.59179: 32061*- 1/7/1 A 204.13.250.3 (212)
IP 204.13.250.136.domain > 172.31.30.115.59836: 47624*- 1/7/1 AAAA 2001:500:90:1::3 (224)
IP 204.13.250.136.domain > 172.31.30.115.56792: 59367*- 0/1/1 (131)
IP 204.13.250.136.domain > 172.31.30.115.20181: 23229*- 1/7/1 A 204.13.251.3 (212)
IP 204.13.250.136.domain > 172.31.30.115.23689: 49237*- 1/7/1 AAAA 2001:500:94:1::3 (224)
IP 204.13.250.136.domain > 172.31.30.115.60180: 12063*- 1/7/1 A 208.78.70.3 (212)
IP 192.33.14.30.domain > 172.31.30.115.29332: 41065*- 0/6/1 (760)
IP 172.31.30.115.45512 > 192.35.51.30.domain: 2908% [1au] AAAA? e2p-v4.gycs.b.yahoodns.net. (55)
IP 172.31.30.115.48965 > 192.35.51.30.domain: 16552% [1au] A? e2p-v4.gycs.b.yahoodns.net. (55)
IP 192.35.51.30.domain > 172.31.30.115.45512: 2908- 0/9/9 (803)
IP 192.35.51.30.domain > 172.31.30.115.48965: 16552- 0/9/9 (803)
IP 172.31.30.115.20105 > 68.142.255.16.domain: 16315% [1au] AAAA? e2p-v4.gycs.b.yahoodns.net. (55)
IP 172.31.30.115.29503 > 68.142.255.16.domain: 50107% [1au] A? e2p-v4.gycs.b.yahoodns.net. (55)
IP 68.142.255.16.domain > 172.31.30.115.20105: 16315- 0/4/3 (179)
IP 68.142.255.16.domain > 172.31.30.115.29503: 50107- 0/4/3 (179)
IP 172.31.30.115.44871 > 68.180.130.15.domain: 45208% [1au] AAAA? e2p-v4.gycs.b.yahoodns.net. (55)
IP 172.31.30.115.11781 > 68.180.130.15.domain: 48190% [1au] A? e2p-v4.gycs.b.yahoodns.net. (55)
IP 68.180.130.15.domain > 172.31.30.115.44871: 45208*- 0/1/1 (125)
IP 68.180.130.15.domain > 172.31.30.115.11781: 48190*- 4/0/1 A 69.147.92.14, A 69.147.82.57, A 69.147.82.56, A 69.147.92.13 (119)
IP 172.31.30.115.59783 > 192.35.51.30.domain: 13560% [1au] DS? yahoodns.net. (41)
IP 192.35.51.30.domain > 172.31.30.115.59783: 13560*- 0/6/1 (762)
IP 172.31.30.115.domain > 54.242.90.155.32918: 35896 5/4/2 CNAME e2p-v4.gycs.b.yahoodns.net., A 69.147.82.57, A 69.147.92.13, A 69.147.82.56, A 69.147.92.14 (257)
IP 172.31.30.115.domain > 54.242.90.155.32918: 2913 1/1/0 CNAME e2p-v4.gycs.b.yahoodns.net. (139)
```

I found before the 'telnet' running in the client, my client sent some PTR requests for '1.16.31.172.in-addr.arpa' and '218.24.13.126.in-addr.arpa'. The former looks loke the AWS internal IP address(private address).And my client also ask address for 'softbank126013024218.bbtec.net'. These behaviors make me feel puzzled.
My client sent request to server for 'www.tumblr.com'. Then server will search its CNAME and ip address, and return the result to my client.


## Third scenarios
For example, I perform a reverse host look up for '104.244.42.193' which not yet in my DNS server's cache.

```bash
[root@ip-172-31-30-115 t]# tcpdump -w tcpdump.out port not 22 &
[1] 19863
[root@ip-172-31-30-115 t]# tcpdump: listening on eth0, link-type EN10MB (Ethernet), capture size 65535 bytes
arp -d -a
gateway (172.31.16.1) at 0e:8a:cb:2d:0b:70 [ether] on eth0
[root@ip-172-31-30-115 t]# dig -x 104.244.42.193

; <<>> DiG 9.9.4-RedHat-9.9.4-38.el7_3.2 <<>> -x 104.244.42.193
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: SERVFAIL, id: 14873
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;193.42.244.104.in-addr.arpa.	IN	PTR

;; Query time: 20 msec
;; SERVER: 127.0.0.1#53(127.0.0.1)
;; WHEN: Sun Mar 19 20:45:42 EDT 2017
;; MSG SIZE  rcvd: 56

[root@ip-172-31-30-115 t]# kill %1
[root@ip-172-31-30-115 t]# 30 packets captured
30 packets received by filter
0 packets dropped by kernel

[1]+  Done                    tcpdump -w tcpdump.out port not 22
```
Result:

```bash
[root@ip-172-31-30-115 t]# tcpdump -t -n -r tcpdump.out udp port 53
reading from file tcpdump.out, link-type EN10MB (Ethernet)
IP 172.31.30.115.13797 > 199.253.183.183.domain: 18802% [1au] PTR? 193.42.244.104.in-addr.arpa. (56)
IP 199.253.183.183.domain > 172.31.30.115.13797: 18802- 0/8/1 (387)
IP 172.31.30.115.10452 > 199.180.180.63.domain: 62185% [1au] PTR? 193.42.244.104.in-addr.arpa. (56)
IP 199.180.180.63.domain > 172.31.30.115.10452: 62185- 0/6/1 (363)
IP 172.31.30.115.44763 > 162.88.61.21.domain: 55611% [1au] A? ns1.p34.dynect.net. (47)
IP 172.31.30.115.36069 > 162.88.61.21.domain: 34433% [1au] AAAA? ns1.p34.dynect.net. (47)
IP 172.31.30.115.atmtcp > 162.88.61.21.domain: 27190% [1au] A? ns2.p34.dynect.net. (47)
IP 172.31.30.115.56824 > 162.88.61.21.domain: 1127% [1au] AAAA? ns2.p34.dynect.net. (47)
IP 172.31.30.115.44520 > 162.88.61.21.domain: 22087% [1au] A? ns3.p34.dynect.net. (47)
IP 172.31.30.115.9172 > 162.88.61.21.domain: 9046% [1au] AAAA? ns3.p34.dynect.net. (47)
IP 172.31.30.115.8847 > 162.88.61.21.domain: 31946% [1au] A? ns4.p34.dynect.net. (47)
IP 172.31.30.115.16122 > 162.88.61.21.domain: 60963% [1au] AAAA? ns4.p34.dynect.net. (47)
IP 162.88.61.21.domain > 172.31.30.115.atmtcp: 27190*- 1/0/1 A 204.13.250.34 (63)
IP 162.88.61.21.domain > 172.31.30.115.56824: 1127*- 0/1/1 (131)
IP 162.88.61.21.domain > 172.31.30.115.44520: 22087*- 1/0/1 A 208.78.71.34 (63)
IP 162.88.61.21.domain > 172.31.30.115.9172: 9046*- 1/0/1 AAAA 2001:500:94:1::34 (75)
IP 172.31.30.115.30710 > 204.13.250.34.domain: 35918% [1au] PTR? 193.42.244.104.in-addr.arpa. (56)
IP 162.88.61.21.domain > 172.31.30.115.44763: 55611*- 1/0/1 A 208.78.70.34 (63)
IP 162.88.61.21.domain > 172.31.30.115.16122: 60963*- 0/1/1 (131)
IP 162.88.61.21.domain > 172.31.30.115.36069: 34433*- 1/0/1 AAAA 2001:500:90:1::34 (75)
IP 162.88.61.21.domain > 172.31.30.115.8847: 31946*- 1/0/1 A 204.13.251.34 (63)
IP 204.13.250.34.domain > 172.31.30.115.30710: 35918 Refused- 0/0/1 (56)
IP 172.31.30.115.38732 > 208.78.71.34.domain: 17860% [1au] PTR? 193.42.244.104.in-addr.arpa. (56)
IP 208.78.71.34.domain > 172.31.30.115.38732: 17860 Refused- 0/0/1 (56)
IP 172.31.30.115.31531 > 204.13.251.34.domain: 16321% [1au] PTR? 193.42.244.104.in-addr.arpa. (56)
IP 204.13.251.34.domain > 172.31.30.115.31531: 16321 Refused- 0/0/1 (56)
IP 172.31.30.115.53208 > 208.78.70.34.domain: 33024% [1au] PTR? 193.42.244.104.in-addr.arpa. (56)
IP 208.78.70.34.domain > 172.31.30.115.53208: 33024 Refused- 0/0/1 (56)
```

```bash
[root@ip-172-31-30-115 t]# tcpdump -t  -r tcpdump.out udp port 53
reading from file tcpdump.out, link-type EN10MB (Ethernet)
IP ip-172-31-30-115.ec2.internal.13797 > b.in-addr-servers.arpa.domain: 18802% [1au] PTR? 193.42.244.104.in-addr.arpa. (56)
IP b.in-addr-servers.arpa.domain > ip-172-31-30-115.ec2.internal.13797: 18802- 0/8/1 (387)
IP ip-172-31-30-115.ec2.internal.10452 > r.arin.net.domain: 62185% [1au] PTR? 193.42.244.104.in-addr.arpa. (56)
IP r.arin.net.domain > ip-172-31-30-115.ec2.internal.10452: 62185- 0/6/1 (363)
IP ip-172-31-30-115.ec2.internal.44763 > ns6.dynamicnetworkservices.net.domain: 55611% [1au] A? ns1.p34.dynect.net. (47)
IP ip-172-31-30-115.ec2.internal.36069 > ns6.dynamicnetworkservices.net.domain: 34433% [1au] AAAA? ns1.p34.dynect.net. (47)
IP ip-172-31-30-115.ec2.internal.atmtcp > ns6.dynamicnetworkservices.net.domain: 27190% [1au] A? ns2.p34.dynect.net. (47)
IP ip-172-31-30-115.ec2.internal.56824 > ns6.dynamicnetworkservices.net.domain: 1127% [1au] AAAA? ns2.p34.dynect.net. (47)
IP ip-172-31-30-115.ec2.internal.44520 > ns6.dynamicnetworkservices.net.domain: 22087% [1au] A? ns3.p34.dynect.net. (47)
IP ip-172-31-30-115.ec2.internal.9172 > ns6.dynamicnetworkservices.net.domain: 9046% [1au] AAAA? ns3.p34.dynect.net. (47)
IP ip-172-31-30-115.ec2.internal.8847 > ns6.dynamicnetworkservices.net.domain: 31946% [1au] A? ns4.p34.dynect.net. (47)
IP ip-172-31-30-115.ec2.internal.16122 > ns6.dynamicnetworkservices.net.domain: 60963% [1au] AAAA? ns4.p34.dynect.net. (47)
IP ns6.dynamicnetworkservices.net.domain > ip-172-31-30-115.ec2.internal.atmtcp: 27190*- 1/0/1 A 204.13.250.34 (63)
IP ns6.dynamicnetworkservices.net.domain > ip-172-31-30-115.ec2.internal.56824: 1127*- 0/1/1 (131)
IP ns6.dynamicnetworkservices.net.domain > ip-172-31-30-115.ec2.internal.44520: 22087*- 1/0/1 A 208.78.71.34 (63)
IP ns6.dynamicnetworkservices.net.domain > ip-172-31-30-115.ec2.internal.9172: 9046*- 1/0/1 AAAA 2001:500:94:1::34 (75)
IP ip-172-31-30-115.ec2.internal.30710 > ns2.p34.dynect.net.domain: 35918% [1au] PTR? 193.42.244.104.in-addr.arpa. (56)
IP ns6.dynamicnetworkservices.net.domain > ip-172-31-30-115.ec2.internal.44763: 55611*- 1/0/1 A 208.78.70.34 (63)
IP ns6.dynamicnetworkservices.net.domain > ip-172-31-30-115.ec2.internal.16122: 60963*- 0/1/1 (131)
IP ns6.dynamicnetworkservices.net.domain > ip-172-31-30-115.ec2.internal.36069: 34433*- 1/0/1 AAAA 2001:500:90:1::34 (75)
IP ns6.dynamicnetworkservices.net.domain > ip-172-31-30-115.ec2.internal.8847: 31946*- 1/0/1 A 204.13.251.34 (63)
IP ns2.p34.dynect.net.domain > ip-172-31-30-115.ec2.internal.30710: 35918 Refused- 0/0/1 (56)
IP ip-172-31-30-115.ec2.internal.38732 > ns3.p34.dynect.net.domain: 17860% [1au] PTR? 193.42.244.104.in-addr.arpa. (56)
IP ns3.p34.dynect.net.domain > ip-172-31-30-115.ec2.internal.38732: 17860 Refused- 0/0/1 (56)
IP ip-172-31-30-115.ec2.internal.31531 > ns4.p34.dynect.net.domain: 16321% [1au] PTR? 193.42.244.104.in-addr.arpa. (56)
IP ns4.p34.dynect.net.domain > ip-172-31-30-115.ec2.internal.31531: 16321 Refused- 0/0/1 (56)
IP ip-172-31-30-115.ec2.internal.53208 > ns1.p34.dynect.net.domain: 33024% [1au] PTR? 193.42.244.104.in-addr.arpa. (56)
IP ns1.p34.dynect.net.domain > ip-172-31-30-115.ec2.internal.53208: 33024 Refused- 0/0/1 (56)
```

My server communicate with these name servers:

199.253.183.183			b.in-addr-servers.arpa
199.180.180.63			r.arin.net
162.88.61.21			ns6.dynamicnetworkservices 	

These servers aren't the root servers. And I also use 'whois' try to find their operators, but there isn't any message about them.
