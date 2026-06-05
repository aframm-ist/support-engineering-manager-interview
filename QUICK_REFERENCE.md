# Quick Reference for Interviewers

## Interview Schedule (2.5 hours)

| Segment | Duration | Topics |
|---------|----------|--------|
| **Technical** | 60 min | K8s troubleshooting, observability, support tooling, APIs |
| **Leadership** | 60 min | Team mgmt, metrics, process, difficult situations |
| **Product & Fit** | 30 min | Feedback loop, Istari knowledge, excitement |
| **Debrief & Notes** | 10–15 min | Document assessment |

---

## 5 Key Questions (If Time is Short)

1. **Walk me through the last time you debugged a pod crash on production.** (Technical + communication)
2. **Tell me about hiring or developing someone on your team. What made them successful?** (Leadership)
3. **You notice the same issue reported 5 times in a month. What do you do?** (Product thinking + operations)
4. **Tell me about a time you had to advocate for a customer with an engineering team that didn't want to listen.** (Leadership + product sense)
5. **What excites you about this role, and what are your concerns?** (Fit + honesty)

---

## Scoring Reminder

| Rating | Meaning |
|--------|---------|
| **5** | Exceptional. Would hire immediately. |
| **4** | Strong. Clear fit. Minimal concerns. |
| **3** | Competent. Growth areas exist, but coachable. |
| **2** | Below expectations. Significant gaps. |
| **1** | Not suitable for this role. |

**Target thresholds**:
- **Technical**: ≥3
- **Leadership**: ≥4 (this is a manager role!)
- **Product Thinking**: ≥3
- **Istari Fit**: ≥4

**Recommendation**:
- All four ≥ threshold → **Strong Yes**
- Three of four ≥ threshold → **Yes** (if one gap is addressable)
- Two or fewer ≥ threshold → **No** or **Maybe** (depends on severity)

---

## Red Flags Checklist

- [ ] Struggles to articulate their thinking clearly
- [ ] No hands-on K8s or troubleshooting experience
- [ ] Limited or no team management experience
- [ ] Treats support as transactional ("fix and move on")
- [ ] Doesn't ask intelligent questions about Istari or the role
- [ ] Avoids accountability or blames others
- [ ] Reluctant to admit gaps or learn new things
- [ ] Says "I don't know" and stops (vs. "I haven't done that, but here's how I'd approach it")

---

## What to Prepare Before the Interview

1. **Read the resume** — What stands out? What questions do you have?
2. **Skim their recent background** — Are they coming from similar roles? Different industry?
3. **Prepare your own story** — Why do you work at Istari? What's exciting about this team?
4. **Have an example ready** — If they ask "What's a common customer issue?", be ready with a real one.
5. **Set your phone to Do Not Disturb** — This deserves your full attention.

---

## During the Interview

**Start** (5 min):
- Welcome, put them at ease
- Quick intro: "I manage/work on [X], so I'm really interested in your support background"
- Set expectations: "We'll dig into technical depth, leadership, and how you think about product. Feel free to ask questions along the way."

**Middle** (2 hours):
- Take notes. Use their words when possible.
- If they meander, gently redirect: "That's interesting. Let me make sure I understand..."
- Don't be afraid of silence. Let them think.
- Ask follow-ups. "Tell me more" and "What did you do after that?" are fair game.

**End** (10–15 min):
- "What questions do you have for me?"
- "What excites you about this role, and what concerns you?"
- "Timeline: If we moved forward, when would you be available?"
- Thank them, give a sense of next steps.

---

## After the Interview

**Within 30 minutes**:
- Document your assessment using CANDIDATE_EVAL_TEMPLATE.md
- Rate them on the four dimensions
- Note specific quotes or examples
- Flag anything you want to probe in a follow-up

**Within 24 hours**:
- Sync with other interviewers if multiple people interviewed
- Discuss and calibrate
- Make a recommendation (yes/no/maybe)
- If "maybe," identify what would move the needle

---

## Example Strong Answers (See INTERVIEWER_CALIBRATION.md for Details)

**"Walk me through debugging a pod crash"**:
- Systematic (get status, check logs, describe pod, investigate layers)
- Uses the right tools
- Thinks about ownership (product bug vs. customer config)

**"Tell me about developing someone"**:
- Specific hiring criteria
- Intentional onboarding
- Recognition of growth edges
- Targeted interventions
- Measured over time

**"Recurring issue—what do you do?"**:
- Consolidate into a runbook/KB
- Assess if it's a product bug
- Escalate to engineering
- Measure impact

---

## Difficult Situations (How They Might Handle Them)

### Scenario: Support queue is backed up, tickets are aging

**What to listen for**:
- Do they dig into why (are TSEs slow, are they inexperienced, is triage broken)?
- Or do they just say "hire more people"?
- Do they think about short-term relief vs. long-term fix?

### Scenario: Customer escalates a product bug, engineering doesn't want to fix it

**What to listen for**:
- Do they advocate for the customer?
- Can they present the bug in a way engineering respects (reproducibility, severity)?
- Do they offer a workaround while escalating?

### Scenario: One TSE is underperforming

**What to listen for**:
- Early intervention (not waiting for it to blow up)
- Diagnosis (is it capability, motivation, environment, tools?)
- Clear expectations + support
- Willingness to make hard calls

---

## Common Mistakes Interviewers Make

1. **Only asking technical questions** — You need to assess leadership and judgment too.
2. **Falling in love with credentials** — "They have a CKA" doesn't mean they can manage people.
3. **Not probing vague answers** — "It was good" needs follow-up: "What made it work?"
4. **Comparing to past candidates** — Judge this candidate on the role's needs, not "better than X."
5. **Selling too hard** — Focus on evaluating first. You can sell Istari if they're a fit.
6. **Letting them off the hook** — If you don't understand their answer, it's fair to ask again.
7. **Taking silence as a negative** — Some people need to think. Give them space.

---

## Contact / Questions?

- **Questions about the role**: Reach out to VP of Engineering
- **Questions about a candidate**: Sync with other interviewers
- **Feedback on these interview guides**: Let's iterate!
