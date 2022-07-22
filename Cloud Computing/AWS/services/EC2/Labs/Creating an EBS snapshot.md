# Labs for EC2

## Creating an EBS snapshot
* Steps:
    * Using the AWS console:
        1. Open the [Amazon EC2 console](https://console.aws.amazon.com/ec2/).
        2. In the navigation pane, choose **Snapshots**, **Create snapshot**.
        3. For **Resource type**, choose **Volume**.
        3. For **Volume ID**, select the volume from which to create the snapshot.
        The **Encryption** field indicates the selected volume's encryption status. If the selected volume is encrypted, the snapshot is automatically encrypted using the same KMS key. If the selected volume is unencrypted, the snapshot is not encrypted.
        4. (Optional) For **Description**, enter a brief description for the snapshot.
        5. (Optional) To assign custom tags to the snapshot, in the **Tags** section, choose **Add tag**, and then enter the key-value pair. You can add up to 50 tags.
        6. Choose **Create snapshot**