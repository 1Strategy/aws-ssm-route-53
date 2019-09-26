# aws-ssh-ssm-script

## ** Please note that this script is currently BETA **
Please submit an issue/pull request with any suggestions.

TODO:
* Add support for Public IPs (via DNS entry)
* Add support for IPs
* Improve error handling

------

The purpose of this script is to serve as a unified way to SSH OR SSM (start-session) into an EC2 instance using a Private Hosted Zone in Route 53 for DNS lookups. 

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
* `chmod +x ssh-into` to allow it to execute
* Copy the `ssh-into` to your /usr/local/bin/ or otherwise add it to your `PATH`

### Optional - Add to AWS CLI

Add the following block to `~/.aws/cli/alias`
```ssh-into = 
  !f() {
    bash <path/to/ssh-into/installtion/location> $@
  }; f
```
## Usage

```
aws ssh-into  [ssh-user@]<server>.<domain>.com
              [-i | --identity-file] <path/to/pem/file>
              [-p | --profile] <aws-cli-profile-name>

aws ssh-into  [ssh-user@]i-instanceid
              [-i | --identity-file] <path/to/pem/file>
              [-p | --profile] <aws-cli-profile-name>
```


### Examples:
* `ssh-into www.1strategy-sandbox.com` -> Access instance using session manager
* `ssh-into ec2-user@www.1strategy-sandbox.com` -> Access instance private ip using SSH and the default ssh key `~/.ssh/id_rsa`
* `ssh-into ec2-user@www.1strategy-sandbox.com -i ~/.ssh/1strategy.pem` -> Access instance private ip using SSH and `1strategy.pem` ssh key.
* `ssh-into i-a47461d858527dd824` -> Access instance using session manager
* `ssh-into ec2-user@i-a47461d858527dd824` -> Access instance private ip using SSH and the default ssh key `~/.ssh/id_rsa`
* `ssh-into ec2-user@i-a47461d858527dd824 -i ~/.ssh/1strategy.pem` -> Access instance private ip using SSH and `1strategy.pem` ssh key.


