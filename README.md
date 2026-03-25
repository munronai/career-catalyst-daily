# career-catalyst-daily
Assistant skills performing role searches and profile gap analysis with optional application/interview prep.

:exclamation: NOTE: Claude Code (on Pro) is very expensive when performing the web search. The positives are that it is thorough but it spends too much time on this task and can easily burn through your daily limit.


:+1: RECOMMENDATION: You can achieve good results without the CLI by uploading the skills into Claude.ai.

Alternatively, add the skills to Gemini CLI - more efficient with the web search but often requires more explicit prompting. 

You could also use the SKILL.md file and profile to set up a Gem for Gemini if you can't use, or don't want to use, the CLI.

#### Table of Contents

- [:mag:  job-search skill](#job-search-skill)
- [📈 role-prep skill](#role-prep-skill)
- [:construction: proposal-builder skill](#proposal-builder-skill)

## :mag: job-search skill {#job-search-skill}
Run a daily job search for Product Manager roles, with configurable search criteria, deduplication against previously seen listings, detailed match/gap analysis against a candidate profile, and keyword mapping per role. Trigger this skill whenever the user asks to find jobs, run a job search, check for new PM roles, look for work, show or edit their search criteria, or do anything related to their job hunt.

## 📈 role-prep skill {#role-prep-skill}

Prepares the candidate for applying and interviewing for a specific job role. Use this skill whenever the user selects a role from a job search, asks to prepare for an interview, wants to research a company before applying, needs help understanding what a role will involve, or asks for interview questions. Also triggers when the user says things like "help me prepare for this role", "what should I know about this company", "what questions will they ask me", "let's work on this one", or "I want to apply for [role]". Always use this skill when the user is moving from job search to application or interview preparation.

*The role-prep skill may be chained from the job-search skill*

## :construction: proposal-builder skill {#proposal-builder-skill}

Rapidly prototypes and documents high-value proposals to support job applications.
  Turns role-prep ideas into "Proof of Value" packages including research, PRDs,
  strategy, architecture, and agent reviews.

*The proposal-builder skill may be chained from the role-prep skill*

The original prompt for Gemini CLI when creating the proposal-builder skill is recorded at the end of this document.


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
- Assist the user in developing a prototype (documentation and/or software) for one of the potential actions
- Run the process daily with as little user intervention as possible (with the exception of review and any prototyping)

### Current Status

Currently
- the `job-search` skill is ready and has been used for searches
- the `role-prep` skill is ready and has been used to generate preparation material 
- an initial version of `proposal-builder` is ready

## How to Use

### Setup
```bash
git clone https://github.com/munronai/career-catalyst-daily.git
```
- Copy the contents of the skills directory into the appropriate CLI skills config directory (e.g. into .claude/skills for Claude Code) or upload the skills to Claude.ai if not using Claude Code. Alternatively, add the skills directory contents into .gemini/skills for Gemini CLI)
- Create a profile.md in the `job-search/references` directory that reflects your profile (Tip: use Claude to help you create this profile from the `job-search/references/profile-template.md`
- Update the `job-search/references/default-search-config.md`. By default, this matches my requirements at the time this skill was created (Tip: use Claude to guide you through the creation of a personalised set of search criteria)

### Run

In Claude Code (or Gemini CLI), you can use the `/job-search` or `/role-prep` or `/proposal-builder` commands or simply ask for a job search


## What I Learned

- When running in Claude in the browser, the web search was efficient and did not have a long running time. In Claude Code, the search became recursive and very expensive (I hit my limits on a single search).
- I transferred the skill to Gemini CLI and asked for some changes to improve the efficiency of the search to make it less expensive. Gemini executed a less expensive search but did not strictly adhere to the instructions (e.g. salary/comp information was not checked). Further chnages were required to ensure the search and the report output were more consistent.
- The job search performs the gap analysis on all roles found. This resulted in an unexpected bonus for me because it pulled out roles that I had dismissed (and therefore had not performed any gap analysis more thorough than my gut reaction). This opened up more opportunities.
- The proposal builder skill was originally intended to be a guide, a workflow for the assistant to impose upon the user. It was intended to be something that might require 3-4 hours. However, on the first run, the assistant (Gemini CLI) went ahead and generated the documents for all of the steps. I felt that this was more likely to be a faster experience where there was a base for me to work from to verify and then build out the proposal with the time I had available.
- The process of having Claude help me with my profile offered another angle on my experience and expertise.
- I primarily used LinkedIn for job searches. The skill cannot do a thorough job here because it requires auth for this. A possible solution here is to find a tool (MCP) that can extend the search into LinkedIn.

## Skill validation using skill-validator (https://github.com/agent-ecosystem/skill-validator)

## *job-search*

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

---

## *role-prep*

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

-----

## *proposal-builder:*

### Structure

- **Pass:** SKILL.md found

### Frontmatter

- **Pass:** name: "proposal-builder" (valid)
- **Pass:** description: (197 chars)

### Markdown

- **Pass:** no unclosed code fences found

### Tokens

| File | Tokens |
| --- | ---: |
| SKILL.md body | 974 |
| **Total** | **974** |

### Content Analysis

| Metric | Value |
| --- | ---: |
| Word count | 621 |
| Code block ratio | 0.00 |
| Imperative ratio | 0.20 |
| Information density | 0.20 |
| Instruction specificity | 1.00 |
| Sections | 10 |
| List items | 36 |
| Code blocks | 0 |

### Contamination Analysis

| Metric | Value |
| --- | --- |
| Contamination level | low |
| Contamination score | 0.00 |
| Scope breadth | 0 |

**Result: passed**

---

**1 skill validated: all passed**


## Next Steps

- Updates from regular usage


### proposal-builder original skill creation prompt:

```
   Let's look at creating a proposal-builder    
   skill that builds on the proposals that are generated by the role-prep skill.                                                                   

   Note that for this skill we shall build a proposal from the two files mentioned but the skill should be able to be used for any proposal in future.       
                  
   The overall goal of this skill is to be able to quickly prototype something that may be used to support an application for a role while at the same time helping the user   
   to familiarise themselves with the role and the company as much as is possible with the info available.                                                                     
  
   In many cases, it may not be prototype software that is required but a fuller proposal in terms of research and documentation. 

   It is important that the proposal puts the user in the "Here is what I can do for you/Here is where I am bringing value to you" position for applying for the role.       


   To build this skill, let's look at the "Quote Precision AI Auditor"                                                                                                         
   - Let's create a research step. In this case, we need to gather data into a tabulated report or spreadsheet so that we can do some more analysis (e.g. does the quoted      
   price change on all type of legal request or is it particular areas that are not being quoted accurately). The research reports and files need to go into a research        
   directory                                                         

   - Assist the user in writing a PRD or other requirements document and a one-pager. For these we need two directories, a prds directory and a one-pagers directory           
   - Assist the user in writing a strategy/vision document and also where this fits in the wider company strategy (albeit with limited information given that the user does    
   not have the role yet. Assumptions and decisions need to be clearly stated). This should go in the strategy directory.                                                      
   - For cases where we need to develop prototype software or a demo, we need to create some technical architecture documentation. This documentation goes in the              
   technical-architecture directory                                                                                                                                            
   - Assist the user in creating a McKinsey-style 5 slide presentation deck for the proposal. This should go in the presentations directory                                    
   - Assist the user in creating user stories for any software prototype development. These go in the user-stories directory                                                   
   - Create three agent profiles specific to the role and the company that can review the documentation and provide feedback reports as markdown docs. The three profiles are: 
   Executive (covering vision, strategy, finance), Engineering, and User Research. Assist the user in having these reports generated and record the output reports in the      
   reviews directory                                                                                                                                                           
                                                                                                                                                                               
   For this exercise, time is of the essence.                                                                                                                                  
   - the user (Candidate) does not have days to do this work. It is better to have something that demonstrates thinking and supports the application than perfection. The user 
   can always iterate later after an application is submitted. The user should be able to complete something with your help in 3 to 4 hours.                                   
   - the user is also trying to demonstrate an ability to deliver quickly using the AI tools at hand                                                                           
                                                                                                                                                                               
   NOTE: This is a complex set of instructions and a single skill.md may not be enough. Please advise how the skill is being broken down if this becomes necessary. The skill  
   must be repeatable and all steps must be carried out unless the user advises otherwise.                                                                                 
   ```


