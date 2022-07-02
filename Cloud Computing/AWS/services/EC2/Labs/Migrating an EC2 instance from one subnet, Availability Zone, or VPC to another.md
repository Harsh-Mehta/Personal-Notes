# Labs for EC2

## Migrating an EC2 instance from one subnet, Availability Zone, or VPC to another

### Intent:
* It's not possible to move an existing instance to another subnet, Availability Zone, or VPC. Instead, you can manually migrate the instance by creating a new Amazon Machine Image (AMI) from the source instance. Then, launch a new instance using the new AMI in the desired subnet, Availability Zone, or VPC. Finally, you can reassign any Elastic IP addresses from the source instance to the new instance.

* There are two methods for migrating the instance:
    * Use the AWS Systems Manager automation document _AWSSupport-CopyEC2Instance_.
    * Manually copy an instance and a launch a new instance from the copy.

### Notes before you begin:
* AMIs are based on Amazon Elastic Block Store (Amazon EBS) snapshots. For large file systems without a previous snapshot, AMI creation can take several hours. To decrease the AMI creation time, create an Amazon EBS snapshot before you create the AMI.
* Creating an AMI doesn't create a snapshot for instance store volumes on the instance.
* The new EC2 instance has a different private IPv4 or public IPv6 IP address. You must update all references to the old IP addresses (for example, in DNS entries) with the new IP addresses that are assigned to the new instance. If you're using an Elastic IP address on your source instance, be sure to attach it to the new instance
* Domain security identifier (SID) conflict issues can occur when the copy launches and tries to contact the domain. Before you capture the AMI, use Sysprep or remove the domain-joined instance from the domain to prevent conflict issues.

### Methods:
1. Use the AWS System Manager automation runbook AWSSupport-CopyEC2Instance
    * You can use the AWS Systems Manager Automation runbook [AWSSupport-CopyEC2Instance](https://console.aws.amazon.com/systems-manager/automation/execute/AWSSupport-CopyEC2Instance) to complete the following tasks automatically:
        * Create a new image
        * Launch a new instance
    
    * After these procedures complete, follow the instructions in _Reassign the Elastic IP address_ section, if needed.
    
    * To run the automation, do the following:
    
        1. Open the [AWSSupport-CopyEC2Instance](https://console.aws.amazon.com/systems-manager/automation/execute/AWSSupport-CopyEC2Instance) runbook.
            
            **Note: Make sure that you're in the same Region as the instance that you want to copy.**
        2. For **Execute automation document**, choose **Simple execution**.
        3. For **Input parameters**, enter the **InstanceID** of the EC2 instance you want to copy. If you use the Interactive instance picker, then make sure that you select **Show all instances** from the dropdown list.
        4. Provide the destination **Region** and/or the **SubnetID** where you want to copy the instance to.
        5. Complete any of the additional optional fields that are required for your use case, and then select **Execute**.
        6. To monitor the execution progress, open the Systems Manger console, and then choose **Automation** from the navigation pane. Choose the running automation, and then review the **Executed steps**. To view the automation output, expand **Outputs**.
2. Manually copy the instance and launch a new instance from the copy
    * Create a new image
        1. Open the Amazon EC2 console, and then choose **Instances** from the left navigation pane.
        2. Select the instance that you want to move, and then choose **Actions, Instance State, Stop**. This makes sure that the data is consistent between the old and new EBS volumes. <br>
        **Note:** You can skip this step if you're testing this procedure or if you don't want to stop or reboot your instance.
        3. Choose **Actions, Image, Create Image**. <br>
        For **Image name**, enter a name for the image. <br>
        For **Image description**, enter a description of the image. <br>
        **Note:** If you select **No reboot** on the **Create Image** page, then the file system integrity of the image can't be guaranteed.
        4. Choose **Create Image**.
        5. Under **Create Image request received**, choose **View pending image [ID]**. Wait for the **Status** to change from **pending** to **available**. <br>
        **Note:** You can also view pending images by choosing **AMIs** from the **Images** section of the navigation pane.
    * Launch a new instance
        1. Select the new AMI, and then choose **Launch**.
        2. Choose the same instance type as the instance that you want to move, and then choose **Next: Configure Instance** Details. <br>
        For **Network**, choose your VPC. <br>
        For **Subnet**, choose the subnet where you want to launch the new instance. <br>
        If the instance is a production instance, then for **Enable termination** protection, choose **Protect against accidental termination**.
        3. Choose **Next: Add Storage**.
        4. Accept the defaults, and then choose **Next: Add Tags**. <br>
        For **Key**, enter **Name**. <br>
        For **Value**, enter your instance name.
        5. Choose **Next: Configure Security Group**.
        6. Choose the same security group that's applied to the instance that you're moving. <br>
        **Note:** If you're moving your instance between VPCs, you must create a new security group on the destination VPC.
        7. Choose **Review and Launch**.
        8. Choose **Launch**.
        9. For **Select a key pair**, choose your key pair from the drop-down menu.
        10. Select the agreement check box, and then choose **Launch Instances**.
        11. Choose the instance ID to return to the EC2 console.

### Reassign the Elastic IP address
To reassign the Elastic IP address, you must first disassociate the Elastic IP address from the source instance. Then, you can reassociate the Elastic IP address with the new instance. For instructions, see Disassociate an [Elastic IP address](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html#using-instance-addressing-eips-associating-different).

Note: Elastic IP addresses can be used in only one Region. If you move an instance to a different Region, you can't use the same Elastic IP address.