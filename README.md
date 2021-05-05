
<h1 align="center">Consul HSRE 1400</h1>


<br>

## :dart: About ##

The Objective: To install Consul on all the instances & containers in AWS. 


## :rocket: Technologies ##

The following UI is used in this project:

- [Consul-UI](https://consul-Mother.consul.7f00190b-f5e0-4010-ba52-d6cb799f4985.aws.hashicorp.cloud)


## :white_check_mark: Requirements ##

Before starting :checkered_flag:, you need to have [Git](https://git-scm.com) and [Consul](https://www.consul.io/) installed.

AWS account Number: 404083424001

VPC ID: vpc-062715adebaadd00a

VPC Region of Deploy: us-east-1

VPC CIDR block: 10.0.0.0/16





## :checkered_flag: Starting ##

```bash
# Clone this project
$ git clone https://github.com/{{ws-el-gato}}/consul-hsre-1400

# Access
$ cd consul-hsre-1400

# Review the following checklist to make sure you have all the required configuration artifacts, and that you understand what each of them provides.
$ ls
ca.pem client_acl.json client_config.json

# The ca.pem file will be used to authenticate via mTLS.
# The client_acl.json file has the ACL token that will be used to authorize with the ACL system.
# The client_config.json file has the gossip encryption key, the path to where you are about to move the ca.pem file, and the retry_join endpoint that the agent needs to use to join the Consul cluster.

# Install dependencies
$ sudo apt update -y && sudo apt upgrade -y
$ sudo apt install consul unzip -y
$ sudo mkdir -p /opt/consul/
$ aws s3 cp s3://wellsky-jordan-test/consul-agent-config.zip .
$ unzip consul-agent-config.zip
$ cp -rf consul-agent-config/* /opt/consul/

# You can now start the client agent using the consul agent command.

$ sudo consul agent -config-dir=/opt/consul -data-dir=/opt/consul

```

Notes on installing Consul via Cloud Managed via hashicorp.

Install has been easy. I was able to get the VPC and Peering done today in the sandbox account... this is on Read-Only Fridays.argh But this is just testing. So no alerts should happen. 

# The Objective: 

To install Consul on all the instances & containers in AWS. 

# Let's talk about the naming system. 

  * Alpha test will start with an A appending a Number
        Example: consul-A1 , consul-A2 , consule-A3 ect.. 
  
  * Beta test will start with a B followed by a Number
        Example: consul-B1 , consul-B2 , consule-B3 ect.. 

 These Groups Alpha and Beta will be test cases to report back to Consul-Mother. 


Managed Consul UI URL: 
https://hhh-consul-mother.consul.7f00190b-f5e0-4010-ba52-d6cb799f4985.aws.hashicorp.cloud/ui/dc1/nodes


-- Truthfully this managed way is much easier then sliced bread. This is the Pitch right here. Have Hashicorp do it. --

# While at it. Shot out to Managed Consul on Hashicorp.
 

{command_run}
jordan.robison@WS-C02D35PQMD6R ~ % aws ec2 --region us-east-1 accept-vpc-peering-connection --vpc-peering-connection-id pcx-0bee6526bea614079


{
    "VpcPeeringConnection": {
        "AccepterVpcInfo": {
            "CidrBlock": "172.17.0.0/16",
            "CidrBlockSet": [
                {
                    "CidrBlock": "172.17.0.0/16"
                }
            ],
            "OwnerId": "404083424001",
            "PeeringOptions": {
                "AllowDnsResolutionFromRemoteVpc": false,
                "AllowEgressFromLocalClassicLinkToRemoteVpc": false,
                "AllowEgressFromLocalVpcToRemoteClassicLink": false
            },
            "VpcId": "vpc-0b97e54f4477fa766",
            "Region": "us-east-1"
        },
        "RequesterVpcInfo": {
            "CidrBlock": "172.25.16.0/20",
            "CidrBlockSet": [
                {
                    "CidrBlock": "172.25.16.0/20"
                }
            ],
            "OwnerId": "892415907660",
            "VpcId": "vpc-069bb9aee4b3bc228",
            "Region": "us-east-1"
        },
        "Status": {
            "Code": "provisioning",
            "Message": "Provisioning"
        },
        "Tags": [],
        "VpcPeeringConnectionId": "pcx-0bee6526bea614079"
    }
}


{command_run}
jordan.robison@WS-C02D35PQMD6R ~ % aws ec2 describe-vpc-peering-connections --filters Name=requester-vpc-info.vpc-id,Values=vpc-079741e2ac20a8c50 --output=table


---------------------------------------------------------------
|                DescribeVpcPeeringConnections                |
+-------------------------------------------------------------+
||                   VpcPeeringConnections                   ||
|+-----------------------------+-----------------------------+|
||  VpcPeeringConnectionId     |  pcx-0ab54341eff9186f5      ||
|+-----------------------------+-----------------------------+|
|||                     AccepterVpcInfo                     |||
||+------------------+--------------------------------------+||
|||  CidrBlock       |  172.20.0.0/19                       |||
|||  OwnerId         |  404083424001                        |||
|||  Region          |  us-east-1                           |||
|||  VpcId           |  vpc-0b6d4fe0c0c9f489c               |||
||+------------------+--------------------------------------+||
||||                     CidrBlockSet                      ||||
|||+-----------------------+-------------------------------+|||
||||  CidrBlock            |  172.20.0.0/19                ||||
|||+-----------------------+-------------------------------+|||
||||                    PeeringOptions                     ||||
|||+----------------------------------------------+--------+|||
||||  AllowDnsResolutionFromRemoteVpc             |  False ||||
||||  AllowEgressFromLocalClassicLinkToRemoteVpc  |  False ||||
||||  AllowEgressFromLocalVpcToRemoteClassicLink  |  False ||||
|||+----------------------------------------------+--------+|||
|||                    RequesterVpcInfo                     |||
||+------------------+--------------------------------------+||
|||  CidrBlock       |  10.0.0.0/19                         |||
|||  OwnerId         |  404083424001                        |||
|||  Region          |  us-east-1                           |||
|||  VpcId           |  vpc-079741e2ac20a8c50               |||
||+------------------+--------------------------------------+||
||||                     CidrBlockSet                      ||||
|||+------------------------+------------------------------+|||
||||  CidrBlock             |  10.0.0.0/19                 ||||
|||+------------------------+------------------------------+|||
||||                    PeeringOptions                     ||||
|||+----------------------------------------------+--------+|||
||||  AllowDnsResolutionFromRemoteVpc             |  False ||||
||||  AllowEgressFromLocalClassicLinkToRemoteVpc  |  False ||||
||||  AllowEgressFromLocalVpcToRemoteClassicLink  |  False ||||
|||+----------------------------------------------+--------+|||
|||                         Status                          |||
||+-----------------------------+---------------------------+||
|||  Code                       |  active                   |||
|||  Message                    |  Active                   |||
||+-----------------------------+---------------------------+||
|||                          Tags                           |||
||+-------------------+-------------------------------------+||
|||        Key        |                Value                |||
||+-------------------+-------------------------------------+||
|||  Application      |  HHH                                |||
|||  Environment      |  Validation                         |||
|||  Service          |                                     |||
|||  Name             |  atlantis to HHH-validation         |||
|||  Owner            |  HHH SRE                            |||
|||  BusinessUnit     |  HHH                                |||
||+-------------------+-------------------------------------+||


# To describe all instances with Tag "Name" and its value as "consul-A1" Use: 
aws ec2 describe-instances --filters "Name=tag:Name,Values=consul-A1" --output=table

[code]
-------------------------------------------------------------------------------------------------
|                                       DescribeInstances                                       |
+-----------------------------------------------------------------------------------------------+
||                                        Reservations                                         ||
|+--------------------------------------+------------------------------------------------------+|
||  OwnerId                             |  404083424001                                        ||
||  ReservationId                       |  r-0982012a4c3e09426                                 ||
|+--------------------------------------+------------------------------------------------------+|
|||                                         Instances                                         |||
||+-------------------------------+-----------------------------------------------------------+||
|||  AmiLaunchIndex               |  0                                                        |||
|||  Architecture                 |  x86_64                                                   |||
|||  ClientToken                  |                                                           |||
|||  EbsOptimized                 |  False                                                    |||
|||  EnaSupport                   |  True                                                     |||
|||  Hypervisor                   |  xen                                                      |||
|||  ImageId                      |  ami-042e8287309f5df03                                    |||
|||  InstanceId                   |  i-0fe10b93fe6b2a9b1                                      |||
|||  InstanceType                 |  t2.micro                                                 |||
|||  KeyName                      |  hashicorp-consul                                         |||
|||  LaunchTime                   |  2021-04-09T16:37:59+00:00                                |||
|||  PrivateDnsName               |  ip-10-212-224-210.sandbox.hhh.wellsky.dev                |||
|||  PrivateIpAddress             |  10.212.224.210                                           |||
|||  PublicDnsName                |                                                           |||
|||  RootDeviceName               |  /dev/sda1                                                |||
|||  RootDeviceType               |  ebs                                                      |||
|||  SourceDestCheck              |  True                                                     |||
|||  StateTransitionReason        |                                                           |||
|||  SubnetId                     |  subnet-03ee37ae3bfa21587                                 |||
|||  VirtualizationType           |  hvm                                                      |||
|||  VpcId                        |  vpc-0d049a920cda5aca1                                    |||
||+-------------------------------+-----------------------------------------------------------+||
||||                                   BlockDeviceMappings                                   ||||
|||+---------------------------------------------+-------------------------------------------+|||
||||  DeviceName                                 |  /dev/sda1                                ||||
|||+---------------------------------------------+-------------------------------------------+|||
|||||                                          Ebs                                          |||||
||||+-------------------------------------+-------------------------------------------------+||||
|||||  AttachTime                         |  2021-04-09T16:38:00+00:00                      |||||
|||||  DeleteOnTermination                |  True                                           |||||
|||||  Status                             |  attached                                       |||||
|||||  VolumeId                           |  vol-09a6cb3e3c8ef8bca                          |||||
||||+-------------------------------------+-------------------------------------------------+||||
||||                            CapacityReservationSpecification                             ||||
|||+-----------------------------------------------------------------------+-----------------+|||
||||  CapacityReservationPreference                                        |  open           ||||
|||+-----------------------------------------------------------------------+-----------------+|||
||||                                       CpuOptions                                        ||||
|||+---------------------------------------------------------------------+-------------------+|||
||||  CoreCount                                                          |  1                ||||
||||  ThreadsPerCore                                                     |  1                ||||
|||+---------------------------------------------------------------------+-------------------+|||
||||                                   HibernationOptions                                    ||||
|||+-----------------------------------------------------+-----------------------------------+|||
||||  Configured                                         |  False                            ||||
|||+-----------------------------------------------------+-----------------------------------+|||
||||                                   IamInstanceProfile                                    ||||
|||+-----+-----------------------------------------------------------------------------------+|||
||||  Arn|  arn:aws:iam::404083424001:instance-profile/AmazonSSMRoleForInstancesQuickSetup   ||||
||||  Id |  AIPAV4FJ7XMA4KLPWJE5H                                                            ||||
|||+-----+-----------------------------------------------------------------------------------+|||
||||                                     MetadataOptions                                     ||||
|||+-------------------------------------------------------------+---------------------------+|||
||||  HttpEndpoint                                               |  enabled                  ||||
||||  HttpPutResponseHopLimit                                    |  1                        ||||
||||  HttpTokens                                                 |  optional                 ||||
||||  State                                                      |  applied                  ||||
|||+-------------------------------------------------------------+---------------------------+|||
||||                                       Monitoring                                        ||||
|||+-------------------------------------+---------------------------------------------------+|||
||||  State                              |  disabled                                         ||||
|||+-------------------------------------+---------------------------------------------------+|||
||||                                    NetworkInterfaces                                    ||||
|||+-------------------------------------+---------------------------------------------------+|||
||||  Description                        |  Primary network interface                        ||||
||||  InterfaceType                      |  interface                                        ||||
||||  MacAddress                         |  02:db:56:31:d5:b1                                ||||
||||  NetworkInterfaceId                 |  eni-06699097885babad2                            ||||
||||  OwnerId                            |  404083424001                                     ||||
||||  PrivateIpAddress                   |  10.212.224.210                                   ||||
||||  SourceDestCheck                    |  True                                             ||||
||||  Status                             |  in-use                                           ||||
||||  SubnetId                           |  subnet-03ee37ae3bfa21587                         ||||
||||  VpcId                              |  vpc-0d049a920cda5aca1                            ||||
|||+-------------------------------------+---------------------------------------------------+|||
|||||                                      Attachment                                       |||||
||||+-----------------------------------+---------------------------------------------------+||||
|||||  AttachTime                       |  2021-04-09T16:37:59+00:00                        |||||
|||||  AttachmentId                     |  eni-attach-01c8256c164cc9cf3                     |||||
|||||  DeleteOnTermination              |  True                                             |||||
|||||  DeviceIndex                      |  0                                                |||||
|||||  Status                           |  attached                                         |||||
||||+-----------------------------------+---------------------------------------------------+||||
|||||                                        Groups                                         |||||
||||+-----------------------------+---------------------------------------------------------+||||
|||||  GroupId                    |  sg-0428644ed74113b96                                   |||||
|||||  GroupName                  |  default                                                |||||
||||+-----------------------------+---------------------------------------------------------+||||
|||||                                  PrivateIpAddresses                                   |||||
||||+---------------------------------------------+-----------------------------------------+||||
|||||  Primary                                    |  True                                   |||||
|||||  PrivateIpAddress                           |  10.212.224.210                         |||||
||||+---------------------------------------------+-----------------------------------------+||||




-------------------------------------------------------------------------------------------------
|                                       DescribeInstances                                       |
+-----------------------------------------------------------------------------------------------+
||                                        Reservations                                         ||
|+--------------------------------------+------------------------------------------------------+|
||  OwnerId                             |  404083424001                                        ||
||  ReservationId                       |  r-0982012a4c3e09426                                 ||
|+--------------------------------------+------------------------------------------------------+|
|||                                         Instances                                         |||
||+-------------------------------+-----------------------------------------------------------+||
|||  AmiLaunchIndex               |  0                                                        |||
|||  Architecture                 |  x86_64                                                   |||
|||  ClientToken                  |                                                           |||
|||  EbsOptimized                 |  False                                                    |||
|||  EnaSupport                   |  True                                                     |||
|||  Hypervisor                   |  xen                                                      |||
|||  ImageId                      |  ami-042e8287309f5df03                                    |||
|||  InstanceId                   |  i-0fe10b93fe6b2a9b1                                      |||
|||  InstanceType                 |  t2.micro                                                 |||
|||  KeyName                      |  hashicorp-consul                                         |||
|||  LaunchTime                   |  2021-04-09T16:37:59+00:00                                |||
|||  PrivateDnsName               |  ip-10-212-224-210.sandbox.hhh.wellsky.dev                |||
|||  PrivateIpAddress             |  10.212.224.210                                           |||
|||  PublicDnsName                |                                                           |||
|||  RootDeviceName               |  /dev/sda1                                                |||
|||  RootDeviceType               |  ebs                                                      |||
|||  SourceDestCheck              |  True                                                     |||
|||  StateTransitionReason        |                                                           |||
|||  SubnetId                     |  subnet-03ee37ae3bfa21587                                 |||
|||  VirtualizationType           |  hvm                                                      |||
|||  VpcId                        |  vpc-0d049a920cda5aca1                                    |||
||+-------------------------------+-----------------------------------------------------------+||
||||                                   BlockDeviceMappings                                   ||||
|||+---------------------------------------------+-------------------------------------------+|||
||||  DeviceName                                 |  /dev/sda1                                ||||
|||+---------------------------------------------+-------------------------------------------+|||
|||||                                          Ebs                                          |||||
||||+-------------------------------------+-------------------------------------------------+||||
|||||  AttachTime                         |  2021-04-09T16:38:00+00:00                      |||||
|||||  DeleteOnTermination                |  True                                           |||||
|||||  Status                             |  attached                                       |||||
|||||  VolumeId                           |  vol-09a6cb3e3c8ef8bca                          |||||
||||+-------------------------------------+-------------------------------------------------+||||
||||                            CapacityReservationSpecification                             ||||
|||+-----------------------------------------------------------------------+-----------------+|||
||||  CapacityReservationPreference                                        |  open           ||||
|||+-----------------------------------------------------------------------+-----------------+|||
||||                                       CpuOptions                                        ||||
|||+---------------------------------------------------------------------+-------------------+|||
||||  CoreCount                                                          |  1                ||||
||||  ThreadsPerCore                                                     |  1                ||||
|||+---------------------------------------------------------------------+-------------------+|||
||||                                   HibernationOptions                                    ||||
|||+-----------------------------------------------------+-----------------------------------+|||
||||  Configured                                         |  False                            ||||
|||+-----------------------------------------------------+-----------------------------------+|||
||||                                   IamInstanceProfile                                    ||||
|||+-----+-----------------------------------------------------------------------------------+|||
||||  Arn|  arn:aws:iam::404083424001:instance-profile/AmazonSSMRoleForInstancesQuickSetup   ||||
||||  Id |  AIPAV4FJ7XMA4KLPWJE5H                                                            ||||
|||+-----+-----------------------------------------------------------------------------------+|||
||||                                     MetadataOptions                                     ||||
|||+-------------------------------------------------------------+---------------------------+|||
||||  HttpEndpoint                                               |  enabled                  ||||
||||  HttpPutResponseHopLimit                                    |  1                        ||||
||||  HttpTokens                                                 |  optional                 ||||
||||  State                                                      |  applied                  ||||
|||+-------------------------------------------------------------+---------------------------+|||
||||                                       Monitoring                                        ||||
|||+-------------------------------------+---------------------------------------------------+|||
||||  State                              |  disabled                                         ||||
|||+-------------------------------------+---------------------------------------------------+|||
||||                                    NetworkInterfaces                                    ||||
|||+-------------------------------------+---------------------------------------------------+|||
||||  Description                        |  Primary network interface                        ||||
||||  InterfaceType                      |  interface                                        ||||
||||  MacAddress                         |  02:db:56:31:d5:b1                                ||||
||||  NetworkInterfaceId                 |  eni-06699097885babad2                            ||||
||||  OwnerId                            |  404083424001                                     ||||
||||  PrivateIpAddress                   |  10.212.224.210                                   ||||
||||  SourceDestCheck                    |  True                                             ||||
||||  Status                             |  in-use                                           ||||
||||  SubnetId                           |  subnet-03ee37ae3bfa21587                         ||||
||||  VpcId                              |  vpc-0d049a920cda5aca1                            ||||
|||+-------------------------------------+---------------------------------------------------+|||
|||||                                      Attachment                                       |||||
||||+-----------------------------------+---------------------------------------------------+||||
|||||  AttachTime                       |  2021-04-09T16:37:59+00:00                        |||||
|||||  AttachmentId                     |  eni-attach-01c8256c164cc9cf3                     |||||
|||||  DeleteOnTermination              |  True                                             |||||
|||||  DeviceIndex                      |  0                                                |||||
|||||  Status                           |  attached                                         |||||
||||+-----------------------------------+---------------------------------------------------+||||
|||||                                        Groups                                         |||||
||||+-----------------------------+---------------------------------------------------------+||||
|||||  GroupId                    |  sg-0428644ed74113b96                                   |||||
|||||  GroupName                  |  default                                                |||||
||||+-----------------------------+---------------------------------------------------------+||||
|||||                                  PrivateIpAddresses                                   |||||
||||+---------------------------------------------+-----------------------------------------+||||
|||||  Primary                                    |  True                                   |||||
|||||  PrivateIpAddress                           |  10.212.224.210                         |||||
||||+---------------------------------------------+-----------------------------------------+||||
||||                                        Placement                                        ||||
|||+----------------------------------------------------+------------------------------------+|||
||||  AvailabilityZone                                  |  us-east-1a                        ||||
||||  GroupName                                         |                                    ||||
||||  Tenancy                                           |  default                           ||||
|||+----------------------------------------------------+------------------------------------+|||
||||                                     SecurityGroups                                      ||||
|||+------------------------------+----------------------------------------------------------+|||
||||  GroupId                     |  sg-0428644ed74113b96                                    ||||
||||  GroupName                   |  default                                                 ||||
|||+------------------------------+----------------------------------------------------------+|||
||||                                          State                                          ||||
|||+------------------------------------+----------------------------------------------------+|||
||||  Code                              |  16                                                ||||
||||  Name                              |  running                                           ||||
|||+------------------------------------+----------------------------------------------------+|||
||||                                          Tags                                           ||||
|||+----------------+------------------------------------------------------------------------+|||
||||       Key      |                                 Value                                  ||||
|||+----------------+------------------------------------------------------------------------+|||
||||  Test          |  Consul                                                                ||||
||||  Name          |  consul-A1                                                             ||||
||||  name          |  hhh-consul-managed-hashicorp                                          ||||
|||+----------------+------------------------------------------------------------------------+|||


```
After figuring out that the UI wasn't public I decided to restart to make the UI public but I had to clean up my VPC routing.


aws ec2 --region us-east-1 authorize-security-group-ingress --group-id sg-09145d5853dd77e97 --ip-permissions 
IpProtocol=tcp,FromPort=8300,ToPort=8300,IpRanges='[{CidrIp=172.25.16.0/20}]' 
IpProtocol=tcp,FromPort=8301,ToPort=8301,IpRanges='[{CidrIp=172.25.16.0/20}]' 
IpProtocol=udp,FromPort=8301,ToPort=8301,IpRanges='[{CidrIp=172.25.16.0/20}]' 
IpProtocol=tcp,FromPort=8301,ToPort=8301,UserIdGroupPairs='[{GroupId=sg-09145d5853dd77e97}]' 
IpProtocol=udp,FromPort=8301,ToPort=8301,UserIdGroupPairs='[{GroupId=sg-09145d5853dd77e97}]' 
IpProtocol=tcp,FromPort=80,ToPort=80,IpRanges='[{CidrIp=172.25.16.0/20}]' 
IpProtocol=tcp,FromPort=443,ToPort=443,IpRanges='[{CidrIp=172.25.16.0/20}]'

Then had to clean up the VPC Route table
aws ec2 --region us-east-1 create-route --route-table-id rtb-0498a437514f7b580 --destination-cidr-block 172.25.16.0/20 --vpc-peering-connection-id pcx-0bee6526bea614079

Okay We have a working example mannully done. Now time to work the automation out.

Remote Host needed These files which can be located in 
ubuntu@ip-10-0-1-26:~$ ls /opt/consul/
ca.pem  client_acl_json  client_config.json  node-id  serf
```

## :memo: License ##

This project is under license from MIT. For more details, see the [LICENSE](LICENSE.md) file.


Made with :heart: by <a href="https://github.com/{{ws-el-gato}}" target="_blank">{{jordan robison}}</a>

&#xa0;

<a href="#top">Back to top</a>
