# Amazon CloudWatch Setup for EC2 Instance Monitoring

This project demonstrates how to set up Amazon CloudWatch for monitoring an EC2 instance running Ubuntu, including creating alarms for CPU usage. The step-by-step guide covers installing the CloudWatch agent, configuring it, starting the service, and creating CloudWatch alarms.

---

## Project Overview

- **Operating System:** Ubuntu (on EC2)
- **Tools Used:** Amazon CloudWatch, CloudWatch Agent
- **Objective:** Monitor EC2 instance metrics and configure alarms for CPU utilization.

---

## Prerequisites

1. An Ubuntu EC2 instance with appropriate IAM role permissions attached:
   - `AmazonEC2RoleforSSM`
   - `CloudWatchAgentServerPolicy`
2. Basic knowledge of Linux commands.
3. Access to the AWS Management Console.

---

## Step-by-Step Implementation

### 1. Connect to Your EC2 Instance

ssh -i /path/to/your-key.pem ubuntu@<your-instance-public-IP>

2. Update the System:
----------------------
Ensure the instance is updated:

    sudo apt update
    sudo apt upgrade -y

3.Install the CloudWatch Agent:
-------------------------------
Download and install the Amazon CloudWatch agent:
--------------------------------------------------
sudo wget https://s3.amazonaws.com/amazoncloudwatch-agent/ubuntu/amd64/latest/amazon-cloudwatch-agent.deb
sudo dpkg -i amazon-cloudwatch-agent.deb
sudo apt install -f

4.Configure the CloudWatch Agent:
----------------------------------
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard

5.Configuration Example:
-------------------------
amazon-cloudwatch-agent.json

6.Start the CloudWatch Agent:
------------------------------
Start the agent to begin sending metrics to CloudWatch:

sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl \
    -a start \
    -c file:/opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json \
    -m ec2

7.Create a CloudWatch Alarm for CPU Usage:
-------------------------------------------
1.Log into the AWS CloudWatch Console.
2.Navigate to Alarms > Create Alarm.
3.Select the CWAgent namespace and the desired CPU metric (e.g., cpu_usage_idle).
4.Set a threshold (e.g., alarm if CPU usage is less than 20%).
5.Configure an action (e.g., send an SNS notification).
6.Name the alarm (e.g., HighCPUUsageAlarm) and complete the setup.

8.Verification:
---------------
1.Check the CloudWatch dashboard:
Navigate to Metrics > CWAgent > Per-Instance Metrics to view the collected metrics.
2.Test the alarm by simulating a high CPU load.

9.Conclusion:
-------------
By following this guide, you successfully:

1.Monitored EC2 instance metrics using CloudWatch.
2.Set up alarms to notify you of CPU usage thresholds.

10.Repository Structure:
----------------------
/
├── README.md    # Project documentation (this file)
├── amazon-cloudwatch-agent.json  # Example agent configuration




