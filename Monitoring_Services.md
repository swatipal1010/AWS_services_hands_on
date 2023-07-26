## Monitoring Services in AWS
## Creating a CloudWatch Alarm That Initiates an Amazon SNS Message
### Create an Amazon CloudWatch alarm to notify you when the account has spent over a certain amount of money. The alarm sends a message to Amazon Simple Notification Service (Amazon SNS) to send an email or text notification.

### Task 1. Create and subscribe to an SNS topic
1. Choose the **Services** menu, locate the **Application Integration** section, and choose **Simple Notification Service**.
2. In the left navigation pane, select **Topics**.
   - **Note:** If you don't see the left navigation pane, choose the hamburger menu  icon.
3. Select **Create topic**
   - A Topic acts as a communication channel where messages from alerts and events can be posted.
4. For **Type**, select **Standard**.
5. For **Name**, enter `MoneyAlert`.
6. Choose **Create topic**.
   - Now, you will subscribe to that topic so when a message is posted to the topic, it will be pushed to your phone or email.
7. In the **Subscriptions** section, choose **Create subscription**.
8. For **Topic ARN**, select the **MoneyAlert** topic you created.
9. For **Protocol**, select **Email** to get an email alert.
10. For **Endpoint**, enter your email address or phone number, depending on what you selected for **Protocol**.
11. Select **Create subscription**.
    - **Note:** A confirmation message displays at the top of the page. Make sure to **Confirm subscription** once the email is received.


### Task 2. Create a CloudWatch alarm
- Now you will create the billing alert.
12. Choose the **Services** menu, locate the **Management & Governance** section, and choose **CloudWatch**.
13. In the left navigation pane, select **Alarms**.
14. Choose **Create alarm**.
15. Choose **Select metric**.
16. Select **Billing**.
17. Select **Total Estimated Charge**.
18. Check the box for **EstimatedCharges**.
19. Choose **Select metric**.
20. In the **Conditions** section, configure the following:
    - For **Threshold type**, select **Static**.
    - For **Whenever EstimatedCharges is…**, select **Greater**.
    - For **than...**, enter `100` into the textbox.
21. Choose **Next**.
22. In the **Notification** section, configure the following:
    - For **Alarm state trigger**, choose **In alarm**.
    - For **Send a notification to the following SNS topic**, choose **Select an existing SNS topic**.
    - For **Send a notification to...**, choose the **MoneyAlert** topic.
23. Choose **Next**.
24. For **Alarm name**, enter `MoneyAlertAlarm`.
25. Choose **Next**.
26. Review the settings. Scroll down and choose **Create alarm**.

- Congratulations! You have set up a CloudWatch alarm that uses Amazon SNS to send an alert when the cost of services reaches $100.




