*The content of this repository, including this readme, is lifted entirely from [Pulumi's examples repository](https://github.com/pulumi/examples/aws-py-s3-folder)*
<br>

# Host a Static Website on Amazon S3

A static website that uses [S3's website support](https://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteHosting.html).
For a detailed walkthrough of this example, see the tutorial [Static Website on AWS S3](https://www.pulumi.com/docs/tutorials/aws/s3-website/).

## Deploying and running the program

Note: some values in this example will be different from run to run.  These values are indicated
with `***`.

1. Connect your workspace to your Pulumi account
   1. Go to https://app.pulumi.com/account/tokens
   2. Click on `Create Token`
   3. Copy the token value (It starts with `pul-`)
   4. Back into your coding environment, on the terminal type: `pulumi login` and paste the token value when prompted.

2. Make sure your terminal is in this directory, and create a new stack:

    ```bash
    $ pulumi stack init website-testing
    ```

3. Set the AWS region:

    ```bash
    $ pulumi config set aws:region ap-southeast-2
    ```

4. Run `pulumi up` to preview and deploy changes.  After the preview is shown you will be prompted if you want to continue or not.

    ```bash
    $ pulumi up
    Previewing update (dev):

        Type                    Name                  Plan       
    +   pulumi:pulumi:Stack     aws-py-s3-folder-dev  create     
    +   ├─ aws:s3:Bucket        s3-website-bucket     create     
    +   ├─ aws:s3:BucketObject  index.html            create     
    +   ├─ aws:s3:BucketObject  python.png            create     
    +   ├─ aws:s3:BucketObject  favicon.png           create     
    +   └─ aws:s3:BucketPolicy  bucket-policy         create     

    Resources:
        + 6 to create

    Do you want to perform this update?
    > yes
      no
      details
    ```

5. To see the resources that were created, run `pulumi stack output`:

    ```bash
    $ pulumi stack output
    Current stack outputs (2):
        OUTPUT                                           VALUE
        bucket_name                                      s3-website-bucket-***
        website_url                                      ***.s3-website-us-west-2.amazonaws.com
    ```

6. To see that the S3 objects exist, you can either use the AWS Console or the AWS CLI:

    ```bash
    $ aws s3 ls $(pulumi stack output bucket_name)
    2018-04-17 15:40:47      13731 favicon.png
    2018-04-17 15:40:48        249 index.html
    ```

7. Open the site URL in a browser to see both the rendered HTML, the favicon, and Python splash image:

    ```bash
    $ pulumi stack output website_url
    ***.s3-website-us-west-2.amazonaws.com
    ```

8. To clean up resources, run `pulumi destroy` and answer the confirmation question at the prompt.
