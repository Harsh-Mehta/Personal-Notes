# Labs for ASG

## Creating an Auto Scaling Group for AWS EC2

### Tasks
* Step 1: Create a launch template
* Step 2: Create a single-instance Auto Scaling group
* Step 3: Verify your Auto Scaling group

#### Step 1: Create a launch template
1. Open the [Launch templates page](https://console.aws.amazon.com/ec2/v2/#LaunchTemplates) of the Amazon EC2 console.
2. On the navigation bar at the top of the screen, select an AWS Region. The launch template and Auto Scaling group that you create are tied to the Region that you specify.
3. Choose **Create launch template**.
4. For **Launch template name**, enter a name name you like.
5. Under **Auto Scaling guidance**, select the check box.
6. For **Application and OS Images (Amazon Machine Image)**, choose a version of Amazon Linux 2 (HVM) from the **Quick Start** list. The AMI serves as a basic configuration template for your instances.
7. For **Instance type**, choose a hardware configuration that is compatible with the AMI that you specified.
8. (Optional) For **Key pair (login)**, choose an existing key pair. You use key pairs to connect to an Amazon EC2 instance with SSH. Connecting to an instance is not included as part of this tutorial. Therefore, you don't need to specify a key pair unless you intend to connect to your instance using SSH.
9. For **Network settings, Security groups**, choose a security group in the same VPC that you plan to use as the VPC for your Auto Scaling group. If you don't specify a security group, your instance is automatically associated with the default security group for the VPC.
10. You can leave **Advanced network configuration** empty. Leaving the setting empty creates a primary network interface with IP addresses that we select for your instance based on the subnet to which the network interface is established. If instead you choose to configure a network interface, the security group must be a part of it.
11. Choose **Create launch template**.
12. On the confirmation page, choose **Create Auto Scaling group**.

#### Step 2: Create a single-instance Auto Scaling group
1. On the **Choose launch template or configuration** page, for **Auto Scaling group name**, enter any name you like.
2. Choose **Next**. <br>
The **Choose instance launch options** page appears, allowing you to choose the VPC network settings you want the Auto Scaling group to use and giving you options for launching On-Demand and Spot Instances (if you chose a launch template).
3. In the **Network** section, keep **VPC** set to the default VPC for your chosen AWS Region, or select your own VPC. The default VPC is automatically configured to provide internet connectivity to your instance. This VPC includes a public subnet in each Availability Zone in the Region.
4. For **Availability Zones and subnets**, choose a subnet from each Availability Zone that you want to include. Use subnets in multiple Availability Zones for high availability.
5. [Launch template only] In the **Instance type requirements** section, use the default setting to simplify this step. (Do not override the launch template.) For this tutorial, you will launch only one On-Demand Instance using the instance type specified in your launch template.
6. Keep the rest of the defaults for this tutorial and choose **Skip to review**.
7. On the **Review** page, review the information for the group, and then choose **Create Auto Scaling group**.

#### Step 3: Verify your Auto Scaling group
1. Open the [Auto Scaling groups page](https://console.aws.amazon.com/ec2/v2/home?#AutoScalingGroups) of the Amazon EC2 console.
2. Select the check box next to the Auto Scaling group that you just created. <br>
A split pane opens up in the bottom of the **Auto Scaling groups** page. The first tab available is the **Details** tab, showing information about the Auto Scaling group.
3. Choose the second tab, **Activity**. Under **Activity history**, you can view the progress of activities that are associated with the Auto Scaling group. The **Status** column shows the current status of your instance. While your instance is launching, the status column shows ```PreInService```. The status changes to ```Successful``` after the instance is launched. You can also use the refresh button to see the current status of your instance.
4. On the **Instance management** tab, under **Instances**, you can view the status of the instance.
5. Verify that your instance launched successfully. It takes a short time for an instance to launch.
    * The _Lifecycle_ column shows the state of your instance. Initially, your instance is in the ```Pending``` state. After an instance is ready to receive traffic, its state is ```InService```.
    * The _Health status_ column shows the result of the EC2 instance health check on your instance.