## AWS PRICING CALCULATOR
### Use the AWS Pricing Calculator to estimate the cost of using Amazon Web Services (AWS).

### Lab steps
1. Navigate to the calculator at https://calculator.aws/ and choose **Create estimate**.
2. Recognize how the calculator console is organized.
   - To use the calculator, you select a service (labeled as _step 1_ on the left) and then you configure the service (_step 2_).
   - You can create an estimate that accounts for the use of multiple AWS services. As you add and configure different services, the upfront cost, monthly cost, and total 12 month cost estimate will be displayed at the bottom of the screen.

- Create a pricing estimate, based on the following scenario:
3. You would like to run a Linux EC2 instance of type t2.medium for an average of 8 hours per day, 7 days per week, in the us-west-2 region. You do not want to pay any upfront costs for it.
4. You would also like to store 60 GB of data in an S3 bucket in the us-west-2 region, using standard S3 storage. You anticipate that there will be 100 requests per month to access the data from the internet.
5. Create the EC2 cost estimate. Configure as described:
   - Keep **Search by location** type chosen.
   - Choose a location type: **Region**
   - Choose a Region: **US West (Oregon)**
   - Find Service: Type in `ec2` and then in the list of filtered results below, in the **Amazon EC2** box, choose **Configure**.
   - A  _Configure Amazon EC2_ screen appears. Configure the details:
     - Description: `on demand EC2 instance`
     - Operating system: **Linux**
     - Number of instances: `1`
     - Search instance type: search for and select the `t2.medium` type.
     - In the _Payment options_ screen, choose **On-Demand**. Then set the details:
       - Usage: `8 `
       - Usage type: `Hours / Day`
       - Choose **Save and add service**.
- Notice that the _Upfront cost_ is $0.00 USD, because you chose the On-Demand payment option. Also notice that the _Monthly cost and Total 12 month cost_ now include the estimated cost of running the EC2 instance, based on the details you provided.
6. Create the S3 cost estimate. Configure as described:
  - In the **Find Service** search area, type in `S3` then in the list of filtered results below, in the _Amazon Simple Storage Service (S3)_ box, choose **Configure**.
  - Description: `data storage`
  - For storage class, keep both **S3 Standard** and **Data Transfer** selected.
  - S3 Standard storage: `60` GB per month
  - Keep _The specified amount of data is already stored in S3 Standard_ selected.
  - in the _GET, SELECT, and all other requests from S3 Standard_ field, enter `100`
  - In the Data Transfer area, for **Outbound Data Transfer**, choose **Data transfer to Internet** and set the amount to `3` GB per month.
  - Choose **Save and view summary**.
- Notice that you now have two line items in your estimate. One line shows the cost for the EC2 instance and the other line shows the cost for S3 storage.
7. Add the cost of a basic AWS support plan to the estimate.
   - Choose **Add support**.
   - Description: `basic support`
   - Keep the other defaults, including **Basic support plan** selected.
- **Tip**: Notice the price differences between the different support plans listed.
   - Choose **Add to my estimate**.
- Notice that the estimated cost of the basic support plan added $0.00 to the total cost estimate. If you had chosen a higher level of support, there would be a cost associated with it.
8. Export the estimate.
  - Choose the **Export** menu and then select the format you would like to export as. For example, choose **PDF**.
  - In the dialog that appears, choose **OK** and optionally save the estimate to your computer.
- As you can see, the AWS Pricing Calculator offers a set of features that can be used create an estimate for what your use of AWS services will likely cost when you know which services you will be using and how you plan to use them. 
