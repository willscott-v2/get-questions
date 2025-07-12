# Questions Generator: Semrush + AlsoAsked + GSC v3.0
## Project Documentation & Handoff Guide

### 📋 Project Overview

This Make.com automation generates comprehensive keyword research by pulling question-type search queries from multiple data sources and analyzing them with AI for search intent and relevance scoring.

**Data Sources:**
- Semrush Questions API
- Semrush Related Keywords API  
- AlsoAsked API
- Google Search Console API

**AI Analysis:**
- OpenAI GPT-4o-mini for search intent classification
- OpenAI GPT-4o-mini for relevance scoring (1-10 scale)

**Output:**
- Consolidated Google Sheets database with all questions, metrics, and AI analysis
- Email notification upon completion

---

## 🏗️ System Architecture

### Flow Structure
```
Form Submission → Variable Extraction → Router →
├── Route 1: Semrush Questions
├── Route 2: Semrush Related Keywords  
├── Route 3: AlsoAsked
└── Route 4: Google Search Console
```

### Key Modules by Route

**Route 1: Semrush Questions**
1. Semrush Questions API Call
2. Parse Questions CSV  
3. Check Questions Duplicates
4. Questions Intent AI Analysis
5. Questions Relevance AI Analysis
6. Save Semrush Questions

**Route 2: Semrush Related**
1. Semrush Related API Call
2. Parse Related CSV
3. Check Related Duplicates  
4. Related Intent AI Analysis
5. Related Relevance AI Analysis
6. Save Semrush Related

**Route 3: AlsoAsked**
1. AlsoAsked API Call
2. Process AlsoAsked Questions (Iterator)
3. Check AlsoAsked Duplicates
4. AlsoAsked Intent Analysis
5. AlsoAsked Relevance Score
6. Save AlsoAsked Results

**Route 4: Google Search Console**
1. GSC URL Extraction Variable
2. Google Search Console API Call
3. Check GSC Duplicates
4. GSC Intent Analysis  
5. GSC Relevance Analysis
6. Save GSC Questions

---

## 🔧 Configuration Details

### Form Input Fields
- **Field 1**: Keyword (seed keyword for research)
- **Field 2**: Page Content (for relevance analysis)
- **Field 3**: URL (for GSC root domain extraction)
- **Field 4**: Result Count (number of results to fetch)
- **Field 5**: Email (for completion notification)

### Key Variables
- **KW**: `{{1.`1`}}` - Seed keyword
- **Rows**: `{{1.`4`}}` - Result count limit
- **Email**: `{{1.`5`}}` - Notification email
- **GSC_URL**: `{{substring(1.`2`; 0; indexOf(1.`2`; "/"; indexOf(1.`2`; "://") + 3)) + "/"}}` - Root URL extraction

### API Configurations

**Semrush API:**
- Type: `phrase_questions` / `phrase_related`
- Database: `us`
- Export Columns: `Ph,Nq,Cp,Co,Nr,Td,In`
- Display Limit: `{{3.Rows}}`

**AlsoAsked API:**
- Language: `en`
- Region: `us`  
- Depth: `3`
- Fresh: `false`

**Google Search Console:**
- Start Date: `{{addDays(now; -28)}}` (28 days ago)
- End Date: `{{now}}`
- Dimensions: Query
- Dimension Filter: Question regex pattern
- Regex: `(?i)^(who|what|when|where|why|how|can|could|should|would|do|did|does|is|are|was|were|will|if)\b`

### AI Analysis Prompts

**Intent Classification:**
```
System: Analyze the search intent of the given question. Classify it as one of: informational, navigational, commercial, transactional. Respond with only the classification word.
```

**Relevance Scoring:**
```
System: You are a semantic SEO expert. Rate relevance on a scale of 1-10 where 1 = completely irrelevant and 10 = highly relevant. Respond with only the number (1-10).

User: Seed keyword: {{KW}}
Page content: {{Page Content}}
Question: {{Question}}

Rate how relevant this question is to someone interested in the page content:
```

---

## 📊 Output Schema

### Google Sheets Columns
| Col | Field | Description | Source |
|-----|-------|-------------|---------|
| A | Question | Cleaned question text | All sources |
| B | Number of Results | Search result count | Semrush |
| C | CPC | Cost per click | Semrush |
| D | Competition | Competition level | Semrush |
| E | Search Volume | Monthly searches | Semrush/GSC clicks |
| F | Trends | Search trends | Semrush |
| G | Relevance | AI relevance score (1-10) | AI Analysis |
| H | Intent | Search intent classification | AI Analysis |
| I | Source Keyword | Original seed keyword | Form input |
| J | AA_Level | AlsoAsked depth level | AlsoAsked |
| K | AA_Parent | AlsoAsked parent question | AlsoAsked |
| L | AA_Fresh | Date/freshness indicator | AlsoAsked/GSC |
| M | Data_Source | Source identifier | All sources |
| N | Question_ID | Unique identifier | Generated |
| O | Position | Average search position | GSC only |
| P | CTR | Click-through rate | GSC only |
| Q | Impressions | Search impressions | GSC only |
| R | Clicks | Actual clicks | GSC only |
| S | GSC_Date | Last crawl date for question | GSC only |

### Data Source Identifiers
- `"Semrush Questions"`
- `"Semrush Related"`  
- `"AlsoAsked"`
- `"Google Search Console"`

---

## 🔗 External Dependencies

### API Connections Required
1. **Semrush API** - Keyword research data
2. **AlsoAsked API** - People Also Ask questions
3. **Google Search Console** - Real search performance
4. **OpenAI API** - AI analysis (GPT-4o-mini)
5. **Google Sheets** - Data storage
6. **Gmail** - Completion notifications

### Rate Limits & Quotas
- **Semrush**: Check your plan limits
- **AlsoAsked**: API rate limits apply
- **Google Search Console**: 1000 requests/day  
- **OpenAI**: Token-based pricing

---

## 🚀 How to Use

### Basic Operation
1. Submit form with:
   - Target keyword
   - Page content for relevance analysis
   - Website URL
   - Desired result count
   - Email for notification

2. Automation runs across all 4 data sources
3. AI analyzes each question for intent & relevance
4. Results saved to Google Sheets
5. Email notification sent upon completion

### Advanced Usage
- **Bulk Processing**: Submit multiple forms for different keywords
- **Filtering**: Results automatically deduplicated across sources
- **Analysis**: Use relevance scores to prioritize content creation
- **Performance**: GSC data shows actual search performance vs theoretical opportunities

---

## 🛠️ Troubleshooting

### Common Issues

**CSV Parsing Errors:**
- Check delimiter settings (semicolon vs comma)
- Enable "Skip empty lines" and "Relax column count"
- Verify API response format

**Empty GSC Results:**
- Verify URL is properly configured in GSC
- Check date range (try 90 days instead of 28)
- Ensure domain matches GSC property exactly
- Verify regex filter isn't too restrictive

**AI Analysis Failures:**
- Check OpenAI API key and limits
- Verify prompt formatting
- Monitor token usage

**Duplicate Processing:**
- Duplicate checking looks for exact matches in column A
- Questions are cleaned (lowercase, special chars removed)
- Each source maintains separate question_ID format

### Error Resolution

**Invalid URL Extraction:**
- Formula: `{{substring(1.`2`; 0; indexOf(1.`2`; "/"; indexOf(1.`2`; "://") + 3)) + "/"}}`
- Handles www/non-www domains
- Extracts root domain only

**Missing Data Fields:**
- Check API response structure
- Verify field mapping in Google Sheets modules
- Ensure all required fields are mapped

---

## 📈 Enhancement Opportunities

### Immediate Improvements (Low Effort, High Impact)

1. **Enhanced Filtering**
   - Add search volume minimums
   - Filter by competition levels
   - Exclude branded terms

2. **Better Deduplication**
   - Fuzzy matching for similar questions
   - Stem-based duplicate detection
   - Cross-source question merging

3. **Additional Metrics**
   - Keyword difficulty scores
   - SERP feature presence
   - Seasonal trend analysis

### Medium-Term Enhancements (Moderate Effort)

4. **Content Gap Analysis**
   - Compare GSC performance vs opportunities
   - Identify high-opportunity, low-competition questions
   - Suggest content creation priorities

5. **Competitive Intelligence**
   - Add competitor keyword analysis
   - SERP position tracking
   - Content gap identification

6. **Advanced AI Analysis**
   - Topic clustering
   - Content angle suggestions
   - User journey mapping

### Long-Term Strategic Additions (High Effort, High Value)

7. **Performance Tracking**
   - Historical trend analysis
   - ROI measurement for implemented keywords
   - Content performance correlation

8. **Integration Expansions**
   - Ahrefs/SEMrush keyword expansion
   - Answer The Public integration
   - Social listening data

9. **Automated Content Planning**
   - Content calendar generation
   - Keyword-to-content mapping
   - Editorial workflow integration

---

## 🔒 Security & Maintenance

### API Key Management
- Store all API keys securely in Make.com connections
- Regularly rotate sensitive credentials
- Monitor API usage and billing

### Data Privacy
- Ensure client data handling complies with privacy policies
- Consider data retention policies for client information
- Secure Google Sheets sharing permissions

### Regular Maintenance
- **Weekly**: Monitor execution logs for errors
- **Monthly**: Review API usage and costs
- **Quarterly**: Update AI prompts based on output quality
- **Annually**: Review and update data sources and integrations

### Backup & Recovery
- Export Make.com scenario as blueprint (attached)
- Document all API configurations
- Maintain Google Sheets template copies
- Test disaster recovery procedures

---

## 📋 Success Metrics

### Operational Metrics
- **Execution Success Rate**: >95%
- **Data Accuracy**: Manual verification of random samples
- **Processing Time**: <10 minutes per keyword
- **Deduplication Effectiveness**: <5% duplicate entries

### Business Value Metrics
- **Keyword Discovery**: Questions found per seed keyword
- **Action Rate**: Percentage of questions used for content creation
- **Performance Improvement**: Ranking improvements for implemented keywords
- **Time Savings**: Hours saved vs manual research

---

## 📞 Support & Contact

### Technical Support
- Make.com scenario: Questions Generator v3.0
- Blueprint file: `Questions Generator- Semrush + AlsoAsked v3.0.blueprint.json`
- Google Sheets template: [Link to template]

### Documentation Updates
- Last updated: [Current Date]
- Version: 3.0
- Next review date: [3 months from current date]

---

## 🏆 Version History

### v3.0 (Current)
- ✅ Added Google Search Console integration
- ✅ Enhanced URL extraction for any domain format  
- ✅ Added GSC-specific metrics (Position, CTR, Impressions, Clicks)
- ✅ Added Column S (GSC_Date) for last crawl date tracking
- ✅ Improved question filtering with regex patterns
- ✅ 4-source parallel data collection

### v2.5 (Previous)
- ✅ Semrush Questions + Related Keywords
- ✅ AlsoAsked integration
- ✅ AI intent and relevance analysis
- ✅ Google Sheets consolidation
- ✅ Email notifications

---

## 🏁 Quick Start Checklist

**Pre-Launch Setup:**
- [ ] All API connections configured and tested
- [ ] Google Sheets template created with proper permissions
- [ ] Form submission process documented
- [ ] Test run completed with sample data
- [ ] Email notification template customized
- [ ] Error handling procedures documented

**Go-Live:**
- [ ] Scenario activated in Make.com
- [ ] Form published and accessible
- [ ] Team trained on usage and output interpretation
- [ ] Monitoring alerts configured
- [ ] Success metrics baseline established

**Post-Launch:**
- [ ] Regular execution monitoring
- [ ] Data quality assessments
- [ ] User feedback collection
- [ ] Performance optimization opportunities identified
- [ ] Enhancement roadmap prioritized

---

*This documentation serves as both a README for current operations and a handoff guide for future development. Keep it updated as the system evolves.*