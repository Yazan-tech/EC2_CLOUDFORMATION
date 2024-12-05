# 🚀 **AWS EC2 CloudFormation Template**  

This CloudFormation template simplifies the deployment of a **Linux-based Amazon EC2 instance** with robust configurations. It includes security measures and automation, making it ideal for hosting web applications or experimenting with AWS infrastructure.

---

## 🌟 **Features**

- **Amazon EC2 Instance**: Deploys a Linux virtual machine using the latest Amazon Linux 2 AMI.
- **Customizable Parameters**:
  - VPC and Subnet Selection.
  - Instance Type (default: `t2.micro`).
  - Key Pair for SSH access.
  - Configurable SSH access IP range.
- **Security Group**:
  - Enables **SSH (port 22)** and **HTTP (port 80)** traffic.
- **Automated Setup**:
  - Installs and configures **Apache HTTP Server** automatically via user data scripts.
- **Dynamic AMI Management**:
  - Fetches the latest Amazon Linux 2 AMI using AWS Systems Manager (SSM) Parameter Store.
  
---

## 🔧 **Usage**

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/Yazan-tech/EC2_CLOUDFORMATION.git
   cd EC2_CLOUDFORMATION
   ```

2. **Deploy the Stack**:
   Use the AWS Management Console or AWS CLI to deploy:
   ```bash
   aws cloudformation create-stack --stack-name MyEC2Stack \
     --template-body file://template.yaml \
     --parameters ParameterKey=KeyName,ParameterValue=YourKeyName \
                  ParameterKey=VpcId,ParameterValue=YourVpcId \
                  ParameterKey=SubnetId1,ParameterValue=YourSubnetId \
     --capabilities CAPABILITY_NAMED_IAM
   ```

3. **Access the Instance**:
   - Retrieve the **Public IP** from CloudFormation Outputs.
   - SSH into the instance:
     ```bash
     ssh -i YourKey.pem ec2-user@<PublicIP>
     ```
   - Open your browser and navigate to `http://<PublicIP>` to verify the Apache server is running.

---

## 📋 **Parameters**

| Parameter        | Description                                                | Default       |
|------------------|------------------------------------------------------------|---------------|
| **VpcId**        | The ID of the VPC where the instance will be launched.      | *(Required)*  |
| **SubnetId1**    | The ID of the subnet for the instance.                      | `subnet-0af28a919a3624ec7` |
| **KeyName**      | Key pair for SSH access.                                    | *(Required)*  |
| **InstanceType** | Instance type for the EC2 (supports t2.micro).              | `t2.micro`    |
| **SSHLocation**  | Allowed IP CIDR for SSH access.                             | `0.0.0.0/0`   |
| **LatestAmiId**  | Latest Amazon Linux 2 AMI ID via SSM Parameter Store.       | Predefined    |

---

## 🖼️ **Outputs**

- **InstanceId**: The unique identifier of the EC2 instance.
- **Availability Zone**: The zone where the instance is deployed.
- **Public DNS**: The public DNS name for the instance.
- **Public IP**: The instance's public IP address.

---

## 🤝 **Contributing**

Feel free to fork this repository, make enhancements, and submit pull requests. Your contributions are always welcome!

---

## 📜 **License**

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---
