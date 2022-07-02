# Labs for EC2

## Creating an EBS volume and attaching it to an instance
* Steps:
    * Using AWS Console:
        1. In the AWS Management Console, choose Services, and search for and open **EC2**.
        2. On the EC2 dashborad, click on _Volumes_.
        3. Click on _Create Volume_.
        4. Select the volume type of your choice from the dropdown.
        5. Enter the size of the volume you want to create
        6. Select the Availability Zone from the dropdown
        7. Optional — If you want to creat a volume from a snapshot, select the snapshot from the dropdown
        8. Optional — Check the box if you want to enable encryption
        9. Optional — Add tags to the volume
        10. Click on **Create Volume**
        11. Wait for the volume to get created. Once done, select the volume to attach and choose **Actions**, **Attach volume**.
        12. For **Instance**, enter the ID of the instance or select the instance from the list of options.
        13. For **Device name**, enter a supported device name for the volume. This device name is used by Amazon EC2. The block device driver for the instance might assign a different device name when mounting the volume. For more information, see [Device names on Linux instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/device_naming.html).
        14. Choose **Attach volume**.
        15. Connect to the instance and mount the volume. For more information, see [Make an Amazon EBS volume available for use on Linux](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-using-volumes.html).