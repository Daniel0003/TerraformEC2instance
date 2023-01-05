# LevelUp! Lab for Deploying EC2 instances using Terraform 
## Lab Overview And High Level Design

Let's start with the High Level Design.
![terrinsta](https://user-images.githubusercontent.com/46236273/210797038-e5a18e57-35f1-4985-a391-336cf1a54cbe.jpg)
Hello Everyone, and Happy 2023 to all of the techies out there!
In this blog, I will help you to create an EC2 instance using Terraform and Visual Studio Code 2022. Prior experience using an AWS account required.

## Prerequisites

- AWS Account 
- Visual Studio Code installed on your local system
- Terraform latest version installed 

### 1. Create a new project repository and install the extensions on Visual Studio Code

 - Create a new project folder named Ec2InstaTerraform on your local folder and open it using Visual studio code.
Select Extensions on the top bar and search for AWS Toolkit for Visual Studio, and install the extension. This extension will help you to connect to your AWS Account without hardcoding your credentials on your code.
- After installing the toolkit, search for Terraform and install it. Terraform extension will help you to support Terraform files. including syntax highlighting, brace completion etc.

![awstool](https://user-images.githubusercontent.com/46236273/210797291-fe628e7d-3875-41de-884a-b7722083cd6a.jpg)

### 2. Setup AWS Toolkit

- Once you install the extension, you can open it to create a new AWS profile which will grant the environment access to the AWS account. This is a new feature of AWS and Visual Studio to access your account.

![visual](https://user-images.githubusercontent.com/46236273/210797510-a40bdb55-f9db-4451-9f0a-0d548a11c929.jpg)

- Enter your access key id and secret access key of your AWS account.
- Click Ok to configure your account, and you will be seeing the list of resources available on your dashboard. (Please see the screenshot above)

### 3. Create, Validate and Deploy EC2 instance

- Create two files named ec2.tf and providers.tf under the project folder.
- Under the variables.tf file, copy and paste the following code :

```go
# Configure the AWS Provider
variable "aws" {
type    = string
default = "us-east-1"
}
```
#### Note: Make sure that the region you select here aligns with your AWS account.

On your terminal, type terraform init and press enter to execute the command. This piece of code should be run after writing a new Terraform configuration.
![terrinit](https://user-images.githubusercontent.com/46236273/210797723-28bd2812-1795-4f52-aa4b-260b027dff80.jpg)


Then, type terraform validate and press enter to execute it. This command will validate the configuration files in a directory, referring only to the configuration and not accessing any remote services such as remote state, provider APIs, etc.

Under ec2.tf file, copy and paste the following code :

```go
provider "aws" {
  region     = "us-east-1"
}

resource "aws_instance" "web" {
  ami           = " enter your ami id here " 
  instance_type = "t2.micro"

  tags = {
    Name = "NewEC2Instance"
  }
}
```

Here we have already initialized the instance type to t2.micro (free-tier) and tagged the instance with a name. Now, we need to copy the AMI id of the instance we need to deploy. For this scenario, I will be selecting Amazon linux ID: ami-0b5eea76982371e91 .
![instid](https://user-images.githubusercontent.com/46236273/210797868-86b4d76d-4081-427a-b993-d3ad6bc7abb2.jpg)

After pasting your id on the code, go to your terminal and execute this command: terraform plan. This command lets you preview the actions Terraform would take to modify your infrastructure or save a speculative plan which you can apply later.

- Once you execute the code, you will be seeing a list of actions that Terraform will perform.
- Type terraform apply and execute the command. This executes the actions proposed in a terraform plan. You will be prompted to enter a value, type YES and press enter to continue.
- Within a few seconds, your instance will be created on the AWS account. Please log in to see your instance.

![awsfinal](https://user-images.githubusercontent.com/46236273/210797922-8b712320-126c-48ba-a026-4ab913e7e24f.png)

Finally, you have created your instance using Terraform on AWS cloud, and you can use the same code to deploy multiple instances, saving your time configuring and deploying the virtual machines. This is one of the best use cases of using Terraform to automate the process and avoid human errors.








