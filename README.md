# 📂 telegram-to-bale-file-transfer-bot - Move files between messengers with ease

[![](https://img.shields.io/badge/Download-Release_Page-blue.svg)](https://github.com/Sino3371/telegram-to-bale-file-transfer-bot/releases)

This application acts as a bridge between Telegram and Bale. It allows you to forward files from your Telegram bot to a Bale bot automatically. The system keeps your data secure by restricting access to authorized users only.

## 📋 What this tool does

You likely use both Telegram and Bale for your daily tasks. Sometimes you need to move a file from one platform to the other without manual downloads and uploads. This tool automates that process. It sits in the cloud and waits for your files. When it detects a new file in your Telegram chat, it sends a copy to the specified Bale account.

The system uses Cloudflare Workers. This technology runs the code in the background. You do not need to keep your computer turned on. Once you set up the link between the two services, the bot handles the traffic for you. Only people you choose can trigger the transfer.

## ⚙️ System requirements

To run and manage this bot, you need certain tools on your Windows machine:

1. A stable internet connection.
2. A web browser like Chrome, Firefox, or Edge.
3. Access to a Cloudflare account.
4. Active Telegram and Bale bot tokens.

You do not need a high-end computer. Because the bot runs on the internet infrastructure of Cloudflare, your personal computer only serves as the control center for the initial setup.

## 📥 How to download the software

Follow these steps to find the right files for your needs.

1. Go to the [official release page](https://github.com/Sino3371/telegram-to-bale-file-transfer-bot/releases).
2. Look for the latest version at the top of the list.
3. Click the link labeled "Source code" if you want to inspect the files, or look for compiled scripts if provided.
4. Save the files to a folder on your desktop where you can find them later.

You must ensure that you always use the version marked as "Latest" to stay compatible with changes made by Telegram or Bale.

## 🛠️ Setting up the bot

Follow these steps to authorize the bot and link your accounts.

### 1. Create your bots
Before you use the software, you must create bots on both platforms. 
- Create a bot on Telegram using the BotFather. Record the Token provided.
- Create a bot on Bale using the BotFather feature. Record the Token provided.

### 2. Configure authorized users
The bot includes a security layer. You must define a list of IDs that have permission to use the file transfer feature. Open the configuration file within the downloaded folder. Locate the section labeled `AUTHORIZED_USERS`. Add the Telegram ID of each person you want to allow. If you leave this empty, the bot rejects all file transfer requests.

### 3. Deploy to Cloudflare
Since this is a Cloudflare Worker, you need to upload the script to your Cloudflare dashboard.
- Sign in to your Cloudflare account.
- Navigate to the "Workers & Pages" section.
- Click "Create Application" and then "Create Worker".
- Copy the text from the `index.js` file in your release folder.
- Paste this text into the Cloudflare code editor.
- Click "Save and Deploy".

### 4. Connect your tokens
In the Cloudflare dashboard, go to the "Settings" tab for your new worker. Find the "Variables" section. You need to add your bot tokens here safely:
- Set `TELEGRAM_TOKEN` to your Telegram bot token.
- Set `BALE_TOKEN` to your Bale bot token.
- Save your changes.

## ⚡ Using the bot

Once you deploy the worker, the system starts listening for messages. Open your Telegram bot in the app. Send a file to the bot. The worker detects the file immediately. It authenticates your ID against the list you created earlier. If you are on the list, it downloads the file and pushes it to your Bale bot destination.

The process takes a few seconds depending on the file size. You can verify the transfer by opening your Bale application and checking the chat associated with your Bale bot.

## 🛡️ Security features

The bot focuses on privacy and security. By default, it ignores messages from unknown users. This prevents strangers from using your bot resources. Because the code runs on Cloudflare infrastructure, your private bot tokens never touch your local machine after the initial setup. This keeps your credentials secure even if someone gains access to your Windows computer.

## 🔍 Frequently asked questions

**Where do I see error logs?**
Go to the Cloudflare dashboard and select your worker. Click the "Logs" tab. If a file fails to transfer, you will see a red indicator telling you why.

**Can I change the bot behavior?**
You can modify the code in the Cloudflare editor. If you have basic knowledge of text files, you can adjust the labels or response messages the bot sends back to you.

**Is there a limit on file size?**
Cloudflare Workers have limits on how much data they can process at once. Very large files might time out. Keep your file transfers under 10 megabytes for the best results.

**How do I update the bot?**
When a new version appears on the release page, download the new script and paste it over your existing code in the Cloudflare dashboard. Always save a copy of your configuration variables before you overwrite the script.

**What happens if the service goes down?**
The service relies on Cloudflare's global network. If you experience issues, check the Cloudflare status page. Typically, your bot remains online without any intervention from you.

## 📖 Support and resources

If you encounter issues during the setup, verify your tokens first. Invalid tokens remain the number one reason for transfer failures. Ensure you copied the full string of characters from the Telegram and Bale BotFather chats. Check that your Telegram ID is correct. You can find your ID by messaging a generic "ID Bot" on Telegram. 

If you find that the file arrives in Bale but lacks the correct filename, check the worker code for the header processing section. Sometimes, different messengers handle file metadata in unique ways. The current version handles standard file types like documents, images, and photos. Very obscure file formats may not transfer correctly if the destination API does not recognize the file extension. 

We recommend testing with a small image file first. Once you confirm the image transfers from Telegram to your Bale bot, try a larger document. This confirms that your configuration is correct before you rely on the system for important data transfers.