# Deploy-React-App-To-AWS
Deploys a React App to an S3 bucket, and then invalidates the Cloudfront cache for that bucket, so changes are seen when the bucket is re-deployed
# How to Use: 
Below is an example
```
name: Deploy To AWS
secrets: inherit
uses: aasmal97/deploy-react-app-to-aws
with:
  aws_region: us-east-1
  aws_access_key_id: ${{ secrets.access_key_id }}
  aws_secret_access_key: ${{ secrets.secret_key }}
  cloudfront_distribution_id: ${{ secrets.distribution_id }}
  bucket_name: ${{ secrets.bucket_name }}
  deployment_url: www.example.com
  environment_name: production
```
# Inputs:
 - `aws_region`: The region your cloudfront distribution and s3 bucket are initated/setup in.
 - `aws_access_key_id`: An AWS user's or role's access key id. This is needed for AWS authentication.
 - `aws_secret_access_key`: An AWS user's or role's secret key. This is needed for AWS authentication.
 - `cloudfront_distribution_id`: The cloudfront distribution id that needs to be invalidated since it is hosting the S3 bucket
 - `bucket_name`: the s3 bucket name that the react app will be deployed to
 - `deployment_url`: The url the deployment can be found at
 - `environment_name`: The custom environment that this action is running in
