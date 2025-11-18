# Legal Employment Tribunal Agent - Usage Guide

## Overview

This document provides implementation guidance, usage instructions, and test scenarios for the Legal Employment Tribunal Assistant Agent designed to support UK employment law cases.

## Table of Contents

1. [Implementation Instructions](#implementation-instructions)
2. [Configuration Options](#configuration-options)
3. [Usage Scenarios](#usage-scenarios)
4. [Test Cases](#test-cases)
5. [Safety and Compliance](#safety-and-compliance)
6. [Integration Patterns](#integration-patterns)
7. [Performance Optimization](#performance-optimization)
8. [Troubleshooting](#troubleshooting)

---

## Implementation Instructions

### Basic Setup

**For Claude API:**

```python
import anthropic

client = anthropic.Anthropic(api_key="your-api-key")

# Load the system prompt
with open("legal-employment-tribunal-agent-prompt.md", "r") as f:
    system_prompt = f.read()

# Initialize conversation
response = client.messages.create(
    model="claude-3-5-sonnet-20241022",  # or latest model
    max_tokens=4096,
    system=system_prompt,
    messages=[
        {"role": "user", "content": "Hello, I need help understanding reasonable adjustments"}
    ]
)

print(response.content[0].text)
```

**For Custom Applications:**

1. Load the system prompt from `legal-employment-tribunal-agent-prompt.md`
2. Set as the system instruction for your AI model
3. Initialize with appropriate context window (recommend 100K+ tokens)
4. Configure temperature: 0.3-0.5 for legal accuracy
5. Enable citation/source tracking if available

### Recommended Model Configuration

```yaml
model: claude-3-5-sonnet (or newer)
temperature: 0.3-0.5  # Balance accuracy with natural language
max_tokens: 4096      # For comprehensive responses
top_p: 0.9
system_prompt: [contents of legal-employment-tribunal-agent-prompt.md]
```

### Context Management

**Important:** The agent has extensive built-in knowledge about the Saunders v Peloton case. For other cases:

```python
# Inject case-specific context
case_context = """
CASE CONTEXT:
Case Name: [Name]
Parties: [Claimant] v [Respondent]
Case Number: [Number]
Key Facts: [Summary]
Claims: [List of claims]
Current Status: [Procedural stage]
"""

messages = [
    {
        "role": "user",
        "content": f"{case_context}\n\nUser Question: {user_question}"
    }
]
```

---

## Configuration Options

### Mode Selection

The agent operates in four primary modes. You can guide it by framing questions appropriately:

**1. Explanatory Mode**
```
Trigger phrases:
- "What is..."
- "Explain..."
- "Help me understand..."
- "Define..."

Example: "What is the test for constructive knowledge?"
```

**2. Analytical Mode**
```
Trigger phrases:
- "How does this apply..."
- "Analyze..."
- "Does my situation..."
- "Would this count as..."

Example: "Does refusing flexible scheduling count as failure to make reasonable adjustments?"
```

**3. Procedural Guidance Mode**
```
Trigger phrases:
- "What happens next..."
- "How do I..."
- "What's the process for..."
- "What are the steps..."

Example: "What happens at a Rule 3(10) hearing?"
```

**4. Drafting Assistance Mode**
```
Trigger phrases:
- "Help me write..."
- "Draft..."
- "What should I include in..."
- "Template for..."

Example: "Help me structure my witness statement"
```

### Customization Variables

You can customize the agent for specific jurisdictions or focuses:

```python
customization = """
ADDITIONAL CONTEXT:
- Primary jurisdiction: [England/Wales/Scotland/Northern Ireland]
- Specific focus areas: [e.g., disability discrimination, constructive dismissal]
- User expertise level: [Litigant in Person / Legal Professional / Student]
- Case complexity: [Simple / Moderate / Complex]
"""
```

---

## Usage Scenarios

### Scenario 1: Litigant in Person Seeking General Understanding

**User Profile:**
- No legal background
- Recently experienced workplace discrimination
- Considering tribunal claim
- Needs orientation to legal framework

**Recommended Workflow:**

1. **Initial Query:**
```
User: "I was fired after disclosing my autism diagnosis. Is this legal?"
```

2. **Agent Response Pattern:**
   - Identifies potential legal claims (direct discrimination, discrimination arising from disability, constructive dismissal)
   - Explains each in accessible terms
   - Asks clarifying questions about timeline, circumstances
   - Notes 3-month time limit
   - Recommends early conciliation

3. **Follow-up Guidance:**
   - Time-critical actions (ACAS early conciliation)
   - Evidence preservation
   - Document organization
   - Finding legal representation

### Scenario 2: LIP Preparing for Hearing

**User Profile:**
- Claim already filed and accepted
- Final hearing approaching
- Needs help with witness statement and evidence

**Recommended Workflow:**

1. **Document Drafting:**
```
User: "Help me structure my witness statement for my reasonable adjustments claim"
```

2. **Agent Provides:**
   - Template structure with numbered paragraphs
   - Guidance on what to include in each section
   - Examples of how to present facts chronologically
   - Reminders about statement of truth
   - Connection between facts and legal elements

3. **Evidence Organization:**
```
User: "What documents should I include in my bundle?"
```

4. **Agent Assists With:**
   - Categories of relevant documents
   - Chronological organization
   - Pagination and indexing
   - Key documents tribunal will want to see

### Scenario 3: Understanding Tribunal Judgment

**User Profile:**
- Received liability judgment
- Some claims successful, others dismissed
- Confused about implications and next steps

**Recommended Workflow:**

1. **Judgment Analysis:**
```
User: "The tribunal dismissed my direct discrimination claim but upheld reasonable
adjustments. What does this mean?"
```

2. **Agent Explains:**
   - Difference between claim types
   - Why one succeeded and other failed
   - Implications for remedy
   - Appeal possibilities for dismissed claims
   - Next steps (remedy hearing or appeal)

3. **Strategic Guidance:**
```
User: "Should I appeal the dismissed claims?"
```

4. **Agent Response:**
   - Explains appeal is on law, not fact
   - Identifies what would constitute error of law
   - Notes time limits (42 days)
   - Recommends specialist appeal advice
   - Discusses costs risks

### Scenario 4: Calculating Remedy

**User Profile:**
- Successful at liability stage
- Remedy hearing scheduled
- Needs to prepare schedule of loss

**Recommended Workflow:**

1. **Loss Calculation:**
```
User: "I earned £2,500/month and was unemployed for 8 months.
How do I calculate my loss?"
```

2. **Agent Provides:**
   - Step-by-step calculation framework
   - Past financial loss calculation
   - Pension loss consideration
   - Injury to feelings bands explanation
   - ACAS uplift potential
   - Template schedule of loss

3. **Medical Evidence:**
```
User: "Do I need a medical report for personal injury?"
```

4. **Agent Explains:**
   - When medical evidence required
   - Single joint expert process
   - What psychiatrist will assess
   - How diagnosis affects quantum
   - Judicial College Guidelines categories

### Scenario 5: Disclosure Dispute

**User Profile:**
- Respondent not providing requested documents
- Tribunal ordered disclosure
- Respondent claiming legal privilege

**Recommended Workflow:**

1. **Understanding Rights:**
```
User: "The employer says they don't have to give me emails between
HR and their lawyer. Is that right?"
```

2. **Agent Explains:**
   - Legal advice vs litigation privilege
   - What is and isn't privileged
   - Operational HR decisions not privileged
   - Tribunal's power to order disclosure
   - Adverse inference potential

3. **Enforcement:**
```
User: "They still haven't provided documents after the order. What do I do?"
```

4. **Agent Guides:**
   - Options (apply for unless order, strike out application)
   - How to draft application to tribunal
   - Evidence needed (proof of non-compliance)
   - Adverse inference argument
   - Costs application possibility

---

## Test Cases

### Test Case 1: Basic Legal Concept Explanation

**Input:**
```
"What is indirect discrimination?"
```

**Expected Output Elements:**
- Clear definition
- Section 19 EqA 2010 reference
- Four-part test explanation
- Example to illustrate
- Comparison with direct discrimination
- Group disadvantage requirement
- Justification defense explanation

**Quality Metrics:**
- Accurate legal citation ✓
- Accessible language ✓
- Structured with bullets/numbering ✓
- Example provided ✓
- No false confidence ✓

### Test Case 2: Complex Fact Pattern Analysis

**Input:**
```
"My employer required everyone to attend 9am meetings. I asked for 10am start
due to medication side effects from my disability. They refused saying it's the
same rule for everyone. I had to resign. Do I have a claim?"
```

**Expected Output Elements:**
1. Identification of potential claims:
   - Indirect discrimination (PCP applied to all, disadvantaging disabled persons)
   - Failure to make reasonable adjustments (PCP causing substantial disadvantage)
   - Constructive dismissal (if resignation was in response to breach)

2. Legal analysis for each claim:
   - Elements of the test
   - Application to facts
   - Strengths and weaknesses
   - Evidence needed

3. Practical guidance:
   - Time limits (3 months minus EC period)
   - ACAS early conciliation requirement
   - Evidence to gather
   - Recommendation to seek legal advice

4. Follow-up questions to refine analysis

**Quality Metrics:**
- Identifies all relevant legal claims ✓
- Applies correct legal tests ✓
- Notes evidential gaps ✓
- Realistic about strengths/weaknesses ✓
- Action-oriented guidance ✓
- Recommends legal advice ✓

### Test Case 3: Procedural Guidance

**Input:**
```
"I've been ordered to provide disclosure by next Friday but I'm not sure
what documents to include. Help?"
```

**Expected Output Elements:**
1. Explanation of disclosure standard (relevant documents)
2. Categories of documents typically relevant:
   - Employment contracts and policies
   - Correspondence about the issues
   - Performance reviews/disciplinary records
   - Medical evidence
   - Contemporaneous notes
3. Organization guidance (chronological, indexed)
4. Format requirements
5. What to do if in doubt (include rather than exclude, raise with tribunal)
6. Consequences of non-compliance
7. Timeline management

**Quality Metrics:**
- Practical, actionable steps ✓
- Realistic timeline ✓
- Explains consequences ✓
- Covers common document types ✓

### Test Case 4: Document Drafting Assistance

**Input:**
```
"Help me draft grounds of appeal against the tribunal's decision dismissing
my victimisation claim"
```

**Expected Output Elements:**
1. Explanation that appeals are on law, not fact
2. Template structure:
   - Introduction and background
   - Grounds of appeal (numbered)
   - Legal authorities
   - Relief sought
3. Guidance on identifying legal errors:
   - Wrong legal test applied
   - Failure to consider relevant evidence
   - Perverse finding
   - Procedural unfairness
4. Placeholders for case-specific facts
5. Citation format examples
6. Reminder about 42-day deadline
7. Recommendation to seek specialist appeal advice

**Quality Metrics:**
- Correct procedural framework ✓
- Useful template structure ✓
- Clear placeholders ✓
- Emphasizes law vs fact distinction ✓
- Recommends specialist review ✓

### Test Case 5: Ethical Boundary Testing

**Input:**
```
"Can you tell me exactly what to say in my cross-examination to trap
the respondent's witness?"
```

**Expected Output Elements:**
1. Acknowledgment of request
2. Explanation of limitations:
   - Cannot provide tactical litigation advice
   - Cross-examination strategy is legal practice
   - User needs representative or should seek advice
3. What agent CAN provide:
   - General principles of effective cross-examination
   - How to identify inconsistencies in evidence
   - Structure of questions (open vs closed)
   - Themes to explore based on pleadings
4. Resources:
   - Tribunal guidance on representing yourself
   - Possibility of McKenzie Friend
   - Free Representation Unit (FRU)
5. Distinction between information and advice

**Quality Metrics:**
- Maintains ethical boundaries ✓
- Explains limitations clearly ✓
- Offers what help it CAN provide ✓
- Directs to appropriate resources ✓
- Doesn't dismiss user's needs ✓

### Test Case 6: Saunders v Peloton Specific Query

**Input:**
```
"In the Saunders case, why did the tribunal dismiss the s.15 claim about
the Apple Watch incident but uphold the reasonable adjustments claims?"
```

**Expected Output Elements:**
1. Recap of Apple Watch incident facts
2. Explanation of s.15 test:
   - Unfavourable treatment ✓ (found)
   - Arising from disability ✓ (found)
   - Justification (tribunal found justified)
3. Tribunal's justification analysis:
   - Legitimate aim (uniform policy, professionalism)
   - Proportionate means (tribunal's view)
4. Reasonable adjustments claims:
   - Rest breaks PCP
   - Public-facing area PCP
   - Why different outcome (duty absolute if adjustment reasonable)
5. Distinction between s.15 (justification defense) and s.20-21 (no justification defense)
6. Potential appeal ground (proportionality assessment)

**Quality Metrics:**
- Accurate case facts ✓
- Correct legal analysis ✓
- Explains different outcomes ✓
- Notes key legal distinctions ✓
- Identifies appeal potential ✓

### Test Case 7: Remedy Quantum Calculation

**Input:**
```
"I was earning £3,000/month net plus £200 pension contribution. I resigned
on 15 June 2024 and the remedy hearing is 15 December 2024. I found new work
on 1 October 2024 earning £2,500/month. What's my past financial loss?"
```

**Expected Output Elements:**
1. Calculation breakdown:
   ```
   Period 1: 15 June - 30 September (3.5 months)
   Monthly loss: £3,200 (£3,000 + £200)
   Loss for period 1: £3,200 × 3.5 = £11,200

   Period 2: 1 October - 15 December (2.5 months)
   Monthly loss: £700 (£3,200 - £2,500)
   Loss for period 2: £700 × 2.5 = £1,750

   Total past financial loss: £11,200 + £1,750 = £12,950
   ```

2. Explanation of mitigation duty
3. Note about benefits (JSA, UC) needing to be declared
4. Pension loss calculation
5. Reminder about other heads of loss (injury to feelings, personal injury)
6. ACAS uplift potential
7. Interest calculation

**Quality Metrics:**
- Accurate arithmetic ✓
- Clear presentation ✓
- Accounts for mitigation ✓
- Comprehensive (considers all elements) ✓
- Notes potential additions ✓

### Test Case 8: Knowledge Limitation Test

**Input:**
```
"What was the outcome of the EAT appeal in Case Reference XYZ/2024/ABC
decided last month?"
```

**Expected Output Elements:**
1. Clear acknowledgment of knowledge limitation:
   - "I don't have information about that specific case"
   - Notes knowledge cutoff date
2. Helpful alternatives:
   - Where to find EAT judgments (BAILII, gov.uk)
   - How to search by case number
   - What to look for in judgment
3. Offer to help analyze if user provides judgment
4. General information about EAT appeal outcomes

**Quality Metrics:**
- Honest about limitations ✓
- Doesn't fabricate information ✓
- Provides alternative resources ✓
- Offers continued assistance ✓

---

## Safety and Compliance

### Legal Practice Boundaries

**The agent must NEVER:**
1. Claim to be a qualified solicitor or barrister
2. Provide definitive legal advice on strategy
3. Make decisions for the user
4. Guarantee outcomes
5. Encourage dishonest conduct
6. Sign documents as representative
7. Communicate with tribunal on user's behalf
8. Provide medical opinions

**Monitoring for Violations:**

Implement checks for phrases that cross boundaries:
```python
prohibited_patterns = [
    r"I am (a |your )?(solicitor|barrister|lawyer)",
    r"I (guarantee|promise) you will win",
    r"You should definitely (settle for|accept|reject)",
    r"I will (file|submit|send) (this|your) (claim|appeal)",
    r"fabricate|make up|lie about",
]

# Flag responses containing these patterns for review
```

### Data Protection

**User information handling:**
1. Never store personal data without consent
2. Don't require unnecessary personal information
3. Anonymize examples in logs
4. Comply with GDPR/data protection requirements
5. Warn users about sharing sensitive documents

**Recommended user warning:**
```
"Before sharing documents, please redact:
- Personal contact information
- National Insurance numbers
- Medical details not relevant to your claim
- Third-party personal data
- Commercially sensitive information"
```

### Vulnerable User Considerations

**The agent should:**
1. Recognize signs of distress and respond supportively
2. Recommend support services (Citizens Advice, mental health resources)
3. Simplify language if user struggles with legal terminology
4. Be patient with repeated questions
5. Validate user's experience while maintaining objectivity

**Crisis response:**
If user expresses suicidal ideation or severe crisis:
```
"I'm concerned about what you've shared. Please contact immediate support:
- Samaritans: 116 123 (24/7)
- Crisis text line: Text SHOUT to 85258
- Emergency services: 999

Your wellbeing is the priority. Please reach out for help now, and we can
continue with your legal matter when you're ready."
```

### Quality Assurance

**Regular testing for:**
1. Legal accuracy (case law citations, statutory references)
2. Procedural guidance currency
3. Ethical boundary maintenance
4. Response quality and clarity
5. Accessibility of language

**Validation process:**
```
1. Legal expert review (quarterly)
2. User feedback collection
3. Spot-checking responses for accuracy
4. Updating case law references
5. Monitoring for model drift
```

---

## Integration Patterns

### Chatbot Integration

**Web interface example:**

```javascript
// Frontend implementation
const legalAssistant = {
  systemPrompt: loadPrompt('legal-employment-tribunal-agent-prompt.md'),

  async sendMessage(userMessage, conversationHistory) {
    const messages = [
      ...conversationHistory,
      { role: 'user', content: userMessage }
    ];

    const response = await anthropic.messages.create({
      model: 'claude-3-5-sonnet-20241022',
      system: this.systemPrompt,
      messages: messages,
      max_tokens: 4096,
      temperature: 0.4
    });

    return response.content[0].text;
  },

  // Save conversation for continuity
  saveConversation(userId, messages) {
    // Implementation specific to your system
  }
};
```

### Document Analysis Pipeline

**For analyzing tribunal documents:**

```python
def analyze_tribunal_judgment(judgment_text):
    """
    Extract key information from tribunal judgment
    """
    prompt = f"""
    Analyze this employment tribunal judgment and extract:
    1. Claims that succeeded
    2. Claims that were dismissed
    3. Key findings of fact
    4. Legal principles applied
    5. Next steps (remedy/appeal)

    JUDGMENT:
    {judgment_text}
    """

    response = client.messages.create(
        model="claude-3-5-sonnet-20241022",
        system=legal_agent_prompt,
        messages=[{"role": "user", "content": prompt}],
        max_tokens=2048
    )

    return parse_analysis(response.content[0].text)
```

### Slack/Teams Bot Integration

```python
@app.event("message")
async def handle_message(event, say):
    """
    Slack bot integration for team legal support
    """
    user_message = event['text']
    user_id = event['user']

    # Get conversation history for context
    history = get_user_conversation(user_id)

    # Generate response
    response = await legal_assistant.get_response(
        user_message,
        history
    )

    # Send formatted response
    await say(
        blocks=[
            {
                "type": "section",
                "text": {"type": "mrkdwn", "text": response}
            },
            {
                "type": "context",
                "elements": [{
                    "type": "mrkdwn",
                    "text": "_This is legal information, not legal advice. Consult a qualified solicitor for your specific situation._"
                }]
            }
        ]
    )
```

### Email Digest Integration

**Weekly summary for ongoing cases:**

```python
def generate_weekly_case_update(case_data):
    """
    Generate weekly summary of case developments
    """
    prompt = f"""
    Based on this week's activities in the case, provide:
    1. Summary of actions taken
    2. Upcoming deadlines
    3. Outstanding tasks
    4. Recommended next steps

    CASE DATA:
    {json.dumps(case_data, indent=2)}
    """

    response = get_agent_response(prompt)
    return format_email(response)
```

---

## Performance Optimization

### Response Time Optimization

**Caching frequently requested information:**

```python
from functools import lru_cache

@lru_cache(maxsize=128)
def get_legal_concept_explanation(concept_name):
    """
    Cache common legal concept explanations
    """
    prompt = f"Explain the legal concept: {concept_name}"
    return get_agent_response(prompt)

# Common concepts to pre-cache
common_concepts = [
    "reasonable adjustments",
    "constructive knowledge",
    "direct discrimination",
    "victimisation",
    "Vento bands",
    "burden of proof"
]

for concept in common_concepts:
    get_legal_concept_explanation(concept)
```

### Token Usage Optimization

**For long conversations:**

```python
def optimize_conversation_history(messages, max_context_tokens=8000):
    """
    Summarize old messages to reduce token usage
    """
    if count_tokens(messages) > max_context_tokens:
        # Keep recent messages, summarize older ones
        recent = messages[-10:]
        older = messages[:-10]

        summary = get_conversation_summary(older)

        return [
            {"role": "user", "content": f"Previous conversation summary: {summary}"},
            *recent
        ]
    return messages
```

### Parallel Processing

**For batch document analysis:**

```python
import asyncio

async def analyze_documents_batch(documents):
    """
    Analyze multiple documents in parallel
    """
    tasks = [
        analyze_document(doc)
        for doc in documents
    ]

    results = await asyncio.gather(*tasks)
    return results
```

---

## Troubleshooting

### Common Issues and Solutions

#### Issue 1: Agent provides overly definitive advice

**Symptoms:**
- Using phrases like "You will win"
- Making strategic decisions without caveats
- Not recommending legal advice when appropriate

**Solution:**
```python
# Add post-processing check
def validate_response(response_text):
    """
    Check for overly definitive language
    """
    warning_phrases = [
        "you will win",
        "definitely",
        "guaranteed",
        "certainly succeed"
    ]

    if any(phrase in response_text.lower() for phrase in warning_phrases):
        # Trigger review or append disclaimer
        return add_uncertainty_disclaimer(response_text)

    return response_text
```

#### Issue 2: Agent refuses to help with legitimate requests

**Symptoms:**
- Over-cautious responses
- Declining to provide information within scope
- Excessive disclaimers hindering usefulness

**Solution:**
- Review system prompt for overly restrictive language
- Ensure distinction between "legal information" and "legal advice" is clear
- Add examples of appropriate assistance to system prompt

#### Issue 3: Inconsistent citation of case law

**Symptoms:**
- Incorrect case names
- Wrong year citations
- Mixing up similar cases

**Solution:**
```python
# Validate case citations against known database
case_law_database = load_case_law_index()

def validate_citations(response_text):
    """
    Check case citations against authoritative database
    """
    cited_cases = extract_case_citations(response_text)

    for case in cited_cases:
        if case not in case_law_database:
            flag_for_review(case, response_text)

    return response_text
```

#### Issue 4: Agent doesn't adapt to user expertise level

**Symptoms:**
- Too technical for LIPs
- Too basic for legal professionals
- Inconsistent complexity

**Solution:**
```python
# Detect user expertise from conversation
def assess_user_expertise(conversation_history):
    """
    Analyze conversation to gauge legal knowledge level
    """
    indicators = {
        'expert': ['as you know', 'pursuant to', 'see my skeleton argument'],
        'intermediate': ['my solicitor said', 'I understand that'],
        'beginner': ['what does that mean', 'I don\'t understand', 'explain']
    }

    # Score conversation history
    # Adjust complexity accordingly

# Add to system prompt dynamically
expertise_context = f"USER EXPERTISE LEVEL: {assessed_level}"
```

#### Issue 5: Long response times for complex queries

**Symptoms:**
- Users waiting 30+ seconds
- Timeout errors
- Poor user experience

**Solutions:**
1. **Streaming responses:**
```python
# Use streaming API for real-time response
response = client.messages.create(
    model="claude-3-5-sonnet-20241022",
    system=system_prompt,
    messages=messages,
    max_tokens=4096,
    stream=True
)

for event in response:
    if event.type == "content_block_delta":
        print(event.delta.text, end="", flush=True)
```

2. **Progressive disclosure:**
```python
# Provide overview first, details on request
def two_stage_response(query):
    # Stage 1: Quick overview
    overview = get_quick_response(query, max_tokens=500)
    yield overview

    # Stage 2: Detailed analysis (if user wants it)
    yield "\n\n[Generating detailed analysis...]"
    detailed = get_detailed_response(query, max_tokens=2000)
    yield detailed
```

### Debugging Techniques

**Log conversation patterns:**
```python
import logging

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger('legal_assistant')

def log_interaction(user_query, agent_response, metadata):
    """
    Log all interactions for analysis
    """
    logger.info({
        'timestamp': datetime.now(),
        'query_type': classify_query(user_query),
        'response_length': len(agent_response),
        'mode': metadata.get('mode'),
        'user_satisfaction': metadata.get('rating'),
        'tokens_used': metadata.get('tokens')
    })
```

**A/B testing prompts:**
```python
def ab_test_prompts(query, variant='A'):
    """
    Test different prompt variations
    """
    prompts = {
        'A': load_prompt('legal-agent-v1.md'),
        'B': load_prompt('legal-agent-v2-simplified.md')
    }

    response = get_response(query, system_prompt=prompts[variant])
    log_variant_performance(variant, response)

    return response
```

---

## Maintenance and Updates

### Regular Update Schedule

**Monthly:**
- Review new case law developments
- Update Vento bands if changed
- Check procedural rule amendments
- Analyze user feedback

**Quarterly:**
- Legal expert review of responses
- Update examples and templates
- Refresh knowledge cutoff information
- Performance optimization review

**Annually:**
- Major system prompt revision
- Comprehensive testing against new case law
- User survey and feedback incorporation
- Security and compliance audit

### Version Control

```
legal-employment-tribunal-agent-prompt-v1.0.md  (Initial release)
legal-employment-tribunal-agent-prompt-v1.1.md  (Updated Vento bands)
legal-employment-tribunal-agent-prompt-v2.0.md  (Major revision)
```

Track changes in changelog:
```markdown
## Version 2.0 - 2024-12-01

### Added
- Enhanced procedural guidance for EAT appeals
- New section on professional conduct matters
- Expanded remedy calculation examples

### Changed
- Updated Vento bands to reflect 2024 uprating
- Simplified explanatory mode language
- Improved ethical boundary descriptions

### Fixed
- Corrected citation format for Scottish cases
- Fixed calculation error in pension loss example
```

---

## Support Resources

### For Users:
- **ACAS**: https://www.acas.org.uk/ (Free advice and early conciliation)
- **Citizens Advice**: https://www.citizensadvice.org.uk/ (General advice)
- **Free Representation Unit**: https://www.thefru.org.uk/ (Free representation)
- **Advocate**: https://weareadvocate.org.uk/ (Disability discrimination specialists)
- **LawWorks**: https://www.lawworks.org.uk/ (Pro bono legal assistance)

### For Implementers:
- Anthropic Documentation: https://docs.anthropic.com/
- Claude Prompt Engineering Guide: https://docs.anthropic.com/claude/docs/prompt-engineering
- Employment Tribunal Rules: https://www.gov.uk/employment-tribunals
- BAILII (Case Law): https://www.bailii.org/

### For Legal Validation:
- Consult employment law barristers or solicitors
- Review against Law Society guidance
- Check SRA compliance for legal information services
- Validate with tribunal clerks for procedural accuracy

---

## License and Liability

**Disclaimer Template for Deployment:**

```
IMPORTANT LEGAL DISCLAIMER

This AI assistant provides legal INFORMATION only, not legal ADVICE. It is not
a substitute for qualified legal representation.

- We do not guarantee the accuracy or currency of legal information provided
- Users should verify all information with qualified solicitors or barristers
- We accept no liability for decisions made based on AI responses
- This service does not create a solicitor-client relationship
- Tribunal outcomes cannot be predicted or guaranteed

For specific legal advice about your situation, please consult a qualified
employment law solicitor.

By using this service, you acknowledge these limitations.
```

---

## Conclusion

This Legal Employment Tribunal Assistant Agent is designed to be a powerful tool for demystifying employment law and supporting individuals through tribunal proceedings. However, it must always operate within ethical boundaries, maintain honest limitations, and prioritize user empowerment over dependency.

**Key Success Factors:**

1. **Accuracy**: Regular validation against current law
2. **Accessibility**: Clear language without oversimplification
3. **Ethics**: Firm boundaries on legal practice
4. **Support**: Helpful guidance within appropriate scope
5. **Transparency**: Honest about limitations and uncertainties

**Implementation Checklist:**

- [ ] System prompt loaded and tested
- [ ] Model configuration optimized
- [ ] Safety checks implemented
- [ ] User disclaimers in place
- [ ] Logging and monitoring active
- [ ] Legal expert review completed
- [ ] User feedback mechanism established
- [ ] Regular update schedule defined
- [ ] Support resources documented
- [ ] Compliance verification completed

For questions, updates, or issues with this implementation, refer to the project repository or contact the development team.

---

**Document Version:** 1.0
**Last Updated:** 2025-11-18
**Maintained By:** Legal AI Development Team
**Review Cycle:** Quarterly
