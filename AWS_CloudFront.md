## USING CloudFront AS A CDN FOR WEBSITE
### Using CloudFront to create content delivery network (CDN) for a website that is stored in Amazon S3
### Task 1. Create an S3 bucket using the AWS CLI
- In this task, you will create an S3 bucket using the AWS Command Line Interface (AWS CLI). The AWS CLI is an open-source tool that you can use to interact with AWS services using commands in your command line shell.
1. Choose the **Service**s and **Developer Tools** and choose **CloudShell**.
   - If a welcome pop-up window appears, choose **Close**.
   - AWS CloudShell is a browser-based shell that gives you command line access to your AWS resources in the selected AWS Region.

2. Copy and paste the following code into a text editor:
   ```text
   cd ~
   aws s3api create-bucket --
   bucket (bucket-name) --
   region us-east-1
   ```
3. In the code that you copied, replace (**bucket-name**) with a unique Domain Name System (DNS)-compliant name for your new bucket.
   - Follow these naming guidelines:
     - The name must be unique across all existing bucket names in Amazon S3.
     - The name must be between 3 and 63 characters long.
     - The name can consist only of lowercase letters, numbers, dots (.), and hyphens (-).
     - The name must begin and end with a letter or number.
     - The name must not be formatted as an IP address (for example, 192.168.5.4).
     - After you create the bucket, you cannot change the name, so choose wisely.
     - Choose a bucket name that reflects the objects in the bucket. This is because the bucket name is visible in the URL that points to the objects that you’re going to put in your bucket.
**Note**: The us-east-1 Region has been entered in the command. When you create a bucket, the best practice is to choose a Region close to you to minimize latency and costs, or to address regulatory requirements. Objects stored in a Region never leave that Region unless you explicitly transfer them to another Region.
4. Run the updated code in the CloudShell terminal.
   - If a pop-up window appears, choose **Paste**.
   - The output should look similar to the following:
     
    ![image](https://github.com/swatipal1010/AWS_services_handson/assets/110754474/5632556b-6580-4293-90be-287b48b6feba)
     
**Note** : When you create a bucket with this command, the bucket is open to the public. We recommend that you keep all settings enabled unless you know that you need to turn off one or more of them for your use case, such as to host a public website.

### Task 2. Add a bucket policy
5. In the console, choose the **Services** menu, locate the **Storage** section, and choose **S3**.
6. Choose the name of the bucket that you just created.
7. Choose the **Permissions** tab. Under **Block public access (bucket settings)** choose **Edit**. Remove the checkmark for **Block all public access**. Choose **Save changes**. Confirm the changes.
8. Under **Object Ownership** choose **Edit**. Choose **ACLs enabled**. Check the acknowledgement and choose **Save changes**.
9. In the **Bucket policy** section, choose **Edit**.
10. To grant public read access for your website, copy and paste the following bucket policy into the policy editor.
    ```text
    {
    "Version":"2012-10-17",
    "Statement":[
      {
         "Sid":"PublicReadForGetBucketObjects",
         "Effect":"Allow",
         "Principal":"*",
         "Action":[
            "s3:GetObject"
         ],
         "Resource":[
            "arn:aws:s3:::example-bucket/*"
         ]
      }
    ]
    }
    ```
11. In the policy, replace **example-bucket** with the name of your bucket.
12. At the bottom of the page, choose **Save changes**.


### Task 3. Upload an HTML document
- In this task, you will upload the index.html file for your webpage to the S3 bucket.

13. Open the context menu (right-click) for the following link, and then choose **Save link as**: [index.html](https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-100-ACCAIC-1-35050/03-lab-5-cloudfront/s3/index.html)
14. Save the index.html file to your local computer.
15. In the console, choose the **Objects** tab.
16. Upload the index.html file to your bucket.
    - Choose **Upload**.
    - Drag and drop the index.html file onto the upload page. An alternative is to choose **Add files**, navigate to the file, and choose **Open**.
17. Expand the **Permissions** section.
18. Under **Predefined ACLs**, select **Grant public-read access**.
    - A warning message similar to **Granting public-read access is not recommend** appears below the setting you selected.
19. Below the warning, check the box next to **I understand....**
20. At the bottom of the page, choose **Upload**.
21. Choose **Close**.
    - The index.html file appears in the **Objects** list.
      


