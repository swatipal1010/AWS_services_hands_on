## AWS Identity and Access Management (IAM)
- In this lab, you will explore users, groups, and policies in the AWS Identity and Access Management (IAM) service.

### Task 1. Explore the users and groups
- In this task, you will explore the users and groups that have already been created for you in IAM.
1. First, note the Region that you are in; for example, **N. Virginia**. The Region is displayed in the upper-right corner of the console page.
   - You might need this information later in the lab.
2. Choose the Services menu, locate the **Security, Identity, & Compliance** services, and choose **IAM**.
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/b762b9f3-0d18-478d-b763-778d90f58646)

3. In the navigation pane on the left, choose **Users**.
   - The following IAM users have been created for you:
     - user-1
     - user-2
     - user-3
     ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/d11664f4-3cd0-4fdc-ab42-d7e7f7981166)

4. Choose the name of **user-1**.
   - This brings you to a summary page for user-1. The **Permissions** tab will be displayed.
   - Notice that user-1 does not have any permissions.
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/21a22b9f-7a6e-453b-b02a-8222eb023727)

5. Choose the **Groups** tab.
   - Notice that user-1 also is not a member of any groups.
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/51cee074-d75f-43a3-b008-57d0453dfdf7)

6. Choose the **Security credentials** tab.
   - Notice that user-1 is assigned a **Console password**. This allows the user to access the AWS Management Console.
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/0d698790-9105-4058-84da-91c41992b8ce)

7. In the navigation pane on the left, choose **User groups**.
   - The following groups have already been created for you:
     - EC2-Admin
     - EC2-Support
     - S3-Support
     ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/ed336ea1-469d-4794-ba44-380ec42afad8)

8. Choose the name of the **EC2-Support** group.
   - This brings you to the summary page for the **EC2-Support** group.
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/ba8badd5-fb26-45f7-a798-c43113066b1d)

9. Choose the **Permissions** tab.
   - This group has a managed policy called **AmazonEC2ReadOnlyAccess** associated with it. Managed policies are prebuilt policies (built either by AWS or by your administrators) that can be attached to IAM users and groups. When the policy is updated, the changes to the policy are immediately applied against all users and groups that are attached to the policy.
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/fe68c64a-9ca0-467b-be2e-961d6bad3364)

10. Under **Policy Name**, choose the link for the **AmazonEC2ReadOnlyAccess** policy.
11. Choose the **{} JSON** tab.
    - A policy defines what actions are allowed or denied for specific AWS resources. This policy is granting permission to *List* and *Describe* (view) information about Amazon Elastic Compute Cloud (Amazon EC2), Elastic Load Balancing, Amazon CloudWatch, and Amazon EC2 Auto Scaling. This ability to view resources, but not modify them, is ideal for assigning to a support role.
    - Statements in an IAM policy have the following basic structure:
      - **Effect** says whether to *Allow* or *Deny* the permissions.
      - **Action** specifies the API calls that can be made against an AWS service (for example, *cloudwatch:ListMetrics*).
      - **Resource** defines the scope of entities covered by the policy rule (for example, a specific Amazon Simple Storage Service [Amazon S3] bucket or Amazon EC2 instance; an asterisk [ * ] means *any resource*).
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/707e633a-7a0d-44a4-aa19-8a0d4e1195da)

12. In the navigation pane on the left, choose **User groups**.
13. Choose the name of the **S3-Support** group.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/0598392a-4661-4e32-a259-815e2d34bf1a)

14. Choose the **Permissions** tab.
    - The S3-Support group has the **AmazonS3ReadOnlyAccess** policy attached.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/16f3ffde-04dc-493c-8e2c-fe160adaccde)

15. Under **Policy Name**, choose the link for the **AmazonS3ReadOnlyAccess** policy.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/1821302d-eb39-48e7-aa9a-3e624b0372dd)

16. Choose the **{} JSON** tab.
    - This policy has permissions to *Get* and *List* for *all* resources in Amazon S3.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/42fd0e56-c444-4d49-8bcb-1af9a441d8c9)

17. In the navigation pane on the left, choose **User groups**.
18. Choose the name of the **EC2-Admin** group.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/0fb257ae-9b39-4abd-9155-276173d4dc1b)

19. Choose the **Permissions** tab.
    - This group is different from the other two. Instead of a managed policy, the group has an *inline policy*, which is a policy assigned to just one user or group. Inline policies are typically used to apply permissions for specific situations.
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/efd32084-7276-413a-b648-ac41c4943f0b)

20. Under **Policy Name**, choose the name of the **EC2-Admin-Policy** policy.
21. Choose the **JSON** tab.
    - This policy grants permission to *Describe* information about Amazon EC2 instances, and also the ability to *Start* and *Stop* instances.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/4f213278-338b-49ac-aa65-c60819033af6)

22. At the bottom of the screen, choose **Cancel** to close the policy.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/5846ea6b-e6c6-480e-b10d-13550b33d965)



### Business scenario
- For the remainder of this lab, you will work with these users and groups to enable permissions that support the following business scenario.
- Your company is growing its use of AWS services, and is using many Amazon EC2 instances and Amazon S3 buckets. You want to give access to new staff depending upon their job function, as indicated in the following table:
![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/5313918a-a5ff-498d-a7ba-6c0ef7df2136)



### Task 2. Add users to groups
- You have recently hired ***user-1*** into a role where they will provide support for Amazon S3. You will add them to the ***S3-Support*** group so that they inherit the necessary permissions via the attached ***AmazonS3ReadOnlyAccess*** policy.
- Ignore any **"not authorized"** errors that appear during this task


### Add user-1 to the S3-Support group
23. In the left navigation pane, choose **User groups**.
24. Choose the name of the **S3-Support** group.
25. On the **Users** tab, choose **Add users**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/a71a5268-6de5-4649-9a6d-39111100fc0a)

26. Select  **user-1**, and choose **Add users**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/dce9cd08-bd20-46c5-aba3-be160fad6b52)

    - On the **Users** tab, notice that *user-1* has been added to the group.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/b82b40dc-a81d-49f9-892e-32ebc116030a)



### Add user-2 to the EC2-Support group
- You have hired ***user-2*** into a role where they will provide support for Amazon EC2. You will add them to the ***EC2-Support group*** so that they inherit the necessary permissions via the attached ***AmazonEC2ReadOnlyAccess*** policy.
27. Use what you learned from the previous steps to add *user-2* to the *EC2-Support* group.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/1373d28c-1d1d-4418-8a2b-9adbbd522524)
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/b7ef78f9-2352-4b38-81b8-9fb500717d2b)

    - *user-2* should now be part of the *EC2-Support* group.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/47d9b532-ce01-4279-bb53-941ab01c7e9d)


### Add user-3 to the EC2-Admin group
- You have hired ***user-3*** as your Amazon EC2 administrator to manage your EC2 instances. You will add them to the ***EC2-Admin*** group so that they inherit the necessary permissions via the attached ***EC2-Admin-Policy***.
28. Use what you learned from the previous steps to add *user-3* to the *EC2-Admin group*.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/777cc666-3ea2-4366-97a6-acbb173a2ca0)
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/3e8b4fa2-5966-4f8e-8cdd-f2ad1c7055f5)

    - *user-3* should now be part of the *EC2-Admin group*.
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/bb45067c-6ec6-4da0-bb1b-53caf2fb43a2)

29. In the navigation pane on the left, choose **User groups**.
    - Each group should have a **1** in the **Users** column. This indicates the number of users in each group.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/3e573abe-dfd7-40ac-af9d-2dc21ea1c8cf)

    - If you do not have a **1** for the **Users** column for a group, revisit the previous steps to ensure that each user is assigned to a group, as shown in the table in the **Business scenario** section.


### Task 3. Sign in and test users
- In this task, you will test the permissions of each IAM user in the console.

#### Get the console sign-in URL
30. In the navigation pane on the left, choose **Dashboard**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/760c0330-1b45-49fe-9fc0-851490e450d4)

    - Notice the **Sign-in URL for IAM users** in this account section at the top of the page.
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/d952f7fe-70d2-4a4f-95af-b9e919e8c3f0)

    - The sign-in URL looks similar to the following:
      - **https://123456789012.signin.aws.amazon.com/console**
    - This link can be used to sign in to the AWS account that you are currently using.
31. Copy the sign-in link to a text editor.

#### Test user-1 permissions
32. Open a private or incognito window in your browser.
33. Paste the sign-in link into the private browser, and press ENTER.
    - You will now sign-in as *user-1*, who has been hired as your Amazon S3 storage support staff.
34. Sign in with the following credentials:
    - **IAM user name**: `user-1`
    - **Password**: `Lab-Password`
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/8e51d23d-909c-407c-9498-cd5f6951f0c6)

35. Choose the **Services** menu, and choose **S3**.
36. Choose the name of one of your buckets, and browse the contents.
    - Because this user is part of the S3-Support group in IAM, they have permissions to view a list of Amazon S3 buckets and their contents.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/1d47a2d3-c45c-4cdb-8fb8-ef46bf0bf31e)

    - Now, test whether the user has access to Amazon EC2.
37. Choose the **Services** menu, and choose **EC2**.
38. In the left navigation pane, choose **Instances**.
    - You cannot see any instances. Instead, an error message says *you are not authorized to perform this operation*. This user has not been assigned any permissions to use Amazon EC2.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/6e78b73a-a5e7-47b1-84d7-460fca4dba3c)

    - You will now sign in as *user-2*, who has been hired as your Amazon EC2 support person.
39. First, sign out *user-1* from the console:
    - In the upper-right corner of the page, choose **user-1**.
    - Choose **Sign Out**.

#### Test user-2 permissions
40. Paste the sign-in link into the private browser again, and press ENTER.
41. Sign in with the following credentials:
    - **IAM user name**: `user-2`
    - **Password:** `Lab-Password`
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/ddae6832-3fab-4a4e-8e05-8dbce8525638)

42. Choose the **Services** menu, and choose **EC2**.
43. In the navigation pane on the left, choose **Instances**.
    - You are now able to see an EC2 instance. However, you cannot make any changes to Amazon EC2 resources because you have read-only permissions.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/74b63845-2b1e-4617-bcf0-daa1ca57a607)

    - If you cannot see an EC2 instance, then your Region might be incorrect. In the upper-right corner of the page, choose the Region name, and then choose the Region that you were in at the beginning of the lab (for example, **N. Virginia**).
44. Select the EC2 instance.
45. Choose the **Instance state** menu, and then choose **Stop instance**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/f411cd2f-8913-4592-8dc5-d15a03aeaed8)

46. To confirm that you want to stop the instance, choose **Stop**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/bdda64b2-dae9-4647-bb72-eba7f29d73d0)

    - An error message appears and says that *You are not authorized to perform this operation*. This demonstrates that the policy only allows you to view information without making changes.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/62779df3-f4a4-484e-8e00-5205c790b2fe)

    - Next, check if *user-2* can access Amazon S3.
47. Choose the **Services** menu, and choose **S3**.
    - An error message says *You don't have permissions to list buckets because user-2 does not have permissions to use Amazon S3*
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/f0e74f31-566d-44af-8a49-9807d5e50f1c)

    - You will now sign-in as *user-3*, who has been hired as your Amazon EC2 administrator.
48. First, sign out *user-2* from the console:
    - In the upper-right corner of the page, choose **user-2**.
    - Choose **Sign Out**.

#### Test user-3 permissions
49. Paste the sign-in link into the private browser again, and press ENTER.
50. Sign in with the following credentials:
    - **IAM user name:** `user-3`
    - **Password:** `Lab-Password`
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/a4a1a20f-567d-42fa-b700-e6e703ac1f35)

51. Choose the **Services** menu, and choose **EC2**.
52. In the navigation pane on the left, choose **Instances**.
    - An EC2 instance is listed. As an Amazon EC2 Administrator, this user should have permissions to *Stop* the EC2 instance.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/33ef21c1-e22a-40b0-b7a1-0e9633733b0a)

    - If you cannot see an EC2 instance, then your Region might be incorrect. In the upper-right corner of the page, choose the Region name, and then choose the Region that you were in at the beginning of the lab (for example, **N. Virginia**)
53. Select the EC2 instance.
54. Choose the **Instance state** menu, and then choose **Stop instance**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/faf14d1b-6328-425c-b792-138661bd257c)

55. To confirm that you want to stop the instance, choose **Stop**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/c5b7b766-c952-426e-9fff-fb881e34115b)

    - This time, the action is successful because *user-3* has permissions to stop EC2 instances. The **Instance state** changes to *Stopping and starts to shut down*.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/7f33ab48-7ca1-4251-b867-20facaeba57c)

56. Close your private browser window.





    

