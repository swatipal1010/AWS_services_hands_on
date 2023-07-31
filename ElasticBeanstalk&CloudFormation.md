## Amazon Elastic BeanStalk and Amazon CloudFormation
### Create an application using AWS Elastic Beanstalk. Also use a template and AWS CloudFormation to build a Virtual Private Cloud (VPC).

### Task 1. Deploy an application using Elastic Beanstalk
1. Choose the **Services** menu, locate the **Compute** services, and choose **Elastic Beanstalk**.
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/7539bd40-69a0-4e6d-840e-155e1c1a6725)

2. Choose **Create Application**.
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/c9dbacf3-1b1c-4659-9a63-d94f7e713f6e)

3. For **Application name**, enter a name for your application; for example, `MyLabApp`
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/b8957e4a-4969-4b58-9d1e-945d8feefcb8)
   

4. For **Platform**, select **PHP**.
   
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/599d9a75-a928-41de-ba56-503e5fa78cd5)
   

5. For **Application code**, select **Sample application**.
   
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/a5ce2cb5-1f52-4bf1-82e5-6e700885633f)
   

6. Choose **Next**.
    
7. Under **Existing service roles** choose the drop-down and select **EMR_EC2_DefaultRole**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/ca1d2567-2c96-4b0f-97bc-c6828f4aec98)

8. Under **EC2 key pair** choose the drop-down and select **vockey**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/68e23c62-eacb-41a0-9ce8-b2eea5fb638e)

9. Under **EC2 instance profile** choose the drop-down and select **EMR_EC2_DefaultRole**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/578b49b2-5af6-4e1b-9b8e-1c0ab6bc86cf)

10. Choose **Next**.
11. Under **VPC** select the **available VPC**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/2830d7b0-8744-4194-918a-88cf6c9041f1)

12. Under **Public IP address** select **Activated**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/75d97b42-1926-46e7-808d-c86de12b44c8)

13. Under **Instance subnets** select at least two.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/a790b17c-b4b2-4c8c-8c72-2851f627376f)

14. Choose **Next**.
15. Under **EC2 Security groups** select the **default**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/b19a3b5f-a0db-47b0-a2b8-63d553734ffd)

16. Choose **Next**.
17. Under **Health reporting** choose **Basic**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/0aa768f8-e6a3-454c-add3-db3e2d16ddb3)

18. Under **Managed updates** de-select **Activated**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/50ae7bb7-2d20-4ebe-84aa-e8e46e19e00e)

19. Choose **Next**.
20. Choose **Submit**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/11fd2147-1595-45c8-bb9f-d09df6fdcd41)
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/a480f8ee-15e7-4090-9538-ec962ea7b468)
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/c99b33b8-8ef2-4531-9591-5108ccd4e122)
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/714db5f4-333a-49ee-8bd1-16c1e0e21cea)
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/5d21493a-af1f-4ec4-8f78-44f36520ebf6)



    - Watch the console as Elastic Beanstalk creates and runs the necessary resources to run the application. It takes 5-10 minutes for the process to complete.
    - Elastic Beanstalk creates an Amazon Simple Storage Service (Amazon S3) storage bucket and a security group, launches an Amazon Elastic Compute Cloud (Amazon EC2) instance, and runs the code.
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/1ec23428-5164-4185-b010-bee3c801b181)

    - When complete, the screen changes to show the newly created environment. It is ready for you to upload a PHP application.
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/a59de390-e68b-4a38-b60a-261ee24646c0)

21. Open a new browser tab or window. Navigate to the AWS Tutorials and Samples web page.
22. On the page, in the second list of downloads, find **PHP – php.zip**. Download the sample **PHP** application to your computer.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/cb8f6fc9-a1a0-4590-aafe-4dfeb9a424a7)

    - You should now have a file called _php.zip_.
23. Return to the Elastic Beanstalk console tab.
24. Choose **Upload and deploy**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/23f380b8-c2f6-40b9-a904-152ccd627379)

25. Choose **Choose file**, navigate to and select the **php.zip** file that you downloaded, and choose **Open**.
    
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/1c76c9c7-fd1a-4dbf-8507-218ed506f6a2)
    
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/7c2bb649-2f68-4a30-9465-74392d73f9a3)

26. Choose **Deploy**.
    - The application deploys to the environment using all of the cloud resources Elastic Beanstalk provisioned.
      
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/3d49fcb6-d517-49ec-8b7f-31e821e061b0)

27. To see your PHP website, in the left navigation pane, choose **Go to environment**.
    
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/7e0a4b71-c60f-44ad-844f-049d9ce65c74)
    

    - The web application opens in a new tab.
      
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/a5c4291c-fca9-483d-998f-47eaf3d75735)



### Task 2. Deploy an application using CloudFormation
28. Return to the AWS Management Console tab.
29. Choose the **Services** menu, locate the **Compute** services, and choose **EC2**.
30. In th left navigation pane, under **Network & Security**, choose **Key Pairs**.
31. Choose **Create key pair**.
32. For **Name**, enter `CFLearner`
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/58abaaab-5940-43c1-8d06-a46de09df26f)

33. Choose **Create key pair**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/84441b19-4ff5-460d-b3d2-4c31f31a255a)

34. When the download window opens, choose **Cancel**. You do not need to download the file.
35. Choose the **Services** menu, locate the **Management & Governance** services, and choose **CloudFormation**.
   - The **Stacks** list appears and displays the CloudFormation stacks that were created in your lab environment. Notice the stack whose **Description** says _AWS Elastic Beanstalk environment_. This stack was created automatically when you deployed your application through Elastic Beanstalk.
     ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/10f11f8a-3aab-49aa-a1ff-98999f2c1c58)

   - This demonstrates how the two services work together to create an environment to run your code.
36. Choose **Create stack**, and then choose **With new resources (standard)**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/c0e40c52-e903-4406-9010-3f4ba33ca3c4)

37. In the **Prerequisite** section, choose **Use a sample template**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/dc437587-6e1b-48a8-8730-bd5353fb93af)

38. In the **Select a sample template** section, select **WordPress blog**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/73fc6c5a-56a6-4375-97f6-bf1405367379)

    - WordPress is web software that you can use to create a website or blog. This template installs a highly available and scalable WordPress deployment using an Amazon Relational Database Service (Amazon RDS) database instance for storage.
39. Select **Next**.
40. For **Stack name**, enter `WordPressStack`
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/d27c3b2b-3538-4635-b3ca-063a44c36e01)

41. In the **Parameters** section, configure the following:
    - **DBPassword:** Enter `Testing1 ` 
    - **DBUser:** Enter `testadmin`
    - **KeyName:** Choose the **CFLearner** key pair
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/1b13c8bf-3867-4e07-8858-fe164af4a640)

42. Choose **Next**, and then choose **Next** again.
    - You will use the default stack options.
43. Review the stack configuration, and then choose **Submit**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/f951fd73-5076-4080-ac5c-8bec95f15f74)

    - This initiates the deployment of the resources. You can watch the CloudFormation stack events on the **Events** tab as a complete WordPress site is created.
