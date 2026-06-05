# Notes from Previous Interviews

## Jordan Fike Interview (Background)

### Candidate Profile

**Background**:
- 10 years in defense contracting
- Infrastructure as Code (IaC) specialist: Ansible, some Terraform
- Certifications: CKA, SAFe Practice Consultant, CompTIA Security+
- Recent experience: GitLab CI/CD (more than Jenkins)
- No current open-source projects; studying for CKS

**Core Motivation** (per candidate):
- "I like to solve problems" (self-identified as a "two things" about him)
- Red Hat background (likes the talent, first IaC system that really works)
- Team-first person

---

### Project Context (What He Presented)

**Environment**:
- Edge hardware devices for field operations
- Software builds in accredited cloud environments
- Goal: Continuous deployment with testing for edge HW that can't connect to cloud

**Architecture**:
```
GitLab --[trigger pipeline]--> Orchestration Container (Helm, Ansible)
```

**Challenges Overcome**:
1. Linking environments and network communications
2. Political: Had to navigate security process with customer partner to enable changes
3. Software engineering adoption: Engineers creating ad hoc pipelines; lack of generalized solutions
4. Solutions weren't given space to mature or be optimized

**Results**:
- After interruption, solution was adopted as baseline for deployment across project
- Captured methodology in architecture diagram and wiki for reuse
- Good outcomes with the orchestration container model

---

### Key Feedback Points

#### Strengths Observed

1. **Problem-solving focus**: Drove orchestration container model—centralizes resources, allows standardization + flexibility
2. **Technical depth in IaC**: Comfortable with Ansible, Terraform, CI/CD
3. **Recognition of patterns**: Noted that container images often too large (VM appliances vs. focused tools)
4. **Defense background**: Likely familiar with compliance, change control, risk management

---

#### Weaknesses & Concerns

1. **Communication & Presentation**:
   - Awkward delivery
   - Ugly, hard-to-follow slides
   - "Really boring" presentation overall
   - Hard to gauge technical competency because he couldn't clearly articulate his thinking

2. **Adoption & Change Management**:
   - When facing resistance, "the client just accepted it" (passive, not driven)
   - Struggled to actively drive adoption or iterate on solutions
   - Interview note: "Doesn't deal with many political situations well"
   - Weak answer on escalation: "It's tough" without clarity on thresholds

3. **GitOps Knowledge**:
   - Not familiar with how to leverage GitOps for cluster management
   - Suggested Ansible can roll out cluster profiles, but unclear on declarative vs. imperative paradigm shift

4. **System Design Thinking**:
   - CI/CD pipeline description was vague
   - Couldn't clearly walk through stages (build, test, deploy, rollback, strategy)
   - Weak grasp of deployment strategies (blue/green, canary, rollback mechanisms)

5. **Technical Communication**:
   - Couldn't clearly present his own solutions
   - Difficult to understand what problem he solved vs. how he solved it
   - Risk: If he can't communicate with a team, he can't lead one

---

### Lessons for Future Interviews

#### Interview Techniques
- **Probe communication**: If an answer is vague, ask follow-ups. Don't accept "I did it" without details.
- **Watch for lack of clarity**: If you can't understand their reasoning after two follow-ups, that's a signal. It might indicate shallow depth, not just presentation nerves.
- **Ask them to teach you**: "Explain this concept as if I were a customer with limited Kubernetes experience." This reveals both depth and communication ability.

#### Red Flags to Watch
- **Passive approach to adoption**: Do they drive change, or do they accept "that's how it is"?
- **Weak escalation judgment**: When do they ask for help? What's their threshold?
- **Vague technical answers**: Can they explain a system design, deployment strategy, or architecture clearly?
- **Difficulty with change management**: Defense contracting doesn't require strong soft skills—but managing support requires influence without authority.

#### What Matters for This Specific Role
- **Communication is non-negotiable**: They need to lead 2 TSEs, explain issues to engineering, and document runbooks. If they struggle to articulate ideas, they'll fail.
- **Change management matters**: Support requires driving adoption of tooling, processes, and standards. Passive acceptance doesn't cut it.
- **Product thinking matters**: Can they see the system holistically (not just infrastructure)? Do they ask "why is this happening" or just "how do I fix it"?

---

### Question Calibration for This Role

If we're interviewing another IaC specialist or defense contractor:

1. **Ask for a clear walk-through**: "Walk me through one complete CI/CD pipeline from code commit to prod deployment. I want to understand each stage and decision point."
2. **Ask about adoption**: "Tell me about a time you had to convince a team to use a tool or process they were skeptical of. What was the pushback, and how did you move them?"
3. **Test communication**: "Explain Kubernetes StatefulSets to someone who's never used them. What would you emphasize?"
4. **Probe escalation**: "When do you ask for help? Tell me about a time you recognized you needed external support and how you handled it."

---

## Patterns to Watch Across Future Candidates

### Red Flags
- [ ] Awkward or unclear communication under normal interview conditions
- [ ] Can't articulate their own projects or decisions clearly
- [ ] "The customer just accepted it" attitude (passive)
- [ ] Weak judgment on when to escalate or ask for help
- [ ] No examples of actively driving adoption or change
- [ ] Strong technical depth but weak on people/leadership aspects

### Green Flags
- [ ] Clear, methodical explanations (even if nervous)
- [ ] Specific examples with concrete outcomes
- [ ] Recognition of adoption challenges and active strategies to overcome them
- [ ] Good judgment on escalation and collaboration
- [ ] Evidence of communication skill (docs, presentations, mentoring)
- [ ] Technical depth + people skills balance

### Questions That Worked Well
- "Walk me through a full CI/CD pipeline" — reveals depth and communication
- "Tell me about the biggest adoption challenge you faced" — reveals soft skills and judgment
- "How do you know when to escalate or ask for help?" — reveals self-awareness and team fit
- "Explain a technical concept to someone non-technical" — communication + depth

---

## Recommendation for Future Hiring

For a **Support Engineering Manager** role (unlike some infrastructure roles), we need:

1. **Technical depth** — Yes, mandatory. But not the primary factor.
2. **Communication ability** — Critical. They lead a team and bridge engineering/customers.
3. **Leadership experience** — Proven ability to develop people, set expectations, make decisions.
4. **Product thinking** — Ability to see the system holistically, not just fix tickets.
5. **Change management** — Drive adoption, overcome resistance, iterate.

A candidate like Jordan (strong IaC, defense background) would be a great **Technical Support Engineer** or **Support Infrastructure Lead**. But as a **Manager**, communication, leadership, and product thinking are just as important as technical depth.

Screen for communication ability early—if you can't understand their thinking in the interview, they likely can't lead a team or document processes effectively.
