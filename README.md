# 🚀 EC2 Monitoring with CloudWatch & SNS (Auto Stop on High CPU) 




**This project demonstrates how to:**




Launch an Ubuntu EC2 instance


Create an SNS Topic with Email Subscription


Configure a CloudWatch Alarm


Monitor CPU Utilization


Automatically Stop EC2 instance when CPU > 20%


Generate CPU load using stress command




🛡️ Services Used


Amazon EC2


Amazon SNS


Amazon CloudWatch




🎯 Learning Outcome


Understand CloudWatch Metrics


Configure SNS Notifications


Automate EC2 actions


Monitor Infrastructure Health


Simulate CPU stress testing




🏗️ Architecture Overview


EC2 Instance → CloudWatch Alarm → SNS Email Notification → Auto Stop EC2




🖥️ Step 1: Create EC2 Instance


Go to AWS Console → EC2


Click Launch Instance


Instance Name:


monitor_ec2


AMI: Ubuntu


Instance Type: t2.micro (Free tier eligible)


Create / Select Key Pair


Configure Security Group (Allow SSH - Port 22)


Launch Instance


After launch, copy the Instance ID.




📢 Step 2: Create SNS Topic & Subscription


Go to AWS Console → SNS


Create Topic


Name:


ec2_monitor


Type: Standard




Create Topic


Create Email Subscription


Open created topic


Click Create Subscription


Protocol: Email


Endpoint: Your Email Address


Click Create Subscription


📩 Go to your email and click Confirm Subscription




🔐 Change Access Policy 


Edit Access Policy to allow CloudWatch to publish messages:




Example policy:



```       
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowCloudWatchPublish",
      "Effect": "Allow",
      "Principal": {
        "Service": "cloudwatch.amazonaws.com"
      },
      "Action": "SNS:Publish",
      "Resource": "arn:aws:sns:us-east-1:975050016558:YOUR_TOPIC_NAME"
    }
  ]
}
  
  ```




📊 Step 3: Create CloudWatch Alarm


Go to AWS Console → CloudWatch → Alarms → Create Alarm


Select Metric


Choose EC2


Select Per-Instance Metrics


Paste EC2 Instance ID


Select:


CPUUtilization




Specify Metric & Conditions


Statistic: Average


Period: 5 Minutes


Condition:


Greater than 20




Configure Actions


🔔 SNS Notification


Select existing topic:


ec2_monitor


🛑 EC2 Action


Add Action:


Stop this instance




Alarm Details


Alarm Name:


EC2_CPU_Utilization_Alarm


Description:


Stop EC2 instance if CPU utilization exceeds 20% for 5 minutes.


Create Alarm ✅



🔗 Step 4: Connect to EC2




🔥 Step 5: Increase CPU Utilization


```  sudo stress --cpu 4 --timeout 600 ```


This will:


Use 4 CPU workers


Run for 600 seconds (10 minutes)


Trigger CloudWatch Alarm


Send Email Notification


Automatically Stop EC2 Instance




📬 Expected Output


SNS Email received when CPU > 20%


EC2 Instance state changes to Stopped


Alarm state changes to In Alarm




👨‍💻 Author


Sairaj Patil 

