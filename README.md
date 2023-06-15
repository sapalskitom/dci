# CloudFormation Template: VPC with Auto-Scaling for a Demo Flask Web Application

This CloudFormation template creates a new Virtual Private Cloud (VPC) in AWS along with two public subnets. It also provisions an Application Load Balancer (ALB) that utilizes auto-scaling to deploy and host a Flask application using the Gunicorn service. The template returns the URL of the Flask application hosted on the ALB in the Outputs section.

## Prerequisites

- AWS account with appropriate permissions to create resources.

## Usage

1. Access the AWS Management Console.
2. Open the CloudFormation service.
3. Click on "Create stack" or "Create a new stack."
4. Select "Upload a template file" and choose this `auto-flaskwebserver.json` file.
5. Click "Next" to proceed with the stack creation.
6. Provide a stack name and configure the desired parameters.
7. Review the stack settings and click "Next."
8. On the "Configure stack options" page, you can optionally configure additional settings.
9. Click "Next" to proceed.
10. Review the stack details, and if everything looks correct, click "Create stack."
11. Wait for the stack creation to complete. This process may take a few minutes.
12. Make sure to wait until the initialization process of an EC2 instance is finished.
13. Once the stack is created successfully, navigate to the CloudFormation stack outputs.
14. Retrieve the ALB URL provided in the outputs section.
15. Access the Flask application using the ALB URL.

## CloudFormation Template Structure

The CloudFormation template consists of the following resources:

- **VPC**: A new Virtual Private Cloud is created with a CIDR block of your choice.
- **Internet Gateway**: An Internet Gateway is attached to the VPC to enable internet connectivity.
- **Public Subnets**: Two public subnets are created within the VPC, each associated with a different availability zone.
- **Route Table**: A route table is created for the subnets, with a default route to the Internet Gateway.
- **Security Groups**: Security groups are created to control inbound and outbound traffic for the EC2 instances hosting the Flask application as long as the Application Load Balancer.
- **Launch Configuration**: A launch configuration is defined to specify the instance details for the auto-scaling group.
- **Auto Scaling Group**: An auto-scaling group is created with minimum, maximum, and desired capacity parameters to manage the number of EC2 instances.
- **Application Load Balancer**: An Application Load Balancer is created and associated with the auto-scaling group to distribute incoming traffic.
- **Target Group**: A target group is created to route traffic from the ALB to the instances in the auto-scaling group.
- **Listener**: A listener is configured on the ALB to listen for incoming requests and forward them to the target group.
- **Flask Application**: A Flask application is deployed on the EC2 instances using the Gunicorn service.

## Parameters

The following parameters can be configured when creating the CloudFormation stack:

- **InstanceType**: The EC2 instance type to use for the Flask application instances. Default: `t2.small`.
- **KeyName**: The name of the existing EC2 key pair to associate with the instances for SSH access.
- **SSHLocation**: The IP address range that can be used to SSH to the EC2 instances. Default: `0.0.0.0/0`.
- **VpcCIDR**: The CIDR block for the VPC. The size used will be 'x.x.0.0/16'. Default (x.x): `10.1`.

## Outputs

The CloudFormation stack provides the following output:

- **WebsiteURL**: The URL of the Application Load Balancer where the Flask application is accessible. Navigate to the root website to see 'Hello World!' or add any text (for example Adam) to see 'Hello Adam!'
