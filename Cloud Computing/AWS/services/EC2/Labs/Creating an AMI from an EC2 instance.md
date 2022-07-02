# Labs for EC2

## Creating an AMI from an EC2 instance

### Intent:
* Creating a custom AMI from a EC2 Instance
* Creating a new EC2 instance from the custom AMI

### Assumption:
* An EC2 instance with the required software has been created

### Steps:
* Using the AWS console:
    1. Right click on the instance ID of the instance from which image has to be created.
    2. Go to **Images and Templates** and click on **Create image**
    3. Enter the name of the image, configure the volumes if needed, add tags if required and then click **Create image**
    4. In the side panel, under the **Images** section, select **AMI** and wait until the status show **Available**
    5. Once the AMI is available, create a new instance using the same steps above but using the recently created AMI.