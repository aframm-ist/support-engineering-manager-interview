# Support Engineering Manager Interview Guide
## Istari Digital — Software Product Support

**Role**: Support Engineering Manager (Software Product)  
**Reports To**: VP Engineering  
**Team Size**: 2 Technical Support Engineers  
**Key Platforms**: Kubernetes, Docker, PostgreSQL, observability stacks, REST/GraphQL APIs, Pylon (support ticketing)

---

## Interview Structure

**Total Duration**: 2.5–3 hours  
**Format**: Technical (80 min) → Leadership/Operations (60 min) → Product Strategy & Fit (30 min)

---

## Part 1: Technical Competency (80 minutes)

**Breakdown** (tailored to Douglas's background):
- 1.1 Quality, Testing & Release Automation (12 min) ← **His strength**
- 1.2 Monitoring, Incident Response & Observability (18 min) ← **His strength**
- 1.3 Bug Triage, Quality Gates & Support Processes (12 min) ← **His strength**
- 1.3b CI/CD Pipeline & Release Management (12 min) ← **His strength**
- 1.3c Infrastructure as Code & Deployment Automation (10 min) 
- 1.3d Customer Deployment & Support Context (10 min)
- 1.4 APIs & Networking Context (6 min)

### 1.1 Quality, Testing & Release Automation (12 min)

**Question**: Walk me through your approach to test automation. What frameworks have you used, and how do you decide what to automate vs. what to test manually?

**What to Look For**:
- **Tool experience**: Playwright, Puppeteer, Selenium, Appium, Detox (from his resume—what's he actually used?)
- **Scope**: Unit tests, API tests, E2E tests, visual regression, performance testing
- **Strategy**: ROI on automation—what's worth automating? Flaky tests? Maintenance cost?
- **Coverage vs. speed**: Can they balance comprehensive testing with release velocity?
- **CI/CD integration**: How do tests gate releases? Failure handling?
- **Examples**: Specific test suites he's built and maintained

**Follow-ups**:
- "You have 1,000 E2E tests taking 45 minutes to run. Release is blocked. What do you do?"
- "Tests are flaky—sometimes pass, sometimes fail for the same code. How do you fix it?"
- "You're testing a mobile app across iOS and Android. How do you scale test infrastructure?"

**Red Flags**:
- No hands-on test automation experience
- "We test everything manually" or "100% automation coverage" (unrealistic)
- Doesn't understand trade-offs between automation cost and benefit
- Never maintained a test suite at scale

---

**Question**: Tell me about a time you had to establish or improve a quality gate in a CI/CD pipeline. What metrics did you use to measure success?

**What to Look For**:
- **What changed**: Did they add security scans (SAST/DAST)? Coverage gates? Performance tests? Staging deployment?
- **Measurement**: How do they know it's working? (faster releases, fewer prod bugs, MTTR?)
- **Buy-in**: How did they convince teams to adopt stricter gates without slowing releases too much?
- **Balance**: Do they understand the tension between safety and velocity?
- **Rollback**: What happens when a gate incorrectly blocks a good release?

**Examples from resume**: He "significantly reduced manual testing overhead and accelerated release cycles for the QA organization" with Playwright/Appium. What was the specific gate he built?

---

### 1.2 Monitoring, Incident Response & Observability (18 min)

**Question**: Tell me about a monitoring solution you've built or configured. What tools did you use (Datadog, Sentry, New Relic, BugSnag?), and what metrics/alerts did you set up?

**What to Look For**:
- **Tool experience**: Which of the tools on his resume has he actually used?
- **Metrics vs. logs vs. traces**: Does he understand the distinction and when to use each?
- **Actionable alerts**: Are his alerts tied to runbooks or just noise?
- **Cost awareness**: Did he think about storage, retention, pricing?
- **Development velocity**: How does monitoring help developers ship faster?
- **Integration**: How does it tie into incident response?

**Follow-ups**:
- "A customer has high error rates. You're getting 1,000 Sentry errors a day. How do you prioritize?"
- "You're paying $10K/month for Datadog. Is it worth it? How do you audit usage?"
- "Error spikes at 2 AM, but the team is asleep. How does your monitoring+alerting handle that?"

**Red Flags**:
- Only used SaaS monitoring dashboards, never configured alerts
- Doesn't understand metric cardinality or cost implications
- Thinks monitoring is for Ops, not for developers

---

**Question**: You're being paged at 2 AM because of high error rates. Walk me through your incident response process—how do you triage, investigate, and communicate while debugging?

**What to Look For**:
- **Immediate actions**: Check Datadog/Sentry dashboard? Pull logs? Check recent deployments?
- **Communication**: Slack alert to team? Create incident ticket? Notify customers?
- **Investigation methodology**: How do they narrow down: code, infrastructure, dependency, or configuration?
- **Correlation**: Can they tie error spikes to deployments, traffic patterns, or external events?
- **Runbooks**: Do they have documented procedures, or improvising?
- **Escalation**: When do they loop in other teams?
- **Post-incident**: Do they do a blameless post-mortem and update docs?

**Follow-ups**:
- "Error rate spiking, but no recent deploy. What else would you check?"
- "Need to rollback at 2 AM safely. How do you do it?"
- "Issue only affects 5% of customers. How do you narrow it down?"

**Red Flags**:
- No on-call experience
- Reactive, no documented process
- Doesn't communicate with stakeholders
- No post-incident follow-up

---

**Question**: Tell me about alert fatigue and how you've solved it. Have you had to tune, disable, or redesign alerts?

**What to Look For**:
- **Problem recognition**: Do they understand the cost of noisy alerts?
- **Root causes**: Overly sensitive thresholds, seasonal patterns, transient spikes
- **Solutions**: Alert threshold tuning, deduplication, composite alerts, context
- **Examples**: Specific alerts they've adjusted (e.g., "CPU alerts at 80% fired nightly during backups—raised to 95%")
- **Measurement**: Tracked improvements? (reduced alert volume, team satisfaction, MTTR?)
- **Collaboration**: Worked with teams to understand what matters?

**Follow-ups**:
- "Getting 10,000 alerts/day. Walk me through how you'd fix that."
- "Alert fires correctly every time but team ignores it because it's always going off. What's the fix?"
- "You silence an alert to make the noise stop. Is that the right move?"

**Red Flags**:
- No alerting system experience
- Thinks "more alerts = better observability"
- Never evaluated alert usefulness

---

### 1.3 Bug Triage, Quality Gates & Support Processes (12 min)

---

**Question**: You're implementing a new support ticket system (like Pylon) and need to define SLA rules, routing, and escalation paths. Walk me through your approach.

**What to Look For**:
- **SLA design**: P1 (critical, <1h), P2 (major, <4h), P3 (minor, <24h), P4 (cosmetic, best effort)?
- **Routing logic**: Who gets what tickets? How do they define "security issue" vs. "config question"?
- **Escalation paths**: When does a TSE loop in engineering? When does it hit a manager?
- **Metrics**: CSAT, time-to-close, first-response time, recurring issues
- **Customer-facing comms**: Do they think about status page, escalation notifications, workarounds?

**Follow-ups**:
- "How do you prevent P4 tickets from clogging the queue while still being responsive?"
- "A P3 ticket sits for 18 hours. Your SLA says 24 hours. What do you do?"
- "How do you know if your SLA is too aggressive or too lenient?"

---

**Question**: You notice the same issue reported 5 times in the past month, each time resolved by a different TSE with a slightly different workaround. What do you do?

**What to Look For**:
- **Knowledge consolidation**: Are they thinking about runbooks, docs, KB?
- **Root cause thinking**: Is this a product bug, a gap in the docs, or a real-world edge case?
- **Feedback loop**: Do they escalate to product to fix the root cause?
- **Team development**: Do they turn this into a training moment for TSEs?
- **Process improvement**: Do they update support routing or intake to catch it earlier?

---

### 1.3b CI/CD Pipeline & Release Management (12 min)

**Question**: Describe your ideal CI/CD pipeline. What stages does it have, what gates releases, and how do you handle failures?

**What to Look For**:
- **Pipeline stages**: Checkout, build, lint, test, scan, deploy—in what order?
- **Gating criteria**: What has to pass before code reaches production? (tests, coverage, security scans, manual approval?)
- **Deployment strategy**: Blue/green? Canary? Rolling? How do they minimize risk?
- **Rollback**: How fast can they rollback if something breaks? Is it automated?
- **Observability post-deploy**: Do they monitor metrics/errors after each release?
- **Deployment frequency**: How often do they ship? (daily, per-commit, weekly?)
- **Tools**: What does he use? (GitHub Actions, GitLab CI, Jenkins, CircleCI?)

**Follow-ups**:
- "A broken build gets deployed to production. How do you prevent that?"
- "You want to deploy 50 times a day safely. What does your pipeline look like?"
- "A deploy causes a production outage. How do you rollback, and what went wrong?"

**Red Flags**:
- Never built or managed a CI/CD pipeline
- Manual deployments ("SSH and run scripts")
- No automated testing in the pipeline
- Can't articulate what gates releases

---

**Question**: Tell me about a time you had to unblock a release or improve release velocity. What was the bottleneck, and how did you fix it?

**What to Look For**:
- **Problem**: Was it slow tests, manual approval, deployment time, fear of breaking things?
- **Root cause analysis**: Did they dig into why, or just add more resources?
- **Solution**: Was it process change (parallelizing tests), tooling (better deployment), or organizational (clearer approval process)?
- **Measurement**: Did they measure improvement? (time to deploy, release frequency, deployment success rate?)
- **Balance**: Did they maintain safety while improving speed?
- **Example from resume**: He "accelerated release cycles for the QA organization" with E2E testing. How specifically?

**Red Flags**:
- Sacrificed safety for speed ("we just deploy more")
- Doesn't measure the outcome
- Blames external factors instead of solving the problem

---


---

### 1.3c Infrastructure as Code & Deployment Automation (10 min)

**Question**: Tell me about your experience with Infrastructure as Code. What tools have you used, and how do you validate changes before applying them?

**What to Look For**:
- **Tools & hands-on experience**: Terraform, CloudFormation, Helm, or other—which has he actually used?
- **Safety before deployment**: Does he use `terraform plan`? Run tests? Policy as code?
- **Version control**: Does he treat IaC like code (git, reviews, testing)?
- **State management**: Does he understand the risks of shared state, remote backends?
- **Multi-environment**: How does he manage dev/staging/prod differences without duplication?

**Follow-ups**:
- "A Terraform apply fails halfway through. How do you recover?"
- "You want to deploy the same infrastructure to 3 regions. How do you avoid copy-paste?"

**Red Flags**:
- Only used cloud console (no IaC)
- "I let someone else handle infrastructure"
- Can't explain why version control for infra matters

---

### 1.3d Customer Deployment & Support Context (10 min)

**Question**: You're supporting a customer who's deploying Istari to their infrastructure. What questions do you ask, and what could go wrong?

**What to Look For**:
- **Environment questions**: On-prem or cloud? Kubernetes or VMs? What's their network topology?
- **Constraints**: Air-gapped? Behind proxies? Custom CA? Compliance requirements?
- **Handoff**: Are they doing a cutover from an old system? How do you minimize downtime?
- **Monitoring**: How do you set up observability so they can debug issues on their end?
- **Documentation**: What docs do they need vs. what can they figure out?

**Example**: GE Aerospace was air-gapped with Zscaler. What additional complexity did that introduce?

**Red Flags**:
- No experience supporting customers on deployments
- Assumes all environments are the same
- Doesn't ask questions about constraints

---

**Question**: A customer says "the system is slow" after you deploy an update. Walk me through your investigation.

**What to Look For**:
- **Triage**: Is it their infrastructure, the network, or Istari?
- **Metrics**: What would they check? (Pod CPU/memory? Database connections? Network latency?)
- **Comparison**: Was it slow before the update? Can they rollback?
- **Customer communication**: How do you keep them informed while you investigate?

---

### 1.4 API & Networking Context (10 min)

**Question**: Tell me about a time you diagnosed an API integration issue. What was wrong, and how did you narrow it down?

**What to Look For**:
- TLS/certificate validation, proxy/firewall issues, DNS, rate limiting, auth (API key, OAuth, mTLS)
- Request/response inspection tools (`curl`, Postman, packet capture)
- Understanding of REST vs. GraphQL trade-offs
- Ability to read API docs and spot misconfigurations

---

**Question**: A customer is in an air-gapped environment and can't easily send logs back to you. How do you work with them?

**What to Look For**:
- Pragmatic problem-solving: logs via email, file transfer, manual SSH session
- Security awareness: are they careful with sensitive data?
- Patience and clarity: can they guide a non-engineer through log collection?
- Remote troubleshooting skills: can they diagnose without full visibility?

---

## Part 2: Leadership & Operations (60 minutes)

### 2.1 Team Management (20 min)

**Question**: Tell me about a time you hired or developed a technical support person. What made them successful (or what held them back)?

**What to Look For**:
- Do they think about hiring criteria that match Istari's needs? (Kubernetes, Docker, databases, troubleshooting rigor)
- Do they invest in onboarding and mentoring?
- Can they recognize when someone is underperforming and address it?
- Do they celebrate growth and learning?

---

**Question**: You have two TSEs. One is great at deep technical investigation but slow at documentation. The other is super responsive but sometimes misses root causes. How do you balance their strengths?

**What to Look For**:
- **Specialization**: Can they lean into strengths while closing knowledge gaps?
- **Coverage**: Do they think about rotation, on-call, vacation coverage?
- **Growth paths**: Are they developing both toward the same skill level, or allowing differentiation?
- **Manager accountability**: Do they own the team's growth, or delegate it?

---

**Question**: Describe a conflict or difficult conversation you've had with someone on your team. What was the issue, and how did you handle it?

**What to Look For**:
- Ownership of the problem (not blaming the report)
- Directness and clarity (not avoiding hard conversations)
- Fairness and documentation (protecting both sides)
- Follow-through (did they check in to see if the issue resolved?)

---

### 2.2 Metrics, Reporting & Accountability (15 min)

**Question**: Design a monthly support operations dashboard. What KPIs would you track, and why?

**What to Look For**:
- SLA compliance (% of tickets closed within SLA)
- CSAT or NPS (customer satisfaction)
- Ticket volume by severity, category, resolution time
- Recurring issues (how many tickets repeat the same root cause?)
- TSE productivity (not just speed, but quality)
- Engineering collaboration (bugs escalated, fixed, documented)

**Red Flags**:
- Only volume-based metrics (# of tickets closed) with no quality signal
- No connection between support metrics and product roadmap

---

**Question**: A month ago, you promised the VP that you'd reduce time-to-resolution for database-related issues. It's improved, but not as much as expected. How do you communicate this?

**What to Look For**:
- Honest assessment of progress vs. commitment
- Root cause analysis of the gap (not just "it was harder than expected")
- Realistic next steps and revised timeline
- Accountability without excuse-making

---

### 2.3 Process & Tooling (15 min)

**Question**: You're inheriting a support function with no runbooks, inconsistent SLAs, and Pylon is misconfigured. Where do you start in the first 90 days?

**What to Look For**:
- **Quick wins**: SLA configuration, routing rules, intake workflows (high impact, doable in weeks)
- **Documentation**: Not a lower priority—this is how TSEs share knowledge and prevent repeats
- **Team involvement**: Are they asking TSEs what's broken, or imposing solutions top-down?
- **Measurement**: How do they know when things improve?

---

**Question**: Tell me about a support or operations process you designed or redesigned. What was the "before," what changed, and what was the impact?

**What to Look For**:
- Hands-on process improvement, not just high-level strategy
- Measurement of impact (reduced tickets, faster resolution, better CSAT)
- Iterative: did they refine it, or was it "set and forget"?
- Did the process survive after they left (buy-in from the team)?

---

### 2.4 Handling Difficult Situations (10 min)

**Question**: A customer escalates a critical issue that your team investigated, but the root cause is actually a product bug that engineering is reluctant to fix. How do you handle it?

**What to Look For**:
- **Advocacy for the customer**: Do they take the issue seriously, or default to "that's engineering's problem"?
- **Engineering communication**: Can they present the bug in a way engineering respects (reproducibility, severity, impact)?
- **Interim support**: Do they offer a workaround or temporary mitigation?
- **Escalation path**: Do they know when to loop in a director or VP?

---

**Question**: One of your TSEs consistently misses SLAs or misdiagnoses issues. Other team members are starting to complain. What do you do?

**What to Look For**:
- Early intervention (not waiting for it to blow up)
- 1-on-1 diagnosis (is it capability? motivation? environment? tooling?)
- Clear expectations and support (what success looks like, what help they'll get)
- Documented improvement plan, with a realistic timeline
- Willingness to make hard decisions if it doesn't improve

---

## Part 3: Product Strategy & Fit (30 minutes)

### 3.1 Product Feedback Loop (15 min)

**Question**: Describe your approach to collecting and prioritizing customer feedback. How do you ensure it reaches the product team?

**What to Look For**:
- **Systematic collection**: Do they synthesize across tickets, or rely on memory?
- **Quarterly digests**: They should mention assembling themes, not raw bug lists
- **Severity assessment**: Can they distinguish "this one customer is annoyed" from "this pattern affects many customers"?
- **Product relationship**: How frequently do they talk to product? Is it ceremonial or collaborative?
- **Speed to impact**: Can they describe a time feedback → shipped?

---

**Question**: A feature ships with poor documentation. Support gets flooded with basic questions. Product says "it's in the release notes." How do you respond?

**What to Look For**:
- **Quality gate perspective**: Support is detecting a product problem, not executing a support problem
- **Constructive escalation**: "Release notes aren't enough; users need a tutorial" vs. just complaining
- **Interim solutions**: Do they write a quick KB article for customers while product improves docs?
- **Relationship**: Can they maintain respect for product while being direct about gaps?

---

### 3.2 Istari Product Knowledge (10 min)

**Question**: Tell me what you know about Istari's platform, and ask me questions about what you don't understand yet.

**What to Look For**:
- Did they research before the interview? (check our docs, look at Pylon config, etc.)
- Do they ask intelligent questions about Kubernetes integration, support tooling, or customer deployment patterns?
- Can they connect their experience (e.g., "in my last role, we had X problem; do you see that here?")

**Candidate should ask about**:
- How customers are currently using Istari
- Common failure modes or deployment challenges
- What engineering cares most about from support (what feedback moves the needle?)
- How the support function integrates with product development

---

### 3.3 Fit & Growth (5 min)

**Question**: What excites you about this role, and what concerns you?

**What to Look For**:
- **Excitement**: Do they light up about the technical challenge, the team, the customer connection, or the product?
- **Honesty about concerns**: "I haven't managed before, but I'm ready to learn" is better than pretending they have it all figured out
- **Growth mindset**: Are they thinking about what they'll learn in this role?

---

## Evaluation Rubric

### Technical (0–5 scale)

**Core competencies** (must score ≥3):
- **Test Automation**: Hands-on with frameworks (Playwright, Appium, Selenium, etc.) and E2E testing strategies
- **Monitoring & Incident Response**: Experience with monitoring tools (Datadog, Sentry, New Relic, BugSnag) and on-call processes
- **CI/CD & Release Management**: Pipeline design, testing gates, deployment strategies, automation
- **Quality Gates & Process**: Ability to design SLAs, triage processes, and prevent recurrence of issues
- **AWS & IaC**: Comfortable with AWS services and Infrastructure as Code (Terraform, CloudFormation)

**Overall Technical Rating**:
- **5**: Deep hands-on across test automation, monitoring, CI/CD, and quality processes. Built systems at scale. Mentors others.
- **4**: Solid production experience across all areas. Can design testing/monitoring strategies; understands trade-offs.
- **3**: Competent in most areas; minor gaps (e.g., limited monitoring tool experience or IaC is new). Can grow.
- **2**: Significant gaps (e.g., no hands-on test automation, no incident response experience). Would need mentoring.
- **1**: Missing core skills (e.g., no QA/testing background, no monitoring, no CI/CD). Not suitable for this role.

### Leadership (0–5 scale)
- **5**: Proven manager. Builds teams, gives feedback, makes hard calls. Process-oriented.
- **4**: Strong individual contributor with some management experience. Growth trajectory clear.
- **3**: Likes the idea of leading; limited track record. Coachable.
- **2**: Struggles with difficult conversations or team dynamics.
- **1**: Not ready to manage others.

### Product Thinking (0–5 scale)
- **5**: Naturally connects support to product. Drives feedback loop systematically.
- **4**: Understands importance of feedback loop; can articulate customer needs clearly.
- **3**: Gets it conceptually; may need guidance on operationalizing it.
- **2**: Transactional view of support (fix tickets, close, move on).
- **1**: Resistant to product thinking.

### Istari Fit (0–5 scale)
- **5**: Excited about the mission, the product, the customer base (engineering teams, mechanical simulation).
- **4**: Sees this as a great opportunity; aligns with career goals.
- **3**: Neutral; could see themselves doing this.
- **2**: Hesitant about certain aspects (customers, technical depth, remote work, etc.).
- **1**: Wrong fit for Istari.

**Target**: Technical ≥3, Leadership ≥4, Product Thinking ≥3, Istari Fit ≥4

---

## Notes for Interviewers

### Red Flags from Previous Interviews
- **Weak presentation/communication skills**: If they struggle to articulate their thinking, how will they lead a team or communicate with customers?
- **Adoption challenges**: "The client just accepted it" suggests they struggled to sell change. Support requires influence without direct authority.
- **Vague technical answers**: If they can't clearly explain what they did, they may not have gone deep enough.
- **Defensive about gaps**: "I don't know much about GitOps" is fine; "GitOps is just Ansible" is a red flag.

### What to Listen For
- **Problem-solving orientation**: Do they enjoy diagnosing issues, or do they see it as a burden?
- **Customer empathy**: Do they think about the customer's pain, or just their own process?
- **Continuous improvement**: Do they iterate and measure, or operate on gut feel?
- **Team first**: Do they invest in their reports, or see them as extensions of themselves?

### Candidate Strengths to Look For
- IaC background (Ansible, Terraform, Helm) — they understand deployment complexity
- Defense/government contracting — likely familiar with compliance, change control, risk management
- CKA or similar cert — proof of Kubernetes depth
- Multi-team collaboration experience — they've had to navigate politics and multiple stakeholders

---

## Follow-up References

For interviewers unfamiliar with Istari's stack:
- **Pylon**: Our support ticket system. Configured with SLAs, routing, intake workflows.
- **Key customer pain points**: Kubernetes upgrades, observability setup, database scaling, integration with customer CI/CD pipelines.
- **Support model**: Quality gate between customers and engineering. Well-documented bugs, not noise.
- **Team**: 2 TSEs, initially. Manager owns the entire function end-to-end.
