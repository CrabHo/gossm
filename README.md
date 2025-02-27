# gossm

`gossm` is interactive CLI tool that you should select server in AWS and then could connect or send files your AWS server using start-session, ssh, scp under AWS Systems Manger Session Manager.
<p align="center">
<img src="https://storage.googleapis.com/gjbae1212-asset/gossm/start.gif" width="500", height="450" />
</p>

<p align="center"/>
<a href="https://circleci.com/gh/gjbae1212/gossm"><img src="https://circleci.com/gh/gjbae1212/gossm.svg?style=svg"></a>
<a href="https://hits.seeyoufarm.com"/><img src="https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2Fgjbae1212%2Fgossm"/></a>
<a href="/LICENSE"><img src="https://img.shields.io/badge/license-MIT-GREEN.svg" alt="license" /></a>
<a href="https://goreportcard.com/report/github.com/gjbae1212/gossm"><img src="https://goreportcard.com/badge/github.com/gjbae1212/gossm" alt="Go Report Card"/></a>
</p>

## Overview
`gossm` is interactive CLI tool that is related AWS Systems Manger Session Manager.
It can select a ec2 server installed aws-ssm-agent and then can connect its server using start-session, ssh.
As well as files can send using scp.  
If you will use `gossm` tool, this mean there will no need to open inbound 22 port in your ec2 server when is using ssh or scp command.  
Because AWS Systems Manger Session Manager is using ssh protocol tunneling.   
<br/>
**Additionally Features**
- `cmd` command has added. this command is executing a command on selected multiple servers, waiting for a response on its result. (**run command**)

## Prerequisite 
- [required] Your ec2 servers in aws are installed [aws ssm agent](https://docs.aws.amazon.com/systems-manager/latest/userguide/ssm-agent.html).
EC2 severs have to apply **AmazonEC2RoleforSSM** iam policy.     
If you would like to use ssh, scp command using gossm, aws ssm agent version **2.3.672.0 or later** is installed on ec2. 
- [required] **aws access key**, **aws secret key**
- [required] **ec2:DescribeInstances**, **ssm:StartSession permission**    
- [optional] It's better to possibly get to additional permission for **ec2:DescribeRegions**, **ssm:TerminateSession**

## Install
Support **x86_64**
```bash 
# homebrew
$ brew tap gjbae1212/gossm
$ brew install gossm

# mac
$ wget https://github.com/gjbae1212/gossm/releases/download/v1.0.5/gossm_1.0.5_Darwin_x86_64.tar.gz

# linux
$ wget https://github.com/gjbae1212/gossm/releases/download/v1.0.5/gossm_1.0.5_Linux_x86_64.tar.gz

# window
$ wget https://github.com/gjbae1212/gossm/releases/download/v1.0.5/gossm_1.0.5_Windows_x86_64.tar.gz
```

## How to use
### global command args
| args           | Description                                               | Default                |
| ---------------|-----------------------------------------------------------|------------------------|
| -c             | (optional) aws credentials file | $HOME/.aws/credentials |
| -p             | (optional) if you are having multiple aws profiles in credentials, it is name one of profiles | default |
| -r             | (optional) region in AWS that would like to connect |  |
| -t             | (optional) instanceId of server in AWS that would like to connect | |

If your machine don't exist $HOME/.aws/.credentials, have to pass `-c` args.  
```
# credentials file format
[default]
aws_access_key_id = AWS ACCESS KEY
aws_secret_access_key = AWS SECRET KEY
``` 
  
`-r` or `-t` don't pass args, it can select through interactive CLI.  
    
### command
#### start
```bash
$ gossm start 
```

#### ssh, scp
`-e` must pass args when is using scp.   
`-e` args is command and args when usually used to pass ssh or scp.
```bash
# ssh(if pem is already registered using ssh-add)
$ gossm ssh -e 'user@server-domain'

# ssh(if pem isn't registered)
$ gossm ssh -e '-i key.pem user@server-domain'

# ssh(if pem is already registered using ssh-add and don't pass -e option) -> select server using interactive cli
$ gossm ssh

# ssh(if pem isn't registered and don't pass -e option) -> select server using interactive cli
$ gossm ssh -i key.pem
 
# scp(if pem is already registered using ssh-add)
$ gossm scp -e 'file user@server-domain:/home/blahblah'

# scp(if pem isn't registered)
$ gossm scp -e '-i key.pem file user@server-domain:/home/blahblah'

```

#### cmd 
`-e` required args, it is a parameter for execute to command on selected servers.

```bash
# It is to execute a command("uptime") on selected multiple servers, waiting for a response on its result.
$ gossm cmd -e "uptime" 
```
 
**ex)**  
<p align="center">
<img src="https://storage.googleapis.com/gjbae1212-asset/gossm/ssh.gif" width="500", height="450" />
</p> 


## LICENSE
This project is following The MIT.
