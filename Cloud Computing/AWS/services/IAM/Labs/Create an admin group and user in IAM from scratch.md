# Labs for IAM

## Create an admin group and user in IAM from scratch <br>

### Intent:
* Creating a user
* Creating an admin group and assigning appropriate policies
* Adding the above created user to the admin group

### Steps: <br>
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