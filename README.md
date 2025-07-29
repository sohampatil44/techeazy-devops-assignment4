# 🔍 Techeazy DevOps CloudWatch Monitoring - Assignment 5

# 🔐 GitHub Secrets Required
Add these secrets to your GitHub repository before running:

#️⃣ AWS_ACCESS_KEY_ID         → Your AWS IAM Access Key ID  
#️⃣ AWS_SECRET_ACCESS_KEY     → Your AWS IAM Secret Access Key  
#️⃣ REPO_ACCESS_TOKEN         → Personal Access Token for private repo access  
#️⃣ INSTANCE_KEY              → Your EC2 PEM key content for SSH access  
#️⃣ ALERT_EMAIL               → Email to receive CloudWatch alarm notifications  
#️⃣ S3_BUCKET_NAME            → S3 bucket name for logs and CloudWatch config

# 🚀 How to Run

## 1️⃣ Deploy Infrastructure
📂 Go to Actions tab in GitHub  
▶️ Click Run workflow  
🧪 Select stage: dev / staging / prod  
✅ Hit Run workflow

## 2️⃣ Confirm Email Subscription
📧 Check your email inbox  
🔗 Click "Confirm subscription" in AWS SNS email  
⚠️ Critical: Alerts won't work without confirmation!

## 3️⃣ Test Error Alerts
💻 SSH into your EC2 instance:
ssh -i your-key.pem ec2-user@your-instance-ip

🧪 Trigger test alert:
echo "ERROR: Test alert system on $(date)" >> /home/ec2-user/app.log

⏳ Wait 5–10 minutes for email notification

# ⚡ How It Works
App Logs with "ERROR" → CloudWatch Agent → CloudWatch Logs → Metric Filter → Alarm → SNS → Your Email

# 🔄 Pipeline Flow
📊 Log Collection       : CloudWatch Agent streams /home/ec2-user/app.log in real-time  
🔍 Error Detection      : Metric filter scans for "ERROR" or "Exception"  
🚨 Smart Alerting       : Alarm triggers if >1 error in 5 minutes  
📧 Instant Notification : SNS sends formatted alert email

# 🎛️ Stage Separation
🧪 Dev  : techeazy-app-logs-dev → app-alerts-topic-dev  
🚀 Prod : techeazy-app-logs-prod → app-alerts-topic-prod  
✅ Each stage = isolated monitoring resources

# 🧪 Testing Checklist
✅ Terraform Apply      : Infrastructure deployed successfully  
✅ Email Confirmed      : SNS subscription activated  
✅ App Running          : EC2 instance healthy  
✅ Logs Streaming       : CloudWatch shows log entries  
✅ Alert Test           : Error simulation triggers email  
✅ Metrics Visible      : ErrorCount metric appears in CloudWatch

# 🔧 Quick Troubleshooting

Issue                    → Solution  
──────────────────────────┬─────────────────────────────────────────────────────  
No email alerts           → Confirm SNS subscription via email link  
Logs not appearing        → Check CloudWatch Agent status on EC2  
Terraform fails           → Verify AWS credentials and permissions  
SSH access denied         → Check security group allows port 22  
