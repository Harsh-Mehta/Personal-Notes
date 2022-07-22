# Labs for EC2
## Create an EC2 Instance with EC2 User Data to have a Website
### Intent:
* Creating an EC2 Instance
* Understanding bootstraping scripts in EC2
### Steps:
* Using the AWS console:
    1. In the AWS Management Console, choose Services, and search for and open **EC2**.
    2. On the EC2 dashborad, click on _Instances_.
    3. Click on _Launch instances_.
    4. Enter the name of your instance in the **Name** field which add a tag with key as _Name_ and value as the name of the instance mentioned.
    5. Select the OS and the architecture for the EC2 instance.
    6. Select the type of the instance depending on the workload requirements.
    7. Next, either an existing key pair can be used or a new key pair can be generated. This is done in order to login into that EC2 instance.
    8. Then comes the security group, in this, either a new group with the inbound/outbound rules can be created or an existing group can be used.
    9. Next comes the storage configuration, where the storage capacity, volume type, encryption and deletion can be configured.
    10. After configuring the storage, click on **Advance Details** and search for the **User Data** textarea and enter the commands that should be run at the first boot of the instance.
    11. Review the summary, and then click on **Launch instance**.