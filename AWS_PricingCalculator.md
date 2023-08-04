## AWS PRICING CALCULATOR
### Use the AWS Pricing Calculator to estimate the cost of using Amazon Web Services (AWS).

### Lab steps
1. Navigate to the calculator at https://calculator.aws/ and choose **Create estimate**.
   ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/7a07378a-f8fa-4415-bfba-d5f0560e1557)

2. Recognize how the calculator console is organized.
   - To use the calculator, you select a service (labeled as _step 1_ on the left) and then you configure the service (_step 2_).
     ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/b1f49bed-429a-4e23-b669-fe03f043a3ab)

   - You can create an estimate that accounts for the use of multiple AWS services. As you add and configure different services, the upfront cost, monthly cost, and total 12 month cost estimate will be displayed at the bottom of the screen.

- Create a pricing estimate, based on the following scenario:
3. You would like to run a Linux EC2 instance of type t2.medium for an average of 8 hours per day, 7 days per week, in the us-west-2 region. You do not want to pay any upfront costs for it.
4. You would also like to store 60 GB of data in an S3 bucket in the us-west-2 region, using standard S3 storage. You anticipate that there will be 100 requests per month to access the data from the internet.
5. Create the EC2 cost estimate. Configure as described:
   - Keep **Search by location** type chosen.
     
     ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/ff4014d4-e098-46df-9347-549273a74ed0)
  

   - Choose a location type: **Region**
     
     ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/a8ae1857-08b8-4844-a3a6-27b93c027ca7)
     

   - Choose a Region: **US West (Oregon)**
     
     ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/80a5b831-14a3-4a09-982d-df7b049814fd)
  

   - Find Service: Type in `ec2` and then in the list of filtered results below, in the **Amazon EC2** box, choose **Configure**.
     
     ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/44680d99-13c2-43a5-936d-9aa01c188738)
     

   - A  _Configure Amazon EC2_ screen appears. Configure the details:
     
     ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/17a7d15e-7c6d-4a24-9195-5d4618fbdd5a)
     

     - Description: `on demand EC2 instance`
       
       ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/b697f342-4b59-4fbf-91da-7acb26a31876)
       

     - Operating system: **Linux**
       
       ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/3e0e4132-0091-4ed1-bbd4-26c28f11c458)
       

     - Number of instances: `1`
       
       ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/42a17253-b75a-4781-a382-2333efc6d77b)
     

     - Search instance type: search for and select the `t2.medium` type.
       
       ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/de876801-5226-459a-bc3b-fc2ef5a91571)
       ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/ecf83f85-15f1-4b3b-b270-367a097e025f)
       

     - In the _Payment options_ screen, choose **On-Demand**. Then set the details:
       
       ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/d3efc642-56c0-49fe-a7b2-51a0c6ef5e0b)
       

       - Usage: `8 `
         
         ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/0db7b077-9d6d-4524-8823-39f34b3d30e4)
       

       - Usage type: `Hours / Day`
         
         ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/38196e32-9d1f-4a2e-8003-7db804e16cd5)
         

       - Choose **Save and add service**.
- Notice that the _Upfront cost_ is $0.00 USD, because you chose the On-Demand payment option. Also notice that the _Monthly cost and Total 12 month cost_ now include the estimated cost of running the EC2 instance, based on the details you provided.
  
  ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/7885967e-b335-4261-ac0c-850fcd367acb)

6. Create the S3 cost estimate. Configure as described:
  - In the **Find Service** search area, type in `S3` then in the list of filtered results below, in the _Amazon Simple Storage Service (S3)_ box, choose **Configure**.
    
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/357f25db-92e4-4c81-adad-b53c7434753e)
    

  - Description: `data storage`
    
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/0de5e1c2-5563-43bb-8757-040ab81afc8f)
    

  - For storage class, keep both **S3 Standard** and **Data Transfer** selected.
    
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/4dd77b10-4d50-49fd-a7ce-1ccff2ae2d98)
    

  - S3 Standard storage: `60` GB per month
    
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/d3282dd8-0719-49b7-b0fd-485860abcfcf)
    

  - Keep _The specified amount of data is already stored in S3 Standard_ selected.
    
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/7b0e034a-6fc4-4b94-8b68-c6c300942170)
    

  - in the _GET, SELECT, and all other requests from S3 Standard_ field, enter `100`
    
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/bab2d37d-1110-4134-b648-4f46d6f23859)
    

  - In the Data Transfer area, for **Outbound Data Transfer**, choose **Data transfer to Internet** and set the amount to `3` GB per month.
    
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/25b29c7f-6796-4896-8195-ff0c343120f4)
    

  - Choose **Save and view summary**.
    
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/996ec271-cc46-4921-9139-389351c18e07)
    

- Notice that you now have two line items in your estimate. One line shows the cost for the EC2 instance and the other line shows the cost for S3 storage.
  
7. Add the cost of a basic AWS support plan to the estimate.
   - Choose **Add support**.
     
     ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/0d173d93-d840-4db3-b778-58fb84d3db5a)
     

   - Description: `basic support`
     
     ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/594b29ff-c84f-484e-bef3-e7c97c8dd1c0)
     

   - Keep the other defaults, including **Basic support plan** selected.
     
     ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/63fa9154-14df-4ec1-8fe6-1c28ff373c8d)
     

- **Tip**: Notice the price differences between the different support plans listed.
   - Choose **Add to my estimate**.
- Notice that the estimated cost of the basic support plan added $0.00 to the total cost estimate. If you had chosen a higher level of support, there would be a cost associated with it.
  
  ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/db03ade4-12d2-4d8f-a4d8-6c9bf851793f)
  

8. Export the estimate.
  - Choose the **Export** menu and then select the format you would like to export as. For example, choose **PDF**.
    ![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/1ba7ed06-256a-4b53-b9f3-ffafa8773664)

  - In the dialog that appears, choose **OK** and optionally save the estimate to your computer.
- As you can see, the AWS Pricing Calculator offers a set of features that can be used create an estimate for what your use of AWS services will likely cost when you know which services you will be using and how you plan to use them.
![image](https://github.com/swatipal1010/AWS_services_hands_on/assets/110754474/b3534d4a-9039-48ee-956d-fbf282c57efe)

