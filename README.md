# n8n-Lead-Qualification-Automation
Automatically score, route, and manage incoming leads with intelligent notifications

<img width="940" height="245" alt="image" src="https://github.com/user-attachments/assets/0ff18ea7-25a3-4df2-b792-dc11e63293b5" />


# 🚀 n8n Lead Qualification Automation

**Automatically score, route, and manage incoming leads with intelligent notifications**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![n8n](https://img.shields.io/badge/n8n-Compatible-FF6D5A.svg)](https://n8n.io/)
[![Google Sheets](https://img.shields.io/badge/Google%20Sheets-Integration-34A853.svg)](https://sheets.google.com/)
[![Slack](https://img.shields.io/badge/Slack-Notifications-4A154B.svg)](https://slack.com/)

## 🎯 Overview

This automated workflow processes incoming leads through a sophisticated scoring system, stores them in Google Sheets, and sends intelligent Slack notifications for high-value opportunities. Built entirely on free-tier services, it's perfect for startups and small businesses looking to optimize their lead qualification process.

### Key Features

- 🔍 **Smart Lead Scoring**: Advanced algorithm based on budget, intent, and company size
- 📊 **Automatic Storage**: Seamless Google Sheets integration with enriched data
- 💬 **Intelligent Notifications**: Slack alerts for hot leads only (reduces noise)
- 🔄 **Real-time Processing**: Sub-30 second lead processing
- 🆓 **Free Tier Compatible**: Works entirely within free service limits
- 📱 **Multi-Form Support**: Works with Tally.so, Typeform, or custom forms

## 📈 Workflow Architecture

```
Webhook → Validation → Scoring → Google Sheets → Hot Lead Check
   ↓          ↓          ↓         ↓               ↓
Error      Error      Success   Success      Hot: Slack + Follow-up
Response   Response   Response  Response     Cold/Warm: Standard Response
```

## 🏆 Lead Scoring System

Our advanced scoring algorithm evaluates leads across multiple dimensions:

| Criteria | Weight | Scoring Tiers |
|----------|--------|---------------|
| **Budget** | 40% | £10k+ (40pts) → £5-9k (25pts) → £2-4k (15pts) → £1-2k (5pts) → <£1k (0pts) |
| **Interest Level** | 35% | High (35pts) → Medium (20pts) → Low (5pts) |
| **Company Size** | 15% | Enterprise (15pts) → Medium (10pts) → Small/Startup (5pts) |
| **Phone Provided** | 10% | Yes (10pts) → No (0pts) |

### Temperature Classification
- 🔥 **Hot Lead**: 70+ points (immediate Slack notification)
- 🌡️ **Warm Lead**: 40-69 points (standard processing)
- ❄️ **Cold Lead**: <40 points (standard processing)

## 🚀 Quick Start

### Prerequisites
- n8n instance (self-hosted or cloud)
- Google account (free)
- Slack workspace (free tier)
- Form provider (Tally.so, Typeform, or custom)

### 1. Repository Setup
```bash
git clone https://github.com/yourusername/n8n-lead-qualification.git
cd n8n-lead-qualification
```

### 2. Import Workflow
1. Open your n8n instance
2. Import the `workflow/lead-qualification-workflow.json` file
3. Follow the configuration steps in `docs/setup-guide.md`

### 3. Configure Integrations
- **Google Sheets**: Follow `docs/google-sheets-setup.md`
- **Slack Integration**: Follow `docs/slack-setup.md`
- **Form Setup**: Choose from `examples/` directory

## 📁 Repository Structure

```
n8n-lead-qualification/
├── 📁 workflow/
│   └── lead-qualification-workflow.json    # Main n8n workflow
├── 📁 docs/
│   ├── setup-guide.md                     # Complete setup instructions
│   ├── google-sheets-setup.md             # Google Sheets configuration
│   ├── slack-setup.md                     # Slack integration guide
│   ├── testing-guide.md                   # Testing procedures
│   └── troubleshooting.md                 # Common issues & solutions
├── 📁 examples/
│   ├── tally-form-config.md              # Tally.so form setup
│   ├── typeform-config.md                # Typeform integration
│   ├── custom-html-form.html             # Sample HTML form
│   └── test-payloads.json                # Test data examples
├── 📁 templates/
│   └── google-sheets-template.xlsx       # Pre-configured sheet template
├── LICENSE                               # MIT License
├── CHANGELOG.md                          # Version history
└── README.md                            # This file
```

## 🧪 Testing Your Setup

Test with our provided sample data:

**Hot Lead Test** (Expected: 100 points)
```json
{
  "full_name": "John Smith",
  "email": "john@enterprise-corp.com",
  "phone": "+44 7123 456789",
  "company_size": "enterprise",
  "budget": "15000",
  "interest_level": "high"
}
```

**Warm Lead Test** (Expected: 45 points)
```json
{
  "full_name": "Sarah Johnson",
  "email": "sarah@medium-biz.com",
  "company_size": "medium",
  "budget": "3000",
  "interest_level": "medium"
}
```

See `examples/test-payloads.json` for complete test suite.

## 📊 Success Metrics

Track these KPIs to measure workflow effectiveness:

- ⚡ **Lead Processing Time**: <30 seconds
- 🎯 **Hot Lead Response**: <5 minutes to first contact
- 📈 **Scoring Accuracy**: Monitor conversion by temperature
- 🔄 **System Uptime**: >99% webhook availability
- ✅ **Data Quality**: <1% validation errors

## 🛠️ Customization Options

### Scoring Algorithm
Modify weights in the Lead Scoring node:
- Budget weight: Currently 40%
- Interest weight: Currently 35%
- Company size: Currently 15%
- Phone bonus: Currently 10%

### Notification Rules
- Change temperature thresholds
- Add multiple Slack channels
- Customize message templates

### Data Fields
- Add custom form fields
- Extend Google Sheets columns
- Include additional validation

## 🔧 Troubleshooting

### Common Issues

**Webhook Not Receiving Data**
- Check n8n workflow is active
- Verify webhook URL in form configuration
- Test with curl or Postman

**Google Sheets Not Updating**
- Confirm service account permissions
- Check sheet ID in workflow
- Verify API quotas

**Slack Notifications Missing**
- Check bot permissions in channel
- Verify webhook URL
- Test Slack integration separately

See `docs/troubleshooting.md` for detailed solutions.

## 🚧 Current Limitations

- No lead deduplication (v2 feature)
- Static scoring weights (configurable UI planned)
- Single Slack channel notifications
- Basic error handling

## 🎯 Roadmap

### Phase 2 Features
- [ ] Lead deduplication by email
- [ ] Dynamic scoring configuration
- [ ] Lead assignment automation
- [ ] Email follow-up integration
- [ ] CRM connector (HubSpot, Salesforce)

### Phase 3 Features
- [ ] Analytics dashboard
- [ ] A/B testing framework
- [ ] Lead enrichment APIs
- [ ] Multi-team routing

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [n8n](https://n8n.io/) for the amazing automation platform
- [Google Sheets API](https://developers.google.com/sheets/api) for seamless data storage
- [Slack API](https://api.slack.com/) for real-time notifications
- The open-source community for inspiration and feedback

## 📞 Support

- 📖 [Documentation](docs/)
- 🐛 [Issues](https://github.com/yourusername/n8n-lead-qualification/issues)
- 💬 [Discussions](https://github.com/yourusername/n8n-lead-qualification/discussions)
- 📧 Email: your-email@example.com

---

**⭐ Star this repository if it helped you automate your lead qualification process!**
