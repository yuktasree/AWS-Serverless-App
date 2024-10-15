# AWS-Serverless-App

This project demonstrates a serverless architecture using various AWS services to automate email reminders. The solution leverages Amazon Simple Email Service (SES), AWS Lambda, Amazon API Gateway, and AWS Step Functions to create a fully cloud-based workflow. The application runs in the browser, loading from an S3 bucket, and communicates with backend services via an API Gateway. Users can configure reminders for tasks such as ‘pet cuddles’, which are sent via email using SES, triggered by a state machine.

Architecture Diagram:

![image](https://github.com/user-attachments/assets/22fba4e1-3fc7-4fda-b4d7-048503693637)


In Stage 1 of the Pet-Cuddle-O-Tron application setup, we verify two email addresses to be used with Amazon Simple Email Service (SES), which starts in sandbox mode to prevent unverified email usage. First, we verify the sending email address (used by the application to send reminders), by adding it in the SES console and confirming the email verification link. Next, we repeat the process to verify the customer email address (used for testing purposes). Both addresses are now whitelisted, enabling the application to send email reminders during testing and later stages of the demo.

<img width="1231" alt="image" src="https://github.com/user-attachments/assets/f6a76bb5-a41b-4f2d-87b4-de9d6de2ff57"> <br>

In Stage 2 of the Pet-Cuddle-O-Tron setup, we create and configure the email_reminder_lambda function, which will send email reminders using Amazon SES. First, an IAM execution role is created via CloudFormation to grant Lambda permissions to interact with SES, SNS, and CloudWatch logs. Then, we create the email_reminder_lambda function using Python in the AWS Lambda console. The function is configured to send emails, and the sender address (from Stage 1) is specified in the function code. Finally, we deploy the function, completing the configuration for sending emails on behalf of the application.

<img width="1231" alt="image" src="https://github.com/user-attachments/assets/a67464f9-be4a-467e-9231-7f8f6e0cd48f"> <br>
<img width="1231" alt="image" src="https://github.com/user-attachments/assets/306c2f09-e034-41cc-a6eb-7e79c2e0c744"> <br>

In Stage 3 of the Pet-Cuddle-O-Tron setup, we create and configure the state machine, which manages the workflow of the serverless application. First, we create an IAM role using CloudFormation, which allows the state machine to interact with AWS services like Lambda, SNS, and CloudWatch Logs. Next, we build the state machine in AWS Step Functions using a predefined Amazon States Language (ASL) workflow that handles timer-based email reminders. The state machine invokes the previously created email_reminder_lambda function to send emails at scheduled intervals. Once the state machine is configured with the correct permissions, it is ready to coordinate AWS services and manage the flow of the serverless application.

<img width="1231" alt="image" src="https://github.com/user-attachments/assets/27a8171c-c1e2-49d3-8309-8136c46a35ab"> <br>
<img width="1231" alt="image" src="https://github.com/user-attachments/assets/bbe9eeea-351d-46df-bd31-fa048cfb55a3"> <br>
<img width="1228" alt="image" src="https://github.com/user-attachments/assets/a710cad9-5aff-4adf-b2da-74bd4ff470f5"> <br>

In Stage 4 of the Pet-Cuddle-O-Tron setup, we configure the API Lambda function and create the necessary API Gateway to enable communication between the client-side application and AWS services. First, we create the api_lambda function, which is triggered by API Gateway to initiate the state machine execution, handling the core logic of the application. Next, we set up the API Gateway, defining the API, resources, and methods to handle requests from the client. The API Gateway is linked to the api_lambda function for processing these requests. Finally, the API is deployed to the prod stage in API Gateway, generating an Invoke URL that will be used by the client-side component of the serverless application to interact with the system.

<img width="1228" alt="image" src="https://github.com/user-attachments/assets/89eb95d1-81a9-4e2f-b622-2a68e7dbf59b"> <br>
<img width="1228" alt="image" src="https://github.com/user-attachments/assets/64304ce8-f1b9-46fb-a76e-cdb6110f9e47"> <br>
<img width="1228" alt="image" src="https://github.com/user-attachments/assets/57da5f59-3dbc-4410-abc2-aa8ec8a9e894"> <br>
<img width="1228" alt="image" src="https://github.com/user-attachments/assets/45fe4ded-07c5-41be-952c-81bc1531e767"> <br>
<img width="1228" alt="image" src="https://github.com/user-attachments/assets/8b0504ae-fcb0-47c2-984b-dc57a77e9c33"> <br>

In Stage 5 of the Pet-Cuddle-O-Tron setup, we create and configure the S3 bucket to host the static website for the serverless application. First, we create an S3 bucket and make it public, allowing access to the website files. Next, we enable static website hosting on the bucket and upload the front-end files, including index.html, main.css, whiskers.png, and serverless.js. The JavaScript file is updated to include the API Gateway Invoke URL, which enables communication between the static website and the serverless backend. Once the files are uploaded, the application can be tested by entering the required parameters (time, message, and email address), triggering the state machine through API Gateway, and watching the serverless workflow execute in Step Functions. At this point, the fully functional serverless application is running with no servers involved, completing the Pet-Cuddle-O-Tron setup.

<img width="1228" alt="image" src="https://github.com/user-attachments/assets/855b34b1-cd94-4d19-9b19-8e3e7bb8dee2"> <br>
<img width="1228" alt="image" src="https://github.com/user-attachments/assets/5d0e08d6-3be2-4d16-a781-044c1bb378a4"> <br>
<img width="1228" alt="image" src="https://github.com/user-attachments/assets/b46627a8-e663-467e-804e-7e8222334f83"> <br>
<img width="1228" alt="image" src="https://github.com/user-attachments/assets/2288e23c-1dab-4d69-a500-be73f8d24dda"> <br>

At the end of this setup, we have a fully functional serverless application that runs entirely on AWS services without the need for any servers. No servers were harmed—or even used—in this production, justifying the true power and scalability of serverless architecture!

<img width="1512" alt="image" src="https://github.com/user-attachments/assets/7f22c17d-047c-42b8-97fc-9146d16e3dc4"> <br>
<img width="1512" alt="image" src="https://github.com/user-attachments/assets/22050cb0-6124-4466-afbf-21b432672e5b"> <br>
<img width="1224" alt="image" src="https://github.com/user-attachments/assets/99a25a70-0575-4675-b133-e57d0f3d19a4"> <br>
<img width="1041" alt="image" src="https://github.com/user-attachments/assets/ce37c014-c8e1-4367-b711-1e1ac7916604"> <br>
<img width="1230" alt="image" src="https://github.com/user-attachments/assets/ce19c886-a0fd-4baa-902a-b84b634ad80f"> <br>
<img width="1230" alt="image" src="https://github.com/user-attachments/assets/06573259-2749-487f-9270-d81be5cfd2ec"> <br>
<img width="1230" alt="image" src="https://github.com/user-attachments/assets/105ec049-ff5e-4072-869b-0fe82629c09f"> <br>
<img width="1254" alt="image" src="https://github.com/user-attachments/assets/f0fec40e-2f96-4d67-8f29-0c9bca2e252d"> <br>

