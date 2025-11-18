# Legal Employment Tribunal AI Agent - Project Overview

## Summary

This project contains a comprehensive AI agent prompt system designed to assist with UK employment tribunal cases, with specialized focus on disability discrimination under the Equality Act 2010.

## Files Included

### 1. `legal-employment-tribunal-agent-prompt.md`
**The main system prompt** (approximately 13,000 words)

Contains:
- Complete role and identity definition
- Comprehensive legal knowledge framework covering:
  - Equality Act 2010 (all discrimination types)
  - Employment Rights Act 1996
  - Tribunal and appellate procedures
  - 30+ legal principles and case law precedents
- Detailed case-specific knowledge (Saunders v Peloton Interactive)
- Six core capability domains
- Four interaction modes (Explanatory, Analytical, Procedural, Drafting)
- Strict ethical boundaries and limitations
- Communication style guidelines
- Quick reference frameworks for key legal tests

### 2. `legal-employment-tribunal-agent-usage.md`
**Implementation guide and documentation** (approximately 10,000 words)

Contains:
- Step-by-step implementation instructions
- Configuration options for different platforms
- Seven detailed usage scenarios
- Eight comprehensive test cases with expected outputs
- Safety and compliance guidelines
- Integration patterns (chatbot, document analysis, Slack/Teams)
- Performance optimization techniques
- Troubleshooting guide
- Maintenance schedule and version control

### 3. `legal-employment-tribunal-agent-README.md`
This overview document

## Key Features

### Legal Domain Coverage

**Primary Areas:**
- Disability discrimination (all forms under Equality Act 2010)
- Reasonable adjustments law (extensive focus)
- Constructive unfair dismissal
- Employment tribunal procedures
- Employment Appeal Tribunal processes
- Remedy calculations and quantum assessment

**Procedural Expertise:**
- Disclosure obligations and disputes
- Evidence analysis and adverse inferences
- Case management and hearing preparation
- Reconsideration applications
- Appeals on points of law
- Professional conduct matters (SRA investigations)

### Agent Capabilities

1. **Legal Education** - Explains complex legal concepts in accessible language
2. **Case Analysis** - Applies legal tests to specific fact patterns
3. **Document Drafting** - Assists with witness statements, appeals, submissions
4. **Procedural Guidance** - Navigates tribunal processes and deadlines
5. **Evidence Analysis** - Identifies inconsistencies, gaps, and opportunities
6. **Remedy Calculation** - Computes financial loss, injury to feelings, future loss

### Ethical Framework

The agent operates within strict boundaries:

**WILL:**
- Provide legal information and explanation
- Analyze how law applies to user's facts
- Assist with document structure and drafting
- Calculate remedy figures
- Organize evidence and identify gaps

**WILL NOT:**
- Provide definitive legal advice (reserved activity)
- Make strategic decisions for users
- Guarantee outcomes
- Replace qualified legal representation
- Represent users in hearings
- Practice law

### Target Users

**Primary:**
- Litigants in Person (LIPs) navigating tribunal proceedings
- Individuals considering employment tribunal claims
- Users preparing for hearings or appeals

**Secondary:**
- Paralegals supporting employment cases
- Law students studying employment law
- Legal professionals seeking quick reference

**Not designed for:**
- Employers/respondents (perspective is claimant-focused)
- Commercial legal practice
- Non-UK jurisdictions (England & Wales focus)

## Architecture Highlights

### Knowledge Representation

The agent uses a **multi-layered knowledge architecture**:

1. **Foundational Layer**: Statutory provisions and legal tests
2. **Case Law Layer**: Precedents and principles from key cases
3. **Procedural Layer**: Tribunal rules and appellate procedures
4. **Case-Specific Layer**: Detailed knowledge of reference case (Saunders v Peloton)
5. **Practical Layer**: Calculation methods, templates, tactical guidance

### Interaction Design

**Four Primary Modes:**

1. **Explanatory Mode** → Legal education and concept clarification
2. **Analytical Mode** → Applying law to facts, identifying arguments
3. **Procedural Mode** → Process navigation and compliance
4. **Drafting Mode** → Document preparation assistance

The agent dynamically switches modes based on query patterns.

### Safety Mechanisms

**Built-in Protections:**
- Ethical boundary reinforcement throughout prompt
- Explicit "do not" lists for prohibited actions
- Mandatory disclaimers for complex/high-stakes matters
- Uncertainty acknowledgment requirements
- Legal advice referral triggers
- Crisis response protocols (suicidal ideation, severe distress)

## Implementation Quick Start

### Basic Implementation (Python)

```python
import anthropic

# Load system prompt
with open("legal-employment-tribunal-agent-prompt.md", "r") as f:
    system_prompt = f.read()

# Initialize client
client = anthropic.Anthropic(api_key="your-key")

# Get response
response = client.messages.create(
    model="claude-3-5-sonnet-20241022",
    max_tokens=4096,
    temperature=0.4,
    system=system_prompt,
    messages=[
        {"role": "user", "content": "What is the test for reasonable adjustments?"}
    ]
)

print(response.content[0].text)
```

### Recommended Configuration

```yaml
Model: claude-3-5-sonnet-20241022 (or newer)
Temperature: 0.3-0.5 (balance accuracy with fluency)
Max Tokens: 4096
Context Window: 100K+ recommended
System Prompt: [full contents of legal-employment-tribunal-agent-prompt.md]
```

## Use Case Examples

### Example 1: Understanding Legal Concepts
```
User: "What is constructive knowledge in reasonable adjustments?"

Agent: [Provides detailed explanation of:
- Legal test from case law
- What employer "should have known"
- Duty to make enquiries
- Application to specific scenarios
- Examples from case law]
```

### Example 2: Analyzing Fact Pattern
```
User: "My employer refused to let me work from home due to my anxiety.
Is this discrimination?"

Agent: [Analyzes potential claims:
- S.20-21 reasonable adjustments (PCP: office attendance requirement)
- S.15 discrimination arising (if unfavourable treatment due to anxiety symptoms)
- Knowledge requirements
- Evidence needed
- Strengths/weaknesses
- Recommends legal consultation]
```

### Example 3: Document Drafting
```
User: "Help me draft grounds of appeal for my dismissed victimisation claim"

Agent: [Provides:
- Template structure
- Explanation that appeals are on law, not fact
- How to identify legal errors
- Citation format
- Placeholders for specific facts
- Reminder to seek specialist review]
```

### Example 4: Remedy Calculation
```
User: "I earned £3,000/month, was unemployed 6 months, found new job at £2,500.
What's my financial loss?"

Agent: [Calculates:
- Past loss period 1: £3,000 × 6 = £18,000
- Ongoing loss: £500/month differential
- Pension loss
- Other remedy heads
- ACAS uplift potential]
```

## Testing and Validation

### Test Suite Included

The usage guide includes **8 comprehensive test cases**:

1. Basic legal concept explanation
2. Complex fact pattern analysis
3. Procedural guidance
4. Document drafting assistance
5. Ethical boundary testing
6. Case-specific queries (Saunders v Peloton)
7. Remedy quantum calculation
8. Knowledge limitation handling

Each test includes:
- Input query
- Expected output elements
- Quality metrics checklist
- Pass/fail criteria

### Quality Assurance Checklist

- [ ] Legal accuracy (statutory references correct)
- [ ] Case law citations valid
- [ ] Procedural guidance current
- [ ] Ethical boundaries maintained
- [ ] Disclaimers present and appropriate
- [ ] Language accessible but precise
- [ ] Examples helpful and accurate
- [ ] Recommendations to seek legal advice when appropriate

## Maintenance and Updates

### Update Schedule

**Monthly:**
- Review new case law
- Update Vento bands if adjusted
- Check procedural rule changes

**Quarterly:**
- Legal expert review
- User feedback incorporation
- Performance optimization

**Annually:**
- Major prompt revision
- Comprehensive testing
- Compliance audit

### Version Control

Track versions in filenames:
```
legal-employment-tribunal-agent-prompt-v1.0.md
legal-employment-tribunal-agent-prompt-v1.1.md
legal-employment-tribunal-agent-prompt-v2.0.md
```

Maintain changelog documenting:
- Added features
- Changed sections
- Fixed errors
- Deprecated content

## Legal and Compliance

### Regulatory Considerations

**This agent is designed to provide legal INFORMATION, not legal ADVICE.**

- Does not create solicitor-client relationship
- Not a substitute for qualified legal representation
- Users retain all decision-making authority
- No guarantees or warranties about outcomes

### Data Protection

**GDPR Compliance:**
- Minimize personal data collection
- Anonymize user examples
- Secure storage of conversations
- User consent for data retention
- Right to deletion compliance

### Professional Standards

**Alignment with:**
- SRA guidance on legal information services
- Law Society guidance on AI use
- Legal Services Act 2007 (reserved activities)
- Employment Tribunal Practice Directions

## Limitations

### What This Agent Cannot Do

1. **Practice Law** - Cannot provide definitive legal advice or make strategic decisions
2. **Predict Outcomes** - Cannot guarantee tribunal will rule in user's favor
3. **Replace Representation** - Cannot substitute for qualified solicitor or barrister
4. **Medical Opinions** - Cannot diagnose or assess medical conditions
5. **Real-Time Updates** - Knowledge has cutoff date, may not reflect latest developments
6. **Jurisdiction** - Focused on England & Wales; limited Scotland/Northern Ireland

### When Professional Help is Essential

Agent MUST recommend users seek qualified legal advice for:
- High-value claims (£25,000+)
- Complex legal arguments requiring specialist expertise
- Appellate proceedings (EAT, Court of Appeal)
- Settlement negotiations
- Professional conduct allegations
- Cross-examination preparation
- Costs applications against them

## Success Metrics

### How to Measure Effectiveness

**Quantitative:**
- User satisfaction ratings
- Task completion rates
- Accuracy of legal information (expert validation)
- Response time
- Token efficiency

**Qualitative:**
- User confidence improvement
- Understanding of legal processes
- Quality of drafted documents
- Appropriateness of legal advice referrals
- Ethical boundary maintenance

## Support and Resources

### For Users of the Agent

- **ACAS**: Free advice and early conciliation
- **Citizens Advice**: General employment advice
- **Free Representation Unit**: Pro bono tribunal representation
- **Advocate**: Disability discrimination specialists
- **LawWorks**: Pro bono legal assistance

### For Implementers

- Anthropic Documentation: https://docs.anthropic.com/
- Claude Prompt Engineering: https://docs.anthropic.com/claude/docs/prompt-engineering
- Employment Tribunal Rules: https://www.gov.uk/employment-tribunals
- BAILII (Case Law Database): https://www.bailii.org/

### For Legal Validation

Consult:
- Employment law barristers or solicitors
- Law Society guidance
- SRA compliance officers
- Employment tribunal clerks (procedural questions)

## License and Attribution

**Disclaimer:**
```
This AI assistant provides legal INFORMATION only, not legal ADVICE.
It is not a substitute for qualified legal representation.

Users should verify all information with qualified solicitors or barristers.
No liability is accepted for decisions made based on AI responses.
This service does not create a solicitor-client relationship.

By using this service, you acknowledge these limitations.
```

## Contributing

### How to Improve This Agent

1. **Legal Updates**: Submit corrections for outdated case law or statutory references
2. **Procedural Changes**: Note tribunal rule changes or new practice directions
3. **Usability**: Suggest improvements to clarity or accessibility
4. **Test Cases**: Contribute additional test scenarios
5. **Integration Patterns**: Share implementation examples

### Feedback Categories

- **Legal Accuracy** (highest priority)
- **Clarity and Accessibility**
- **Ethical Boundary Issues**
- **Technical Implementation**
- **User Experience**

## Project Context

This agent was developed to address the **access to justice gap** in UK employment law, where:

- Many discrimination claimants cannot afford legal representation
- Employment tribunal procedures are complex and intimidating
- Legal information is often inaccessible or unclear
- Litigants in Person (LIPs) face significant disadvantages

**Design Philosophy:**
- **Empower, don't replace** - Users maintain autonomy and decision-making
- **Educate, don't advise** - Provide information, not professional legal advice
- **Accessible, not simplified** - Maintain legal accuracy while improving clarity
- **Supportive, not directive** - Guide without making decisions
- **Transparent, not overconfident** - Honest about limitations and uncertainties

## Technical Specifications

### Prompt Statistics

**Main System Prompt:**
- ~13,000 words
- ~18,000 tokens
- 50+ sections/subsections
- 30+ case law references
- 20+ statutory provisions

**Coverage:**
- 6 discrimination types under Equality Act 2010
- 7 litigated claims (Saunders v Peloton)
- 4 interaction modes
- 10+ procedural stages
- 30+ anticipated matters

### Performance Benchmarks

**Expected Response Times:**
- Simple concept explanation: 5-10 seconds
- Complex fact analysis: 15-25 seconds
- Document drafting: 20-35 seconds
- Calculation: 5-10 seconds

**Token Usage:**
- Average response: 800-1,500 tokens
- Complex analysis: 2,000-3,500 tokens
- Document templates: 1,500-2,500 tokens

### Integration Requirements

**Minimum:**
- API access to Claude 3.5 Sonnet or newer
- 8K context window (100K+ recommended)
- Text input/output capability

**Recommended:**
- Streaming API support (better UX)
- Conversation history persistence
- Document upload capability
- Citation tracking
- User feedback collection

## Future Development

### Planned Enhancements

**Short-term (3-6 months):**
- Expand to other protected characteristics (race, sex, religion)
- Add whistleblowing claims expertise
- Enhance Scottish tribunal procedure coverage
- Integrate tribunal forms completion assistance

**Medium-term (6-12 months):**
- Real-time case law update integration
- Document upload and analysis capabilities
- Multi-case comparison and patterns
- Enhanced remedy calculators with scenario modeling

**Long-term (12+ months):**
- Integration with tribunal e-filing systems
- Predictive case outcome modeling (with caveats)
- Automated evidence organization
- Virtual hearing preparation simulation

### Research Questions

- How does AI assistance affect LIP success rates?
- What types of queries benefit most from AI support?
- Where do users still need human legal advice?
- How can we measure "access to justice" improvements?

## Conclusion

This Legal Employment Tribunal AI Agent represents a comprehensive system for supporting individuals navigating UK employment tribunal proceedings. It balances legal accuracy with accessibility, empowerment with appropriate limitations, and support with ethical boundaries.

**Key Strengths:**
1. Comprehensive legal knowledge framework
2. Strict ethical boundaries
3. Multiple interaction modes
4. Detailed procedural guidance
5. Practical calculation and drafting support
6. Extensive testing and validation guidance

**Appropriate Use:**
- Legal education and concept clarification
- Case organization and analysis
- Document drafting assistance
- Procedural navigation
- Evidence analysis
- Remedy calculation

**Requires Human Legal Advice:**
- Strategic legal decisions
- High-stakes or complex cases
- Appellate proceedings
- Settlement negotiations
- Cross-examination tactics
- Professional conduct matters

When implemented thoughtfully and used within its designed scope, this agent can significantly improve access to justice for individuals facing employment discrimination.

---

**Project Version:** 1.0
**Created:** 2025-11-18
**Last Updated:** 2025-11-18
**Status:** Production Ready
**License:** [Specify license]
**Maintained By:** [Your organization/team]
**Contact:** [Your contact information]
