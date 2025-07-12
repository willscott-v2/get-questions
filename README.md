# Questions Generator Automation

A comprehensive keyword research automation that pulls question-type search queries from multiple data sources and analyzes them with AI for search intent and relevance scoring.

## 📋 Overview

**Platform:** Make.com (formerly Integromat)  
**Current Version:** v3.0  
**Data Sources:** Google Search Console, Semrush (Questions & Related), AlsoAsked  
**AI Analysis:** OpenAI GPT-4o-mini for intent classification and relevance scoring  
**Output:** Consolidated Google Sheets database with email notifications  

## 🏗️ Architecture

### Data Flow
```
Google Form Submission → Variable Extraction → 4-Route Parallel Processing → AI Analysis → Google Sheets → Email Notification
```

### Routes
- **Route 1:** Google Search Console (question-type queries with performance data)
- **Route 2:** Semrush Related Keywords (semantic keyword variations)  
- **Route 3:** Semrush Questions (direct question matches)
- **Route 4:** AlsoAsked ("People Also Ask" data)

## 📁 Repository Structure

```
/
├── README.md                          # This file
├── blueprints/
│   ├── questions-generator-v3.0.json  # Current production version
│   └── [future versions]
├── documentation/
│   └── improvement-roadmap.md          # Planned enhancements
└── examples/
    └── sample-outputs.csv             # Example results
```

## 🚀 Quick Start

### Prerequisites
- Make.com account with scenario import capabilities
- API access to:
  - Google Search Console
  - Semrush API
  - AlsoAsked API  
  - OpenAI API (GPT-4o-mini)
- Google Workspace (Sheets, Forms, Gmail)

### Setup Instructions

1. **Import Blueprint**
   ```bash
   # Download the latest blueprint
   wget https://github.com/[your-org]/questions-generator/blob/main/blueprints/questions-generator-v3.0.json
   ```

2. **Configure API Connections**
   - Import blueprint into Make.com
   - Update all API connection credentials
   - Verify Google Sheets permissions

3. **Set Up Input Form**
   - Create Google Form with required fields (see Field Mapping below)
   - Connect form responses to trigger spreadsheet

4. **Test Execution**
   - Submit test form with known keyword
   - Monitor execution in Make.com
   - Verify output in results spreadsheet

## 📝 Input Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| Keyword | Text | Seed keyword for research | "digital marketing" |
| URL | URL | Website URL for GSC analysis | "https://example.com/blog/post" |
| Context | Text | Additional context for relevance scoring | "Looking for FAQ content for SaaS pricing page" |
| Result Count | Number | Max results per source | 25 |
| Email | Email | Notification recipient | "user@example.com" |

## 📊 Output Schema

Results are saved to Google Sheets with the following columns:

| Column | Field | Description | Sources |
|--------|-------|-------------|---------|
| A | Question | Cleaned question text | All |
| B | Number of Results | Search result count | Semrush |
| C | CPC | Cost per click | Semrush |
| D | Competition | Competition level | Semrush |
| E | Search Volume | Monthly searches | Semrush/GSC |
| F | Trends | Search trends | Semrush |
| G | Relevance | AI relevance score (1-10) | AI Analysis |
| H | Intent | Search intent classification | AI Analysis |
| I | Source Keyword | Original seed keyword | Form Input |
| J | AA_Level | AlsoAsked depth level | AlsoAsked |
| K | AA_Parent | AlsoAsked parent question | AlsoAsked |
| L | AA_Fresh | Date/freshness indicator | AlsoAsked/GSC |
| M | Data_Source | Source identifier | All |
| N | Question_ID | Unique identifier | Generated |
| O-R | GSC Metrics | Position, CTR, Impressions, Clicks | GSC Only |
| S | GSC_Date | Last crawl date | GSC Only |

## 🔧 Configuration

### Key Variables
- `KW`: Seed keyword from form input
- `Rows`: Result count limit  
- `Email`: Notification email address
- `GSC_URL`: Processed root URL for Search Console

### API Rate Limits
- **Semrush:** Check your plan limits
- **AlsoAsked:** Standard API rate limits apply
- **Google Search Console:** 1,000 requests/day
- **OpenAI:** Token-based pricing (GPT-4o-mini)

## 🚧 Known Issues & Limitations

### Current Limitations
- Context field from form is not currently used in AI analysis
- Limited error handling for API failures
- GSC queries are domain-wide, not URL-specific
- No query expansion for failed Semrush searches

### Problematic Query Examples
These queries often return insufficient results:
- "higher education digital marketing"
- "CTT OTT"
- "Marketing during a national crisis"

## 📈 Roadmap

See [`documentation/improvement-roadmap.md`](documentation/improvement-roadmap.md) for detailed enhancement plans.

### Upcoming Releases
- **v3.1:** Context Integration (utilize unused form field)
- **v3.2:** GSC URL-Specific Filtering
- **v3.3:** Semrush Query Expansion
- **v3.4:** Enhanced Email Reporting

## 🛠️ Development

### Making Changes
1. Export current blueprint from Make.com
2. Create new version file: `questions-generator-v3.x.json`
3. Test changes in Make.com development environment
4. Update documentation
5. Commit changes with clear version notes

### Testing
- Use known keywords with predictable results
- Monitor API usage and costs
- Verify deduplication across sources
- Check AI analysis quality

## 📞 Support

### Troubleshooting
1. Check Make.com execution logs
2. Verify API connection status
3. Confirm Google Sheets permissions
4. Review quota limits for all APIs

### Common Fixes
- **Empty Results:** Check API credentials and quota limits
- **Duplicate Questions:** Verify deduplication logic in modules 22, 23, 24, 39
- **Missing AI Analysis:** Check OpenAI API key and token limits

## 📄 License

MIT License - See LICENSE file for details.

Copyright (c) 2025 Will Scott, Search Influence

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

## 🤝 Contributing

1. Fork the repository
2. Create feature branch (`git checkout -b feature/amazing-feature`)
3. Test changes thoroughly
4. Commit changes (`git commit -m 'Add amazing feature'`)
5. Push to branch (`git push origin feature/amazing-feature`)
6. Open Pull Request

---

**Last Updated:** July 12, 2025, 3:52 PM CST  
**Version:** 3.0  
**Maintainer:** Will Scott, AI SEO Expert, CEO of Search Influence