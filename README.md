# aws-ssh-ssm-script

## ** Please note that this script is currently BETA **
Please submit a and issue/pull requests with any suggestions.
TODO:
*Add support for Public IPs (via DNS entry)
*Add support for IPs or instance ids (i-abc123)
*Improve error handling

The purpose of this script is to server as a unified way to SSH OR SSM (start-session) into an EC2 instance using a Private Hosted Zone in Route 53 for DNS lookups. 

https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html


#### Prerequisites
Installation of the AWS Command Line Interface
```
pip install aws-cli
```

Installation of the session-manager-plugin:
https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html

Updated ~/.ssh/config file to use SSM as a proxy:
https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-getting-started-enable-ssh-connections.html





