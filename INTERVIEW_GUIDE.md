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
- 1.3b Infrastructure & DevOps (42 min) ← **Core required skills**
- 1.4 APIs & Networking (10 min)
- 1.5 Wrap-up & Buffer (10 min)

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

### 1.3b Infrastructure & DevOps Fundamentals (20 min)

#### Docker & Container Specifics

**Question**: Walk me through containerizing an application. What are the key decisions you make, and what mistakes have you seen?

**What to Look For**:
- Base image selection (official vs. distroless, size concerns)
- Multi-stage builds (optimization, security)
- Dockerfile best practices (layer caching, minimal layers, avoiding root)
- Registry management (private registries, image signing, scanning)
- Image size optimization (do they think about production footprint?)
- Have they dealt with rootless containers or security contexts?

**Follow-ups**:
- "A container runs fine locally but fails on the customer's Kubernetes cluster. What would you investigate?"
- "You're building an image for an air-gapped environment. What's different?"
- "How do you balance image size with operational convenience?"

**Red Flags**:
- Never built a container image themselves
- "Just use the official image" without understanding trade-offs
- No awareness of image security (scanning, CVEs, signing)

---

**Question**: Tell me about a time you debugged a container networking issue—maybe a DNS problem, port binding, or connectivity between containers. Walk me through your troubleshooting.

**What to Look For**:
- Container networking fundamentals (bridge networks, overlay networks, service discovery)
- DNS resolution issues (inside container vs. external)
- Port exposure and firewall rules
- Tools they'd use (`docker logs`, `docker exec`, `docker inspect`, `netstat`, `ping`, `curl`)
- Understanding of localhost vs. container hostname vs. service DNS
- How they'd test connectivity (curl, nc, telnet)

---

#### PostgreSQL & Relational Databases

**Question**: You're called in because a PostgreSQL database is running slowly. Walk me through how you'd diagnose the issue. What metrics would you look at?

**What to Look For**:
- **System queries**: Can they read `pg_stat_statements`? Do they understand `EXPLAIN ANALYZE`?
- **Connection management**: Are there too many connections? Idle connections? Blocking?
- **Index health**: Do they think about missing indexes, bloated indexes?
- **Disk I/O**: Are queries hitting disk vs. cache? Can they check buffer pool hit ratio?
- **Configuration**: Do they know about `shared_buffers`, `work_mem`, `maintenance_work_mem`?
- **Replication**: Do they understand lag, how to check it, what causes it?

**Follow-ups**:
- "A backup is taking 6 hours. The customer says it used to take 30 minutes. What changed?"
- "You're migrating a customer to a managed database (RDS, CloudSQL). What gotchas are there?"
- "How do you safely roll out a major version upgrade (12 → 13 → 14)?"

**Red Flags**:
- Never tuned a database or only used cloud-managed services
- Can't explain replication, backups, or WAL (Write-Ahead Logging)
- No understanding of ACID guarantees or transaction isolation

---

**Question**: Describe a database backup and recovery procedure. What's your approach, and what could go wrong?

**What to Look For**:
- Backup strategy: Full + incremental? PITR (Point-In-Time Recovery)?
- Testing the backups: Do they actually test recovery? (Restore tests are often skipped!)
- Recovery time objectives (RTO) and recovery point objectives (RPO)
- Backup storage and retention policies
- Encryption of backups
- Cross-region or off-site backup storage
- Understanding of logical vs. physical backups

**Red Flags**:
- Never tested a recovery
- Assumes backups work without verification
- No understanding of RTO/RPO trade-offs

---

#### Observability Tools (Prometheus, Grafana, Log Aggregation)

**Question**: You need to set up monitoring and alerting for a Kubernetes cluster running a database-backed application. Walk me through your approach. What would you monitor, and what would you alert on?

**What to Look For**:
- **Metrics** (Prometheus):
  - Application metrics (latency, error rate, throughput)
  - Infrastructure metrics (CPU, memory, disk, network)
  - Database metrics (connections, slow queries, replication lag)
  - Do they understand cardinality? (Can they avoid exploding metric volumes?)
- **Alerting**:
  - Alert thresholds that are meaningful (not too strict, not too loose)
  - Alert routing (who gets paged? on call?)
  - Alert fatigue (do they recognize noisy alerts?)
  - Runbook links with alerts
- **Dashboards** (Grafana):
  - What would they visualize?
  - RED method (Rate, Errors, Duration) or USE method (Utilization, Saturation, Errors)?
- **Logs**:
  - Log aggregation tool (ELK, Splunk, Datadog, etc.)
  - Structured logging (JSON) vs. unstructured
  - Log retention and cost management
  - Can they write useful log queries?

**Follow-ups**:
- "You're getting 10,000 alerts a day. What's wrong?"
- "A customer is complaining about slow queries, but your monitoring doesn't show high load. What's going on?"
- "You need to debug a one-time issue that happened at 3 AM. How do you approach it?"

**Red Flags**:
- No hands-on experience with Prometheus/Grafana
- Only used third-party hosted observability (never self-hosted)
- Can't explain cardinality or metric explosion risk
- No understanding of alerting best practices

---

**Question**: Have you had to troubleshoot observability itself? (e.g., "we're not seeing metrics we expect," "log aggregation is slow," "we're missing data")

**What to Look For**:
- Pragmatic debugging of monitoring infrastructure
- Understanding of data pipelines (scraping, shipping, querying)
- Recognition that observability adds operational burden
- Examples of iterating on observability as the system evolved

---

#### Linux Administration & Networking

**Question**: A customer is having intermittent connection timeouts to their Istari instance. Walk me through how you'd investigate.

**What to Look For**:
- **Network diagnosis**:
  - Tools: `ping`, `traceroute`, `netstat`, `tcpdump`, `ss`
  - DNS resolution (`nslookup`, `dig`)
  - Network namespaces (especially in Kubernetes context)
  - Firewall rules and security groups
- **Application level**:
  - TCP connection pooling, idle timeout settings
  - Read/write timeouts, connection timeout thresholds
  - Retry logic and backoff strategies
- **Infrastructure**:
  - Kubernetes network policies
  - Service discovery and load balancing
  - Proxy or ingress configuration
- **Customer environment**:
  - Are they behind a proxy, firewall, or VPN?
  - NAT or port forwarding?
  - ISP or connectivity issues?

**Follow-ups**:
- "The issue only happens during business hours. What does that tell you?"
- "You're migrating a customer from on-prem to cloud. What networking issues might they hit?"
- "A customer uses Zscaler (SSL-inspecting proxy). What problems might that cause?"

**Red Flags**:
- Never used network diagnostic tools
- Assumes "it's the network" without investigation
- No understanding of how Kubernetes networking works
- Can't explain DNS, NAT, or proxy concepts

---

**Question**: Tell me about a time you had to troubleshoot a TLS/certificate issue. What was the problem, and how did you solve it?

**What to Look For**:
- Common issues: expired certs, hostname mismatches, self-signed certs, intermediate cert chains
- Tools: `openssl s_client`, certificate inspection, chain validation
- Understanding of certificate rotation and renewal processes
- How self-signed certs affect different scenarios (browsers, APIs, curl, Kubernetes)
- Custom CA bundles and how to configure applications to trust them
- Kubernetes-specific: where certs live (secrets, ingress, istio), how to rotate them

**Red Flags**:
- No hands-on TLS experience
- "Just use Let's Encrypt" without understanding how it works
- No awareness of certificate chains or intermediate certificates

---

#### REST & GraphQL APIs

**Question**: You're integrating Istari with a customer's system. Their API requires authentication. Walk me through how you'd set it up and what could go wrong.

**What to Look For**:
- **Auth mechanisms**:
  - API keys (basic auth, bearer tokens)
  - OAuth2 and OpenID Connect
  - Mutual TLS (mTLS)
  - Custom headers and signatures
- **Integration challenges**:
  - Rate limiting and backoff/retry logic
  - Timeout configuration
  - Certificate pinning or custom CA trust
  - Error handling and status codes
  - Pagination and large result sets
- **Security**:
  - Never logging credentials
  - Secure storage of secrets
  - Audit logging of API calls

**Follow-ups**:
- "The API returns a 500 error on your integration test, but when you call it manually with curl, it works. What might be different?"
- "How do you handle an API that changes its response format?"

---

**Question**: Describe the difference between REST and GraphQL. When would you recommend each? What are the operational implications?

**What to Look For**:
- **REST**: Stateless, resource-oriented, standard HTTP verbs, easy to cache and monitor
- **GraphQL**: Flexible queries, single endpoint, over-fetching vs. under-fetching trade-offs
- **Operational concerns**:
  - Caching strategies (REST: HTTP caching easy; GraphQL: harder)
  - Rate limiting (GraphQL: query complexity; REST: per-endpoint)
  - Monitoring and debugging (GraphQL: opaque queries; REST: clear URLs)
  - Error handling (structured vs. HTTP status codes)
- **Customer context**: Do they think about API versioning and backwards compatibility?

**Red Flags**:
- No real experience with either
- Strong opinion without understanding trade-offs

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

**Required competencies** (must score ≥3 in each):
- **Kubernetes & containers**: Pod debugging, deployment strategies, networking, RBAC
- **Databases (PostgreSQL)**: Query troubleshooting, performance tuning, replication, backups
- **Observability**: Prometheus/Grafana experience, log aggregation, alerting strategy
- **Linux & networking**: Diagnostic tools, TLS/certificates, DNS, network troubleshooting
- **APIs**: REST and/or GraphQL integration, authentication, error handling

**Overall Technical Rating**:
- **5**: Deep hands-on across all required areas. Can architect solutions and mentor others.
- **4**: Solid experience in all areas. Can troubleshoot independently; knows when to escalate.
- **3**: Competent in most areas; minor gaps in 1–2 areas (e.g., database tuning). Can grow into the role.
- **2**: Significant gaps in foundational knowledge (e.g., never tuned a database, no observability setup). Would need substantial mentoring.
- **1**: Missing critical skills (e.g., no K8s, no Linux, no database experience). Not suitable for this role.

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
