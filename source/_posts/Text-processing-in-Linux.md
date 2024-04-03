---
title: Text-processing
date: 2017-08-17 00:32:41
tags: System Administration
cover: /img/default5.png
description: "CS615 Assignment5"
---
<!-- more -->
# Description

* link: http://www.cs.stevens.edu/~jschauma/615/s17-hw5.html

Objective:

The objective of this assignment is for you to practice the use of the common text processing tools available on the Unix systems.

To do this, you will process a large input data set and extract a few bits of information. Each question / exercise can be answered with a simple pipeline of common Unix commands.

This assignment is worth 20 points.

Summary:

Every System Administrator sooner or later finds herself in the position of having to correlate events from e.g. an http log. In this exercise, we will use the web logs provided by the Wikimedia foundation, allowing us to process a sufficiently large and diverse data set.

The Wikimedia Foundation makes available logs of their web servers at https://dumps.wikimedia.org/. The data and format we're interested in is described in more detail on this page. In a nutshell, the files contain lines of data containing a small number of fields:

domain page_title count_views total_response_size
We will be looking at the data from March 27th, 2016: https://dumps.wikimedia.org/other/pagecounts-all-sites/2016/2016-03/pagecounts-20160327-000000.gz

Details:

Create a NetBSD EC2 instance of ami-569ed93c. All your work is to be done on this instance. Your solutions will be tested on such an instance. Do NOT work on your own system; the tools may behave differently and I may not be able to verify your solution..

Answer the following questions. Describe your method, then Provide the exact commands you used to determine the answer, then show the answer. For example, if the question was "How many lines are in the file?", then your answer might be:

Uncompress the input file and pipe output into wc(1):

$ gzcat pagecounts-20160327-000000.gz | wc -l
 9771932
Answer all of these questions:

How many unique objects were requested?
How many unique objects were requested for en only?
Which is the most often requested object for de?
How many requests per second were handled during this hour?
How much data was transferred in total?
Which was the largest object requested for fr?
What is the longest word found on the ten most frequently retrieved English Wikipedia pages?

-----------

# Content

# HW5_CS615
* Ankai Liang
* 10411998

## Create instance of ami-569ed93c and log in

```bash
➜  ~ git:(master) ✗ aws ec2 run-instances --image-id ami-569ed93c --instance-type t1.micro --key-name keypair3 --security-groups mysg 
{
    "OwnerId": "624990436890", 
    "ReservationId": "r-0df0169b808767f43", 
    "Groups": [], 
    "Instances": [
        {
            "Monitoring": {
                "State": "disabled"
            }, 
            "PublicDnsName": "", 
            "KernelId": "aki-8f9dcae6", 
            "State": {
                "Code": 0, 
                "Name": "pending"
            }, 
            "EbsOptimized": false, 
            "LaunchTime": "2017-04-02T21:01:52.000Z", 
            "PrivateIpAddress": "172.31.53.207", 
            "ProductCodes": [], 
            "VpcId": "vpc-adb325cb", 
            "StateTransitionReason": "", 
            "InstanceId": "i-00254b998314cf6b6", 
            "ImageId": "ami-569ed93c", 
            "PrivateDnsName": "ip-172-31-53-207.ec2.internal", 
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
                    "MacAddress": "12:bf:13:6a:ef:d6", 
                    "SourceDestCheck": true, 
                    "VpcId": "vpc-adb325cb", 
                    "Description": "", 
                    "NetworkInterfaceId": "eni-526456a6", 
                    "PrivateIpAddresses": [
                        {
                            "PrivateDnsName": "ip-172-31-53-207.ec2.internal", 
                            "Primary": true, 
                            "PrivateIpAddress": "172.31.53.207"
                        }
                    ], 
                    "PrivateDnsName": "ip-172-31-53-207.ec2.internal", 
                    "Attachment": {
                        "Status": "attaching", 
                        "DeviceIndex": 0, 
                        "DeleteOnTermination": true, 
                        "AttachmentId": "eni-attach-5c5fc570", 
                        "AttachTime": "2017-04-02T21:01:52.000Z"
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
                    "PrivateIpAddress": "172.31.53.207"
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
            "Architecture": "i386", 
            "StateReason": {
                "Message": "pending", 
                "Code": "pending"
            }, 
            "RootDeviceName": "/dev/sda1", 
            "VirtualizationType": "paravirtual", 
            "RootDeviceType": "ebs", 
            "AmiLaunchIndex": 0
        }
    ]
}

```

```
➜  ~ git:(master) ✗ aws ec2 describe-instances --filters "Name=image-id,Values=ami-569ed93c" 
{
    "Reservations": [
        {
            "OwnerId": "624990436890", 
            "ReservationId": "r-0df0169b808767f43", 
            "Groups": [], 
            "Instances": [
                {
                    "Monitoring": {
                        "State": "disabled"
                    }, 
                    "PublicDnsName": "ec2-34-207-94-168.compute-1.amazonaws.com", 
                    "RootDeviceType": "ebs", 
                    "State": {
                        "Code": 16, 
                        "Name": "running"
                    }, 
                    "EbsOptimized": false, 
                    "LaunchTime": "2017-04-02T21:01:52.000Z", 
                    "PublicIpAddress": "34.207.94.168", 
                    "PrivateIpAddress": "172.31.53.207", 
                    "ProductCodes": [], 
                    "VpcId": "vpc-adb325cb", 
                    "StateTransitionReason": "", 
                    "InstanceId": "i-00254b998314cf6b6", 
                    "ImageId": "ami-569ed93c", 
                    "PrivateDnsName": "ip-172-31-53-207.ec2.internal", 
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
                            "MacAddress": "12:bf:13:6a:ef:d6", 
                            "SourceDestCheck": true, 
                            "VpcId": "vpc-adb325cb", 
                            "Description": "", 
                            "Association": {
                                "PublicIp": "34.207.94.168", 
                                "PublicDnsName": "ec2-34-207-94-168.compute-1.amazonaws.com", 
                                "IpOwnerId": "amazon"
                            }, 
                            "NetworkInterfaceId": "eni-526456a6", 
                            "PrivateIpAddresses": [
                                {
                                    "PrivateDnsName": "ip-172-31-53-207.ec2.internal", 
                                    "Association": {
                                        "PublicIp": "34.207.94.168", 
                                        "PublicDnsName": "ec2-34-207-94-168.compute-1.amazonaws.com", 
                                        "IpOwnerId": "amazon"
                                    }, 
                                    "Primary": true, 
                                    "PrivateIpAddress": "172.31.53.207"
                                }
                            ], 
                            "PrivateDnsName": "ip-172-31-53-207.ec2.internal", 
                            "Attachment": {
                                "Status": "attached", 
                                "DeviceIndex": 0, 
                                "DeleteOnTermination": true, 
                                "AttachmentId": "eni-attach-5c5fc570", 
                                "AttachTime": "2017-04-02T21:01:52.000Z"
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
                            "PrivateIpAddress": "172.31.53.207"
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
                            "DeviceName": "/dev/sda1", 
                            "Ebs": {
                                "Status": "attached", 
                                "DeleteOnTermination": true, 
                                "VolumeId": "vol-039aba578c059024c", 
                                "AttachTime": "2017-04-02T21:01:53.000Z"
                            }
                        }, 
                        {
                            "DeviceName": "/dev/sda2", 
                            "Ebs": {
                                "Status": "attached", 
                                "DeleteOnTermination": true, 
                                "VolumeId": "vol-0451313c91b503cd5", 
                                "AttachTime": "2017-04-02T21:01:53.000Z"
                            }
                        }
                    ], 
                    "Architecture": "i386", 
                    "KernelId": "aki-8f9dcae6", 
                    "RootDeviceName": "/dev/sda1", 
                    "VirtualizationType": "paravirtual", 
                    "AmiLaunchIndex": 0
                }
            ]
        }
    ]
}
```
Gain public DNS : ec2-34-207-94-168.compute-1.amazonaws.com

```bash
➜  ~ git:(master) ✗ cd documents
➜  documents git:(master) ✗ ssh -i p.pem root@ec2-34-207-94-168.compute-1.amazonaws.com
The authenticity of host 'ec2-34-207-94-168.compute-1.amazonaws.com (34.207.94.168)' can't be established.
ECDSA key fingerprint is SHA256:auJQpbA0bhRxBdP2BjMaJYvLdaBH+PROUgN5O9WE+SQ.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'ec2-34-207-94-168.compute-1.amazonaws.com,34.207.94.168' (ECDSA) to the list of known hosts.
NetBSD 7.0 (XEN3PAE_DOMU.201509250726Z)
Welcome to NetBSD - Amazon EC2 image!

This system is running a snapshot of a stable branch of the NetBSD
operating system, adapted for running on the Amazon EC2 infrastructure.

The environment is very similar to one provided within a typical Xen domU
installation. It contains a small, autonomous environment (including a
compiler toolchain) that you can run to build your own system.

The file system is lightly populated so you have plenty of space to play with.
Should you need a src or pkgsrc tree, please use the "bootstrap" script found
under /usr to download them.  You can also use the script to set up
binary packages using "pkgin":

                /usr/bootstrap.sh [src|pkgsrc|binpkg|xbase|xsets]

This AMI sends email to the maintainer on first boot, to help get
an idea of what is in use at any given time.  

You are encouraged to test this image as thoroughly as possible.  Should you
encounter any problem, please report it back to the development team using the
send-pr(1) utility (requires a working MTA).  If yours is not properly set up,
use the web interface at: http://www.NetBSD.org/support/send-pr.html

Thank you for helping us test and improve NetBSD's quality!
Terminal type is xterm-256color.
We recommend that you create a non-root account and use su(1) for root access.
ip-172-31-53-207# 
```

Use `scp` copy the data set into instance.

```bash
➜  ~ git:(master) ✗ scp -i ~/Documents/p.pem ~/Desktop/pagecounts-20160327-000000.gz root@ec2-34-207-94-168.compute-1.amazonaws.com:~/pagecounts-20160327-000000.gz
pagecounts-20160327-000000.gz                                                            74%   98MB 301.6KB/s   01:51 ETA

```
keep Waiting until finished.

## Answear Question

Catch a glimpse of the data set. Then I know what the data set looks like.

```bash
ip-172-31-53-207# gzcat pagecounts-20160327-000000.gz | head -n 3
aa File:Boating_accident_injury.jpg 1 10840
aa File:Cash_payment_timeline_on_foreclosures.jpg 2 17202
aa File:Loreephotography.com/leona-dargis/_Loan_graphs.jpg 1 4697
```


1. How many unique objects were requested?

At first time, I found this t1.micor system memory is insufficient. The memory of t1.micor only has 0.613g.
I create another C3.large instance of ami-569ed93c. The process of creation is similar as above, so the same will not be repeated here. The new instance Public DNS is ec2-34-205-154-26.compute-1.amazonaws.com.

I also try to use 'gzcat pagecounts-20160327-000000.gz | cut -f2 -d' ' | sort | uniq | wc -l'. But the memory still insufficient.
By reading the documents in http://www.gnu.org/software/gawk/manual/gawk.html. I figured out this question.

```bash
ip-172-31-53-207# gzcat pagecounts-20160327-000000.gz | awk 'BEGIN{count=0} {if (data[$2]++ == 0){count++}} END{print "There are", count," unique objects."}'
There are 7682184  unique objects.
```

After finish Question3, I used '[ ]' as the delimiter.

```bash
ip-172-31-53-207# gzcat pagecounts-20160327-000000.gz | awk -F '[ ]' 'BEGIN{count=0} {if (data[$2]++ == 0){count++}} END{print "There are", count," unique objects."}'
There are 7682185  unique objects.
```

After reading mail list professor's reply,
I realized "unique pairing of domain and resource name" is a unique objects, so it's very simple:

```bash
ip-172-31-53-207# gzcat pagecounts-20160327-000000.gz | wc -l
 9771932
```


2. How many unique objects were requested for en only?

```bash
ip-172-31-53-207# gzcat pagecounts-20160327-000000.gz | awk 'BEGIN{count=0} {if ($1 == "en" && data[$2]++ == 0){count++}} END{print "There are", count," unique objects for en."}'
There are 2167954  unique objects for en.
```

After finish Question3, I used '[ ]' as the delimiter.
```
ip-172-31-53-207# gzcat pagecounts-20160327-000000.gz | awk -F '[ ]' 'BEGIN{count=0} {if ($1 == "en" && data[$2]++ == 0){count++}} END{print "There are", count," unique objects for en."}'
There are 2167954  unique objects for en.
```

I also found a more clear solution:

```bash
ip-172-31-53-207# gzcat pagecounts-20160327-000000.gz | grep "^en[ ]" | wc -l
 2167954
```


3. Which is the most often requested object for de?

```bash
ip-172-31-53-207# gzcat pagecounts-20160327-000000.gz | awk 'BEGIN{maxCount=0; ob=""} {if ($1 == "de" && $3>maxCount){maxCount = $3; ob = $2}} END{print "The most often requested object for de is", ob, " maxcount is ", maxCount}'
The most often requested object for de is 575  maxcount is  3489854
```
I feel that this result is unnormal. So I check this record.

```bash
ip-172-31-53-207# gzcat pagecounts-20160327-000000.gz | awk '{if ($1=="de" && ($2 =="575")) print $0}'
de  575 3489854
```

Seems like this recode lacked parameter 'page_title' (or the 'page_title' is null), so the `awk` recognized parameter 'count_views' as 'page_title' and 'total_response_size' as 'count_views'. And this is not an accidental phenomena.

```bash
ip-172-31-53-207# gzcat pagecounts-20160327-000000.gz | awk '{if ($4 == "") print $0}'
ar  1053 51660428
ar.m  4 40304
ar.s  5 163840
arz  10 559343
as  2 69937
ast  1 18563
av.v  1 905
...

```

I want to specificly set the delimiter is one whitespace. I tried "-F ' '", but failed. Then I realized the delimiter is a regular expression. I knew how to do:

```bash
ip-172-31-53-207# gzcat pagecounts-20160327-000000.gz | awk -F '[ ]' 'BEGIN{maxCount=0; ob=""} {if ($1 == "de" && $3>maxCount){maxCount = $3; ob = $2}} END{print "The most often requested object for de is", ob, " maxcount is ", maxCount}'
The most often requested object for de is Wikipedia:Hauptseite  maxcount is  15235
```

The most often requested object for de is Wikipedia:Hauptseite.

I also found a more clear solution (we knew that the object in each row is unique):

```bash
ip-172-31-53-207# gzcat pagecounts-20160327-000000.gz | grep "^de[ ]" | sort -t' ' -k3,3nr | head -1 | cut -f1,2 -d' '
de Wikipedia:Hauptseite
```

4. How many requests per second were handled during this hour?

```bash
ip-172-31-53-207# gzcat pagecounts-20160327-000000.gz | awk -F '[ ]' '{count+=$3} END{print count/3600}'
9999.72
```
9999.72 requests per second.

5. How much data was transferred in total?

```bash
ip-172-31-53-207# gzcat pagecounts-20160327-000000.gz | awk -F '[ ]' '{count+=$4} END{print count}'
800635232210
```
800635232210  data was transferred in total.

I look at the detail of this log in https://wikitech.wikimedia.org/wiki/Analytics/Data/Pagecounts-all-sites.
The unit of size is 'byte'. So there are 800635232210 bytes.

6. Which was the largest object requested for fr?
I thought that the size of object equals 'total_response_size'/'count_views'.

```bash
ip-172-31-53-207# gzcat pagecounts-20160327-000000.gz | awk -F '[ ]' 'BEGIN{max=0; ob=""} {if ($1 == "fr" && ($4/$3)>max){max = ($4/$3); ob = $2}} END{print "The largest object requested for fr is", ob, " the size is ", max}'
The largest object requested for fr is Projet:Palette/Maintenance/Listes  the size is  1679324
```

A more clear version:
```bash
ip-172-31-53-207# gzcat pagecounts-20160327-000000.gz | grep "^fr[ ]" | awk -F '[ ]' '{print $0,$4/$3}' | sort -t' ' -k5,5nr | head -1 | cut -f1,2 -d' '
fr Projet:Palette/Maintenance/Listes
```

The largest object requested for fr is Projet:Palette/Maintenance/Listes

7. What is the longest word found on the ten most frequently retrieved English Wikipedia pages?

To solve this proplem, first we should get the ten most frequently retrieved 'page_title'. English pages means domain is 'en' or 'en.*'
At first time, I found some pages can't crawl anything. Then I found:
In https://wikitech.wikimedia.org/wiki/Analytics/Data/Pagecounts-raw#Aggregation_for_.mw

```
Aggregation for .mw
Note: anomaly retained for backward compatibility! These lines better belong in project-level files. Best to ignore .mw lines.
...
So while the .mw abbreviation counts the mobile site, it throws wikipedia, wiktionary into the same bucket. And also, it does not distinguish between page_titles.
```
So I did `grep` to gain the 'en' domain except 'en.mw' domain wikipedia pages, then sort by 'counts_view' and cat the first 10 line.

```bash
ip-172-31-53-207# gzcat pagecounts-20160327-000000.gz | grep "^en" | grep -v "^en.mw" | sort -t' ' -k3,3nr | head -10 | cut -f1,2 -d' '
en.m Main_Page
en Main_Page
en Special:BlankPage
en.m Billy_Joe_Saunders
en.m Batman_v_Superman:_Dawn_of_Justice
en Sine
en Special:Search
en Simon_Pegg
en.m Chris_Eubank,_Jr.
en.m Buddy_Hield
```
Then I need to generate the url of each pages, use `awk`

```bash
ip-172-31-53-207# gzcat pagecounts-20160327-000000.gz | grep "^en" | grep -v "^en.mw" | sort -t' ' -k3,3nr | head -10 | cut -f1,2 -d' ' | awk '{printf ("https://%s.wikipedia.org/wiki/%s\n",$1,$2)}'
https://en.m.wikipedia.org/wiki/Main_Page
https://en.wikipedia.org/wiki/Main_Page
https://en.wikipedia.org/wiki/Special:BlankPage
https://en.m.wikipedia.org/wiki/Billy_Joe_Saunders
https://en.m.wikipedia.org/wiki/Batman_v_Superman:_Dawn_of_Justice
https://en.wikipedia.org/wiki/Sine
https://en.wikipedia.org/wiki/Special:Search
https://en.wikipedia.org/wiki/Simon_Pegg
https://en.m.wikipedia.org/wiki/Chris_Eubank,_Jr.
https://en.m.wikipedia.org/wiki/Buddy_Hield
```

I choose curl to crawl web data. Before that, I need to install curl. Found resource in https://curl.haxx.se/download.html
```bash
ip-172-31-53-207# ftp https://curl.haxx.se/download/curl-7.53.1.tar.gz
Trying 2a00:1a28:1200:9::2:443 ...
ftp: Can't connect to `2a00:1a28:1200:9::2:443': No route to host
Trying 80.67.6.50:443 ...
Requesting https://curl.haxx.se/download/curl-7.53.1.tar.gz
100% |***********************************|  3433 KiB  305.60 KiB/s    00:00 ETA
3516153 bytes retrieved in 00:11 (305.60 KiB/s)
ip-172-31-53-207# tar -zxf curl-7.53.1.tar.gz 
ip-172-31-53-207# cd curl-7.53.1
ip-172-31-53-207# make
...
make install
```

Crawl one pages for test.

```bash
ip-172-31-53-207# curl  https://en.wikipedia.org/wiki/Simon_Pegg
curl: (60) SSL certificate problem: unable to get local issuer certificate
More details here: https://curl.haxx.se/docs/sslcerts.html
curl performs SSL certificate verification by default, using a "bundle"
 of Certificate Authority (CA) public keys (CA certs). If the default
 bundle file isn't adequate, you can specify an alternate file
 using the --cacert option.
If this HTTPS server uses a certificate signed by a CA represented in
 the bundle, the certificate verification probably failed due to a
 problem with the certificate (it might be expired, or the name might
 not match the domain name in the URL).
If you'd like to turn off curl's verification of the certificate, use
 the -k (or --insecure) option.
```
The log say I need to do the SSL certificatation, I choose use -k to skip this step. And I want to ignore the log information in later process.

```bash
ip-172-31-53-207# curl -k -s https://en.wikipedia.org/wiki/Simon_Pegg | head -6
<!DOCTYPE html>
<html class="client-nojs" lang="en" dir="ltr">
<head>
<meta charset="UTF-8"/>
<title>Simon Pegg - Wikipedia</title>
<script>document.documentElement.className = document.documentElement.className.replace( /(^|\s)client-nojs(\s|$)/, "$1client-js$2" );</script>
ip-172-31-24-123# 
```

Then I need to clean up these useless character. I will use 'tr' to replace some symbol and character with space, only leave alpha.

```bash
ip-172-31-53-207# curl -k -s https://en.wikipedia.org/wiki/Simon_Pegg | head -6 | tr -c  "[:alpha:]" " "
  DOCTYPE html   html class  client nojs  lang  en  dir  ltr    head   meta charset  UTF 8     title Simon Pegg   Wikipedia  title   script document documentElement className   document documentElement className replace       s client nojs  s        1client js 2      script  
```

Use 'awk' to calculate the answear. 

```bash
...| awk 'BIGIN {maxWord=0; maxLeng=0;} {for(i=1;i<=NF;i++) if(length($i)>maxLeng){maxWord=$i; maxLeng=length($i);}} END {print maxWord,maxLeng}'

```
In the end, I also need to use 'xargs' to transfer the 'url' to 'curl' one by one, combine all of these:

```bash
ip-172-31-53-207# gzcat pagecounts-20160327-000000.gz | grep "^en" | grep -v "^en.mw" | sort -t' ' -k3,3nr | head -10 | cut -f1,2 -d' ' | awk '{printf ("https://%s.wikipedia.org/wiki/%s\n",$1,$2)}' | xargs curl -k -s | tr -c  "[:alpha:]" " " | awk 'BEGIN {maxWord=0; maxLeng=0;} {for(i=1;i<=NF;i++) if(length($i)>maxLeng){maxWord=$i; maxLeng=length($i);}} END {print maxWord,maxLeng}'
wgRelatedArticlesOnlyUseCirrusSearch 36
```

So the longest word found on the ten most frequently retrieved English Wikipedia pages is wgRelatedArticlesOnlyUseCirrusSearch.


rm $tmp
rm listInstanceId.txt
exit 0



```