---
name: role-prep
description: >
  Prepares the candidate for applying and interviewing for a specific job role. Use this skill
  whenever the user selects a role from a job search, asks to prepare for an interview, wants
  to research a company before applying, needs help understanding what a role will involve, or
  asks for interview questions. Also triggers when the user says things like "help me prepare
  for this role", "what should I know about this company", "what questions will they ask me",
  "let's work on this one", or "I want to apply for [role]". Always use this skill when the
  user is moving from job search to application or interview preparation.
---
 
# Role Preparation Skill
 
Turns a job listing into a structured preparation document: company intelligence, role
reality check, 6-month proposal ideas, and interview questions tailored to each interviewer
type. Output is saved as a markdown file and presented in chat.
 
This skill chains from the **job-search** skill (roles surface there first) and feeds into
the **proposal-builder** skill (coming later), where the candidate develops one of the
proposed strategies into a full PRD, user stories, and prototype.
 
---
 
## Input
 
The user can refer to a role in any of these ways:
 
- **By number** from the most recent search report — e.g. "Role 3" or "the Ebury one"
- **By URL** — paste a job listing link
- **By description** — company name, role title, or both
 
If the reference is ambiguous (e.g. "the API one" could match multiple roles), ask the user
to clarify before proceeding.
 
If the user provides a URL, fetch it directly. If they reference a report role, load the
most recent report from `~/job-search/reports/` to find the URL, then fetch the full JD.
 
---
 
## Step 1 — Resolve and load the job listing
 
1. Identify which role the user means (see Input above)
2. Fetch the full job description from the direct application URL
3. Extract and hold in memory:
   - Role title and seniority
   - Company name
   - Location / remote policy
   - Key responsibilities (verbatim, for later analysis)
   - Requirements and nice-to-haves
   - Any salary or comp information
   - Team context (team size, reporting line, tech stack) if mentioned
 
If the JD can't be fetched (gated behind login, 404, etc.), ask the user to paste the
job description text directly.
 
---
 
## Step 2 — Research the company
 
Run 3–5 web searches to build a picture of the company. Cover:
 
**Fundamentals**
- What does the company actually do? (product, customers, business model)
- Stage: startup / scale-up / public / enterprise — with evidence (funding, headcount, revenue)
- Recent news: funding rounds, product launches, leadership changes, layoffs, acquisitions
 
**People** _(for companies under ~500 employees, or where a named interviewer is known)_
- Founder(s): background, previous companies, public writing or talks
- CPO / Head of Product: background, how they think about product
- CTO / Engineering lead: background, tech philosophy
- Hiring manager if named in the JD
 
**Product & technology**
- What does the product look like? (demos, screenshots, G2/Capterra reviews, user complaints)
- Tech stack if public (job listings, engineering blog, GitHub)
- API surface if relevant: developer docs, public API changelog, known integrations
 
**Culture & working style**
- Glassdoor / Blind signals (if available) — especially around eng/product relationship
- Engineering blog or public writing that reveals how they work
- Any stated values or ways of working in the JD or on the careers page
 
Summarise findings concisely — this is intelligence, not a Wikipedia article. Flag
anything that's a green flag or a potential concern for the candidate.
 
---
 
## Step 3 — Role reality check
 
Based on the JD and company research, write a clear-eyed summary of what this role will
**actually** involve day-to-day. Go beyond the JD's aspirational language.
 
Structure this as:
 
### What you'll spend most of your time on
The realistic 70–80% of the role, based on the company stage, team size, and the specifics
of the JD. Call out if the JD says "strategy" but the company is early-stage and the PM
will really be writing tickets and unblocking engineers.
 
### What success looks like in 3–6 months
Based on the role context: what would a hiring manager consider a good start? What metrics
or milestones are likely implicit in the role?
 
### Where this role could go
Career trajectory signals: is this a role that grows, or is it a steady-state maintainer
role? Are there signals about autonomy and influence?
 
### Flags worth noting
Anything that might be a concern given the candidate's profile and preferences — e.g.
heavy in-office requirement, domain far from their target, signs of churn or instability,
mismatch between title and actual scope.
 
---
 
## Step 4 — Three 6-month proposals
 
Generate **3 distinct proposals** the candidate could credibly own and deliver in the first
6 months if they got the role. These should be:
 
- **Specific to this company and role** — not generic PM activities
- **Grounded in the research** — address a real gap, opportunity, or stated priority
- **Achievable in 6 months** — scoped for a new joiner, not a transformation programme
- **Differentiated from each other** — vary in focus: one might be discovery/strategy,
  one delivery/execution, one cross-functional or ecosystem
 
For each proposal, use this structure:
 
```
### Proposal [N]: [Short title]
 
**The opportunity:** [What problem or gap does this address, and why now?]
 
**What you'd do:** [3–5 concrete activities or workstreams]
 
**Why you're well-placed to lead this:** [Link to candidate's profile — specific
experience or skills that make this credible, not generic claims]
 
**How you'd measure success:** [1–3 specific, observable outcomes at 6 months]
 
**Dependencies and risks:** [What could slow this down or require buy-in?]
```
 
After presenting all three, add a brief note:
> _These proposals are starting points. The proposal-builder skill (coming soon) will help
> you develop whichever one resonates into a full PRD, user stories, and prototype._
 
---
 
## Step 5 — Interview question sets
 
Generate tailored question sets for each likely interviewer. Base these on:
- The company's stage and culture
- The role's scope and seniority
- The specific JD requirements
- What each interviewer type typically cares about
 
### Hiring Manager questions
Focus on: role fit, how you work, what you've shipped, how you handle ambiguity,
stakeholder management, prioritisation. 8–12 questions.
 
### Engineering Manager questions  
Focus on: technical credibility, how you work with engineers, trade-off reasoning,
your understanding of the tech, how you handle disagreement with engineering.
8–12 questions.
 
### Chief Product Officer (or VP/Head of Product) questions
Focus on: product thinking, strategy, how you'd grow, your philosophy on product,
your view of the market, how you'd operate in this company's context.
8–12 questions.
 
For each question, add a one-line coaching note in _italics_ beneath it:
> _What they're really testing: [underlying concern or signal they're looking for]_
 
End this section with:
> **Tip:** If you know who's interviewing you, share their name and LinkedIn profile and
> I can tailor these further to their specific background and public writing.
 
---
 
## Step 6 — Save and present
 
Save the full output as a markdown file:
 
**Path:** `~/job-search/prep/YYYY-MM-DD-[company-slug]-[role-slug].md`
 
Where `company-slug` and `role-slug` are lowercase, hyphenated versions of the company
name and role title (e.g. `2026-03-21-ebury-api-platform-pm.md`).
 
**File format:**
 
```markdown
# Role Prep: [Job Title] — [Company]
_Prepared: [Day, DD Month YYYY]_
_Source: [URL or "JD provided by candidate"]_
 
---
 
## Company Intelligence
[Step 2 output]
 
---
 
## Role Reality Check
[Step 3 output]
 
---
 
## 6-Month Proposals
[Step 4 output — all three proposals]
 
---
 
## Interview Preparation
[Step 5 output — all three question sets]
 
---
 
_Next step: Use the proposal-builder skill to develop one of the proposals above into
a full PRD, user stories, and prototype._
```
 
Create `~/job-search/prep/` if it doesn't exist.
 
After saving, confirm:
> _Prep document saved to `~/job-search/prep/[filename].md`_
 
Then present the file to the user.
 
---
 
## Notes
 
- **Tailor depth to company size.** For a 30-person startup, the founder research is
  critical and will often surface things directly relevant to the interview. For a 2,000-person
  scale-up, focus more on the CPO and the product org structure.
 
- **Be honest about gaps.** If the company has poor Glassdoor reviews or the JD shows
  signs of scope creep or instability, say so. The candidate is better served by honest
  intelligence than a sales pitch.
 
- **The proposals are for the candidate, not for the interview.** They serve two purposes:
  preparing the candidate to talk confidently about what they'd do in the role, and seeding
  the proposal-builder skill. They're not scripts to recite — frame them that way.
 
- **Named interviewers.** If the user knows who they'll be meeting, offer to refine the
  question sets with that person's background in mind. A quick web search on the interviewer
  often surfaces their product philosophy, past companies, or public talks.
 
- **Chaining to proposal-builder.** Once the candidate has chosen a proposal, they can
  invoke the proposal-builder skill (coming later) with something like "let's build out
  Proposal 2". The prep document's proposal structure is intentionally formatted to make
  this handoff clean.