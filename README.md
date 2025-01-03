# Deploy Static Site To AWS

Deploys a static app (SPA, SSG or static pages) to an S3 bucket and then invalidates the Cloudfront cache for that bucket, so changes are seen when the bucket is re-deployed.

This action is useful to deploy:

- [Single Page Applications (SPA)](https://en.wikipedia.org/wiki/Single-page_application)
- [Staticly Generated Sites/Applications using SSG](https://en.wikipedia.org/wiki/Static_site_generator)
- [Simple Static HTML pages](https://en.wikipedia.org/wiki/Static_web_page)

# How to Use:

Below is an example

```yaml
name: Deploy To AWS
uses: aasmal97/deploy-static-app-to-aws@2.0.0
with:
  aws_region: us-east-1
  aws_access_key_id: ${{ secrets.access_key_id }}
  aws_secret_access_key: ${{ secrets.secret_key }}
  cloudfront_distribution_id: ${{ secrets.distribution_id }}
  bucket_name: ${{ secrets.bucket_name }}
  app_secrets: ${{toJson(secrets)}}
  node_verison: 20
  path_to_app: ./
  secrets_prefix: "REACT_APP.*"
```

# Inputs:

- `aws_region`: The region your cloudfront distribution and s3 bucket are initated/setup in.
- `aws_access_key_id`: An AWS user's or role's access key id. This is needed for AWS authentication.
- `aws_secret_access_key`: An AWS user's or role's secret key. This is needed for AWS authentication.
- `cloudfront_distribution_id`: The cloudfront distribution id that needs to be invalidated since it is hosting the S3 bucket
- `bucket_name`: the S3 bucket name that the static app will be deployed to
- `app_secrets`: A stringified object that contains secrets, that will be passed prior to the build step
- `node_verison`: Node JS version that the app will run in. By default this is set to 16
- `path_to_app`: This is the relative path from your root, where the app's `package.json` config file is located.
- `build_dir`: The relative path from the `CURRENT WORKING DIRECTORY (cwd)`, to the build directory. This directory will be uploaded into AWS S3. By default it is `./build`
- `secrets_prefix`: A regex pattern applied to environment variable names, that determines if they are loaded into a `.env` file or not
- `env_file_name`: The name of the generated `.env` file that will will be generated prior to initiating the build command. By default, it is `.env`
- `destination_path`: The **ABSOLUTE PATH**, that you want the .env file to be generated in. By default, it is the **nearest** package.json to the resolved `path_to_app` directory, or if no `package.json` exists, the `path_to_app` directory itself.

# Requirements:
Ensure that the following requirements are met.

- Your build script can be called by using `npm run build`
- Your build script outputs a folder named `build` where the react app's files are compiled to.
- Note: All files in your `build` folder will be uploaded to your s3 bucket.

Note: This action only deploys STATIC sites to AWS. For server-side rendered (SSR) applications, a different workflow is needed, as Cloudfront is a live server environment. For these applications, tools like Render, AWS Amplify, or AWS EC2 are good alternatives
