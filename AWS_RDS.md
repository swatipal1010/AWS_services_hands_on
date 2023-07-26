## AWS Realtional Database Service (RDS)
### Task 1. Set up an RDS DB instance
1. Choose the **Services** menu, locate the **Database** category, and then choose **RDS**.
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/a80eed2f-767c-4cf9-8919-60fbc46f9314)

2. Choose **Create database**.
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/4e3600a1-6ef2-4867-a26b-6f73b5097110)

3. In the **Choose a database creation method** section, choose **Easy create**.
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/4f7fa00e-87ec-4c8c-8ad0-245fc8cbe7e1)

4. In the **Configuration** section, configure:
   - For **Engine type**, choose **Microsoft SQL Server**.
     ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/047c0e1c-3334-48cb-838d-5a6ef55262e6)

   - For **DB instance size**, choose **Free tier**.
     ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/f39fc304-34c6-4840-b272-772a0f8af0fa)

   - Check the box next to **Auto generate a password**.
     ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/bc5201e8-2e17-49f1-83a0-ccd17837a904)

   - Choose **Create database**.
     ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/8f986268-1250-4bc6-b51d-38a2573c78f0)

   - Your new database displays in the list of databases. The status is *Creating*.
     ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/3ad62e11-f487-48e5-841c-b282ea68cfa1)

5. In the banner at the top of the page, choose **View credential details**.
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/ecbc3e88-5d62-4712-9e32-5fe28bf1054d)

   - Your login credentials display.
6. Save the credential information to a text editor to user later in this lab.
7. To close the pop-up window, choose **Close**.


### Task 2. Download and install SQL Server Management Studio
- To connect to your RDS DB instance, you will need to download and install SQL Server Management Studio.
8. In a new browser tab or window, go to https://aka.ms/ssmsfullsetup.
9. Download the installation package to your computer.

**NOTE** : I have worked with WorkStation Instance to download the *SQL Management Studio*. Use this link to work with it : https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-100-ACCAIC-1-35050/07-lab-10-RDS/s3/readme_windows_ec2.html


### Task 3. Make your database publicly accessible
10. In the Amazon RDS console, choose the name of the SQL Server database that you created.
    - In the **Connectivity & security** section, for **Security**, notice that **Public accessibility** is currently set to **No**.
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/74927fb6-7762-4e21-a863-2bff370bbd2a)

    - To change this setting, choose **Modify** at the top of the page.
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/0bc2beda-6c10-43bd-85f3-21d8cb55d732)

11. Scroll down to the **Connectivity** section, and expand **Additional configuration**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/34cbfd41-a1ce-4138-8590-28818c8e3cc2)

12. For **Public access**, choose **Publicly accessible**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/b039a16c-7803-4f05-9ca4-ea63b1a3a8b3)

13. Scroll to the bottom of the page, and choose **Continue**.
14. In the **Scheduling of modifications** section, for **When to apply modifications**, choose **Apply immediately**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/a2e166cf-7b21-453e-a7cc-bf2571341b91)

15. Choose **Modify DB Instance**.
    - After about 30 seconds, the Status for the database changes to *Modifying*. Before continuing, wait until the status changes to *Available*.
    - **Tip:** You might need to refresh the database information. To refresh, choose the refresh icon.


### Task 4. Update your VPC security group
- By default, the virtual private cloud (VPC) default security group does not permit inbound SQL Server traffic from external sources. In this task, you will turn on inbound SQL Server connections from your IP address.
- First, get your IP address.
- In a new browser tab or window, go to https://whatismyipaddress.com/.
- Copy the **IPv4** value to a text editor to use later in this lab.
- Now, modify the security group to permit inbound SQL Server connections from your computer or the WindowsWorkstation instance.
16. Ensure that you are on the **RDS > Databases page**.
17. Choose the name of the database you created.
18. In the **Connectivity & security** section, under **VPC security groups**, choose the name of the security group.
  ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/c57c4e8e-463b-44b0-abc8-b7a89ac7313d)

    - The security group name looks similar to the following: **default (sg-a12345b6)**
19. On the **Security Groups** page, choose the **Inbound rules** tab.
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/2d38b6c1-dd7e-472f-99fe-23e70d475d20)

20. Choose **Edit inbound rules**, and choose **Add rule**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/2a2d3419-06a2-4468-a9d0-fdfd5b304a98)

21. For **Type**, choose **MSSQL**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/ce57bf64-51e1-4ede-9fa6-f1ae5e7ef153)

22. For **Source**, choose **Custom**, and enter your IP address or the IP address of the WindowsWorkstation instance in the text box.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/4973a39b-40e8-4906-8dcf-d070adb8b565)

23. Add `/32` at the end of the IP address. The full text should look similar to the following: **123.12.123.23/32**
24. Choose Save rules.


### Task 5. Connect to your DB instance
- First, you will need to find the Domain Name System (DNS) endpoint and port number for your DB instance.
25. Return to the **RDS > Databases page**.
26. Choose the name of the database you created.
27. On the **Connectivity & security** tab, copy the **Endpoint** value to a text editor.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/bedbd9ab-adee-45ea-9134-f22176009520)

    - The endpoint looks similar to the following: **sample-instance.abc2defghije.us-west-2.rds.amazonaws.com**
28. Notice the **Port** number.
    - The default port for SQL Server is 1433.
    - If your port number is different, copy that value to your text editor.
29. Open the Microsoft SQL Server Management Studio application.
    - The **Connect to Server** dialog box appears.
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/c641f79b-b61e-4491-8ade-503874d13ab2)

30. For **Server type**, choose **Database Engine**.
31. For **Server name**, enter the database endpoint value that you copied.
    - At the end of the endpoint value, add a comma ( , ) and the port number (the default port number is 1433).
    - For example, your server name should look similar to the following: **database.abc2defghije.us-west-2.rds.amazonaws.com,1433**
32. For **Authentication**, choose **SQL Server Authentication**.
33. For **Login**, enter the **username for your DB instance**.
    - This is also known as the administrator username. The default is **admin**.
34. For **Password**, enter the password that you copied for your DB instance.
    - This is also known as the administrator user password.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/2074df32-29da-44cf-9756-ad903788ae32)

35. Choose **Connect**.
    - After a few moments, you are connected to your database.
    - If the connection does not succeed, repeat Task 4 to update the default security group. When you add the inbound rule, for **Source**, choose **Anywhere** instead of **My IP**. (**Note:** Only select **Anywhere** for the purpose of this lab. This selection presents a security risk in the real world.)


### Task 6. Explore the structure of the relational database
36. Great work! You can explore the structure of the relational database by expanding the areas in the **Object Explorer** pane.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/d59d7313-9207-49c7-b588-b70c36db9b33)

    - You will see that the SQL Server has built-in system databases such as model, msdb, and tempdb. You can even create a new database if you would like to experiment more.
      
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/ff19de1b-f607-403d-bfad-8a094b9132ba)

