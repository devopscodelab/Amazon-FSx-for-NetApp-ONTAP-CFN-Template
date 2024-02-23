# Amazon FSx for NetApp ONTAP CloudFormation Template

This CloudFormation template deploys an Amazon FSx for NetApp ONTAP (FSxN) file system into private subnets across separate Availability Zones inside a VPC, ensuring high availability and resilience for your storage needs. It includes configurations for FSxN, a Storage Virtual Machine (SVM), and password management through AWS Secrets Manager.

## Overview

The template sets up an FSxN file system with a multi-AZ deployment model for high availability. It configures a security group to restrict network access to the file system, uses AWS Secrets Manager to securely manage the admin passwords for FSx and SVM, and organizes resources and parameters for clarity and easy management.

## Prerequisites

- An AWS account
- A VPC with at least two private subnets in separate Availability Zones
- An existing KMS key for encryption (optional)

## Parameters

- **FileSystemName**: A name for the FSxN file system for easy identification.
- **myVpc**: The ID of the VPC where the FSxN cluster will be deployed.
- **Subnet1ID & Subnet2ID**: The IDs of the private subnets for the FSxN file system's network interface.
- **FSxONTAPRouteTable**: Route table IDs for FSxONTAP, comma-separated for multiple entries.
- **StorageCapacity**: The storage capacity in GiB. Minimum is 1024 GiB; Maximum is 192 TiB.
- **FSxAllowedCIDR**: CIDR block allowed access to the FSx file system.
- **ThroughputCapacity**: Throughput capacity in MBps. Valid values are 512, 1024, 2048.
- **WeeklyMaintenanceTime**: The preferred start time for weekly maintenance in UTC.
- **FsxAdminPassword**: Password for the "fsxadmin" user, to access the ONTAP CLI or REST API.
- **RootVolumeSecurityStyle**: The security style of the SVM root volume. Values: UNIX, NTFS, MIXED.
- **SvmAdminPassword**: Password for managing SVM, to access the NetApp ONTAP CLI or REST API.

## Deployment Steps

1. **Prepare Your Environment**:
   Ensure that your AWS account has a VPC with the necessary private subnets and a KMS key for encryption if you choose to use one.

2. **Launch the CloudFormation Stack**:
   - Navigate to the AWS CloudFormation console.
   - Choose *Create stack* > *With new resources (standard)*.
   - Upload the CloudFormation template file or paste the template code directly.
   - Fill in the parameters as per your requirements and preferences.

3. **Review and Create**:
   - Review the settings and choose *Next*.
   - On the review page, acknowledge that AWS CloudFormation might create IAM resources.
   - Choose *Create stack* to deploy the FSxN file system.

## Outputs

- **FSxFileSystemID**: The ID of the deployed FSx for NetApp ONTAP file system.
- **FSxAdminPasswordSecretARN**: The ARN for the FSx admin password in AWS Secrets Manager.
- **SVMAdminPasswordSecretARN**: The ARN for the SVM admin password in AWS Secrets Manager.

## Cleanup

To avoid incurring future charges, delete the CloudFormation stack, which will remove the deployed resources.

## Security

This template includes security configurations, like creating a security group that limits access to defined CIDR blocks. Always review and adjust these settings based on your organization's security policies.
