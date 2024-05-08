# CloudFormation Template for ENI Detachment

This README provides a detailed overview of a CloudFormation template designed to manage the detachment of an Elastic Network Interface (ENI) from an Amazon EC2 instance before the instance is terminated. This ensures that the ENI is preserved post-termination.

## Overview

This CloudFormation solution addresses the challenge where an ENI needs to be detached from an EC2 instance without deleting the ENI when the instance is terminated. Due to CloudFormation's native limitations, additional AWS services such as Lambda and AWS CLI (via CommandRunner) are utilized to execute this process.

## Problem Statement

The primary issue involves ensuring the ENI is detached and not deleted when its associated EC2 instance is terminated. The CloudFormation template does not support EC2 termination directly with conditional ENI detachment.

## Solution Strategy

The strategy involves:
1. Setting the EC2 instance's `DeleteOnTermination` attribute for the ENI to `False`.
2. Utilizing a Lambda function or an AWS CLI command executed via CommandRunner to terminate the EC2 instance, ensuring the ENI remains.

## Implementation

As direct code sharing is not possible, below is the general approach used:

1. **EC2 and ENI Configuration:** Define the EC2 instance and ENI within the CloudFormation template, ensuring that the ENI's `DeleteOnTermination` parameter is set to `False`.
2. **Lambda Function or CommandRunner Utilization:** Implement a Lambda function or use CommandRunner to execute an AWS CLI command that manages the instance termination. This ensures the ENI is not deleted upon instance termination.
3. **Outputs:** Configure outputs to return relevant information, such as the instance and ENI IDs, for further processing or verification.

## Usage Instructions

1. Review the CloudFormation template and customize parameters as per your environment.
2. Deploy the template via the AWS Management Console, AWS CLI, or other deployment tools that support CloudFormation.
3. Monitor the outputs and verify the ENI remains after the EC2 instance is terminated.

## Additional Notes

- Ensure that the AWS permissions are correctly set up for Lambda or CommandRunner to interact with EC2 instances.
- Thoroughly test the template in a development environment before applying it in a production setting.

For further customization or issues, refer to the AWS documentation on CloudFormation, Lambda, and EC2 or consult with your AWS support representative.
