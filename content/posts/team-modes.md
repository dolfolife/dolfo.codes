---
title: "Team Modes: Delivery Mode vs. Rescue Mode"
date: 2026-01-29T16:19:43+01:00
---

As engineering leaders, we are constantly juggling competing priorities. We want to deliver value to our customers, but we also need to maintain the health of our systems and the wellbeing of our teams. It's a delicate balancing act, and it's easy to feel like we're always falling short in one area or another. I decided to break down patterns I've encountered over the years building teams, and I've realized that there are two distinct modes that teams operate in: Delivery Mode and Rescue Mode. 

The idea of spliting the team modes into two came from reading the book *The Hard Thing About Hard Things* by Ben Horowitz. In the book, Horowitz talks about the difference between running a company during good times and running a company during bad times. He argues that management techniques must flip entirely depending on the context.
*   **Peacetime CEO:** Focuses on culture, fostering creativity, and minimizing conflict. They have the luxury of time to build consensus.
*   **Wartime CEO:** Focuses on the prime directive (market survival). They care little about feelings or consensus; they care about the strict adherence to the path that leads to safety.

An engineering manager must similarly toggle their style, being an empathetic coach in Peace (Delivery Mode) and a directive commander in War (Rescue Mode).

Trying to apply the same tools, processes, and leadership style to every situation leads to frustration: sprint planning feels bureaucratic during a production outage, and incident style urgency burns people out when applied to routine feature work. The reality is that each mode demands a different point of view and a different set of levers.

By explicitly naming **Delivery Mode** and **Rescue Mode**, you gain clarity:

- **Right tool for the job:** Instead of forcing one process to cover all scenarios, you can adopt tools and rituals purpose built for each context. OKRs and sprint planning for Delivery, incident command and war rooms for Rescue.
- **Faster mode recognition:** Once you learn to identify which mode you're in, you stop wasting time applying the wrong playbook. The question shifts from "why isn't this working?" to "which mode are we in, and what does that mode require?"
- **Reduced cognitive load:** Your team can relax into the current mode's expectations instead of constantly renegotiating how to work.

The goal isn't to eliminate Rescue Mode since some level of crisis is inevitable. The goal is to know which mode you're in, apply the right approach, and transition cleanly when circumstances change. This document is designed to help you do exactly that.

In the sections that follow, we'll define each mode in detail, what triggers it, what success looks like, and what leadership behaviors it demands. We'll also explore the "burst capacity" model (how much Rescue Mode a team can absorb before burning out), dependency management (why other teams' crises become yours), and practical checklists for transitioning between modes. Whether you're currently firefighting or enjoying a calm sprint, this framework will give you a shared vocabulary and a playbook for both.

## Core Concepts

### Delivery Mode: Sustainable Growth

*The default state. Validating the path, optimizing the machine, and growing the team.*

In Delivery Mode, the backlog is clear, and the environment is predictable. Leadership focuses on long-term sustainability, career growth, and system hygiene.

| Aspect | Description |
|--------|-------------|
| **Primary Objective** | Deliver roadmap value sustainably |
| **Mindset** | Thoughtful, predictable, optimize for long-term throughput |
| **Operating Constraints** | Keep work predictable; protect focus time |
| **Typical Signals** | Stable on-call, known backlog, low "unknown unknowns" |
| **Success Metrics** | Velocity, capacity, quality, predictability |

**Key Activities:**

- **Delivery & Planning:** Sprint execution, OKRs, capacity/velocity management
- **People & Org:** Onboarding, coaching/mentoring, performance cycles, hiring
- **Technical Excellence:** System design reviews, refactoring, dev lifecycle improvements, TDD
- **Learning & Leverage:** Stretch goals, deliberate learning, platform investments that compound
- **Artifacts:** Plans/OKRs, design reviews, career plans, tech debt strategy, hiring plan

### Rescue Mode: Crisis Response

*The exception state. High operational intensity, unknown territories, and immediate survival.*

In Rescue Mode, the team faces perceived chaos due toincidents, security threats, or existential business deadlines. The path is unclear or obstructed, and the standard process is often too slow.

| Aspect | Description |
|--------|-------------|
| **Primary Objective** | Restore service/safety fast, reduce blast radius, return to Delivery Mode |
| **Mindset** | Alert, decisive, action-oriented |
| **Operating Constraints** | Context switching is expensive; comms must be tight |
| **Typical Signals** | Sev-0/1, active exploit/CVE, outage, major regression, urgent escalations |
| **Success Metrics** | MTTD, MTTR, customer impact containment |

**Key Activities:**

- **Reliability Incidents:** Sev-0/1 response, on-call escalations, detection + recovery
- **Security Response:** CVEs, active threats, emergency patching/mitigations
- **Operational Interrupts:** Urgent support escalations, after-hours stabilization
- **Business-Critical Crunch:** "Do-or-die" moments, funding deadlines, existential customer impact
- **Artifacts:** Incident timeline, decision log, status updates, postmortem + follow-ups

## The Burst Capacity Model

Every team has a **burst capacity** for Rescue Mode similar to AWS EBS burst credits.

### Key Principles

1. **Finite Resource:** Teams cannot sustain Rescue Mode indefinitely without burning out
2. **Recovery Time Required:** After Rescue Mode, teams need Delivery time to recover and recharge
3. **Predictability Trade-off:** Too much Rescue Mode erodes stability, morale, and predictability
4. **Cannot Be Cut:** Rescue Mode work takes as long as it takes—you cannot artificially constrain it

### Warning Signs of Burnout

- Decreased velocity in Delivery Mode
- Increased employee turnover
- Declining code quality
- Reduced engagement in planning activities
- More incidents (creating a negative feedback loop)

## Critical Success Factors

### For Rescue Mode Success

| Factor | Description |
|--------|-------------|
| **Trust** | Team members must trust each other's technical judgment under pressure |
| **Tooling** | Automated detection, deployment, rollback, and monitoring reduce MTTR |
| **Onboarding** | Every team member must be fully onboarded to contribute during crises |
| **Focus** | Eliminate all distractions outside the critical task |
| **Clear Communication** | Defined incident commander roles and communication protocols |

**DORA Metrics for Rescue Mode:**
- **MTTR (Mean Time to Recovery):** How quickly can you restore service?
- **MTTD (Mean Time to Detection):** How quickly do you identify issues?

### For Delivery Mode Success

| Factor | Description |
|--------|-------------|
| **Rhythm and Ritual** | Establish sustainable work patterns and ceremonies |
| **Automation** | Automate toil work to maximize time for business value |
| **Capacity Planning** | Realistic estimation accounting for potential Rescue Mode interruptions |
| **Career Investment** | Dedicate time to mentoring, feedback, and development |
| **Technical Excellence** | Pay down debt proactively to prevent future incidents |

## Dependency Management and System Resilience

> **Critical Principle:** A system is only as strong as its weakest link (internal or external).

### The Dependency Problem

Your team's Rescue Mode frequency is affected by:
- Number of dependencies on external services
- Hardness of coupling (hard vs. soft dependencies)
- Resilience patterns implemented (circuit breakers, timeouts, graceful degradation)

### Example Scenario

Your service displays customer data including "last 3 orders" from an external Orders service:

| Dependency Type | Behavior | Your Mode |
|-----------------|----------|-----------|
| **Hard Dependency** | Orders service down → Your service appears down | Enter Rescue Mode |
| **Soft Dependency** | Orders service down → Your service shows data without orders | Remain in Delivery Mode |

### Mitigation Strategies

- Make non-critical attributes optional
- Implement circuit breakers and fallbacks
- Cache data for resilience
- Design for graceful degradation
- Establish clear SLA expectations with dependency owners


## Incident Command Structure

Use an incident command structure so the team can execute without everyone trying to lead at once:

| Role | Responsibility |
|------|----------------|
| **Incident Commander (IC)** | Owns decisions + keeps the incident moving |
| **Comms Lead** | Stakeholder/customer updates, keeps noise off responders |
| **Ops/Tech Lead(s)** | Directs technical investigation and mitigations |
| **Scribe** | Timeline + decisions + actions captured live |

### Exit Criteria ("Back to Delivery" Checklist)

- [ ] Customer impact stopped or bounded
- [ ] Monitoring confirms stability trend
- [ ] Short-term mitigation in place (even if root cause isn't fully fixed)
- [ ] Postmortem scheduled and owners assigned

## Leadership Responsibilities by Mode

### Delivery Mode Leadership

- ✓ Focus on career development and growth opportunities
- ✓ Maintain predictable velocity and capacity planning
- ✓ Work on team alignment and priority setting
- ✓ Invest in automation and toil reduction
- ✓ Build resilience through architecture and tooling
- ✓ Create psychological safety and trust
- ✓ Hire and onboard effectively
- ✓ Review and optimize processes

### Rescue Mode Leadership

- ✓ Define clear success criteria for resolution
- ✓ Identify steps to return to Delivery Mode
- ✓ Remove obstacles and distractions
- ✓ Communicate status to stakeholders
- ✓ Ensure proper incident command structure
- ✓ Monitor team energy and prevent burnout
- ✓ Document decisions for AAR
- ✓ Shield team from external pressure

### Post Rescue Mode Leadership

- ✓ Conduct After-Action Reviews (AAR) and postmortems
- ✓ Identify root causes and prevention measures
- ✓ Update runbooks and tooling
- ✓ Give team recovery time
- ✓ Recognize contributions and effort
- ✓ Implement improvements to reduce future occurrence

## Communicating Mode Transitions

Clear communication during mode transitions prevents confusion and sets expectations. Ambiguity about "are we in incident mode or not?" leads to half-measures and delayed responses.

### Entering Rescue Mode (Delivery → Rescue)

**To the Team:**
1. **Explicit declaration:** "We are now in Rescue Mode. [Brief description of the trigger]."
2. **Assign roles immediately:** "IC is [name], Comms is [name]."
3. **State the success criteria:** "We're done when [X metric is restored / customer impact is stopped]."
4. **Clear expectation shift:** "All sprint work is paused. Focus only on this."

**To Stakeholders:**
- Use a standing incident communication template:  
  *"We have identified [issue]. Impact: [scope]. Current status: [investigating/mitigating]. Next update in [30 min]."*
- Over-communicate cadence, under-communicate speculation.

### Exiting Rescue Mode (Rescue → Delivery)

**To the Team:**
1. **Explicit stand-down:** "We are exiting Rescue Mode. The immediate threat is contained."
2. **Acknowledge the work:** Quick recognition of effort before moving on.
3. **Set recovery expectations:** "We're resuming sprint work tomorrow. Today is buffer/decompression."
4. **Schedule the postmortem:** "Postmortem is [date]. Action items will flow into the backlog."

**To Stakeholders:**
- Final incident summary:  
  *"Issue resolved at [time]. Root cause: [brief]. Customer impact: [duration/scope]. Follow-up postmortem scheduled."*

### Rituals That Reinforce Mode Awareness

| Ritual | Purpose |
|--------|---------|
| **Status channel** | A single #team-status channel where mode is always visible ("🟢 Delivery" or "🔴 Rescue: [incident link]") |
| **Standup framing** | Start every standup with "We are in [Mode]." Reinforces shared awareness. |
| **Calendar block** | When entering Rescue Mode, IC or manager cancels/postpones non-essential meetings for the team. |

## Post Incident Follow Through

A postmortem without owners and dates becomes a diary. The value of Rescue Mode isn't just surviving the incident—it's learning from it so it doesn't happen again.

### The Postmortem Checklist

Every postmortem should produce:

| Output | Description |
|--------|-------------|
| **Timeline** | What happened, when, and who did what. Facts only, no blame. |
| **Root Cause(s)** | The underlying issue(s), not just the trigger. Use "5 Whys" or similar. |
| **Contributing Factors** | What made detection slower or impact larger? |
| **Action Items** | Concrete tasks with owners and due dates. |
| **What Went Well** | Reinforce behaviors you want repeated. |

### Tying Actions to the Backlog

Postmortem action items must flow into your tracked work system (Jira, Linear, etc.):

1. **Create tickets immediately** — Don't wait. Do it in the postmortem meeting.
2. **Tag them consistently** — Use a label like `postmortem` or `incident follow up` for visibility.
3. **Assign owners, not teams** — "Team X will fix this" means no one will fix this.
4. **Set realistic due dates** — Balance urgency against current Delivery Mode capacity.
5. **Review in sprint planning** — Postmortem items compete for capacity like any other work.

### Follow Through Rituals

| Ritual | Purpose |
|--------|---------|
| **Postmortem review meeting** | 48-72 hours after incident. Fresh enough to remember, calm enough to think. |
| **Action item standup tag** | Weekly check: "Any postmortem items blocked or at risk?" |
| **Monthly incident review** | Leadership reviews open postmortem actions. Escalates stale items. |
| **Quarterly retro** | Are we seeing repeat patterns? Is our prevention investment working? |

### Anti-Patterns to Avoid

-  **Postmortem delayed indefinitely** — Schedule it before closing the incident.
-  **Actions without owners** — If no one owns it, it won't happen.
-  **"We'll be more careful"** — Not an action. What system change prevents recurrence?
-  **100-item action list** — Pick the 3-5 highest-leverage items. The rest goes to tech debt backlog.
-  **Blame culture** — If people fear punishment, they'll hide information. You'll learn nothing.

## Team Maturity Assessment

How do you know if your team is actually good at operating in both modes? Maturity isn't about never entering Rescue Mode but how smoothly you operate in each mode and how gracefully you transition between them.

Use this framework to assess where your team stands and where to invest.

### Rescue Mode Effectiveness

A mature team in Rescue Mode doesn't panic. They've built the muscle memory and tooling to respond quickly without chaos. Assess your team on:

| Dimension | What to Look For |
|-----------|------------------|
| **Speed of detection and response** | How long between "something is wrong" and "we're actively working on it"? MTTD and MTTR are your primary signals. |
| **Quality of communication** | Are stakeholders informed without responders being interrupted? Is there a single source of truth? |
| **Ability to execute under pressure** | Does the team fragment or unite? Do people know their roles, or is there confusion about who decides what? |
| **Post-incident learning** | Do postmortems happen? Do actions get completed? Are you seeing fewer repeat incidents over time? |

**Red flags:** Finger-pointing during incidents, no clear IC, stakeholders pinging individual engineers for status, repeat incidents on the same root cause.

### Delivery Mode Effectiveness

A mature team in Delivery Mode operates predictably and sustainably. They're not just shipping—they're building capability for the future. Assess your team on:

| Dimension | What to Look For |
|-----------|------------------|
| **Consistent velocity and predictability** | Can you forecast what will ship this sprint with reasonable accuracy? Or is every sprint a surprise? |
| **Proactive debt management** | Is tech debt addressed intentionally, or only when it causes outages? Do you have a debt backlog? |
| **Career development culture** | Are 1:1s happening? Are people growing? Do ICs have visibility into their path forward? |
| **Low unplanned work percentage** | What fraction of your sprint is reactive vs. planned? High unplanned work erodes trust and predictability. |

**Red flags:** "We never have time for refactoring," cancelled 1:1s, engineers surprised by their performance reviews, constant scope creep.

### What Mature Teams Look Like

- **Rescue Mode is a calm workflow, not a panic.** Roles are clear, runbooks exist, and people trust each other.
- **Most time is spent in Delivery Mode.** Rescue Mode is the exception, not the norm.
- **Rescue Mode frequency is decreasing over time.** Prevention investments are paying off.
- **DORA metrics trend positively.** Deployment frequency up, lead time down, change failure rate down, MTTR down.
- **The team can articulate which mode they're in.** Shared vocabulary exists and is used.

## Common Pitfalls and Anti-Patterns

####  Attempting to Budget Rescue Mode Work
- "Ops days" or "on-call effort" percentages are estimates at best
- Rescue Mode work cannot be cut due to time constraints
- Attempting to time-box critical incidents leads to poor outcomes

###  Treating All Work as Delivery Mode
- Applying standard planning processes during crises creates delays
- Requiring extensive documentation before action during incidents
- Not recognizing when to shift gears

###  Operating in Permanent Rescue Mode
- Treating every task as urgent undermines true priorities
- Team burnout and turnover
- No time for strategic improvements
- Accumulating technical debt

###  Ignoring Post-Rescue Recovery
- Immediately returning to normal sprint work without reflection
- No AAR or postmortem process
- Missing opportunities for prevention
- Team exhaustion accumulates

## Final Tips

Engineering leadership requires fluency in both Delivery and Rescue modes. Success comes from:

- **Building trust and capability** during Delivery Mode to enable effective Rescue Mode response
- **Investing in tooling and automation** to reduce toil and improve MTTR/MTTD
- **Managing dependencies** to prevent cascading failures
- **Creating sustainable rhythms** that allow for recovery and growth
- **Learning continuously** from incidents to prevent recurrence

The most mature teams minimize time in Rescue Mode through prevention while maintaining the capability to execute effectively when crises occur. Your role as a leader is to create the conditions for both modes to succeed without burning out your team.
