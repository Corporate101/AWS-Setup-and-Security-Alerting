# AWS-Setup-and-Security-Alerting
<h2>Index</h2>
<ul>
<li>Project Overview</li>
<li>Objectives</li>
<li>Project Steps</li>
<li>Results & Key Takeaways</li>
</ul>

<h2>Project Overview</h2>
This project involved setting up an AWS Free Tier account and implementing security alerting mechanisms using AWS CloudTrail, SNS, and EventBridge. The primary goal was to monitor and receive notifications whenever the AWS root user performed a GetCallerIdentity API call, which can indicate unauthorized access attempts or security breaches.

<h2>Objectives</h2>
<ul>
<li>Set up an AWS Free Tier account for cloud-based experiments.</li>
<li>Configure CloudTrail to log AWS API activity.</li>
<li>Use Amazon SNS (Simple Notification Service) to send email alerts.</li>
<li>Set up Amazon EventBridge to trigger alerts on root user actions.</li>
<li>Test the setup using AWS CLI to confirm functionality.</li>
</ul>

<h2>Technologies Used</h2>
<ul>
<li>AWS CloudTrail:Tracks API calls and logs events.</li>
<li>Amazon SNS: Sends notifications to subscribed users.</li>
<li>Amazon EventBridge: Creates event-driven triggers.</li>
<li>Kali linux CLI: Used to test the security setup.</li>
</ul>

<h2>Project Steps</h2>
<h4>1.  AWS Free Tier Account Setup</h4>
<ul>
<li>Created a Free Tier AWS account on aws.amazon.com.</li>
<li>Configured billing information and identity verification.</li>
<li>Selected "Basic Support – Free" for cost efficiency.</li>
</ul>
<h4>2️. Configured AWS CloudTrail</h4>
<ul>
<li>Accessed CloudTrail in the AWS Management Console.</li>
<li>Created a new trail named MyCloudTrail.</li>
<li>Enabled Management Event Logging for all read/write events.</li>
<li>Configured logs to be stored in an S3 bucket (my-cloudtrail-logs-uniqueid).</li>
<li>Enabled multi-region logging for full coverage.</li>
</ul>
<h4>3️. Set Up SNS for Email Alerts</h4>
<ul>
<li>Created an SNS topic named APICallAlert.</li>
<li>Subscribed an email address to receive notifications.</li>
<li>Confirmed the email subscription via the AWS verification link.</li>
<li>Linked CloudTrail to SNS to trigger notifications when specific events occur.</li>
</ul>

<h4>4️. Configuring EventBridge for Root API Call Alerts</h4>
<ul>
<li>Created an EventBridge Rule named GetCallerIdentityAlert.</li>
<li>Defined a custom event pattern to detect GetCallerIdentity API calls from the root user:</li>

```
{
  "source": ["aws.sts"],
  "detail-type": ["AWS API Call via CloudTrail"],
  "detail": {
    "eventSource": ["sts.amazonaws.com"],
    "eventName": ["GetCallerIdentity"],
    "userIdentity": {
      "type": ["Root"]
    }
  }
}
```

<li>Configured SNS as the target for this rule to send notifications.</li>
<li>Allowed EventBridge to create an IAM role for permissions.</li>
</ul>

<h4>5️. Testing the Setup via kali linux CLI</h4>
<ul>
<li>Installed and configured kali linux with root credentials.</li>
<li>Ran the following command to simulate an API call:</li>
  
```
aws sts get-caller-identity
```

<li>Verified that the API call was logged in CloudTrail.</li>
<li>Checked the SNS email inbox for the alert notification.</li>
</ul>
<h4>Results & Key Takeaways</h4>
<ul>
<li>Successfully implemented real-time monitoring for root user API calls.</li> 
<li>Demonstrated how to configure AWS security alerting using CloudTrail, SNS, and EventBridge.</li>
<li>Gained hands-on experience with AWS event-driven automation.</li>
<li>Ensured that email notifications were triggered on unauthorized root account activity.</li>
</ul>

This project showcases my ability to implement AWS security measures and monitor cloud infrastructure effectively.
