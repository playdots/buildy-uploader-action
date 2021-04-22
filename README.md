# Buildy Uploader

This Github actions is a [composite action](https://docs.github.com/en/actions/creating-actions/creating-a-composite-run-steps-action) of the setps needed to upload build artifact to Build's S3 Bucket.

## Usage

### Pre-requisites
You need to run [configure AWS Credentials](https://github.com/aws-actions/configure-aws-credentials) in a step before using this action.
This action expecct the follow Enveironment Variables to be set
* BUILD_NAME - The name of the build (TwoDots, Garden, Match City, etc..)
* TARGET - The platform target (Android, iOS)
* STABILITY - The build stability tag (Prototype, Develop, Production, Prod-RC, etc..)

### Inputs

* 'build-directory' The directory where the build artifacts exist.

### Example

```
# Configures AWS credentials for AWS CLI.
- name: Configure AWS credentials
  uses: aws-actions/configure-aws-credentials@v1
  with:
    aws-access-key-id: ${{ secrets.AWS_KEY_ID }}
    aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
    aws-region: us-east-1

- name: Upload to Buildy
  uses: playdots/buildy-uploader-action@master
  with:
    build-directory: $DIR
  env:
    DIR: ${{ format('build/{0}', env.TARGET) }}
```
