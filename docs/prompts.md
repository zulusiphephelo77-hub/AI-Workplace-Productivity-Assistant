# AI Prompts — Sample Prompts & Tested Outputs

Each prompt below was drafted and tested in Gemini Pro before being integrated into the Lovable application. One representative test example is included per feature to demonstrate prompt reliability.

---

## 1. Smart Email Generator

**Prompt:**
```
You are a professional email writing assistant. Write a workplace email based on the details below.

Context: {brief description of the situation}
Recipient type: {client / manager / team member}
Tone: {formal / friendly / persuasive}
Key points to include: {bullet points}

Requirements:
- Keep it concise (under 150 words unless context demands more)
- Match the specified tone consistently
- Include a clear subject line
- End with an appropriate call to action or sign-off
- Do not invent facts, dates, or names not provided in the context
```

**Tested example — escalation email (team member to engineering manager, formal tone):**
> Subject: Escalation: Persistent ingestion sync failure affecting Apex Retail Q3 metrics
>
> Dear Marcus, I am escalating an ongoing data pipeline failure impacting our key enterprise client, Apex Retail. During the manual backfill attempt intended to resolve their missing fortnightly transactions, the ingestion service encountered persistent API rate-limiting errors from the upstream provider... I have compiled the server logs, job identifiers, and rate-limit headers in Jira ticket DP-4421. Could you review the ticket and allocate senior engineering support?
>
> Sincerely, Sipho Dlamini

The prompt correctly held tone and structure consistently across a 3-email escalation chain (client → team member → manager) without inventing unstated facts.

---

## 2. Meeting Notes Summarizer

**Prompt:**
```
You are a meeting notes assistant. Summarize the raw notes below into a structured format.

Raw notes: {paste notes}

Output in this exact structure:
1. Summary (2-3 sentences, key outcome of the meeting)
2. Key Decisions (bullet list)
3. Action Items (bullet list, format: Task – Owner – Deadline if mentioned, otherwise "Owner/Deadline not specified")
4. Open Questions (anything unresolved)

Only include information present in the notes. If a section has nothing relevant, write "None noted."
```

**Tested example — output excerpt:**
> **Action Items**
> - Draft and send an interim status update to Elena Vance outlining the reconciliation timeline – Sipho – Today by 17:00
> - Review and approve the hotfix pull request – Marcus – Today by 19:00
> - Contact upstream API provider support to request a rate-limit increase – Marcus – Deadline not specified

The prompt correctly separated decisions from action items and flagged the one item with no stated deadline rather than inventing one.

---

## 3. AI Task Planner / Scheduler

**Prompt:**
```
You are a productivity planning assistant. Build a schedule from the task list below.

Tasks: {list of tasks with any known deadlines/urgency}
Available time: {e.g. 8 hours, Mon-Fri}

Output:
1. A prioritized task list (High/Medium/Low, with 1-sentence reasoning per item)
2. A structured day-by-day or time-blocked schedule
3. One time-optimization suggestion (e.g. batching similar tasks)

If urgency isn't stated, infer it from deadlines only — flag any assumption you make.
```

**Tested example — prioritization output:**
> **Task: Audit Ingestion Sync & Trace Missing Webhook Events (High Priority)**
> Reasoning: Diagnosing why the scheduled batch failed is the critical bottleneck preventing accurate data flow and blocking any resolution for the client.

The model correctly flagged its own assumption about the workday window (08:30–16:30) rather than presenting it as given.

---

## 4. AI Research Assistant

**Prompt:**
```
You are a research assistant. Summarize the topic/article below for a busy professional.

Topic/text: {paste article or topic}

Output:
1. Summary (3-4 sentences, plain language)
2. Key Insights (3-5 bullet points)
3. Practical Recommendation (1-2 sentences on how this applies to the user's work)
4. Caveat: note if the source material is limited, one-sided, or if this should be verified further

Do not present speculation as fact. Distinguish clearly between what the source states and any inference you make.
```

**Tested example — caveat output:**
> This summary focuses strictly on standard API integration engineering and resilience patterns derived from the preceding technical incident. Specific optimal values—such as exact chunk sizes, backoff multipliers, and concurrency limits—depend directly on the upstream vendor's published API agreements, which must be verified against their documentation.

The prompt reliably separated stated facts from its own recommendation and explicitly flagged where further verification was needed.
