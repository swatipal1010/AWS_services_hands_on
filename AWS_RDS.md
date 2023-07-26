## AWS Realtional Database Service (RDS)
### Task 1. Set up an RDS DB instance
1. Choose the **Services** menu, locate the **Database** category, and then choose **RDS**.
2. Choose **Create database**.
3. In the **Choose a database creation method** section, choose **Easy create**.
4. In the **Configuration** section, configure:
   - For **Engine type**, choose **Microsoft SQL Server**.
   - For **DB instance size**, choose **Free tier**.
   - Check the box next to **Auto generate a password**.
   - Choose **Create database**.
Your new database displays in the list of databases. The status is *Creating*.
5. In the banner at the top of the page, choose **View credential details**.
   - Your login credentials display.
6. Save the credential information to a text editor to user later in this lab.
7. To close the pop-up window, choose **Close**.


### Task 2. Download and install SQL Server Management Studio
- To connect to your RDS DB instance, you will need to download and install SQL Server Management Studio.
8. In a new browser tab or window, go to https://aka.ms/ssmsfullsetup.
9. Download the installation package to your computer.


### Task 3. Make your database publicly accessible
10. In the Amazon RDS console, choose the name of the SQL Server database that you created.
    - In the **Connectivity & security** section, for **Security**, notice that **Public accessibility** is currently set to **No**.
    - To change this setting, choose **Modify** at the top of the page.
11. Scroll down to the **Connectivity** section, and expand **Additional configuration**.
12. For **Public access**, choose **Publicly accessible**.
13. Scroll to the bottom of the page, and choose **Continue**.
14. In the **Scheduling of modifications** section, for **When to apply modifications**, choose **Apply immediately**.
15. Choose **Modify DB Instance**.
    - After about 30 seconds, the Status for the database changes to *Modifying*. Before continuing, wait until the status changes to *Available*.
    - **Tip:** You might need to refresh the database information. To refresh, choose the refresh icon.


### Task 4. Update your VPC security group
- By default, the virtual private cloud (VPC) default security group does not permit inbound SQL Server traffic from external sources. In this task, you will turn on inbound SQL Server connections from your IP address.
16. Ensure that you are on the **RDS > Databases page**.
17. Choose the name of the database you created.
18. In the **Connectivity & security** section, under **VPC security groups**, choose the name of the security group.
    - The security group name looks similar to the following: **default (sg-a12345b6)**
19. On the **Security Groups** page, choose the **Inbound rules** tab.
20. Choose **Edit inbound rules**, and choose **Add rule**.
21. For **Type**, choose **MSSQL**.
22. For **Source**, choose **Custom**, and enter your IP address.
23. Add `/32` at the end of the IP address. The full text should look similar to the following: **123.12.123.23/32**
24. Choose Save rules.


### Task 5. Connect to your DB instance
- First, you will need to find the Domain Name System (DNS) endpoint and port number for your DB instance.
25. Return to the **RDS > Databases page**.
26. Choose the name of the database you created.
27. On the **Connectivity & security** tab, copy the **Endpoint** value to a text editor.
    - The endpoint looks similar to the following: **sample-instance.abc2defghije.us-west-2.rds.amazonaws.com**
28. Notice the **Port** number.
    - The default port for SQL Server is 1433.
    - If your port number is different, copy that value to your text editor.
29. Open the Microsoft SQL Server Management Studio application.
    - The **Connect to Server** dialog box appears.
30. For **Server type**, choose **Database Engine**.
31. For **Server name**, enter the database endpoint value that you copied.
    - At the end of the endpoint value, add a comma ( , ) and the port number (the default port number is 1433).
    - For example, your server name should look similar to the following: **database.abc2defghije.us-west-2.rds.amazonaws.com,1433**
32. For **Authentication**, choose **SQL Server Authentication**.
33. For **Login**, enter the **username for your DB instance**.
    - This is also known as the administrator username. The default is **admin**.
34. For **Password**, enter the password that you copied for your DB instance.
    - This is also known as the administrator user password.
35. Choose **Connect**.
    - After a few moments, you are connected to your database.
    - If the connection does not succeed, repeat Task 4 to update the default security group. When you add the inbound rule, for **Source**, choose **Anywhere** instead of **My IP**. (**Note:** Only select **Anywhere** for the purpose of this lab. This selection presents a security risk in the real world.)


### Task 6. Explore the structure of the relational database
36. Great work! You can explore the structure of the relational database by expanding the areas in the **Object Explorer** pane.
    - You will see that the SQL Server has built-in system databases such as model, msdb, and tempdb. You can even create a new database if you would like to experiment more.
