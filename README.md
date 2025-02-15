# Project Chameleon Slack Bot

A Slack bot powered by OpenAI's GPT-3.5 that serves as an AI-powered recruitment assistant.

## Project Files
- `bot_script.py` - Main bot code with OpenAI and Slack integration 
- `.env` - Contains API keys and tokens
- `setup.sh` - AWS EC2 setup script
- `start_bot.sh` - Script to start the bot
- `.gitignore` - Git ignore configuration

## AWS EC2 Setup
1. Launch EC2 instance (demo_bot)
2. Run setup commands:
   ```bash
   # Update system
   sudo yum update -y
   
   # Install Python and pip
   sudo yum install python3 python3-pip -y
   
   # Install required Python packages
   pip3 install slack-bolt openai python-dotenv

   # Clone repository
   git clone <repository-url>
   cd project-chameleon
   ```

## Environment Setup
1. Create `.env` file with required credentials:
   ```
   SLACK_BOT_TOKEN=xoxb-your-token
   SLACK_APP_TOKEN=xapp-your-token
   OPENAI_API_KEY=sk-your-key
   ```

## Running the Bot
1. Make start script executable:
   ```bash
   chmod +x start_bot.sh
   ```

2. Start the bot:
   ```bash
   ./start_bot.sh
   ```

## Security Notes
- Never commit `.env` file with actual credentials
- Rotate API keys periodically
- Use IAM roles for EC2 when possible

## Contributing
1. Fork the repository
2. Create feature branch
3. Submit pull request

## License
MIT License - See LICENSE file for details
