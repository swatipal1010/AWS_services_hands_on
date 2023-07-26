## AWS Elastic Load Balancer (ELB)
### Create and configure a load balancer, register a webpage as a target for the load balancer, and test the load balancer.

### Task 1. Launch an EC2 instance
1. In the search box to the right of **Services**, search for and choose **EC2** to open the EC2 console.
2. In the left navigation pane, choose **EC2 Dashboard** to ensure you are on the dashboard page.
3. Choose the **Launch instance** button in the middle of the page, then select **Launch instance** from the dropdown menu.
4. In the *Name* and *tags* panel:
   - For *Name* enter `Web Server 1`
5. In the *Application* and *OS Images* panel:
   - For **Quick Start**, keep the default **Amazon Linux** chosen
6. In the *Instance type* panel:
   - Keep the default instance type, **t2.micro**.
7. In the *Key pair (login)* panel:
   - From the **Key pair name** - ***required*** dropdown list, choose **vockey**.
8. In the **Network settings** section, choose **Edit**.
   - From the **Subnet** dropdown list, choose the existing subnet in **Availability Zone us-east-1a**.
     ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/91456941-8dcb-456d-91a8-0d4354f09f33)

   - For **Security group name** - ***required***, enter `Web Server security group`
     ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/2bfdfe3d-5745-45fb-9545-c0d8bf02764f)

   - For **Description** - ***required***, enter `Security group for my web server`
     ![Screenshot 2023-07-26 234145](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/051ebd7f-30cc-4c0d-bc6f-080cb76c6d16)


   - In the **Inbound security groups rules** section, Select **Remove** to remove the default rule.
     
   - Choose **Add security group rule** to configure new rule as below
     ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/f3fd13cc-83d7-4d7a-b394-46f072bc3e78)

     - **Type** : HTTP
     - **Source type** : Anywhere
       ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/078184de-bb5a-4543-b2d5-c0d4b91fd17d)

9. In the _Configure storage_ panel:
    - Keep the default storage configuration.

10. Scroll down, and expand **Advanced Details** Panel, then configure:
    - Scroll down to the field **User data**.
    - Copy the following code and paste it into the **User data** field.
      ```text
      #!/bin/bash
      yum update -y
      yum -y install httpd
      systemctl enable httpd
      systemctl start httpd
      echo '<html><h1>Hello World! This is server 1.</h1></html>' > /var/www/html/index.html
      ```
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/efe903f8-d2a1-44dc-b53e-a890e8eefbea)

      - This script does the following:
        - Updates the server
        - Installs an Apache web server (httpd)
        - Configures the web server to automatically start on boot
        - Starts the web server
        - Creates a simple webpage 
11. Choose **Launch instance** .
12. On the next screen, Choose **View all instances**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/73fa8255-9e40-4487-a941-47e964aed2f0)

13. Before you continue, wait for your instance to display the following:
    - **Instance state**:  Running
    - **Status check**:  2/2 checks passed
    - **Tip**: To refresh the instance information,  choose the refresh  icon.


### Task 2. Access your EC2 instance’s website
- In this task, you will access the content from the web server on the EC2 instance that you just created.
14. Select the **Web Server 1** instance that you created earlier in this lab.
15. In the **Details** tab copy the **Public IPv4 address** of your instance, then open a new tab in your web browser and paste in and load the address.
    - It should display the web server page with the message *Hello World! This is server 1.**
    - **Note**: If web page is not displayed, ensure that you are accessing page using http:// (not https://).


### Task 3. Create a second EC2 instance for load balancing
- In this task, you will create a second EC2 instance so that you will later be able to configure load balancing between the two instances.
16. Return to the **EC2 Management Console** browser tab.
17. Select the **Web Server 1** instance.
18. From the **Actions** menu, choose Images and templates****, then choose **Launch more like this**
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/4de188b5-1924-4916-ada7-3c269283fecc)

    - A **Launch an instance** page opens.
19. In the **Name and tags** pane, change the Name to `Web Server 2`.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/19c936a3-1315-4e91-b116-0ff78acf48ac)

20. In the **Key pair (login)** section, from the **Key pair name** - ***required*** dropdown list, choose **vockey**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/a0da4e90-e6e0-451b-ab59-b0a5f9e6e9cf)

21. From the **Subnet** dropdown list, choose the existing subnet in **Availability Zone us-east-1b.**
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/0df784d5-332d-42a2-a73d-40a4fcb7582b)

22. Scroll down, and expand the **Advanced Details** section, then scroll down to the **User data** field.
23. Use copy and paste to replace the existing code with the code shown below.
    ```text
    #!/bin/bash
    yum update -y
    yum -y install httpd
    systemctl enable httpd
    systemctl start httpd
    echo '<html><h1>Hello World! This is server 2.</h1></html>' > /var/www/html/index.html
    ```
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/944a039f-52a1-429b-add7-c3513ada0d13)

    - **Note**: This script is almost the same as the one that you used for the first instance. However, notice that it says *This is server 2*. The text that displays when you access Web Server 2 will be different than the text of Web Server 1. When you access the instances through the load balancer, this difference in text is how you will know which instance is displayed.
24. Choose **Launch instance** .
25. On the next screen, Choose **View all instances**.
26. Before you continue, wait for your instance to display the following:
    - **Instance state**:  Running
    - **Status check**:  2/2 checks passed
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/6ae03054-a31b-4c52-8971-ffa1318b7023)

    - **Tip**: To refresh the instance information, choose the refresh  icon.


### Task 4. Access the website on the second EC2 instance
27. Select the **Web Server 2** instance.
28. In the **Details** tab copy the **Public IPv4 address** of your instance, then open a new tab in your web browser and paste in and load the address.
29. This will open a new tab in your web browser and display the web server page with the message _Hello World! This is server 2_.
    - Make a note of the _Availability Zones_ where the **Web Server 1** and **Web Server 2** instances are running. For example, **us-east-1a** and **us-east-1b**. You will need this information in the next task.


### Task 5. Create a load balancer
30. Back in the EC2 console, in the left navigation pane, under **Load Balancing**, choose **Load Balancers**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/58ae5ee0-2716-4be5-b151-bdb7a57e288b)

31. Select **Create Load Balancer**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/73df8e6d-c7ca-4d45-9f56-19769595cdc1)

    - **Tip**: An _Application Load Balancer_ has many features and can be used for HTTP and HTTPS traffic.
32. Under **Application Load Balancer**, choose **Create**.
33. In the _Basic Configuration_ panel:
    - For **Name**, enter `myloadbalancer`.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/8fd644d9-fcd6-44a8-8ee1-56428a098bf6)

34. In the _Network mapping_ panel:
    - Under Mappings, select the **Availability Zones** that you created the two instances in.
    - For example, **us-east-1a** and **us-east-1b**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/8181d1be-515e-4820-b87c-454d595d59a8)

    - **Note**: The Subnet to use in each selected Availability Zone will be automatically populated.
35. In the _Security Groups_ panel:
    - Choose **Web Server security group** from the drop down menu.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/602540f0-bd6e-4a56-8f51-4ded752224f8)

    - After you close the drop down menu, choose the **X** next to the **default security group** to remove it.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/0c05dfc6-9c4c-483d-9c0f-263844bbbe07)
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/198f7ad9-d453-476a-b15d-e5b58838c7ee)

36. In the _Listeners_ and _routing_ panel:
    - Choose **Create target group**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/7e5bf5d4-4b8c-416b-8acf-e58c183d7031)

    - This will open a new tab in your browser.
37. In the _Basic Configuration_ panel:
    - Keep the target type set to **Instances**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/eb4a5a3b-c454-4cfc-bebf-f6df66d0c762)

    - For **Target group name** enter `myalbTG`
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/f92e5a09-7c49-4138-b91f-3dc56046a0c7)

38. In the _Health checks_ panel:
    - For **Health check path**, enter `index.html` after the forward slash ( / )
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/a40411ff-2d34-440a-9c78-c17f9f28d5ca)

    - The path should look like the following: `/index.html`
39. Choose **Next**.
40. In the **Register targets** page, in the **Available instances** panel, check the boxes next to the **Web Server 1** and **Web Server 2** instances that you created in this lab.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/12698e7c-bfd3-4c7c-a556-50c47892d7d0)

41. Choose **Include as pending below**.
    - Verify that both instances now appear in the **Targets** list below.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/30e3cb51-64d6-4a41-afa9-203fb232ca14)

42. Choose **Create target group**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/c4907cfb-9e36-43a5-9058-be82d3e48f12)

    - A banner displays the message that the target group was successfully created.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/f920c4c6-6cbe-4170-a751-a7e49c6910d8)

43. Return to the **Load Balancers** console tab in the browser.
44. In the **Listeners and routing** section, under **Listener** choose the **refresh icon** .
45. From the dropdown, chose the **myalbTG** target group you created.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/fddad1f5-34d3-445a-b07d-a42271127262)

46. Scroll down and chose **Create load balancer**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/8a0a9212-069f-4ea7-8e26-f0c7aa255dc0)

    - When the load balancer is created, a _Successfully created load balancer_ message displays.
47. Choose **View load balancer**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/e3d393f4-56af-438a-95a1-abdd10f0a139)

    - Before continuing, ensure that the **State** of the load balancer that you just created changes to _Active_.
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/a353ce9a-80ed-4a77-981e-eba064b0923d)

    - It can take a few minutes for it to become active.
    - **Tip**: To refresh the load balancer information, choose the refresh  icon.


### Task 6. Test the load balancer
- In this task, you will test the load balancer that you just created.
48. Select the load balancer that you just created, and expand the **Details** section.
49. Under **Details**, copy the **DNS name** value to your clipboard.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/d00cd710-6ba1-4bda-8a2f-c1a372e66475)

50. Open a new tab in your web browser, paste the DNS name that you just copied, and press **Enter**.
    - If your load balancer is working, the _Hello World!_ message displays. Notice whether the message says _This is server 1_ or _This is server 2_.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/1be8acd0-3fe4-4386-8a67-bd6ab17eb658)

51. Refresh the browser tab a few times.
    - Notice when the message changes between _This is server 1_ and _This is server 2_. When the message changes, it means that the load balancer has directed you to the web server on the other EC2 instance that you created in this lab.
      
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/cde87b5c-3a08-4b44-85b9-e3fef251d4a5)

 
