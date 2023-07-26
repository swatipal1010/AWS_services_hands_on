## Monitoring Services in AWS
## Creating a CloudWatch Alarm That Initiates an Amazon SNS Message
### Create an Amazon CloudWatch alarm to notify you when the account has spent over a certain amount of money. The alarm sends a message to Amazon Simple Notification Service (Amazon SNS) to send an email or text notification.

### Task 1. Create and subscribe to an SNS topic
1. Choose the **Services** menu, locate the **Application Integration** section, and choose **Simple Notification Service**.
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/c378ee25-9abf-4dd2-92d8-b8678557407d)

2. In the left navigation pane, select **Topics**.
   - **Note:** If you don't see the left navigation pane, choose the hamburger menu  icon.
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/d6a1bf8a-3415-4c58-aa3c-8801c7fd4991)

3. Select **Create topic**
   - A Topic acts as a communication channel where messages from alerts and events can be posted.
4. For **Type**, select **Standard**.
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/fc701662-7d7b-4a67-9eec-bfecb5e8b3f7)

5. For **Name**, enter `MoneyAlert`.
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/939c7d1a-b1ce-46d1-9c7b-f34bf2b55772)

6. Choose **Create topic**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/42e5912e-2130-45f5-b463-e71aa02a58ba)

   - Now, you will subscribe to that topic so when a message is posted to the topic, it will be pushed to your phone or email.
7. In the **Subscriptions** section, choose **Create subscription**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/e7f01827-abb9-4d6a-9b0e-2f05cc43dec5)

8. For **Topic ARN**, select the **MoneyAlert** topic you created.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/e6350418-8b52-480c-a5e2-0d329e0b196d)

9. For **Protocol**, select **Email** to get an email alert.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/ff3f7c38-df67-4368-b1f6-bbdbedad6045)

10. For **Endpoint**, enter your email address or phone number, depending on what you selected for **Protocol**.
11. Select **Create subscription**.
    - **Note:** A confirmation message displays at the top of the page. Make sure to **Confirm subscription** once the email is received.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/34292d28-303b-4a7d-99f1-da008d4fc499)



### Task 2. Create a CloudWatch alarm
- Now you will create the billing alert.
12. Choose the **Services** menu, locate the **Management & Governance** section, and choose **CloudWatch**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/9fabbacd-af2a-4176-b2ab-b893e64edf6b)

13. In the left navigation pane, select **Alarms**.
14. Choose **Create alarm**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/3ee70db5-b03e-462e-92ab-7c346ca1ced7)

15. Choose **Select metric**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/638c1ffa-7a64-4b8f-b751-7740ff3b87a2)

16. Select **Billing**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/bf96700b-3256-430e-bd3c-933ba181b03d)

17. Select **Total Estimated Charge**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/c9661015-5abf-4eaf-8b72-67af5388d0fa)

18. Check the box for **EstimatedCharges**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/eac8efce-f1a9-45fc-b7f3-37bb7a1cbb7c)

19. Choose **Select metric**.
20. In the **Conditions** section, configure the following:
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/699b18e7-344f-4e3b-bb71-5c6b2c88885e)

    - For **Threshold type**, select **Static**.
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/262d8f4f-ca7e-4179-a47f-d74dba5b0de4)

    - For **Whenever EstimatedCharges is…**, select **Greater**.
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/89567660-4f01-4daf-911a-8193c3c4d085)
      

    - For **than...**, enter `100` into the textbox.
      
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/9d8fd6a3-96f9-4354-9fe9-0efcfcabd267)

21. Choose **Next**.
22. In the **Notification** section, configure the following:
    - For **Alarm state trigger**, choose **In alarm**.
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/c40afe45-3d97-42a4-bf44-c61b975028ac)

    - For **Send a notification to the following SNS topic**, choose **Select an existing SNS topic**.
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/06f68059-9ef5-4fba-983b-d2bc9541bd3a)

    - For **Send a notification to...**, choose the **MoneyAlert** topic.
      ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/adc33c02-7bbc-489d-9435-7bac1754ddaf)

23. Choose **Next**.
24. For **Alarm name**, enter `MoneyAlertAlarm`.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/8ad7b2b1-d69a-4821-95ff-462300cedf5b)

25. Choose **Next**.
26. Review the settings. Scroll down and choose **Create alarm**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/eaedf3b4-6e6e-4343-9095-516f8115ab57)
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/948059e1-84e7-466d-8147-36f8432568c2)
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/54ea3e51-b119-4b63-b4cb-24f30a50149c)
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/16d29655-4328-41be-a1a6-7a4096d430c1)



- Congratulations! You have set up a CloudWatch alarm that uses Amazon SNS to send an alert when the cost of services reaches $100.




