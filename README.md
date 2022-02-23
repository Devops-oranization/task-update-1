# task-update-1
How to start and stop Ec2 instances using Lambda function

I have created AMI using Lambda function, also I have automated the process using CloudWatch

Create new policy 

 ![image](https://user-images.githubusercontent.com/89199956/155272441-af248f4b-a535-4d66-881f-65ae9fbea53b.png)

Click the JSON and remove JSON format Enter new formate click next 
![image](https://user-images.githubusercontent.com/89199956/155272483-9b78e518-914b-43f7-87e2-0570fd482e32.png)

 
Enter the Policy name and save it
![image](https://user-images.githubusercontent.com/89199956/155272499-5fb6cac1-9619-4edb-8fe0-394a5113900d.png)

 
Policy is added
![image](https://user-images.githubusercontent.com/89199956/155272519-30232f40-de9c-445c-876f-6fd554d6e7b0.png)

 

Now I am going to create IAM roles and select the Lambda and click the next 
![image](https://user-images.githubusercontent.com/89199956/155272536-36a221d6-afe4-4c1a-b7e0-fc500b09391c.png)

  



. Select the lambda
![image](https://user-images.githubusercontent.com/89199956/155272559-39c2c708-8423-43c4-911e-8637f5f0a5b9.png)

 
Please select the permissions policies startstopinstance click next 

 ![image](https://user-images.githubusercontent.com/89199956/155272582-e55acb5b-64f7-41ed-a971-eba70211d857.png)








And give the name of the role details click next 
![image](https://user-images.githubusercontent.com/89199956/155272619-f7990c56-5048-43a1-b945-ea9035a42c4b.png)


 
 
Now my role is created 
![image](https://user-images.githubusercontent.com/89199956/155272643-1f30a3ed-8a8a-4fac-8907-8e771e94a2cd.png)

 


Now I’m going to create lambda service
![image](https://user-images.githubusercontent.com/89199956/155272661-3284cf29-b6ed-4814-8640-eaf309a766ce.png)

 




Create lambda functions enter the name and select the python 3.7 here we select the existing role startinstancenew
![image](https://user-images.githubusercontent.com/89199956/155272679-0d1b0c05-6ace-415c-ab6a-e6dcf6d1e690.png)
![image](https://user-images.githubusercontent.com/89199956/155272719-5a45889c-24c2-4cd3-b31a-9e6c8ece3341.png)
![image](https://user-images.githubusercontent.com/89199956/155272727-db194376-cfc3-4f49-a0c8-504fbbc8a14d.png)


 

 


 

Please remove script 
![image](https://user-images.githubusercontent.com/89199956/155272783-0e96f171-0ad3-489c-9867-4830ea76c550.png)


 
Please go to the ec2 instance 
![image](https://user-images.githubusercontent.com/89199956/155272796-70cf0d76-01dd-44e2-b570-e05149f933b8.png)

 
I copy the two ec2 instance id and regions. Go to the script
And paste here both ids and region here and click on deploy after click the test and enter the name and save it. again click the test .
 ![image](https://user-images.githubusercontent.com/89199956/155272959-757fcdad-006f-4343-b24e-ff8f583f604a.png)
![image](https://user-images.githubusercontent.com/89199956/155272969-44026f9b-852c-4b27-81f9-401f74bddf47.png)


 
Now I’m going to check my ec2 instance start or not 
![image](https://user-images.githubusercontent.com/89199956/155273034-00a9e38b-ad38-4f2f-bbb4-226aa6d0fb7e.png)

 





Again I go create stop instance in lambda service.
![image](https://user-images.githubusercontent.com/89199956/155273155-4b9b7727-a610-45ba-9807-052ee5599ca5.png)
![image](https://user-images.githubusercontent.com/89199956/155273183-ec131e59-7170-4067-9da1-10dff0c71af5.png)

 

 

Please remove the script 
![image](https://user-images.githubusercontent.com/89199956/155273202-6530ac16-a4ce-4e44-abbc-458287f40acb.png)

 

I copy the two ec2 instance id and regions. Go to the script
And paste here both ids and region here and click on deploy after click the test and enter the name and save it. again click the test .
![image](https://user-images.githubusercontent.com/89199956/155273221-ca2d3e43-fdd2-4816-8ac3-9611a2ae9904.png)
![image](https://user-images.githubusercontent.com/89199956/155273274-41ac758e-c585-4b1e-9275-b13b51bc40b5.png)

 


 

Here automatically system was  stoped
![image](https://user-images.githubusercontent.com/89199956/155273309-42a45b21-a04e-49b0-8303-3c2de14a780f.png)

 
====================================================
Python scripts 

jason
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "logs:CreateLogGroup",
        "logs:CreateLogStream",
        "logs:PutLogEvents"
      ],
      "Resource": "arn:aws:logs:*:*:*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "ec2:Start*",
        "ec2:Stop*"
      ],
      "Resource": "*"
    }
  ]
}
----------------------------------------------------------------------------------





stop
import boto3
region = 'ap-south-1'
instances = ['i-070ce588ad11318ec']
ec2 = boto3.client('ec2', region_name=region)

def lambda_handler(event, context):
    ec2.stop_instances(InstanceIds=instances)
    print('stopped your instances: ' + str(instances))
----------------------------------------------------------------------------------
start
import boto3
region = 'ap-south-1'
instances = ['i-12345', 'i-2345']
ec2 = boto3.client('ec2', region_name=region)

def lambda_handler(event, context):
    ec2.start_instances(InstanceIds=instances)
    print('started your instances: ' + str(instances))

	





Now I’m going to create cloudwatch 
![image](https://user-images.githubusercontent.com/89199956/155273352-efb3615e-d83f-428d-a84d-03c6d62eb0f7.png)

 
Click Rules
![image](https://user-images.githubusercontent.com/89199956/155273377-f56461ad-2ca3-444e-b004-17a834e52c1b.png)

 
Click Back cloudwatch Events
![image](https://user-images.githubusercontent.com/89199956/155273388-c72c644a-2e72-4a55-b77c-3c767692e148.png)

 
Create rule
![image](https://user-images.githubusercontent.com/89199956/155273407-1cf817c5-a90c-4c9f-a4cf-8750992cba50.png)

 
Here we select the schedule click the cron expression and click left side add target it will display select the lambda function 
And select the lambdstart and save it.
![image](https://user-images.githubusercontent.com/89199956/155273418-24b9dd0d-c89c-4dea-9339-5c4c26ef353d.png)

 
Here we giving the name and description 
 ![image](https://user-images.githubusercontent.com/89199956/155273435-29796d47-acc7-4f38-bc15-f14fbfd364bb.png)
![image](https://user-images.githubusercontent.com/89199956/155273494-1568402f-138f-49cd-bb90-6956cf7ecb76.png)

 
Now again we creating stop rule click on create rule.
![image](https://user-images.githubusercontent.com/89199956/155273509-7faa4640-a1d9-428f-be48-650a6345885c.png)
![image](https://user-images.githubusercontent.com/89199956/155273524-44241594-7499-4bbc-a8da-e3b7028317d5.png)
![image](https://user-images.githubusercontent.com/89199956/155273544-fb317713-fe21-498e-8f4f-904ded93684c.png)

 
 
 
This way lambda creating the ec2 machine we start or stop 

