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

If you wish to try the game follow the instructions below

### Setup
```bash
git clone https://github.com/munronai/percentages.git
cd percentages
npm install
```

### Run

To start the game server on localhost:3000
```bash
npm run dev
```

To start the relay server 
```bash
npm run relay
```

## How It Works

Enter your name to start - note that this will be stored in browser local storage (use the browser developer tools to inspect)
Select single or multiplayer game
Single player:
- the game begins and starts with a 90% question. This is the only question that make sense (to a human!)
- There is 60 seconds to answer otherwise you lose
- After the first question there are questions for 80% and 70%. These are placeholders for development tests (don't expect too much!). Take a look at the code to see the answers required
- The game ends when you answer all of the questions or fail to answer a question. At that point you can review the questions (and answers) for that game.

Multiplayer:
- This is not yet fully functional; you can create and join a game lobby but that is all.
- To test, open two browser tabs (preferably one of these as an incognito window)
- In one of the tabs, choose to host a public game. This new game should show in the window of the second player and allow you to join the game
- Upon joining, the game lobby should show both players. 

## Tradeoffs and Decisions


- **Delaying the implementation of AI-generated questions:**

The intention was (and still is) to have AI-generated questions however there are multiple challenges that would have delayed the building of the app.
- AI does not seem to be good at generating the puzzle/logic type of questions, never mind getting the level correct (90%, 80% and so on). The percentage is supposed to be based on the percentage of the population that can answer the question. This is difficult to test without extensive survey and therefore more difficult to do on the fly
- To generate questions on the fly, we need to be confident in the question logic and difficulty and currently generating images on the fly for questions would be too slow
- The (financial) cost of generating questions through an API needs to be evaluated

- **What I'd do differently:**

It's not so much a question of doing things differently. The intention to get something working remains. However, I think it would be easier to have AI-generated logic puzzles especially based on wordplay and drop the "strict" comparison/requirement with the percentage difficulty.

- **Multiplayer using a relay:**

A temporary decision to get something up and running. This resulted in a more "agile" iterative approach to the message design and how things should work. It has been a build-test-fix cycle. The relay server is a limiting factor for scalability. The ultimate goal is to use a pub/sub acrhitecture on a platform like Ably.

- **What I'd do differently:**

Take more time to design the architecture and the message content/intention before launching into the multiplayer build.

- **Reliance on PRD and user stories to drive the build:**

The approach has been to create the PRD (including iterations) and the user stories with AI assistance before asking the agent to develop a user story. This works but as the app gets more complex it is becoming difficult to easily know if I'm on the right track.

- **What I'd do differently:**

The next step (I think) will be a refactor. The codebase and the architecture requires better guidance, therefore there is a need to work on this and document how things should be structured (e.g. the aforementioned message use cases, the scalability).


- **Why Gemini CLI over Claude Code:**

I think Claude is more powerful/advanced but I wanted to see how Gemini coped with the same tasks and, I managed to get a reduced price for a few months of Google AI Pro!

- **What I'd do differently:**

For me this will ultimately come down to cost and how this changes in future but if prices are comparable I would choose the service that offers the more comprehensive function (Claude). 
I can see this changing if Gemini catches up and/or surpasses Claude. 
I have also been using jules.google.com because jules finds issues (example: typescript linting issues) that Gemini CLI did not. 
While Jules could be used on any repo (and therefore code created by Claude), the use of jules is included in the cost of Google AI Pro.

## What I Learned

- There is more depth required for my approach. There is a great experience in requesting that the agent ask you questions - even if you know the answers, it helps to make sure the agent knows the answers. It is useful to use the scripted personas (e.g. Engineering Lead) to drive out concerns that can be forgotten during the process. Further depth would be in the use of sub agents to be more efficient - at the moment this is a single person with technology assistant approach; there are more effective ways to use the agent(s) as a team.
- Gemini is currently (Mar 2026) not as capable (as Claude) when it comes to sub-agents that run in the background
- When it comes to asking for development, I find that I am repeating some instructions (mainly around TDD). A skill is a next step for this to avoid repetition.
- I have seen suggestions that PRDs and other documentation is less important in the context of the use of these CLI tools. I understand where that thinking comes from but I think the exercise of documenting and having the AI critique withn different personas remains a useful way of understanding the problem and what you intend to do.
- I noticed that it is easy to continue to prompt when in build mode instead of returning to documentation and user stories first. While it is faster to continue to develop, and it's ok for a personal project like this, the auditability of changes would be necessary in any context where the software would be used by customers (paying or otherwise).

## Next Steps

Read the PRD percentages-prd-2.md and the user stories. The focus is on the multiplayer aspects before the question content is improved.

