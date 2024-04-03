---
title: afewmore
date: 2017-08-17 00:32:41
tags: System Administration
description: "A tool of ec2--how to write a shell tool"
---

# Description

* link: http://www.cs.stevens.edu/~jschauma/615/s17-hw6.html

## Objective:

The objective of this assignment is for you to write a simple system tool to perform a realistic sysadmin task using the EC2 environment. In doing so, you will practice the core principles of writing scalable system tools as discussed in class.

You will also learn to implement a program from a high-level specification. In so doing, you will practice the detection of hidden requirements and decision making in the face of ambiguity.

This assignment is worth 50 points.

Summary:

Implement the afewmore command as specified in this manual page.

Your program will behave exactly as outlined in that manual page, with no additional output or functionality.

Target platform:

The tool you write will be executed (and graded) on an Ubuntu instance ami-6de0dd04 with the 'awscli' package installed via 'sudo apt-get install awscli'. If your tool does not work in this environment, you will not get any points. See also: general homework guidelines.

Programming language

You are free to choose any programming language you like to implement this tool. Obviously, the program needs to be executed/run on the Ubuntu instance, and must not require the additional installation of any tools, libraries etc. besides what is already installed there.

Program behaviour

Your program will not require any modification of the environment (ie, you can assume the user has his/her environment set up for EC2), and exection of the program will be exactly as outlined in the manual page afewmore(1).

Your program will be robust. That is, it will handle error conditions and erroneous input in a graceful manner. Make sure to consider all the edge cases!

-----------

# Content

# afewmore
This is a task of CS615 in Stevens Institute of Technology.

Author

* [Eric Fitzpatrick](https://github.com/efitzpa1)
* [Ankai Liang](https://github.com/AnkaiLiang)

# Program description
For this homework assignment, our group used Bash as our programming language of choice. Bash allowed for us to easily interface with common shell commands and the AWS CLI tool. Since Bash has such low overhead, it also allows us to have competitive performance and write functionality compactly and directly.

# Challenges faced
The main challenge that our group faced is how to determine when a newly created EC2 instance is ready to ssh into. We got around this challenge by using sleep(1) commands to first wait for the instance state to change to 'Running' and then attempting to ssh into the instance a few times after small time intervals.

## Manual
```
AFEWMORE(1)		  BSD General Commands Manual		   AFEWMORE(1)

NAME
     afewmore -- duplicate EC2 instances with their data directory

SYNOPSIS
     afewmore [-hv] [-d dir] [-n num] instance

DESCRIPTION
     The afewmore tool can be used to duplicate a given EC2 instance.  When
     doing so, it creates multiple new instances and populates their data
     directory by copying the data from the original.

OPTIONS
     The source instance is specified via the mandatory argument to afewmore.
     In addition, the following command-line options are supported:

     -d dir   Copy the contents of this data directory from the orignal source
	      instance to all the new instances.  If not specified, defaults
	      to /data.

     -h       Print a usage statement and exit.

     -n num   Create this many new instances.  If not specified, defaults to
	      10.

     -v       Be verbose.

DETAILS
     Frequently, it is necessary to duplicate a given server's configuration
     or setup.	While configuration management and service orchestration sys-
     tems may be able to perform this task, the afewmore tool allows for a
     trivial initial bootstrapping that only concerns itself with data dupli-
     cation, not host configuration.

     Upon invocation, afewmore will identify the type of EC2 instance in ques-
     tion and launch the requested number of duplicates.  It will then copy
     the contents of the given directory from the source instance to all of
     the newly created instances.

OUTPUT
     By default, afewmore prints the instance IDs of the newly created EC2
     instances as the only output.  Unless an error occurs, no other output is
     generated.

     If the -v flag is given, afewmore may print meaningful diagnostic mes-
     sages as it progresses to stdout.

     Any errors encountered cause a meaningful error message to be printed to
     STDERR.

ENVIRONMENT
     The afewmore tool is suitable to be used by any user and does not have
     any user-specific settings or credentials hard coded.

     afewmore assumes that the user has set up their environment for general
     use with the EC2 tools.  That is, it will not set or modify any environ-
     ment variables.

     afewmore also assumes that the user has set up their ~/.ssh/config file
     to access instances in EC2 via ssh(1) without any additional settings.

EXIT STATUS
     The afewmore will exit with a return status of 0 under normal circum-
     stances.  If an error occurred, afewmore will exit with a value >0.

EXAMPLES
     The following examples illustrate common usage of this tool.

     To create ten more instances of the EC2 instance i-0a1b2c3d4f and copy
     the contents of the '/data' directory from that instance:

	   $ afewmore i-0a1b2c3d4f
	   i-1a1b2c3d4f
	   i-2a1b2c3d4f
	   i-3a1b2c3d4f
	   i-4a1b2c3d4f
	   i-5a1b2c3d4f
	   i-6a1b2c3d4f
	   i-7a1b2c3d4f
	   i-8a1b2c3d4f
	   i-9a1b2c3d4f
	   i-0b1b2c3d4f
	   $ echo $?
	   0
	   $

     To create just one more instance and copy the contents of the directory
     '/usr/local/share':

	   $ afewmore -d /usr/local/share -n 1 i-0a1b2c3d4f
	   i-1a1b2c3d4f
	   $

SEE ALSO
     aws help, ssh(1), tar(1), rsync(1)

HISTORY
     afewmore was originally assigned by Jan Schaumann
     <jschauma@cs.stevens.edu> as a homework assignment for the class "Aspects
     of System Administration" at Stevens Institute of Technology in the
     Spring of 2017.

BSD				April 09, 2017				   BSD
```

## The commentary

### Ankai Liang
I decide to use shell script to finish this task.

1. At the beginning, I look for the arguments which inputted by user.
I found two way, one is manually dealing with them. It requires users to input arguments with explicit position. The other way is using `getopts`, a useful tool which can handle the short options. 
[Tutorial](http://wiki.bash-hackers.org/howto/getopts_tutorial)
After testing, I found that if -d is missing an argument, it will instead of taking the next option as the parameter. So I added a check in each options which need value.

2. Then I need to grab the information of target instance by a given instance-id.
I learned how to write a funtion in Shell Script. When I test the result shell function return, I found `$?` only return the numeric result, and the variable without `local` declaration would domain global, a good choice to record the function result.
About the parameter passing, if I use variable to transfer the json data, it will lose the line feeds. So I use the temp file to store the json data.
By the way, using '&' to make `echo command` running in background in funtion and using 'a=`func args`' outside is also a good way to implement funtion return. But in this way, it can't exit entire script in function when meet error. Maybe the main shell create a sub-shell environment to run sub-command.
Tricky point, sometimes the response from aws contains some null data in some attributes. We should filter them by 'grep "^$"'

3. Next I try to ensure what is UserName when ssh to remote server. Create a table, acquire image-Description, and use awk to match UserName. When use awk to do regular expression searching, I have to transfer the shell variables into awk.[Tutorial](https://www.gnu.org/software/gawk/manual/gawk.html#Using-Shell-Variables)

4. I want to check whether shell sucessfully ssh to the Target server. But I noticed when I offer the wrong username, cli will go into interface and ask for password. If I want to automaticlly deal with the interface, I need install `expect`, that's unallowed. I don't have a better way to solve it.

5. When trasfer the data between two instance, my test remote instance is NetBSD without rsync, I decided transfer the data by `scp`.
6. Because setting up instance need some time. so I have to wait a few seconds then execute the copy mission.

7. "Host key verification failed." I fail to use `scp` transfer data from remote instance to another remote one. I realized scp can't do that between two remote nodes. I need to copy one node's rsa public key to the other, then use ssh into one remote to do that transmission.
After communication with classmates, I knew that `scp` has a option '-3', which can transfer data between two remote instance via the local instance. According the principle of least astonishment, I think using `scp -3` without the change of `authorized_keys` file is the better solution.
8. Deal with the directory path. Before using `scp`, I have to make sure the directory's parent path exists. Use pattern matching to adjust `${path}` and `mkdir -p` to create in new instance.
9. Implement all basic function!
10. When testing create instance with other images, I found some of OS login user accounts don't have the authority to create new directory or files in some specific place. So I shoud chang the target directory authority to allow ssh write and execute.

### Eric Fitzpatrick

Ankai and I chose to both develop our own independent versions of the 'afewmore' program and then collaborate to merge the best parts of our implementations together. I also used Bash so this process was straightforward. We took very similar approaches so I chose to refine the version on Ankai's GitHub repository to match up to mine and use as our submission. My main contributions to his version was increasing the error handling capabilities of the program, increasing the verbosity of the usage statement (included flag information), and modifying the script to use the mktemp(1) function instead of an in-directory temp.txt file which could have potentially deleted or modified a user's temp.txt file unintentionally. I also added a trap(1) statement to delete this temporary file upon a SIGINT signal (control+c).

--------------

# Code

```bash
#!/bin/bash

catalog="/data"
num=10
verbose="false"

cleanup()
{
    log "Cleaning up temporary file"
    rm -f $tmp
    exit 1
}
log()
{
	if [ "$verbose" = "true" ];
	then
		echo $@ 
	fi
}

iferr()
{
	if [ $? != 0 ];
	then 
		echo $@ >&2
		exit 1;
	fi
}
usage() 
{
	echo -e "Usage: afewmore [-hv] [-d dir] [-n num] instance\n\n  -d dir  Copy the contents of this data directory from the original source\n          instance to all new instances. If not specified, defaults\n          to /data.\n\n  -h      Print a usage statement and exit.\n\n  -n num  Create this many new instances. If not specified, defaults to\n          10.\n\n  -v      Be verbose."
}
getInfo()
{
	((cat $tmp | grep "\"$1\"") || (echo "Fail to get the $1 info." >&2; exit 1;))\
	 | tr ":\"," " "  | awk '{print $2}' | sort | uniq | grep -v "null" | grep -v "^$"
#	delete the null line

}
getAllInfo()
{
	InstanceId=$1
	aws ec2 describe-instances --output json --filters "Name=instance-id,Values=${InstanceId}" > $tmp
	PublicDnsName=$(getInfo PublicDnsName)
	ImageId=$(getInfo ImageId)
	InstanceType=$(getInfo InstanceType)
	KeyName=$(getInfo KeyName)
	GroupName=$(getInfo GroupName)
	AvailabilityZone=$(getInfo AvailabilityZone)
	PublicDnsName=$(getInfo PublicDnsName)
	iferr "Fail to get the info for ${InstanceId}. Please check instance-id and its state."
}

while getopts ":d:n:hv" arg; 
do
	case ${arg} in
		h)
			usage
			exit 0
			;;
		d)
			catalog=${OPTARG}
			if ! [[ $catalog =~ ^/.*$ ]];
			then
				echo "-d's argument is not a valid Unix style path" >&2
				usage
				exit 1;
			fi
			;;
		n)	
			if [[ $OPTARG =~ ^[0-9]+$ ]]
			then
			    if [ $OPTARG -gt 0 ]
			    then
				num=${OPTARG}
			    else
				echo "-n's argument must be greater than 0." >&2
				exit 1;
			    fi
			else
				echo "-n's argument is not a number." >&2
				usage
				exit 1;
			fi
			;;
		v)
			verbose="true"
			;;
		\?)
			echo "Unknown argument: -$OPTARG" >&2
			usage
			exit 1
			;;
		:)
      		echo "Option -$OPTARG requires an argument." >&2
      		usage
     		exit 1
     		;;
	esac
done

shift $((OPTIND-1)) # shift the instance id arguments to $1
if [ -z $1 ];
then
	echo "Requires an instance id to point out which instance will be replicated." >&2
	usage
	exit 1
fi

log "Arguments format is correct." 
log "Tring to acquire target instance's info..."

# get the info for origin instance

targetId=$1
if ! [[ $targetId =~ ^i-[a-z0-9]+$ ]]
then
    echo "Invalid instance ID '$targetId' provided." >&2
    usage
    exit 1;
fi
tmp=$(mktemp)
trap cleanup SIGINT
getAllInfo $targetId
targetPublicDns=${PublicDnsName}


log "done"
log "Target instance info: InstanceId=${InstanceId}, PublicDnsName=${PublicDnsName}, InstanceType=${InstanceType},\
 ImageId=${ImageId}, KeyName=${KeyName}, GroupName=${GroupName}, AvailabilityZone=${AvailabilityZone}"
log "Tring to ssh to target instance..." 

## get the username according to image-id

aws ec2 describe-images --output json --filters "Name=image-id, Values=${ImageId}" > $tmp
ImageName=$(getInfo Name)
username=$(cat UsernameTable | awk -F ":" -v pat="${ImageName}" 'pat ~ $1 { print $2 }' | head -1)
if [ -z ${username} ]
then
	username="root"
fi

## check can we log into target instance and the directory is exist

if ssh -o StrictHostKeyChecking=no -o LogLevel=quiet ${username}@${targetPublicDns} :;
then 
	log "successful ssh to the target instance"
	log "username=${username}, ImageName=${ImageName}"
else 
	echo "Fail to ssh to the target instance" >&2
	exit 1
fi

if ssh -o StrictHostKeyChecking=no ${username}@${targetPublicDns} test -e ${catalog};
then
	log "${catalog} exists on instance '$targetId'"
else 
	echo "${catalog} does not exist on instance '$targetId', please check the directory path" >&2
	exit 1
fi


# create ${num} new instance. 

log "Trying to create ${num} new instances..."

aws ec2 run-instances --image-id ${ImageId} --count ${num} --instance-type\
 ${InstanceType} --key-name ${KeyName} --security-groups ${GroupName} --placement AvailabilityZone=${AvailabilityZone} > $tmp
iferr "Fail to create new instances, plase check awscli configuration and network"

log "done"
log "Waiting for instances pending..."
getInfo InstanceId > listInstanceId.txt
sleep 100s

## Deal with each new Instance
for line in $(cat listInstanceId.txt)
do
	aws ec2 describe-instances --output json --filters "Name=instance-id,Values=${line}" > $tmp
	state=$(getInfo Name)
	i=0;
	while [ "${state}" != "running" ];
	do
		i=$(( $i + 1 ))
		sleep 5s
		aws ec2 describe-instances --output json --filters "Name=instance-id,Values=${line}" > $tmp
		state=$(getInfo Name) # loop until state = running
		if [ ${i} -gt 10 ]
		then
			echo "Overtime, fail to get PublicDnsName for instance ${line}" >&2
		fi
	done
	
	newPublicDnsName=$(getInfo PublicDnsName)
	iferr "Fail to get newPublicDnsName for instance ${line}"
	log "newPublicDnsName=${newPublicDnsName}"

	log "Testing ssh to new instance ${line}..."
	i=0;
	ssh -o StrictHostKeyChecking=no -o LogLevel=quiet ${username}@${newPublicDnsName} :
	while [ $? != 0 ];
	do
		i=$(( $i + 1 ))
		if [ ${i} -gt 15 ]
		then
			echo "Fail ssh to new instance ${line}" >&2
		fi
		sleep 5s
		ssh -o StrictHostKeyChecking=no -o LogLevel=quiet ${username}@${newPublicDnsName} :
	done
	log "done" 

	log "Prepare the directory on new instance ${line}"
	newcatalog="${catalog%/?*}"
	ssh -o StrictHostKeyChecking=no -o LogLevel=quiet ${username}@${newPublicDnsName} "(test -e ${newcatalog:="/"} || sudo mkdir -p ${newcatalog}) && ([ -w ${newcatalog} ] && [ -x ${newcatalog} ] || sudo chmod a+wx ${newcatalog})"
	iferr "Fail to create directory path on instance ${line}"
	log "Ready. newcatalog=$newcatalog"


	log "Running scp -3 from ${username}@${targetPublicDns}:${catalog} to ${username}@${newPublicDnsName}:${newcatalog}..."
	scp -r -q -p -o StrictHostKeyChecking=no -o LogLevel=quiet -3 ${username}@${targetPublicDns}:${catalog} ${username}@${newPublicDnsName}:${newcatalog}
	iferr "Fail to copy directory content form ${targetId} to ${line}"
	log "done."
done


cat listInstanceId.txt
log "Success."

rm $tmp
rm listInstanceId.txt
exit 0



```