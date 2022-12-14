## Migrate_From_GCS_To_AWS_S3
## Tools we need
1. Install rclone <br />
    * For macOS, `brew install rclone` <br />
    * For windows, https://rclone.org/downloads/ <br />
    * For other linux distributions, `curl https://rclone.org/install.sh | sudo bash` <br />
2. AWS CLI - https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
3. Stable internet connection

## Setup
1. Create [Service Account](https://cloud.google.com/iam/docs/creating-managing-service-accounts) and assign `Storage Admin` Role to that.
2. Create and Download the [keys](https://cloud.google.com/iam/docs/creating-managing-service-account-keys) of that Service Account.
2. For your IAM account, better to have S3 full access and generate `aws_access_key_id`, `aws_secret_access_key` and `aws_session_token` (for organisations we'll have this) <br />
    If you want to migrate 1000GB's of data then `aws_session_token` should definetly set to 12 hours, that can be done from [Session Duration](https://docs.aws.amazon.com/singlesignon/latest/userguide/howtosessionduration.html)
3. Update the rclone.conf file accordinly and store it in 
   * For linux distributions, `~/.config/rclone/rclone.conf`
   * For Windows, `C:\Users\<username>\AppData\Roaming\rclone\rclone.conf`

## How to run
`rclone sync gcs:<GCS Bucket Name> s3:<AWS S3 Bucket Name> --ignore-existing -Pv`

### Abbrevations
* GCS - Google Cloud Storage
* AWS - Amazon Web Services

**NOTE**
Keep an eye on your FUP limit