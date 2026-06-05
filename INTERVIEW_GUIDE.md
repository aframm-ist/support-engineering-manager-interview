# Support Engineering Manager Interview Guide
## Istari Digital — Software Product Support

**Role**: Support Engineering Manager (Software Product)  
**Reports To**: VP Engineering  
**Team Size**: 2 Technical Support Engineers  
**Key Platforms**: Kubernetes, Docker, PostgreSQL, observability stacks, REST/GraphQL APIs, Pylon (support ticketing)

---

## Interview Structure

**Total Duration**: 3 hours (or 2.5 hours with reduced follow-ups)  
**Format**: Technical (90 min) → Leadership/Operations (60 min) → Product Strategy & Fit (30 min)

---

## Part 1: Technical Competency (90 minutes)

**Breakdown**:
- 1.1 Kubernetes & Containers (10 min)
- 1.2 Observability (8 min)
- 1.3 Support Tooling (10 min)
- 1.3b Kubernetes & Deployment Architecture (15 min) ← **Core focus**
- 1.3c AWS & Cloud Deployment (15 min) ← **Core focus**
- 1.3d Infrastructure as Code & Automation (12 min) ← **Core focus**
- 1.3e Customer Deployment & Support Context (10 min)
- 1.4 APIs & Networking (10 min)

### 1.1 Kubernetes & Container Fundamentals (15 min)

**Question**: Walk me through the last time you debugged a pod crash on a production Kubernetes cluster. Take me from "something's wrong" to "root cause identified."

**What to Look For**:
- Do they jump immediately to logs? (`kubectl logs`, `kubectl describe pod`)
- Do they check for infrastructure issues? (node capacity, PVC attachment, RBAC)
- Do they consider application-level issues? (config, secrets, resource constraints)
- Can they distinguish between CrashLoopBackOff vs. Pending vs. ImagePullBackOff?
- Do they think about observability (metrics, events, previous restarts)?

**Follow-ups** (if needed):
- "What if the logs were empty or truncated?"
- "How would you troubleshoot if the pod never reached Running state?"
- "Have you dealt with resource limit-induced crashes? How did you catch that?"

**Red Flags**:
- Vague answers ("I'd ask the DevOps team")
- No mention of investigation steps or tools
- Assumes one cause without methodical elimination

---

**Question**: Describe a time when you had to explain Kubernetes concepts—like Deployments vs. StatefulSets, or service discovery—to a customer or non-technical stakeholder. How did you approach it?

**What to Look For**:
- Can they simplify without losing accuracy?
- Do they use analogies or diagrams?
- Did they listen to what the customer actually needed to know (vs. info-dumping)?
- Can they connect it to the customer's problem?

---

### 1.2 Observability & Troubleshooting (15 min)

**Question**: A customer reports "the system is slow." Walk me through how you'd investigate, what signals you'd look at, and what you'd ask them.

**What to Look For**:
- **Customer signal triage**: "Slow where? Slow for whom? Did it just start? What changed?"
- **Metrics they'd check**: CPU, memory, disk I/O, network latency, application latency percentiles
- **Log investigation**: error rates, latency buckets, trace IDs (if available)
- **Root cause categories**: app bottleneck vs. infra bottleneck vs. external dependency
- **Customer context**: Did they scale up recently? Deploy a new feature? Change config?

**What NOT to assume is bad**:
- If they jump to "increase resources," ask: "What if the issue isn't capacity?"
- If they skip asking the customer questions, note it.

---

**Question**: Have you set up observability from scratch (Prometheus, Grafana, log aggregation, or tracing)? What was the biggest operational challenge?

**What to Look For**:
- Hands-on experience, not just theory
- Understanding of storage costs, retention policies, query complexity
- Recognition that "ship with observability" is better than "add it later"
- Realistic understanding of operational burden

---

### 1.3 Support Tooling & Triage (15 min)

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

### 1.3b Kubernetes & Deployment Architecture (15 min)

**Question**: Walk me through how you'd design a Kubernetes deployment for a complex, multi-service application. What decisions would you make about StatefulSets, DaemonSets, Jobs, and Deployments?

**What to Look For**:
- **Workload types**: Do they understand when to use each (Deployment for stateless, StatefulSet for state, DaemonSet for node agents, Job for one-offs)?
- **Scaling strategy**: How do they think about HPA (Horizontal Pod Autoscaling)? Do they understand metrics-based vs. scheduled scaling?
- **Resource management**: CPU/memory requests and limits—do they think about burstability vs. guaranteed capacity?
- **Health checks**: Liveness, readiness, startup probes—when do they use each?
- **Rolling updates**: Blue/green vs. canary vs. rolling. Trade-offs?
- **Namespace isolation**: Multi-tenancy, RBAC, network policies

**Follow-ups**:
- "You're deploying a database that needs persistent data. Deployment or StatefulSet?"
- "A pod keeps crashing after deploy. Your readiness probe passed, but liveness is failing. What's happening?"
- "You want zero downtime during an upgrade. What's your strategy?"

**Red Flags**:
- Never deployed to Kubernetes in production
- Confuses StatefulSet with Deployment
- No understanding of resource requests/limits implications

---

**Question**: Tell me about a Kubernetes upgrade or major change you've managed. What broke, and how did you handle it?

**What to Look For**:
- **Planning**: Did they test in a staging environment first?
- **Backwards compatibility**: Do they understand API deprecations, CRD migrations?
- **Rollback plan**: What if something breaks in production?
- **Communication**: Did they notify customers or stakeholders?
- **Monitoring**: Did they watch metrics during the upgrade?

---

### 1.3c AWS & Cloud Deployment (15 min)

**Question**: Describe your experience deploying applications on AWS. What services have you used, and what's your approach to architecture?

**What to Look For**:
- **Compute options**: EC2 vs. ECS vs. EKS—when do they choose each?
- **Networking**: VPC, security groups, NAT gateways, load balancers (ALB, NLB)
- **Storage**: RDS vs. DynamoDB, S3 for what?, EBS vs. EFS
- **IAM & security**: How do they think about least-privilege access, instance roles, policy management?
- **Cost optimization**: Do they monitor spend? Ever consolidated or migrated services?
- **Multi-region/AZ**: Disaster recovery and HA patterns

**Follow-ups**:
- "You're deploying Istari to an air-gapped AWS account. What changes?"
- "An RDS instance is running out of storage. How do you resize it without downtime?"
- "You need to give a customer read-only access to their S3 bucket without providing AWS credentials. How?"

**Red Flags**:
- Only used AWS console (no IaC like Terraform/CloudFormation)
- No understanding of security groups, IAM, or VPC concepts
- Never dealt with scaling or multi-AZ deployments

---

**Question**: Tell me about a time you optimized AWS costs. What did you find, and what was the impact?

**What to Look For**:
- **Specific examples**: Unused instances, oversized instances, data transfer costs, storage optimization
- **Measurement**: Did they quantify the savings?
- **Trade-offs**: Did they consider operational burden vs. cost savings?
- **Automation**: Did they implement guardrails to prevent future waste?

**Example from your resume**: You mentioned "10–20% cost reductions through strategic contract renegotiations and proactive cost auditing." Can you walk through a specific example?

---

### 1.3d Infrastructure as Code & Deployment Automation (12 min)

**Question**: How do you approach Infrastructure as Code (IaC)? What tools have you used (Terraform, CloudFormation, Helm, Ansible)? What are the trade-offs?

**What to Look For**:
- **Tools & experience**: Have they actually written IaC, or just observed?
- **State management**: Do they understand Terraform state, remote backends, locking?
- **Testing**: How do they validate IaC before applying? (terraform plan, policy as code?)
- **Drift detection**: Do they monitor for manual changes that deviate from IaC?
- **Versioning**: How do they version infrastructure changes alongside code?
- **Multi-environment**: How do they manage dev, staging, prod with IaC?

**Follow-ups**:
- "A Terraform apply fails halfway through. How do you recover?"
- "You want to migrate from CloudFormation to Terraform. What's your approach?"
- "You have 10 Kubernetes clusters across 3 regions. How do you manage them all with IaC?"

**Red Flags**:
- Only used cloud UI (no IaC experience)
- "I let DevOps handle infrastructure"
- Can't explain the benefits of IaC

---

**Question**: Describe your CI/CD pipeline. How does code get from commit to production?

**What to Look For**:
- **Stages**: Checkout, build, test, scan, deploy—what's in theirs?
- **Gating**: What has to pass before code goes to prod? Unit tests? Integration tests? Security scans?
- **Deployment strategy**: Manual approval? Automated? Canary?
- **Rollback**: How do they rollback if something breaks?
- **Observability**: Do they check metrics/logs after deploy?
- **Frequency**: How often do they deploy? (Once a year? Daily? Continuously?)

**Follow-ups**:
- "A broken build gets deployed to production. How do you prevent that?"
- "You want to deploy 50 times a day safely. What does that look like?"

---

### 1.3e Customer Deployment & Support Context (10 min)

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
- **Kubernetes**: Pod debugging, workload types (Deployment, StatefulSet, DaemonSet), upgrades, resource management
- **AWS**: VPC, EC2/ECS/EKS, RDS, S3, IAM, networking, cost optimization
- **Infrastructure as Code**: Terraform, CloudFormation, Helm, or similar—hands-on experience
- **CI/CD & Deployment**: Pipeline design, testing gates, deployment strategies, rollback

**Overall Technical Rating**:
- **5**: Deep production experience across K8s, AWS, IaC, and CI/CD. Can architect enterprise deployments.
- **4**: Solid hands-on experience in all areas. Can troubleshoot independently; knows scaling patterns.
- **3**: Competent with minor gaps (e.g., limited IaC experience or only ECS, not EKS). Can grow into the role.
- **2**: Significant gaps (e.g., never deployed to K8s in production, IaC is new). Would need substantial mentoring.
- **1**: Missing critical skills (e.g., no cloud experience, no K8s, no IaC). Not suitable for this role.

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
