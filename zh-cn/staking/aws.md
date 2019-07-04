# Getting Started With AWS

## Create an AWS Account

AWS (Amazon Cloud) account creation
Prerequisites:
- Credit card
- Landline or mobile phone

* Navigate to the [AWS official website](https://aws.amazon.com/) and click the “Sign Up” button.
* Fill in all registration information including your personal information and credit card details.
* Next, the system will call to confirm your phone number. Enter the 4-digit number (ending with #) displayed on the computer screen.
* If the account was successfully created, your card will be charged for $1 as part of the verification process (this will be refunded later).

## Create a Suitable EC2 Virtual Machine

EC2 virtual machine set up
##### 1. Create an AWS EC2 instance

Log in to the [EC2 console](https://console.aws.amazon.com/ec2/):

Select the location of the machine in the upper right corner:

![](media/staking1.png)

Find “Instances” in the menu on the left side of the page

![](media/staking2.png)

Then click on the “Launch Instance” button:

![](media/staking3.png)

Choose an Amazon system image: Ubuntu 18.04 is recommended

![](media/staking4.png)

Select the instance type. We recommend the m4.large configuration.

![](media/staking5.png)

Click the “Next: Configure Instance Details” button and input the following default configuration:

![](media/staking6.png)

Click the “Next: Add Storage” button

The recommended setting is 80GB

![](media/staking7.png)


Click the “Next: Add Tags” button to add tags for easy recall:

![](media/staking8.png)

Click the “Next: Configure Security Group” button

Add firewall rule and then click the “Review and Launch” button to verify the instance:

![](media/staking9.png)

Click the “Launch” button to launch the instance

![](media/staking10.png)

Create a key, download the key pair and keep it safe. Use it when logging in by SSH.

![](media/staking11.png)

That completes the EC2 instance creation.

## SSH login to AWS EC2

To use the SSH login method under Linux, set the key file permissions with the following command:

```  
Chmod 400 aws.pem  
```
SSH login command:
```
Ssh -i aws.pem root@public DNS (IPv4)
```
The PuTTy login on Windows needs to use PuTTyGen to convert .pem to ppk, and select ppk file in Auth option of PuTTy tool.

Delete AWS EC2 instance

First terminate the instance:

![](media/staking12.png)

Confirm termination:

![](media/staking13.png)


After termination, check that the volume has been deleted to avoid any costs. In addition, the instance will remain in the list for a while after termination, and will generally disappear within half an hour.
