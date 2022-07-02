# Labs for EC2

## Create an image pipeline using the EC2 Image Builder

### Workflow
* Step 1: Specify pipeline details
* Step 2: Choose recipe
* Step 3: Define infrastructure configuration - optional
* Step 4: Define distribution settings - optional
* Step 5: Review

#### Step 1: Specify pipeline details
1. Open the [EC2 Image Builder console](https://console.aws.amazon.com/imagebuilder/).
2. To begin creating your pipeline, choose **Create image pipeline**.
3. In the **General** section, enter your **Pipeline name** (required).
4. In the **Build schedule** section, you can keep the defaults for the Schedule options. Note that the **Time zone** shown for the default schedule is Universal Coordinated Time (UTC). For more information about UTC time, and to find the offset for your time zone, see Time Zone Abbreviations – Worldwide List. <br>
For **Dependency update settings**, choose the **Run pipeline at the scheduled time if there are dependency updates** option. This setting causes your pipeline to check for updates before starting the build. If there are no updates, it skips the scheduled pipeline build.
5. Choose **Next** to proceed to the next step.

#### Step 2: Choose recipe
1. Image Builder defaults to **Use existing recipe** in the **Recipe** section. For your first time through, choose the **Create new recipe** option.
2. In the **Image type** section, choose the **Amazon Machine Image (AMI)** option to create an image pipeline that will produce and distribute an AMI.
3. In the **General** section, enter the following required boxes:
    * Name – your recipe name
    * Version – your recipe version (use the format <major>.<minor>.<patch>, where major, minor, and patch are integer values). New recipes generally start with _1.0.0_.
4. In the **Source image** section, keep the default values for **Select image, Image Operating System (OS)**, and **Image origin**. This results in a list of Amazon Linux 2 AMIs, managed by Amazon, for you to choose from for your base image.
    * From the _Image name_ dropdown, choose an image.
    * Keep the default for _Auto-versioning options (Use latest available OS version)_.
5. In the **Instance configuration** section, keep the default values for the **Systems Manager agent**. This results in Image Builder keeping the Systems Manager agent after the build and tests are complete, to include the Systems Manager agent in your new image. <br>
Keep **User data** blank for this tutorial. You can use this area at other times to provide commands, or a command script to run when you launch your build instance. However, it replaces any commands that Image Builder might have added to ensure that Systems Manager is installed. When you do use it, make sure that the Systems Manager agent is preinstalled on your base image, or that you include the install in your user data.
6. In the **Components** section, you must choose at least one build component. <br>
In the **Build components – Amazon Linux** panel, you can browse through the components listed on the page. Use the pagination control in the upper right corner to navigate through additional components that are available for your base image OS. You can also search for specific components, or create your own build component using the Component manager. <br>
For this tutorial, choose a component that updates Linux with the latest security updates, as follows:
    * Filter the results by entering the word update in the search bar that's located at the top of the panel.
    * Select the check box for the update-linux build component.
    * Scroll down, and in the upper right corner of the _Selected components_ list, choose _Expand all_.
    * Keep the default for _Versioning options (Use latest available component version)_. If you had selected a component that has input parameters, you would also see the parameters in this area.
7. Choose **Next** to proceed to the next step.

#### Step 3: Define infrastructure configuration - optional
Image Builder launches EC2 instances in your account to customize images and run validation tests. The Infrastructure configuration settings specify infrastructure details for the instances that will run in your AWS account during the build process. <br>

In the **Infrastructure configuration** section, the **Configuration options** default to _Create infrastructure configuration using service defaults_. This creates an IAM role and associated instance profile for the EC2 build and test instances that are used to configure your image. <br>

For this tutorial, we are using the default settings.

* Choose **Next** to proceed to the next step.

#### Step 4: Define distribution settings - optional
Distribution configurations include the output AMI name, specific Region settings for encryption, launch permissions, and AWS accounts, organizations, and organizational units (OUs) that can launch the output AMI, and license configurations. <br>
In the **Distribution settings** section, the **Configuration options** default to _Create distribution settings using service defaults_. This option will distribute the output AMI to the current Region. <br>
For this tutorial, we are using the default settings.
* Choose **Next** to proceed to the next step.

#### Step 5: Review
The **Review** section displays all of the settings you have configured. To edit information in any given section, choose the **Edit** button located in the top right corner of the step section. For example, if you want to change your pipeline name, choose the **Edit** button in the top right corner of the **Step 1: Pipeline details** section.
1. When you have reviewed your settings, choose **Create pipeline** to create your pipeline.
2. You can see success or failure messages at the top of the page, as your resources are created for distribution settings, infrastructure configuration, your new recipe, and the pipeline. To see details for a resource, including the resource identifier, choose **View details**.
3. After you have viewed the details for a resource, you can view details about other resources by choosing the resource type from the navigation pane. For example, to see details for your new pipeline, choose **Image pipelines** from the navigation pane. If your build was successful, your new pipeline is displayed in the **Image pipelines** list.