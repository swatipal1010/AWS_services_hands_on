## USING CloudFront AS A CDN FOR WEBSITE
### Using CloudFront to create content delivery network (CDN) for a website that is stored in Amazon S3
### Task 1. Create an S3 bucket using the AWS CLI
- In this task, you will create an S3 bucket using the AWS Command Line Interface (AWS CLI). The AWS CLI is an open-source tool that you can use to interact with AWS services using commands in your command line shell.
1. Choose the **Service**s and **Developer Tools** and choose **CloudShell**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/1886d28d-0798-45a0-8555-a998b7e043b4)

   - If a welcome pop-up window appears, choose **Close**.
   - AWS CloudShell is a browser-based shell that gives you command line access to your AWS resources in the selected AWS Region.

2. Copy and paste the following code into a text editor:
   ```text
   cd ~
   aws s3api create-bucket --bucket (bucket-name) --region us-east-1
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
![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/29d9e725-e620-4762-99da-24cefa885640)

4. Run the updated code in the CloudShell terminal.
   - If a pop-up window appears, choose **Paste**.
   - The output should look similar to the following:
     
    ![image](https://github.com/swatipal1010/AWS_services_handson/assets/110754474/5632556b-6580-4293-90be-287b48b6feba)
     
**Note** : When you create a bucket with this command, the bucket is open to the public. We recommend that you keep all settings enabled unless you know that you need to turn off one or more of them for your use case, such as to host a public website.

### Task 2. Add a bucket policy
5. In the console, choose the **Services** menu, locate the **Storage** section, and choose **S3**.
6. Choose the name of the bucket that you just created.
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/c285c727-7de4-420b-97ab-ba3d48b4df65)

7. Choose the **Permissions** tab. Under **Block public access (bucket settings)** choose **Edit**. Remove the checkmark for **Block all public access**. Choose **Save changes**. Confirm the changes.
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/3b00de45-5608-4756-97de-951ad282d8b5)
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/c901f642-9c21-4e75-9429-1de351823e59)
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/ef077658-8791-48ff-b0eb-9b27bf202447)

8. Under **Object Ownership** choose **Edit**. Choose **ACLs enabled**. Check the acknowledgement and choose **Save changes**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/207f9c84-2946-4520-bc04-d93da3e2fbf1)
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/f3600af1-f0af-4cf9-b3f8-f22023fb6c06)

9. In the **Bucket policy** section, choose **Edit**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/3c5dccc9-23bb-4459-b70a-c595d0fee59f)

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
    
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/dc770d29-d0be-4c41-a9e8-5c46098fe4bd)
12. At the bottom of the page, choose **Save changes**.


### Task 3. Upload an HTML document
- In this task, you will upload the index.html file for your webpage to the S3 bucket.
13. Open the context menu (right-click) for the following link, and then choose **Save link as**: [index.html](https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-100-ACCAIC-1-35050/03-lab-5-cloudfront/s3/index.html)
14. Save the index.html file to your local computer.
15. In the console, choose the **Objects** tab.
  ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/4c2f9f2b-d9a1-4e4d-9e72-ac3ab0c7e24d)

16. Upload the index.html file to your bucket.
    - Choose **Upload**.
    - Drag and drop the index.html file onto the upload page. An alternative is to choose **Add files**, navigate to the file, and choose **Open**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/683a029b-c454-42ea-8e3f-7e60f7e168c9)
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/e37f349d-70ab-45f7-946e-414bd1aea7e2)

17. Expand the **Permissions** section.
18. Under **Predefined ACLs**, select **Grant public-read access**.
    - A warning message similar to **Granting public-read access is not recommend** appears below the setting you selected.
19. Below the warning, check the box next to **I understand....**
20. At the bottom of the page, choose **Upload**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/0ba1a74e-6aa8-435d-bd2b-895202150d8b)

21. Choose **Close**.
    - The index.html file appears in the **Objects** list.
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/9492d2a9-174c-449f-a398-4ee843c481d8)


### Task 4. Test your website
22. Select the **Properties** tab, and scroll down to the **Static website hosting** section.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/555d91fa-9417-494e-ae42-4e0676610928)

23. Choose **Edit**.
24. Select **Enable**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/5551af25-6124-47bf-8342-57d174bacd58)

25. In the **Index document** text box, enter `index.html`
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/8dc4e656-e316-4be1-a00b-8a75177680e7)

26. Select **Save changes**.
27. Scroll down to the **Static website hosting** section again, and copy the **Bucket website endpoint** URL to your clipboard.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/b7c0f093-e4b8-498c-bfd5-1dc16870fa68)

28. Open a new tab in your web browser, paste the URL you just copied, and press **Enter**.
    - The **Hello World** webpage should display. You have successfully hosted a static website using an S3 bucket!
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/58524be3-b53c-4718-a495-153e87ed541b)


### Task 5. Create a CloudFront distribution to serve your website
- In this task, you will create an Amazon CloudFront distribution to serve your website.
29. Choose the **Services** menu, locate the **Networking & Content Delivery** section, and choose **CloudFront**.
  ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/fdaa37b8-5ac2-4220-9547-e0d899187ad9)

30. Choose Create a **CloudFront Distribution**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/3d607641-f44c-4c55-a847-d41d00140d51)

31. Under **Origin**, choose the text box next to **Origin domain** and select the endpoint from your S3 bucket.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/0daef51d-c880-49aa-9ce6-2d6cc7e07d04)

32. For **Viewer Protocol Policy**, ensure that **HTTP and HTTPS** is selected. Under **Web Application Firewall (WAF)** choose **Do not enable security protections**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/99d89e53-b8c8-4b4b-8495-bf8d594a2d91)
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/d67e22f4-138e-438f-b29a-f9ebe596125c)

33. Scroll to the bottom of the page and select **Create Distribution**.
    - A new CloudFront distribution displays in the distributions list. The Status will say Deploying until your website has been distributed. This may take up to 20 minutes.
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/fd6bd9a4-8e1b-44f1-b52d-18a44738eb86)

    - When the Status says **Enabled**, you can test your distribution.
34. Copy the **Domain Name** value for your distribution and save it to a text editor to use in a later step.
35. Create a new HTML file to test the distribution.
    - Find and download an image from the internet.
    - Navigate to your S3 bucket and upload the image file to it, making sure to grant public access as you did when uploading the HTML file earlier in this lab.
    - Create a new text file using Notepad and copy the following text into it:
      ```text
      <html>
      <head>My CloudFront Test</head>
      <body>
        <p>My test content goes here.</p>
        <p><img src="http://domain-name/object-name" alt="my test image">
      </body>
      </html>
      ```
     - Replace **domain-name** with the domain name that you copied earlier for your CloudFront distribution.
     - Replace **object-name** with the file name of the picture file that you uploaded to your S3 bucket.
     - The edited line of code should look similar to the following:
       ```text
       <p><img src="http://d2f1zrxb2zaf30.cloudfront.net/picture.jpg" alt="my test image">
       ```
     - Save the text file with an HTML extension.
36. Use an internet browser to open the HTML file that you just created.
- If the image that you uploaded shows, your CloudFront distribution was successful. If not, repeat the lab.





