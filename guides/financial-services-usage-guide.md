# Claude.ai Financial Services Prompts - Usage Guide

This directory contains prompts designed to transform Claude.ai into a specialized financial services assistant, mirroring the capabilities of Claude for Financial Services.

## Available Prompts

### 1. Full System Prompt (`claude-ai-financial-services-prompt.md`)
**Use for:** Complete reference documentation and training
**Length:** ~2,500 words
**Best for:**
- Understanding all capabilities and Skills
- Reference guide for your team
- Comprehensive onboarding material
- Project documentation

### 2. Concise Prompt (`claude-ai-financial-services-prompt-concise.md`)
**Use for:** Actual Claude.ai conversations
**Length:** ~400 words
**Best for:**
- Project instructions on Claude.ai
- Start of conversation context
- Quick reference for users
- Day-to-day usage

## How to Use These Prompts

### Option 1: Claude.ai Project Instructions (Recommended)

1. Go to Claude.ai and create a new Project
2. Name it something like "Financial Analysis" or "Investment Research"
3. Click "Project Settings" or "Custom Instructions"
4. Paste the **concise prompt** into the instructions field
5. Upload your financial documents (10-Ks, models, CIMs, etc.)
6. Start conversations - Claude will automatically use the instructions

**Benefits:**
- Instructions apply to all conversations in the project
- Context persists across multiple chats
- Documents are readily available
- Most efficient approach

### Option 2: Conversation Starter

1. Start a new conversation on Claude.ai
2. Paste the **concise prompt** as your first message
3. Then provide your actual request
4. Continue the conversation normally

**Benefits:**
- Works in any conversation
- No project setup required
- Quick one-off analyses

### Option 3: Custom System Prompt (If Available)

If Claude.ai adds support for system prompts:
1. Use the **full system prompt** as a system message
2. Provides comprehensive context for all interactions

## Workflow Examples

### Example 1: Valuation Analysis

**Setup:**
1. Create project: "ACME Corp Valuation"
2. Add concise prompt to project instructions
3. Upload: ACME 10-K, competitor 10-Ks, industry reports

**Conversation:**
```
You: "Build a comps table for ACME comparing to its top 5 peers,
focusing on EV/Revenue and EV/EBITDA multiples"

Claude: [Loads Comps Analysis Skill and creates table]

You: "Now build a DCF model with 5-year projections"

Claude: [Loads DCF Modeling Skill and creates model]

You: "Combine these into an initiating coverage report"

Claude: [Loads Initiating Coverage Skill and creates report]
```

### Example 2: Due Diligence

**Setup:**
1. Create project: "Target Co Due Diligence"
2. Add concise prompt to project instructions
3. Upload: CIM, financial statements, customer contracts, management presentation

**Conversation:**
```
You: "Process these documents and create a due diligence data pack
with normalized financials and key findings"

Claude: [Loads Due Diligence Data Pack Skill]
- Extracts financial data into structured Excel
- Normalizes for one-time items
- Summarizes customer concentration
- Highlights key contract terms
- Creates findings summary
```

### Example 3: Earnings Analysis

**Setup:**
1. Create project: "Portfolio Monitoring Q1 2024"
2. Add concise prompt to project instructions
3. Upload: Latest earnings releases, transcripts, presentations

**Conversation:**
```
You: "Analyze Apple's Q1 earnings - beat/miss analysis and thesis impact"

Claude: [Loads Earnings Analysis Skill]
- Compares to consensus estimates
- Analyzes revenue and margin drivers
- Reviews guidance changes
- Updates investment thesis
- Creates 8-12 page report
```

## Required Financial Skills Setup

These prompts reference six specialized Skills that you should have in your Claude.ai setup:

```
/financial-services/
  SKILL.md (main skill file)
  skills/
    comps-analysis.md
    dcf-modeling.md
    initiating-coverage.md
    strip-profile.md
    due-diligence.md
    earnings-analysis.md
```

**Note:** Skills are loaded dynamically by Claude.ai when relevant to the task. The prompts are designed to work even if you haven't explicitly created these Skill files yet, but having them provides more detailed, specialized guidance.

## Tips for Best Results

### 1. Project Organization
- One project per deal/company/thesis
- Clear naming conventions
- Upload all source documents upfront
- Maintain context across conversations

### 2. Effective Requests
- Be specific about desired output format
- Mention timeframes and data dates
- Specify which methodology/Skill to use if needed
- Provide examples of preferred formatting

### 3. Iterative Development
- Start with high-level analysis
- Drill into details as needed
- Request specific sections separately
- Build complex deliverables step-by-step

### 4. Quality Control
- Always review calculations independently
- Verify formula logic in Excel models
- Check data sources and dates
- Add required compliance disclosures

## Customization

### Adapting for Your Firm

You can customize these prompts by:

1. **Adding firm-specific templates:**
   ```
   "Use our standard investment memo format:
   - Executive Summary (1 page)
   - Investment Thesis (2-3 pages)
   - ..."
   ```

2. **Specifying preferred methodologies:**
   ```
   "For DCF models, always use:
   - 10-year projection period
   - Exit multiple terminal value
   - WACC range of 8-12%"
   ```

3. **Including compliance requirements:**
   ```
   "All valuations must include:
   - Range of outcomes (low/base/high)
   - Key assumption sensitivity
   - Disclaimer: [your standard text]"
   ```

### Sector Specialization

Add sector-specific context:

```
"Focus on SaaS company metrics:
- ARR and net retention
- Rule of 40
- CAC payback period
- LTV/CAC ratio"
```

## Troubleshooting

**Issue:** Skills not loading automatically
**Solution:** Explicitly mention the Skill name in your request

**Issue:** Output format not matching expectations
**Solution:** Provide a template or example of desired format

**Issue:** Missing context from earlier in conversation
**Solution:** Use Projects to maintain context; summarize key points when starting new conversations

**Issue:** Excel formulas not working correctly
**Solution:** Request formula validation; review complex calculations manually

## Next Steps

1. Choose which prompt version to use (concise recommended for daily use)
2. Create a Claude.ai Project for your work
3. Add the prompt to Project instructions
4. Upload your financial documents
5. Start with a simple request to test
6. Iterate and refine based on results

## Support

For questions about:
- **Claude.ai features:** See Claude.ai documentation
- **Financial Skills:** Review individual Skill files
- **Prompt customization:** Modify the prompts to match your needs
- **Workflow optimization:** Experiment with different Project structures

---

**Version:** 1.0
**Last Updated:** 2025-11-14
**Compatibility:** Claude.ai (Sonnet 4.5 and later recommended)
