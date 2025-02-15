# Project Chameleon - Slack Bot

A simple Slack bot implementation using Socket Mode, designed to run on AWS EC2.

## Local Setup

1. Clone this repository
2. Create a `.env` file with your Slack tokens:
   ```
   SLACK_BOT_TOKEN=xoxb-your-token
   SLACK_APP_TOKEN=xapp-your-token
   ```
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Test locally:
   ```bash
   python bot.py
   ```

## AWS EC2 Deployment

### 1. Instance Setup
1. Launch an Amazon Linux 2023 EC2 instance
2. Connect to your instance:
   ```bash
   ssh -i your-key.pem ec2-user@your-instance-ip
   ```

### 2. Automated Deployment
1. Upload deployment files:
   ```bash
   scp -i your-key.pem bot.py deploy_ec2.sh ec2-user@your-instance-ip:~
   ```

2. Make the deployment script executable:
   ```bash
   chmod +x deploy_ec2.sh
   ```

3. Run the deployment script:
   ```bash
   ./deploy_ec2.sh
   ```

The script will:
- Update system packages
- Create project directory in `/opt/project-chameleon`
- Set up Python virtual environment
- Install required packages
- Configure environment variables
- Set up systemd service for auto-restart
- Configure log rotation

### 3. Managing the Bot

#### Check Status
```bash
sudo systemctl status project-chameleon
```

#### View Logs
```bash
# View bot logs
tail -f /var/log/project-chameleon/bot.log

# View error logs
tail -f /var/log/project-chameleon/error.log
```

#### Control the Service
```bash
# Stop the bot
sudo systemctl stop project-chameleon

# Start the bot
sudo systemctl start project-chameleon

# Restart the bot
sudo systemctl restart project-chameleon
```

## Bot Features

1. Responds to direct messages
   - `hello`: Sends a greeting
   - `help`: Shows available commands

2. Responds to mentions
   - Acknowledges when mentioned
   - Provides help information

## Troubleshooting

1. Check service status:
   ```bash
   sudo systemctl status project-chameleon
   ```

2. Verify environment variables:
   ```bash
   source /etc/profile.d/project-chameleon.sh
   echo $SLACK_BOT_TOKEN
   echo $SLACK_APP_TOKEN
   ```

3. Check logs for errors:
   ```bash
   tail -f /var/log/project-chameleon/error.log
   ```

4. Restart the service:
   ```bash
   sudo systemctl restart project-chameleon
   ```

## Security Notes

1. Keep your tokens secure:
   - Never commit tokens to version control
   - Use proper file permissions for `/etc/profile.d/project-chameleon.sh`
   - Consider using AWS Secrets Manager for production

2. EC2 Security:
   - Use minimal required permissions for the EC2 instance
   - Keep system packages updated
   - Monitor logs for unusual activity

3. Maintenance:
   - Regularly check bot logs
   - Update system packages
   - Monitor disk usage for logs 