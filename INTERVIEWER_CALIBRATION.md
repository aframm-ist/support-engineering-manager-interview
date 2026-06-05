# Interviewer Calibration Guide
## Support Engineering Manager Interview

### Purpose
This guide helps interviewers calibrate their assessments and catch blind spots. Use it alongside INTERVIEW_GUIDE.md.

---

## What Good Answers Look Like

### Technical: Kubernetes Troubleshooting

**Example Strong Answer** (K8s debugging scenario):
> "First, I'd get the pod status with `oc get pods` or `kubectl get pods` to see what state it's in—is it Pending, CrashLoopBackOff, or ImagePullBackOff? That tells me where to look next.
> 
> If it's Pending, I'd check node capacity and PVC attachment.
> 
> If it's CrashLoopBackOff, I'd check logs with `kubectl logs --previous` to see what the last attempt told me, then look at events with `kubectl describe pod`.
> 
> I'd also check the environment—is the ConfigMap or Secret it depends on actually there? Any RBAC issues?
> 
> Finally, I'd look at the pod's resource limits—sometimes a memory limit is too low and the process gets OOMKilled silently.
> 
> Once I've identified the root cause, I'd document it and ask: is this a config error on the customer's side, or a gap in our docs? If it's a product issue, I'd flag it to engineering."

**What makes this strong**:
- Systematic troubleshooting (not random guessing)
- Uses the right tools (`kubectl`, `oc`)
- Distinguishes between different failure modes
- Thinks about multiple layers (infra, config, application)
- Connects back to documentation/product feedback

**Example Weak Answer**:
> "I'd ask the DevOps team to look at it."

OR

> "I'd increase the resources and see if that fixes it."

**Why it's weak**:
- Abdicates responsibility; doesn't troubleshoot
- Assumes the problem without investigating
- No methodology, just trial and error

---

### Leadership: Team Development

**Example Strong Answer** (hiring/developing a TSE):
> "Last time I hired a support engineer, I looked for someone with solid Linux and networking fundamentals—I knew I could teach them the product. During onboarding, I paired them with a senior TSE for the first month on all tickets. We had a weekly 1-on-1 where I asked what was confusing, what they felt confident in.
> 
> After 3 months, I noticed they were great at following runbooks but struggled to think beyond the doc when something didn't fit the script. So I started having them lead a weekly 'deep dive' session where they'd pick a ticket and walk the team through their investigation. That forced them to explain their reasoning.
> 
> By month 6, they were independently triaging and escalating correctly. Now, 2 years later, they're the person everyone goes to for database issues."

**What makes this strong**:
- Specific hiring criteria tied to the role
- Intentional onboarding and mentoring
- Recognition of a growth edge
- Targeted intervention (the deep-dive sessions)
- Measured over time; shows real development

**Example Weak Answer**:
> "I hire people who are smart and figure it out."

OR (from previous interview):
> "When he struggled with adoption, I just let the client be... they accepted it."

**Why it's weak**:
- Lacks structure; relies on "smart" people to self-direct
- Doesn't own the development
- Doesn't drive adoption or handle resistance

---

### Product Thinking: Feedback Loop

**Example Strong Answer** (recurring issue → product fix):
> "I keep a spreadsheet of every ticket we close. Once a month, I roll it up by category and severity. If I see the same issue twice, I flag it for a KB article. If I see it three times, I escalate to product.
> 
> Last quarter, we saw four tickets from different customers about the same Kubernetes upgrade path issue. The symptom was different each time (RBAC, CustomResourceDefinition version, etc.), but the root cause was the same. I compiled a detailed reproduction and sent it to engineering.
> 
> They fixed it in the next patch release. Then I updated the docs to warn about the pitfall and created a runbook. Next quarter, we saw zero tickets on that issue.
> 
> I track that as a success metric: 'issues escalated and fixed.' It's how I show the business value of support."

**What makes this strong**:
- Systematic data collection (spreadsheet, categories)
- Clear escalation threshold (1 = KB, 3+ = engineering)
- Root cause analysis, not symptom chasing
- Closed the loop (fix → docs → measurable impact)
- Accountability: tracked the outcome

**Example Weak Answer**:
> "We pass bugs to engineering when customers complain."

OR (from previous interview):
> Not familiar with how to leverage GitOps or systematic feedback collection; treats it as ad hoc.

**Why it's weak**:
- No structure or criteria
- Reactive, not proactive
- Doesn't measure impact

---

### Communication & Clarity

**What to Notice**:

**Strong**: Candidate explains their thinking step-by-step. You could replay their answer to their team and they'd understand the logic.

**Weak**: Answers are vague, rambling, or circular. You ask follow-ups to clarify, and they struggle to articulate what they did or why.

**Note from previous interview**: Jordan's presentation was weak—"awkward," "ugly slides," "really boring." He had good experience, but couldn't clearly articulate it. That's a real concern for a manager who needs to lead a team and communicate with customers.

---

## Red Flags & How to Probe

### Red Flag 1: "The customer just accepted it"
**What this suggests**: They encountered resistance but didn't push back or iterate. That's a problem for support—you need to influence without authority.

**How to probe**:
- "I hear the customer accepted it. Did you follow up to see if they were actually using it?"
- "What would you do differently if you were in that situation now?"
- "Tell me about a time you had to convince someone to adopt an approach they were skeptical of."

---

### Red Flag 2: Weak Technical Communication
**What this suggests**: They may not be able to troubleshoot independently, or may struggle to explain issues to customers and engineering.

**How to probe**:
- Ask them to explain a technical concept (K8s, APIs, observability) as if you were a customer with limited technical knowledge.
- Ask them to walk through a specific ticket they worked. Listen for clarity.
- Ask: "Tell me about a technical decision you explained to a non-technical stakeholder. How did you approach it?"

---

### Red Flag 3: "I Don't Know, That's Not My Area"
**What this suggests**: Could be confidence, could be lack of depth. Depends on context.

**Healthy response**: "I haven't worked with StatefulSets much—my experience is mostly with Deployments. I'd investigate by reading the docs and looking at examples. Here's how I'd approach learning it..."

**Unhealthy response**: "I don't do Kubernetes stuff. That's for DevOps."

For this role, they need breadth. They may not be a Kubernetes expert, but they should have hands-on experience and be willing to learn.

---

### Red Flag 4: Focuses on Metrics That Don't Matter
**What this suggests**: They're optimizing for the wrong thing.

**Examples**:
- "I measure support by number of tickets closed per day"—ignores quality, first-contact resolution, customer satisfaction.
- "I track how many bugs we escalate"—without measuring how many are actually root causes vs. noise.

**How to probe**:
- "Great, so tickets closed. But how do you know if the customer is actually satisfied?"
- "How do you know your SLAs are realistic? Too aggressive? Too lenient?"

---

## Istari-Specific Calibration

### What This Role Actually Needs

**Technical Depth**:
- Not a Kubernetes expert, but comfortable troubleshooting K8s deployments
- Experience with databases (PostgreSQL, config tuning, backups, replication)
- Understand observability (metrics, logs, tracing)
- API integration and REST/GraphQL basics
- Linux administration and networking fundamentals

**Leadership**:
- Proven ability to hire and develop technical people
- Can set expectations and hold people accountable
- Makes decisions and lives with the consequences
- Invests in team growth, not just execution

**Product Sense**:
- Treats support as a quality gate, not a service desk
- Systematically collects and prioritizes feedback
- Bridges engineering and customer needs
- Measures impact (not just volume)

### Questions That Help You Calibrate

**If their K8s knowledge seems shallow**, ask:
- "Walk me through setting up a StatefulSet for a PostgreSQL primary + replica. What would you do differently than a Deployment?"
- "You're migrating an app from a VM to Kubernetes. What's your discovery process?"

**If their leadership experience is limited**, ask:
- "Describe a time you had to say no to someone (customer, peer, boss). How did you handle it?"
- "Tell me about someone you developed who exceeded your expectations."

**If their product sense is unclear**, ask:
- "What's the worst support process you've seen? What would you change?"
- "If you could fix one thing about a product you supported, what would it be?"

---

## How to Handle Edge Cases

### Edge Case 1: Great Technical Depth, Weak Leadership
**Assessment**: Can they grow into management? Do we need to pair them with a mentor/peer?

**Question to ask**: "Have you thought about management? What appeals to you, and what concerns you?"

**Listen for**: Self-awareness. If they say "I'm great at tech but need to work on listening," that's coachable. If they say "I've never managed and don't know what I'm doing," that's honest, but they need support.

---

### Edge Case 2: Strong Leadership, Light Technical Depth
**Assessment**: Can they learn the technical side? How quickly?

**Question to ask**: "Tell me about a time you stepped into a technical area where you were initially out of your depth."

**Listen for**: Evidence they can ramp up. Previous roles where they've had to learn new tech stacks.

**Caveat**: For a manager of support engineers, you need *enough* technical depth to credibly evaluate TSE work and escalate correctly. "I'll learn Kubernetes on the job" is only OK if they have a track record of successful technical ramps.

---

### Edge Case 3: They Seem Overqualified (e.g., Former VP of Engineering)
**Assessment**: Will they be bored? Will they burn out? Will they stay?

**Question to ask**: "This role is smaller than your previous scope. What draws you to it?"

**Listen for**: Genuine interest in support function as a craft, not desperation or a fallback. If it seems like they're retreating from something, understand why.

---

## What NOT to Assess in This Interview

- **Writing ability**: You'll see writing samples in other contexts (KB article, runbook, email). Ignore spelling in the interview.
- **Sales or customer-facing charm**: Important, but secondary to technical credibility and leadership capability.
- **Perfect presentation skills**: Some nerves are normal. What matters is whether you can understand their thinking.
- **Exhaustive product knowledge**: They should ask smart questions about Istari, but they don't need to know our docs by heart. You're hiring for learning capability.

---

## Interviewer Dos & Don'ts

### Do:
- Listen more than you talk. They should be doing 70% of the talking.
- Ask follow-up questions if an answer is vague. "Tell me more about that" is fair game.
- Take notes. Direct quotes are helpful for calibration later.
- Probe on concrete examples, not hypotheticals. "Tell me a time you..." beats "How would you handle...?"
- Distinguish between "they don't know" and "they weren't clear." Ask again.

### Don't:
- Sell the role during the interview. You'll do that *after* you've assessed them.
- Let them off the hook if you don't understand their answer. It's your job to make sure you can evaluate them.
- Assume "quiet" = "not smart." Some people are thoughtful and need a second.
- Let them ramble. If they're going off track, a gentle redirect: "That's interesting. Let me bring us back to..."
- Share your opinions or challenge their answers harshly. Stay neutral.

---

## Debrief Template

**After the interview**, spend 10 minutes documenting:

1. **First impression** (gut reaction, not final judgment): What's your instinct about this person?
2. **Strongest moment**: When did they shine? What did they say or do?
3. **Weakest moment**: Any part of the interview where they struggled?
4. **One thing you'd ask in a follow-up**: If you had one more chance, what would you clarify?
5. **Recommendation**: Strong yes / yes / maybe / no. With reasoning.

---

## Calibration Between Interviewers

If multiple people are interviewing, schedule a 15-minute sync **before** seeing results:

- **Align on what "strong" looks like** for each dimension.
- **Agree on weighting**: If Technical is a 3 but Leadership is a 5, is that a yes?
- **Discuss any red flags** you're watching for based on the candidate's background.

Then interview independently, and debrief together. This prevents groupthink and catches different perspectives.
