# Deploy-React-App-To-AWS
Deploys a React App to an S3 bucket, and then invalidates the Cloudfront cache for that bucket, so changes are seen when the bucket is re-deployed
# How to Use: 
Below is an example
```
name: Deploy To AWS
uses: aasmal97/deploy-react-app-to-aws
with:
  aws_region: us-east-1
  aws_access_key_id: ${{ secrets.access_key_id }}
  aws_secret_access_key: ${{ secrets.secret_key }}
  cloudfront_distribution_id: ${{ secrets.distribution_id }}
  bucket_name: ${{ secrets.bucket_name }}
  react_app_secrets: ${{toJson(secrets)}}
  node_verison: 16
  path_to_app: ./test-app
```
# Inputs:
 - `aws_region`: The region your cloudfront distribution and s3 bucket are initated/setup in.
 - `aws_access_key_id`: An AWS user's or role's access key id. This is needed for AWS authentication.
 - `aws_secret_access_key`: An AWS user's or role's secret key. This is needed for AWS authentication.
 - `cloudfront_distribution_id`: The cloudfront distribution id that needs to be invalidated since it is hosting the S3 bucket
 - `bucket_name`: the s3 bucket name that the react app will be deployed to
 - `react_app_secrets`: A stringified object that contains react app secrets that will be passed prior to the build step
 - `node_verison`: Node JS version that the app will run in. By default this is set to 16
 - `path_to_app`: This is the relative path from your root, where the app's `package.json` config file is located.
# Caveats: 
If you are using `create-react-app` to create and package your react application, then there is no need to read further as `create-react-app` builds the react app files in its proper configuration. However, if you are using your own custom packaging scripts, ensure that the following requirements are met.
- Your build script can be called by using `npm run build` 
- Your build script outputs a folder named `build` where the react app's files are compiled to. 
- Note: All files in your `build` folder will be uploaded to you s3 bucket.

