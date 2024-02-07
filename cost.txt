#!/bin/bash

# Set the start date for the cost data
START_DATE="2023-11-01"
# Dynamically set the end date to today's date
END_DATE=$(date +%Y-%m-%d)

# List of AWS regions you want to query
REGIONS=("us-east-1" "us-west-1" "eu-west-1" "ap-southeast-1")

for region in "${REGIONS[@]}"
do
  echo "Fetching costs for REGION: $region"
  echo "----------------------------------------"
  
  # Use the AWS CLI to call the AWS Cost Explorer API and query costs for the specified region
  aws ce get-cost-and-usage \
    --time-period Start=$START_DATE,End=$END_DATE \
    --granularity MONTHLY \
    --metrics "UnblendedCost" \
    --group-by Type=DIMENSION,Key=SERVICE \
    --filter "Dimensions={Key=REGION,Values=$region}" | jq -r '
      .ResultsByTime[] | "\(.TimePeriod.Start) to \(.TimePeriod.End):",
      (.Groups[] | "Service: \(.Keys[0]) - Cost: \(.Metrics.UnblendedCost.Amount | tonumber | . as $num | $num | tostring | capture("^(?<intPart>\\d+)\\.(?<decPart>\\d{1,3})") | "\(.intPart).\(.decPart)") USD"),
      "*********"'
  
  echo "----------------------------------------"
  
  # Wait a bit between API calls to avoid rate limiting
  sleep 1
done
