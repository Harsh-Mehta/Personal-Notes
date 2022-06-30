# Labs for IAM
* Create an admin group and user in IAM from scratch <br>
    * Intent: <br> 
        * Creating a user
        * Creating an admin group and assigning appropriate policies
        * Adding the above created user to the admin group
    * Steps: <br>
        * Using AWS console:
            1. In the AWS Management Console, choose **Services**, and search for and open **IAM**
            2. In the navigation pane, choose **Users** and then choose **Add users**
            3. Enter the user name and in the **User name** field and check **Password - AWS Management Console access**
            4. Select **Custom Password** and enter the password in the text field
            5. Uncheck the checkbox in the **Require password reset** section
            6. Choose **Next: Permissions**
            7. Choose **Create group**
            8. Enter the group name
            9. From the policies section, check the **AdministratorAccess** policy
            10. Choose **Create group**
            11. Choose **Next: Tags**
            12. In the **Key** field, enter *Department* and in the **Value** field enter *Engineering*. This step is optional
            13. Choose **Next: Review**
            14. Choose **Create user**
            15. You can choose to create an account alias for this user by clicking on edit in **AWS Account > Account Alias** section and enter the alias. This alias can be used when logging into the console. This step is optional.
* Create a policy in IAM from scratch <br>
    * Intent: Creating an IAM policy from scratch using visual editor
    * Steps: <br>
        * Using AWS console:
            1. In the AWS Management Console, choose **Services**, and search for and open **IAM**
            2. In the navigation pane, choose **Policies** and then choose **Create policy**
            3. There are 2 methods to create an IAM policy: using plain JSON, using Visual Editor
            4. Under the **Visual Editor** section, select *Choose a service* and select the service(s)
            5. Select the actions that you need. In order for specific actions, search for the action using the given search box
            6. Choose the best option as per requirement.
            11. Choose **Next: Tags**
            12. Enter the key-value paires should you like or you can ignore it too.
            13. Choose **Next: Review**
            14. Enter the name of the policy in the **Name** field
            14. Choose **Create policy**
* To create access keys for an IAM user:
    1. Sign in to the AWS Management Console and open the IAM console at https://console.aws.amazon.com/iam/.
    2. In the navigation pane, choose **Users**.
    3. Choose the name of the user whose access keys you want to create, and then choose the **Security credentials** tab.
    4. In the **Access keys** section, choose **Create access** key.
    5. To view the new access key pair, choose **Show**. You will not have access to the secret access key again after this dialog box closes. Your credentials will look something like this:
        * Access key ID: AKIAIOSFODNN7EXAMPLE
        * Secret access key: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
    6. To download the key pair, choose **Download .csv file**. Store the keys in a secure location. You will not have access to the secret access key again after this dialog box closes. <br>
    Keep the keys confidential in order to protect your AWS account and never email them. Do not share them outside your organization, even if an inquiry appears to come from AWS or Amazon.com. No one who legitimately represents Amazon will ever ask you for your secret key.
    7. After you download the _.csv_ file, choose **Close**. When you create an access key, the key pair is active by default, and you can use the pair right away.
