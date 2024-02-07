# AWS Cost Explorer Script

This script provides a convenient way to fetch and display AWS costs and usage data for multiple regions, grouped by service, over a specified time period. It utilizes the AWS Cost Explorer API through the AWS CLI to retrieve detailed cost information, which can help in monitoring and managing AWS expenses.

## Features

- Fetch AWS costs and usage data across multiple regions.
- Group costs by AWS service for detailed insight.
- Dynamically set the date range for cost data retrieval.
- Format output for easy readability, including service costs and total costs for specified periods.

## Prerequisites

Before you can run this script, you need to have the following:

- AWS CLI installed and configured with appropriate permissions. [AWS CLI Installation Guide](https://aws.amazon.com/cli/)
- `jq` installed for processing JSON data. [jq Installation Guide](https://stedolan.github.io/jq/download/)

Ensure your AWS account has the necessary permissions to access the Cost Explorer API.

## Setup

1. Clone this repository to your local machine.

    ```bash
    git clone https://github.com/al3v/AWS-Cost-Script.git
    ```

2. Navigate to the cloned directory.

    ```bash
    cd AWS-Cost-Script
    ```

3. Make the script executable.

    ```bash
    chmod +x cost.sh
    ```

## Configuration

Edit the `cost.sh` script to specify your desired `START_DATE` and the AWS regions you wish to query. The `END_DATE` is set dynamically to the current date.

```bash
START_DATE="2024-01-01"
REGIONS=("us-east-1" "us-west-1" "eu-west-1" "ap-southeast-1")
 ```

## Running the Script
```bash
   ./cost.sh
```

## Output Format
```bash
Fetching costs for region: us-east-1
----------------------------------------
2024-01-01 to 2024-02-01:
Service: Amazon EC2 - Cost: 123.456 USD
Service: Amazon S3 - Cost: 78.910 USD
*********
----------------------------------------

```
![image](https://github.com/al3v/AWS-Cost-Script/assets/73062283/5615f8bc-4329-4cf9-9c6a-43e43fc14b88)







