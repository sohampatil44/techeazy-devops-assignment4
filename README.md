🔍 Techeazy DevOps CloudWatch Monitoring - Assignment 5


🔐 GitHub Secrets Required
Add these secrets to your GitHub repository before running:
🔐 Secret Name📝 DescriptionAWS_ACCESS_KEY_IDYour AWS IAM Access Key IDAWS_SECRET_ACCESS_KEYYour AWS IAM Secret Access KeyREPO_ACCESS_TOKENPersonal Access Token for private repo accessINSTANCE_KEYYour EC2 PEM key content for SSH accessALERT_EMAILEmail address to receive CloudWatch alarm notifications 📧S3_BUCKET_NAMES3 bucket name for logs and CloudWatch config storage

🚀 How to Run
1. Deploy Infrastructure

Go to Actions tab in GitHub 📂
Click Run workflow ▶️
Select stage: dev 🧪 / staging 🛡️ / prod 🚀
Hit Run workflow button ✅

2. Confirm Email Subscription

Check your email inbox 📧
Click "Confirm subscription" in AWS SNS email ✅
⚠️ Critical: Alerts won't work without confirmation!

3. Test Error Alerts
bash# SSH to your EC2 instance
ssh -i your-key.pem ec2-user@your-instance-ip

# Trigger test alert
echo "ERROR: Test alert system on $(date)" >> /home/ec2-user/app.log

# Wait 5-10 minutes for email notification 📧

⚡ How It Works
Your App Logs ERROR → CloudWatch Agent → CloudWatch Logs → Metric Filter → Alarm → SNS → Your Email 📧
🔄 The Magic Pipeline:

📊 Log Collection: CloudWatch Agent streams /home/ec2-user/app.log in real-time
🔍 Error Detection: Metric filter scans for "ERROR" or "Exception" keywords
🚨 Smart Alerting: Alarm triggers if >1 error in 5 minutes
📧 Instant Notification: SNS sends formatted email alert immediately

🎛️ Stage Separation:

Dev: techeazy-app-logs-dev → app-alerts-topic-dev 🧪
Prod: techeazy-app-logs-prod → app-alerts-topic-prod 🚀
Each stage = isolated monitoring resources ✅


🧪 Testing Checklist

✅ Terraform Apply: Infrastructure deployed successfully
✅ Email Confirmed: SNS subscription activated
✅ App Running: EC2 instance healthy
✅ Logs Streaming: CloudWatch shows log entries
✅ Alert Test: Error simulation triggers email
✅ Metrics Visible: ErrorCount metric appears in CloudWatch


💰 Free Tier Optimized

5GB CloudWatch Logs ingestion free 📊
1M SNS publishes per month free 📧
Auto log cleanup after 7 days (cost control) 💲
Minimal resources - maximum efficiency ⚡


🔧 Quick Troubleshooting
🚨 Issue🔧 SolutionNo email alertsConfirm SNS subscription via email linkLogs not appearingCheck CloudWatch Agent status on EC2Terraform failsVerify AWS credentials and permissionsSSH access deniedCheck security group allows port 22

Ready to monitor like a pro! 🚀📊🎯