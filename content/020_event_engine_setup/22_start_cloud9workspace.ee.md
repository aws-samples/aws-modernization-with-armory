---
title: "Create a Workspace"
chapter: false
weight: 10
---

You have a choice to use your own IDE and SSH client, or follow steps to setup Cloud9 cloud IDE to run this module steps.

[AWS Cloud9](https://aws.amazon.com/cloud9/) is a cloud-based integrated development environment (IDE) that lets you write, run, and debug your code with just a browser. It includes a code editor, debugger, and terminal. Cloud9 comes prepackaged with essential tools for popular programming languages, including JavaScript, Python, PHP, and more, so you don’t need to install files or configure your laptop for this workshop.

We will use Amazon Cloud9 to modify Armory configuration, and deploy it via SSH connection to the Bastion host. There are a few steps to complete to set this up

### How to access pre-deployed Cloud9 environment (AWS events)

If you are attending AWS event, you can just navigate to [Cloud9 environments](https://us-east-2.console.aws.amazon.com/cloud9/home) and use pre-deployed *armory-workshop* environment. Select the environment and click *Open IDE*.

### How to create a new Cloud9 IDE environment in your AWS account (Self-guided)

1. Within the AWS console, use the region drop list to select **us-east-2**.  This will ensure the workshop script provisions the resources in this same region.
1. Navigate to the [Cloud9 console](https://console.aws.amazon.com/cloud9/home) or just search for it under the **AWS console services** menu.
1. Click the **Create environment** button
1. For the name use `armory-workshop`, then click **Next step**
1. Select the default instance type **t2.micro**
1. Leave all the other settings as default and click **Next step** followed by **Create environment**

{{% notice info %}}
This will take about 1-2 minutes to provision
{{% /notice %}}

### Configure Cloud9 IDE environment

When the environment comes up, customize the environment by:

1. Close the **welcome page** tab
1. Close the **lower work area** tab
1. Open a new **terminal** tab in the main work area.

{{% notice tip %}}
If you don't like this dark theme, you can change it from the **View / Themes** Cloud9 workspace menu.
{{% /notice %}}

{{% notice tip %}}
Cloud9 requires third-party-cookies. You can whitelist the [specific domains](https://docs.aws.amazon.com/cloud9/latest/user-guide/troubleshooting.html#troubleshooting-env-loading).  You are having issues with this, Ad blockers, javascript disablers, and tracking blockers should be disabled for the cloud9 domain, or connecting to the workspace might be impacted.
{{% /notice %}}

### Setup Access to GitHub in Cloud9 Environment

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
    1. Add a title (for example *Armory workshop Cloud9 environment*)
    1. Paste the public key text from above into the **Key** section
    1. Click **Add SSH key**

3. Start the SSH agent in your Cloud9 environment if it's not already running, and add your new private SSH key to its registry. Enter the passphrase you used when creating the key when asked.
    ```sh
    eval $(ssh-agent -s) && \
    ssh-add /home/ec2-user/.ssh/id_rsa
    ```

