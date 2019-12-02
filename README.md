# aws-ssm-route-53

### ** Please note that these scripts are currently BETA **
Please submit an issue/pull request with any suggestions.

------

The purpose of this group of utilities is decrease the friction of switching from SSH to SSM.
- `ssh-into` connects to an instance over SSM either directly or by using ssh over SSM.
- `pforward` forwards a port over SSM, providing functionality similar to the -D flag for ssh.

Instance IDs are supported, but if hostnames are provided then DNS lookups are performed using a Private Hosted Zone in Route 53.

https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html

#### Prerequisites
* Installation of the AWS Command Line Interface
```
  pip install awscli
```
* Installation of the session-manager-plugin:  
  https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html
* Updated ~/.ssh/config file to use SSM as a proxy:  
  https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-getting-started-enable-ssh-connections.html
* IAM permissions to access SSM session manager
* A Route 53 Hosted Zone with Private Ips

## Installation
* Clone the repo locally
* `chmod u+x ssh-into pforward` to grant execution privileges
* `cp {ssh-into,pforward} /usr/local/bin/` or otherwise add them to your `PATH`

### Optional - Add to AWS CLI

Add the following block to `~/.aws/cli/alias`
```ssh-into = 
  !f() {
    bash <path/to/ssh-into/installtion/location> $@
  }; f
```
## Usage
### ssh-into
```
Usage: ssh-into [user@]<destination> [options...]
Destination: Either a hostname (server.env) or an instance-id

Optional Arguments:
 -i, --identity_file      Identity file (~/.ssh/id_rsa)
 -p, --profile            AWS Profile (default)
 -h, --help               Displays this help text
```
#### Examples:
* `ssh-into www.1strategy-sandbox.com` -> Access instance using session manager
* `ssh-into ec2-user@www.1strategy-sandbox.com` -> Access instance private ip using SSH and the default ssh key `~/.ssh/id_rsa`
* `ssh-into ec2-user@www.1strategy-sandbox.com -i ~/.ssh/1strategy.pem` -> Access instance private ip using SSH and `1strategy.pem` ssh key.
* `ssh-into i-a47461d858527dd824` -> Access instance using session manager
* `ssh-into ec2-user@i-a47461d858527dd824` -> Access instance private ip using SSH and the default ssh key `~/.ssh/id_rsa`
* `ssh-into ec2-user@i-a47461d858527dd824 -i ~/.ssh/1strategy.pem` -> Access instance private ip using SSH and `1strategy.pem` ssh key.
### pforward
```
Usage: pforward <destination> [options...]
Destination: Either a hostname (server.env) or an instance-id

Required arguments:
 -r, --remote       Remote port
 -l, --local        Local port

Optional Arguments:
 -p, --profile      AWS Profile (default)
 -h, --help         Displays this help text
```
#### Examples:
* `pforward www.1strategy-sandbox.com -l 9999 -r 80` -> Access the remote server's web traffic on `localhost:9999`
* `pforward i-a47461d858527dd824 -r 80 -l 9999` -> Access the remote server's web traffic on `localhost:9999`

-----

TODO:
* Add support for Public IPs (via DNS entry)
* Add support for IPs
