# Questions Generator Automation

A comprehensive keyword research automation that pulls question-type search queries from multiple data sources and analyzes them with AI for search intent and relevance scoring.

## 📋 Overview

**Platform:** Make.com (formerly Integromat)  
**Current Version:** v3.2  
**Data Sources:** Google Search Console, Semrush (Questions & Related), AlsoAsked  
**AI Analysis:** OpenAI GPT-4o-mini for intent classification and relevance scoring  
**Output:** Consolidated Google Sheets database with email notifications  

## 🏗️ Architecture

### Data Flow
```
Google Form Submission → Variable Extraction → 4-Route Parallel Processing → AI Analysis → Google Sheets → Email Notification
```

### Routes
- **Route 1:** Google Search Console (URL-specific + domain-wide question queries with performance data) 🆕
- **Route 2:** Semrush Related Keywords (semantic keyword variations)  
- **Route 3:** Semrush Questions (direct question matches)
- **Route 4:** AlsoAsked ("People Also Ask" data)

### GSC Smart Routing (v3.2) 🆕
```
URL-Specific GSC Query → Result Count Check →
├── ≥10 Results: Direct Processing (Route 1)
└── <10 Results: Enhanced with Domain-Wide (Route 2)
```

## 📁 Repository Structure

```
/
├── README.md                                    # This file
├── .gitignore                                   # Protects sensitive blueprint files
├── LICENSE                                      # MIT License
├── blueprints/
│   ├── questions-generator-v3.2-public.json    # Current production version (sanitized) 🆕
│   ├── questions-generator-v3.0-baseline.blueprint.json # v3.0 baseline (protected)
│   ├── questions-generator-v3.1-baseline.blueprint.json # v3.1 baseline (protected)
│   ├── questions-generator-v3.2-baseline.blueprint.json # v3.2 baseline (protected)
│   └── [future versions]
├── documentation/
│   ├── improvement-roadmap.md                  # Planned enhancements
│   └── v32_final_handoff.md                    # v3.2 final project handoff
└── examples/
    └── sample-outputs.csv                      # Example results
```

## 🚀 Quick Start

### Prerequisites
- Make.com account with scenario import capabilities
- API access to:
  - Google Search Console (with domain property verified) 🆕
  - Semrush API
  - AlsoAsked API  
  - OpenAI API (GPT-4o-mini)
- Google Workspace (Sheets, Forms, Gmail)

## 🔒 Security & Privacy

### Important: Sanitized Public Version
This repository contains a **sanitized public version** of the automation blueprint. Before using:

1. **Replace placeholder values** in `blueprints/questions-generator-v3.2-public.json`:
   - `YOUR_GOOGLE_SHEET_ID` → Your actual Google Sheets ID
   - `your-email@example.com` → Your notification email
   - `your-restricted-email@example.com` → Your Google restricted connection email

2. **Update email template** HTML with your actual sheet URL

### What We've Sanitized
- Google Sheets IDs and URLs
- Email addresses and connections
- Direct links in email templates

**Never commit your actual API keys, sheet IDs, or email addresses to public repositories.**

### Setup Instructions

1. **Import Blueprint**
   ```bash
   # Download the latest sanitized blueprint
   wget https://github.com/[your-org]/questions-generator/blob/main/blueprints/questions-generator-v3.2-public.json
   ```

2. **Configure API Connections & Replace Sensitive Data**
   - Import blueprint into Make.com
   - **Replace all placeholder values** with your actual:
     - Google Sheets ID in all modules
     - Email addresses in connection labels
     - Sheet URL in email template HTML
   - Update all API connection credentials
   - **Verify Google Search Console property access** 🆕
   - Verify Google Sheets permissions

3. **Set Up Input Form**
   - Create Google Form with required fields (see Field Mapping below)
   - Connect form responses to trigger spreadsheet

4. **Test Execution**
   - Submit test form with known keyword and specific URL 🆕
   - Monitor execution in Make.com
   - Verify output in results spreadsheet

## 📝 Input Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| Keyword | Text | Seed keyword for research | "digital marketing" |
| URL | URL | **Specific page URL for GSC analysis** 🆕 | "https://example.com/blog/seo-guide" |
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
| T | GSC_Page | **Specific page URL from GSC** 🆕 | GSC Only |

## 🎯 Key Features

### Smart GSC Integration (v3.2) 🆕
- **URL-Specific Targeting**: Discovers questions people actually search for about specific pages
- **Intelligent Fallback**: Automatically enhances results with domain-wide context when needed
- **Dual-Query System**: Combines page-specific insights with broader site context
- **Smart Routing**: Optimizes processing based on available data volume

### Advanced Question Discovery
- **Multiple Data Sources**: GSC, AlsoAsked, Semrush integration
- **Question Pattern Recognition**: Regex-based question identification
- **Relevance Scoring**: AI-powered relevance assessment
- **Intent Classification**: Automatic categorization of search intent

### AI-Powered Analysis
- **Relevance Assessment**: Context-aware relevance scoring (1-10)
- **Intent Classification**: Automatic intent categorization
- **Duplicate Detection**: Smart deduplication across all sources
- **Quality Filtering**: Removes low-relevance questions automatically

## 💡 v3.2 Benefits

### 🎯 **Precision + Coverage**
- Get questions specific to your exact page content
- Never miss broader opportunities with automatic domain-wide enhancement
- Perfect balance of targeted relevance and comprehensive coverage

### 📊 **Real Search Data**
- Questions come from actual Google Search Console data
- See real impressions, clicks, and positions for each question
- Understand what people are actually searching for about your content

### 🚀 **Automatic Optimization**
- High-traffic pages get ultra-targeted questions
- Low-traffic pages get enhanced with contextual questions
- New pages benefit from established domain authority insights
- Zero configuration required - works intelligently out of the box

### 💡 **Content Strategy Insights**
- Discover content gaps specific to individual pages
- Understand page-level vs site-level search opportunities
- Identify questions driving traffic to similar pages
- Plan content expansion based on real search behavior

## 📖 Usage Examples - v3.2 Enhanced

### Example 1: High-Traffic Blog Post
**Input**: `https://yourblog.com/ultimate-guide-to-seo`  
**v3.2 Result**: 
- 15+ questions specific to SEO guide content
- Real GSC data showing what readers actually search
- Direct processing (Route 1) for optimal speed

### Example 2: New Product Page
**Input**: `https://yourstore.com/new-widget-2024`  
**v3.2 Result**:
- 3 questions specific to the new widget
- Enhanced with 8 questions about similar products from domain
- Combined processing (Route 2) for comprehensive coverage

### Example 3: Service Landing Page
**Input**: `https://youragency.com/ppc-management`  
**v3.2 Result**:
- 12 questions about PPC management services
- Enhanced with broader digital marketing questions
- Perfect mix of service-specific and agency-wide insights

## 🔧 Configuration

### Key Variables
- `KW`: Seed keyword from form input
- `Rows`: Result count limit  
- `Email`: Notification email address
- `GSC_URL`: Processed root URL for Search Console
- **`URL`: Specific page URL for targeted GSC queries** 🆕

### GSC Configuration (v3.2) 🆕

#### Requirements
- Google Search Console property properly configured
- GSC connection authenticated in Make.com
- Domain verification completed in GSC

#### Automatic Features
- **URL-Specific Filtering**: Automatically targets questions for specific pages
- **Domain-Wide Fallback**: Automatically enhances with broader context when needed
- **Smart Routing**: Optimizes processing based on available data
- **No Additional Setup**: v3.2 enhancements work automatically with existing GSC connections

### API Rate Limits
- **Semrush:** Check your plan limits
- **AlsoAsked:** Standard API rate limits apply
- **Google Search Console:** 1,000 requests/day
- **OpenAI:** Token-based pricing (GPT-4o-mini)

## 🚧 Known Issues & Limitations

### Resolved in v3.2 ✅
- ~~GSC queries are domain-wide, not URL-specific~~ → **Now supports both URL-specific and domain-wide**
- ~~No intelligent fallback for low-traffic pages~~ → **Smart routing with automatic enhancement**

### Current Limitations
- Context field from form is not currently used in AI analysis
- Limited error handling for API failures
- No query expansion for failed Semrush searches

### Security Notes 🆕
- Public blueprint contains sanitized placeholder values
- Users must replace all sensitive data before use
- Email templates require manual URL updates

### Problematic Query Examples
These queries often return insufficient results:
- "higher education digital marketing"
- "CTT OTT"
- "Marketing during a national crisis"

## 📈 Version History

### v3.2 - GSC URL-Specific Filtering (COMPLETED) 🆕
**Release Date**: July 13, 2025

**Major Features:**
- **URL-Specific GSC Queries**: Targets questions specific to the input URL
- **Smart Fallback System**: Automatically supplements with domain-wide results when needed
- **Dual-Query Architecture**: Combines targeted + contextual question discovery
- **Intelligent Routing**: ≥10 URL-specific results = direct processing, <10 = enhanced with domain-wide

**Technical Improvements:**
- Advanced array merging system using HTTP passthrough method
- Router-based conditional logic for optimal data flow
- Enhanced GSC filtering with both page-specific and domain-wide searches
- Improved result relevance through targeted query prioritization

**Benefits:**
- **Higher Relevance**: Questions directly related to specific page content
- **Better Coverage**: Domain-wide fallback ensures comprehensive question discovery
- **Smarter Processing**: Automatic optimization based on available data
- **Maintained Performance**: All v3.1 functionality preserved and enhanced

**Use Cases:**
- High-traffic pages get ultra-targeted questions
- New/low-traffic pages get enhanced with domain context
- Corporate sites benefit from both page-specific and company-wide queries
- Blog posts get both article-specific and site-wide question coverage

### v3.0 - Multi-Source Integration
**Release Date**: July 12, 2025
- Initial multi-source implementation
- GSC, Semrush, AlsoAsked integration
- AI-powered analysis and scoring
- Google Sheets output with email notifications

## 📈 Roadmap

See [`documentation/improvement-roadmap.md`](documentation/improvement-roadmap.md) for detailed enhancement plans.

### Upcoming Releases
- **v3.3:** Context Integration (utilize unused form field)
- **v3.4:** Semrush Query Expansion
- **v3.5:** Enhanced Email Reporting
- **v3.6:** Performance Analytics Dashboard

## 🛠️ Development

### Making Changes
1. Export current blueprint from Make.com
2. Create new version file: `questions-generator-v3.x.json`
3. Test changes in Make.com development environment
4. Update documentation
5. Commit changes with clear version notes

### Testing
- Use known keywords with predictable results
- **Test both high-traffic and low-traffic URLs for v3.2 routing** 🆕
- Monitor API usage and costs
- Verify deduplication across sources
- Check AI analysis quality

## 📞 Support

### Troubleshooting
1. Check Make.com execution logs
2. Verify API connection status
3. **Confirm GSC property access for target domain** 🆕
4. Confirm Google Sheets permissions
5. Review quota limits for all APIs

### Common Fixes
- **Empty Results:** Check API credentials and quota limits
- **Missing URL-Specific Data:** Verify GSC property includes target URL 🆕
- **Missing Sensitive Data:** Replace placeholder values with actual IDs/emails 🆕
- **Duplicate Questions:** Verify deduplication logic in modules 22, 23, 24, 39
- **Missing AI Analysis:** Check OpenAI API key and token limits

## 📄 License

MIT License - See LICENSE file for details.

Copyright (c) 2025 [Will Scott, AI SEO Expert](https://willscott.me/), [Search Influence](https://www.searchinfluence.com/)

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

**Last Updated:** July 13, 2025, 4:25 PM CST  
**Version:** 3.2  
**Maintainer:** [Will Scott, AI SEO Expert](https://willscott.me/), CEO of [Search Influence](https://www.searchinfluence.com/)