---
title: "SSH into the Bastion Host"
chapter: false
weight: 20
---

Navigate to [EC2 Dashboard](https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-2#Instances:) and find *EKSBastion* EC2 instance. Click on *Instance ID* link, and find *Public IPv4 address* field. Copy IP address (and keep it nearby or EC2 instance page open) for SSH connection.

### SSH via AWS Management Console

Select EKSBastion and click *Connect*
![Connect to EKSBastion](/images/setup/connect_to_eksbastion.png)

#### Setup Access to GitHub using SSH

1. Generate an SSH key pair and display the public key to be copied to GitHub. Leave the default file name by pressing enter when asked for a file to save the key, and enter a passphrase of your choice (twice to confirm). You will see the key starting from "ssh-rsa"
    ```sh
    ssh-keygen -t rsa && \
    cat /home/ec2-user/.ssh/id_rsa.pub
    ```
You will see your new public SSH key printed to the terminal like the following:
<pre>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDAnxipo/s/uvxguhwfTbNCM+iWoPa+gpQV7wKlOo5cZ+VUpekodpaiFV/QB3jq41qrZfdvAYqapJN1YZOeCkY90T3kNgLvpGNOuqOB95sLKlBCni568l9qYi/eDm/gTpGxiNwtI9muqzfRSPPTvKQLkTM49oTLjsGAWE4IaZ5YtmZkyUMDTMcjDvKSO6FtvzBhNwS6mEZ5A5P1IVYy1TdKXIXHHo5bUScddM5vyiAWjAgT5R0TwOXGEgX5HA9GkG957kP0TZfAxS2pc6C5GKBhaTpcAaz64zUpT03b28gNgw0lWbB5eqZBt1oqZRVASdU3xOmjzDRIBMF/IkU3kHkj ec2-user@ip-172-38-0-139</pre>
Select and copy all the printed text of the key.

2. Create a new SSH key authorization in GitHub:
    1. Go to your GitHub account [keys](https://github.com/settings/keys)
    1. Click **New SSH Key**
    1. Add a title (for example *Armory workshop EKSBastion*)
    1. Paste the public key text from above into the **Key** section
    1. Click **Add SSH key**

3. Start the SSH agent in your environment if it's not already running, and add your new private SSH key to its registry. Enter the passphrase you used when creating the key when asked.
    ```sh
    eval $(ssh-agent -s) && \
    ssh-add /home/ec2-user/.ssh/id_rsa
    ```
   
### VSCode Remote SSH Plugin

https://code.visualstudio.com/docs/remote/ssh

https://code.visualstudio.com/blogs/2019/07/25/remote-ssh

```
    vi ~/.ssh/config
```

```
    Host <PublicBastionIP>
      HostName EKSBastion
      IdentityFile ~/.ssh/<youkeyfilename>.pem
      User ec2-user
```