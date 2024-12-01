# Opportunity and Account Summarizer Snap-In  

## Overview  
The **Opportunity and Account Summarizer Snap-In** automates the tracking and summarization of closed deals in DevRev. Summaries are sent to a configurable Slack channel, helping sales teams stay updated and make better decisions with real-time, actionable insights.  

---

## Key Features  

1. **Automated Summaries**: Generates summaries whenever deals are closed.  
2. **Slack Integration**: Sends notifications directly to your Slack workspace.  
3. **Insightful Metrics**: Includes key details like deal size, closing date, sales reps, and more.  
4. **Customizable Configurations**: Easily tailor the behavior to match your team’s requirements.  
5. **Real-Time Updates**: Ensure your team stays informed without delays.  

---

## Usage - 

### How It Works  

1. **Monitor Opportunities**: The snap-in monitors opportunity statuses in DevRev.  
2. **Generate Summaries**: When a deal is marked as closed, a summary is automatically created.  
3. **Send Notifications**: The summary is posted to a Slack channel.  

### Example Slack Notification  

```plaintext  
**Deal Closed!**  
- **Deal Name**: Enterprise Expansion Package  
- **Account**: FutureTech Solutions  
- **Amount**: $750,000  
- **Closing Date**: 2024-12-01  
- **Sales Rep**: Jane Doe  
- **Insights**: Deal closed 10% faster than the average.  

Fantastic work! Let's keep winning! 🎉  
```  

---

## Installation  

### Prerequisites  

1. **DevRev Access**: API token with permission to access opportunities and accounts.  
2. **Slack API Token**: A Slack workspace with a bot-enabled API token and the target channel ID.  
3. **Node.js**: Installed for running the snap-in locally or deploying it.  

### Steps  

1. **Clone the Repository**  

   ```bash  
   git clone https://github.com/your-username/opportunity-account-summarizer.git  
   cd opportunity-account-summarizer  
   ```  

2. **Install Dependencies**  

   ```bash  
   npm install  
   ```  

3. **Set Up Environment Variables**  

   Create a `.env` file in the project root:  
   ```plaintext  
   DEVREV_API_TOKEN=<your_devrev_api_token>  
   SLACK_API_TOKEN=<your_slack_api_token>  
   SLACK_CHANNEL_ID=<your_slack_channel_id>  
   ```  

4. **Start the Server**  

   Run the server locally:  
   ```bash  
   npm run dev  
   ```  

5. **Deploy**  

   Deploy the snap-in using:  
   ```bash  
   npm run deploy  
   ```  

---

## Configuration  

Customize the snap-in by editing the `config.json` file:  

```json  
{  
  "summary_template": {  
    "deal_name": "Deal Name: {{deal.name}}",  
    "account_name": "Account: {{account.name}}",  
    "amount": "Amount: ${{deal.amount}}",  
    "closing_date": "Closing Date: {{deal.closing_date}}",  
    "sales_rep": "Sales Rep: {{deal.sales_rep}}"  
  },  
  "minimum_deal_value": 50000,  
  "notifications": {  
    "enabled": true,  
    "channel": "sales-updates"  
  }  
}  
```  

### Configurable Options  

- **Minimum Deal Value**: Set a threshold for which deals trigger notifications.  
- **Notification Template**: Modify the Slack message format.  
- **Target Channel**: Choose the Slack channel for updates.  

---

## Code Example  

Here's a simplified view of the notification logic:  

```javascript  
const axios = require('axios');  
require('dotenv').config();  

const postToSlack = async (message) => {  
  const url = 'https://slack.com/api/chat.postMessage';  
  const payload = {  
    channel: process.env.SLACK_CHANNEL_ID,  
    text: message,  
  };  

  await axios.post(url, payload, {  
    headers: {  
      Authorization: `Bearer ${process.env.SLACK_API_TOKEN}`,  
      'Content-Type': 'application/json',  
    },  
  });  
};  

const generateSummary = (deal) => {  
  return `  
 **Deal Closed!**  
- **Deal Name**: ${deal.name}  
- **Account**: ${deal.account_name}  
- **Amount**: $${deal.amount}  
- **Closing Date**: ${deal.closing_date}  
- **Sales Rep**: ${deal.sales_rep}  

 
  `;  
};  

const handleDealClosure = async (deal) => {  
  if (deal.amount < 50000) return; // Skip small deals  

  const summary = generateSummary(deal);  
  await postToSlack(summary);  
};  

// Example Usage  
const exampleDeal = {  
  name: 'Growth Plan Upgrade',  
  account_name: 'Innovate Ltd.',  
  amount: 120000,  
  closing_date: '2024-12-01',  
  sales_rep: 'Alice Johnson',  
};  

handleDealClosure(exampleDeal);  
```  

---

## Development  

### Testing  

Run tests to validate functionality:  

```bash  
npm run test  
```  

### Contributing  

1. Fork the repository.  
2. Create a new branch for your changes.  
3. Submit a pull request with detailed explanations.  

---

## Support  

For help or feature requests, contact [support@devrev.com](mailto:support@devrev.com).  

---
 

 


