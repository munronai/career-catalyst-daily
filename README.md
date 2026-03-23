# career-catalyst-daily
Assistant skills performing role searches and profile gap analysis with optional application/interview prep.

## :mag: job-search skill
Run a daily job search for Product Manager roles, with configurable search criteria, deduplication against previously seen listings, detailed match/gap analysis against a candidate profile, and keyword mapping per role. Trigger this skill whenever the user asks to find jobs, run a job search, check for new PM roles, look for work, show or edit their search criteria, or do anything related to their job hunt.

## 📈 role-prep skill

Prepares the candidate for applying and interviewing for a specific job role. Use this skill whenever the user selects a role from a job search, asks to prepare for an interview, wants to research a company before applying, needs help understanding what a role will involve, or asks for interview questions. Also triggers when the user says things like "help me prepare for this role", "what should I know about this company", "what questions will they ask me", "let's work on this one", or "I want to apply for [role]". Always use this skill when the user is moving from job search to application or interview preparation.

*The role-prep skill may be chained from the job-search skill*

## The Problem

During a job search, the use of AI assistants helps to perform a gap analysis between a (my) profile and the role description. 
Preparing for a role application and interview (research, mock interview questions) is time-consuming even with AI assistants.
From my perspective, the process is also applied for each role and generally only for roles that I have selected.
The core of the problem is that there is a repeatable process being done manually and therefore less time-efficient that it could be.

## The Solution

The vibe-coded app Career Catalyst (https://github.com/munronai/career-catalyst) provides a UI over a simple prompt that does the gap analysis between a CV/profile and a role description. 
The solution is to extend the idea of Career Catalyst to be able to
- Search for roles posted in the last 6 days that match specified search criteria that the user provides
- Perform the gap analysis between the user's profile and the roles found
- Prepare for interview by carrying out company research, generating likely interview questions, and identifying potential actions that the role would propose and/or deliver in the first 6 months
- TDB: Assist the user in developing a prototype (documentation and/or software) for one of the potential actions
- Run the process daily with as little user intervention as possible (with the exception of review and any prototyping)

### Current Status

Currently
- the `job-search` skill is ready and has been used for searches
- the `role-prep` skill is ready and has been used to generate preparation material 

## How to Use

### Setup
```bash
git clone https://github.com/munronai/career-catalyst-daily.git
```
- Copy the contents of the skills directory into the appropriate CLI skills config directory (e.g. into .claude/skills for Claude Code) or upload the skills to Claude.ai if not using Claude Code.
- Create a profile.md in the `job-search/references` directory that reflects your profile (Tip: use Claude to help you create this profile from the `job-search/references/profile-template.md`
- Update the `job-search/references/default-search-config.md`. By default, this matches my requirements at the time this skill was created (Tip: use Claude to guide you through the creation of a personalised set of search criteria)

### Run

In Claude Code, you can use the `/job-search` or `/role-prep` commands or simply ask for a job search


## What I Learned

- The job search performs the gap analysis on all roles found. This resulted in an unexpected bonus for me because it pulled out roles that I had dismissed (and therefore had not performed any gap analysis more thorough than my gut reaction). This opened up more opportunities.
- The process of having Claude help me with my profile offered another angle on my experience and expertise.
- I primarily used LinkedIn for job searches. The skill cannot do a thorough job here because it requires auth for this. A possible solution here is to find a tool (MCP) that can extend the search into LinkedIn.

## Skill validation using skill-validator (https://github.com/agent-ecosystem/skill-validator)

*job-search*

### Structure

- **Pass:** SKILL.md found
- **Pass:** all files in references/ are referenced

### Frontmatter

- **Pass:** name: "job-search" (valid)
- **Pass:** description: (410 chars)

### Markdown

- **Pass:** no unclosed code fences found

### Tokens

| File | Tokens |
| --- | ---: |
| SKILL.md body | 2,225 |
| references/default-search-config.md | 884 |
| references/profile-template.md | 828 |
| references/profile.md | 1,576 |
| **Total** | **5,513** |

*Note: your default-search-config.md and profile.md shall generate different results*
### Content Analysis

| Metric | Value |
| --- | ---: |
| Word count | 1,540 |
| Code block ratio | 0.09 |
| Imperative ratio | 0.06 |
| Information density | 0.08 |
| Instruction specificity | 1.00 |
| Sections | 21 |
| List items | 28 |
| Code blocks | 2 |

### References Content Analysis

| Metric | Value |
| --- | ---: |
| Word count | 2,297 |
| Code block ratio | 0.06 |
| Imperative ratio | 0.04 |
| Information density | 0.05 |
| Instruction specificity | 0.80 |
| Sections | 25 |
| List items | 95 |
| Code blocks | 4 |

### Contamination Analysis

| Metric | Value |
| --- | --- |
| Contamination level | medium |
| Contamination score | 0.30 |
| Primary language category | markup |
| Scope breadth | 1 |
- **Multi-interface tool detected:** grpc

### References Contamination Analysis

| Metric | Value |
| --- | --- |
| Contamination level | medium |
| Contamination score | 0.30 |
| Scope breadth | 1 |
- **Multi-interface tool detected:** aws, graphql, grpc, kafka

*Note: the "Multi-iterface tool detections are not correct. The terms appear in my profile as technology keywords for searching and gap analysis*

**Result: passed**

*role-prep*

### Structure

- **Pass:** SKILL.md found

### Frontmatter

- **Pass:** name: "role-prep" (valid)
- **Pass:** description: (623 chars)

### Markdown

- **Pass:** no unclosed code fences found

### Tokens

| File | Tokens |
| --- | ---: |
| SKILL.md body | 2,098 |
| **Total** | **2,098** |

### Content Analysis

| Metric | Value |
| --- | ---: |
| Word count | 1,520 |
| Code block ratio | 0.10 |
| Imperative ratio | 0.05 |
| Information density | 0.08 |
| Instruction specificity | 0.22 |
| Sections | 20 |
| List items | 39 |
| Code blocks | 2 |

### Contamination Analysis

| Metric | Value |
| --- | --- |
| Contamination level | low |
| Contamination score | 0.00 |
| Primary language category | markup |
| Scope breadth | 1 |

**Result: passed**


## Next Steps

- Updates from regular usage
- working version of the prototyping skill

