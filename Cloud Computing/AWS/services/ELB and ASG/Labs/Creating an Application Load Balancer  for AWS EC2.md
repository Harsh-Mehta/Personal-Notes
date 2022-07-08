# Labs for ELB

## Creating an Application Load Balancer for AWS EC2

### Tasks
* Before you begin
* Step 1: Configure your target group
* Step 2: Choose a load balancer type
* Step 3: Configure your load balancer and listener
* Step 4: Test your load balancer

#### Before you begin
* Decide which two Availability Zones you will use for your EC2 instances. Configure your virtual private cloud (VPC) with at least one public subnet in each of these Availability Zones. These public subnets are used to configure the load balancer. You can launch your EC2 instances in other subnets of these Availability Zones instead.
* Launch at least one EC2 instance in each Availability Zone. Be sure to install a web server, such as Apache or Internet Information Services (IIS), on each EC2 instance. Ensure that the security groups for these instances allow HTTP access on port 80.

#### Step 1: Configure your target group
1. Open the [Amazon EC2 console](https://console.aws.amazon.com/ec2/).
2. In the navigation pane, under Load Balancing, choose Target Groups.
3. Choose Create target group.
4. Under Basic configuration, keep the Target type as instance.
5. For Target group name, enter a name for the new target group.
6. Keep the default protocol (HTTP) and port (80).
7. Select the VPC containing your instances. Keep the protocol version as HTTP1.
8. For Health checks, keep the default settings.
9. Choose Next.
10. On the Register targets page, complete the following steps. This is an optional step for creating the load balancer. However, you must register this target if you want to test your load balancer and ensure that it is routing traffic to this target.
11. For Available instances, select one or more instances.
12. Keep the default port 80, and choose Include as pending below.
13. Choose Create target group.

#### Step 3: Configure your load balancer and listener
1. For Load balancer name, enter a name for your load balancer. For example, my-alb.
2. For Scheme and IP address type, keep the default values.
3. For Network mapping, select the VPC that you used for your EC2 instances. Select at least two Availability Zones and one subnet per zone. For each Availability Zone that you used to launch your EC2 instances, select the Availability Zone and then select one public subnet for that Availability Zone.
4. For Security groups, keep the default. This is the default security group that the console creates for the load balancer on your behalf. It includes rules that allow it to communicate with registered targets on both the listener port and the health check port.
5. For Listeners and routing, keep the default protocol and port, and select your target group from the list. This configures a listener that accepts HTTP traffic on port 80 and forwards traffic to the selected target group by default. For this tutorial, you are not creating an HTTPS listener.
6. For Default action, select the target group that you created and registered in Step 1: Configure your target group.
7. (Optional) Add a tag to categorize your load balancer. Tag keys must be unique for each load balancer. Allowed characters are letters, spaces, numbers (in UTF-8), and the following special characters: + - = . _ : / @. Do not use leading or trailing spaces. Tag values are case-sensitive.
8. Review your configuration, and choose Create load balancer. A few default attributes are applied to your load balancer during creation. You can view and edit them after creating the load balancer.

#### Step 4: Test your load balancer
1. After you are notified that your load balancer was created successfully, choose Close.
2. In the navigation pane, under Load Balancing, choose Target Groups.
3. Select the newly created target group.
4. Choose Targets and verify that your instances are ready. If the status of an instance is initial, it's probably because the instance is still in the process of being registered, or it has not passed the minimum number of health checks to be considered healthy. After the status of at least one instance is healthy, you can test your load balancer.
5. In the navigation pane, under Load Balancing, choose Load Balancers.
6. Select the newly created load balancer.
7. Choose Description and copy the DNS name of the load balancer (for example, my-load-balancer-1234567890abcdef.elb.us-east-2.amazonaws.com). Paste the DNS name into the address field of an internet-connected web browser. If everything is working, the browser displays the default page of your server.
8. (Optional) To define additional listener rules.