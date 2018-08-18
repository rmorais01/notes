# Connecting Securely to Linux Instances Running in a Private Amazon VPC Subnet 

Never place your SSH private keys on the bastion instance. Instead, use SSH agent forwarding to connect 
first to the bastion and from there to other instances in private subnets. 
This approach lets you keep your SSH private key just on your computer.

## Configuring ssh-agent

To use SSH agent forwarding with EC2 instances a bastion must be configured in your VPC.

The NAT Gateway in the public subnet can act as a bastion. 

```sh
ssh-add -K myPrivateKey.pem
chmod 400 path/to/key.pem
```

Adding the key to the agent lets you use SSH to connect to an instance without having to use the –i <keyfile> option.

Verify that the keys are stored

```sh
ssh-add –L
```

## Connecting to EC2 Instances in a Private VPC Subnet

To connect to an instance in a private subnet, enter the following command to enable SSH agent forwarding using the bastion instance.

```sh
ssh –A user@<bastion-IP-address
```

After connecting to the bastion instance, use SSH to connect to a specific instance as follows

```sh
ssh user@<instance-IP-address or DNS-entry>
```

Refer: <https://aws.amazon.com/blogs/security/securely-connect-to-linux-instances-running-in-a-private-amazon-vpc/> 
