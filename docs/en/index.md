<div style="text-align: right; margin-bottom: 20px;">
  <a href="../">中文</a> | <a href="./">English</a>
</div>

---
layout: page
title: Main
---

## Introduction

> All great thoughts and actions begin with an insignificant start.

Disclaimer: The language of this article was polished by AI.

Vibecoding is a new programming paradigm first proposed half-jokingly by AI researcher Andrej Karpathy in early 2025 and quickly adopted by developers worldwide. The term may also be one of the hottest words in the tech world in 2025, and was even selected as Collins Dictionary’s Word of the Year. The core of Vibecoding is one sentence: “Describe your requirements in natural language, AI writes the code for you, and you can even forget that code exists.”

My club website—a full-stack project built from scratch—was created this way. Simply put, Vibecoding is **driving software development through conversation with AI**—you describe requirements, AI generates code, you review and apply it. This sounds like something out of science fiction, but it has already happened, and it is changing how countless developers learn and work.

But Vibecoding is by no means as simple as “letting AI write code for you.” Over this long development process, I gradually came to understand that truly efficient Vibecoding requires a whole collaboration methodology—how to describe requirements to AI, how to manage AI’s context, how to distill experience into reusable rules, and how to achieve real technical growth with AI’s help. These are the core essentials of Vibecoding.

This article is a systematic summary of my hands-on Vibecoding experience as an independent developer who grew from zero foundation. It is both a development record of a project, a review of a cognitive upgrade, and a sharing of a Vibecoding methodology.

Before officially beginning, it is necessary to first outline several core concepts for readers unfamiliar with the AI field. These terms will run through the entire article, and understanding them is the prerequisite for deeply understanding Vibecoding.

**Token**: The smallest unit through which AI understands the world. AI does not read character by character; it breaks text into tokens for understanding. Your input is encoded into tokens, and AI’s output is also tokens. Token is both the measure of AI capability and the meter of cost—APIs charge by the number of Tokens.

**Context**: An information set composed of massive tokens, and the only basis for AI reasoning. You can understand context as everything AI can “see” in a conversation. When the context window is full, AI “forgets” the earliest information—this is why AI “loses memory” in long conversations.

**Prompt**: The instruction you give AI. An excellent Prompt is not simply a sentence, but a structured document containing role setting, task description, and output format. It is the only bridge between you and AI.

**Tool**: Gives AI the ability to interact with the outside world. In Vibecoding, common Tools include reading and writing files, executing terminal commands, searching codebases, etc. With Tools, AI is no longer just an advisor “talking strategy on paper,” but an executor capable of directly operating the project.

**Agent**: When AI simultaneously has complex Prompts, sufficient Context, and diverse Tools, it evolves from a passive “question-answering machine” into an Agent capable of autonomous planning, execution, and verification. It can decide on its own when to read files, when to modify code, and when to execute commands. For example, Codex and Claude Code are well-known professional programming Agents on the market.

**MCP (Model Context Protocol)**: A standardized tool interface protocol. It allows any tool conforming to the protocol to be plug-and-play for AI, greatly expanding the boundary of an Agent’s capabilities.

**Skill**: This is the highest form in Vibecoding practice. A Skill packages a set of complex Prompts, specific Context (reference files, knowledge bases), and possibly Tools (scripts) into a reusable “professional solution.” With Skills, every time a new conversation begins, the Agent instantly transforms from a “new apprentice” into a “master with ten years of experience.”

Among these concepts, Tool, MCP, and Skill are specifically used together with Agent, aiming to make Vibecoding—from the initial process of “AI web page generates code, developer manually copies and pastes into IDE”—more automated and standardized. This is also an important factor driving the arrival of Agents.

The relationship between these concepts can be summarized in one sentence: **You issue a Prompt to the Agent; the Agent consults Skills in Context and calls various MCP-compliant Tools to complete the work; all this workload is measured and billed in Tokens.**

With these basic concepts understood, we can officially enter the practical world of Vibecoding.


## One Idea, Starting from Nothing

A few months ago, I received a difficult task: the club needed a platform for external publicity and internal communication.

The requirements were clear: internal members needed permission management, the three departments (Art Department, Mechanical Department, Software Department) needed their own activity spaces, there needed to be a forum for technical discussions, and a cloud drive for sharing materials and files. Externally, there needed to be a public homepage to showcase the club and publish activity notices.

But reality was harsh. I had just finished learning the basics of HTML, CSS, and JavaScript, had roughly studied Vue.js, and could only write simple responsive pages, while knowing almost nothing about backend development, database design, or server deployment.

This is the first core principle of Vibecoding: **requirements-driven, not technology-driven**.

A true Vibecoder does not solve problems because they have already learned the technology; they learn technology because they need to solve problems. The real need of the club website became the baton for all my subsequent technical learning. What I needed was not “learn Node.js well,” but “implement user login”—and then I discovered JWT; I needed to “upload files and store them by category”—and then I discovered Multer and sharp; I needed “administrators to be able to ban users”—and then I discovered I needed to design a bans table.

The learning of every technical point was forced by real requirements. The efficiency of this learning method is astonishing—this is exactly how it works in Vibecoding. Everything you learn can be used immediately, and you can understand in practice why it was designed that way. This is a common consensus in the IT industry: for programming, the learning effect of writing code hands-on is far greater than poring over books.


## Technology Selection and “Let the Frontend Run First”

Facing a pile of completely unfamiliar domains, what is most needed is rapid decision-making ability. Technology selection is the first threshold.

After much comparison and AI advice, I ultimately chose the full-stack JavaScript route of **Vue 3 + Node.js + MySQL**. The logic behind this choice was very pragmatic: I had already mastered Vue.js on the frontend, and using the same JavaScript language on the backend could minimize the learning curve. ES6 module syntax (import/export) is unified between frontend and backend, so I did not need to learn two language systems at once.

But the more critical decision was the development strategy of **“let the frontend run first.”**

At that time, the backend was still a blank slate—the Express framework was not set up, the database was not created, and not a single API endpoint had been written. But frontend development did not stop for a single day. Why? Because I used Mock data. In the Axios wrapper layer, I set a switch: when the backend API was unavailable, the frontend automatically used local Mock data. This meant that without any backend support, I could independently complete the development and debugging of all frontend pages—login page, forum list, cloud drive interface, etc.—through AI.

This strategy later proved to be one of the most efficient decisions in the entire project. It allowed me to accumulate a great deal of Vue 3 practical experience during the frontend development stage—Composition API, Pinia state management, Vue Router navigation guards—and these still played a role during backend development, because I had already built an intuitive understanding of data flow.

This is the second core principle of Vibecoding: **first make things run, then talk about optimization.**

The first iron rule of Vibecoding: first make the code run; optimization comes later. In the project, this principle ran through everything: the cloud drive file list was initially loaded in full, with hundreds of files requested at once, and only later was it refactored into backend pagination; CSS styles initially hard-coded many color values, and only later were they refactored into global design tokens; forum post sorting was initially done on the frontend, and only after pagination was it moved to backend SQL.

Do not pursue one-step perfection. First build a minimal version that runs, then iterate and optimize it through real use. This not only validates ideas quickly, but also accumulates more accurate requirement awareness through feedback.


## From the Frontend Comfort Zone to the Backend “Panic Zone”

After frontend development was completed, the real challenge had only just begun.

I still remember the anxiety at the time: “I now have no backend development foundation and no database foundation. I still have no clue how the website connects to the server.”

This is a typical state for many frontend beginners transitioning to full stack—you can write beautiful pages, but you do not know where data comes from, how it is stored, or how it is validated. The gap in between is not a single knowledge point, but a complete shift in mindset.

With the help of AI and online materials, I started from the Express framework and conquered concept after concept. JWT authentication, bcrypt password encryption, Multer file upload, CORS cross-origin handling, middleware design patterns… Each concept was not learned in isolation, but introduced within a real feature requirement.

Take JWT: I did not first learn JWT theory and then look for an application scenario. Instead, I first needed to implement the feature “keep the user logged in after login,” then discovered I needed JWT, and only then learned the generation and verification mechanism of JWT. This **problem-driven learning approach** makes abstract concepts concrete and perceptible.

For Vibecoding, in most cases the requirement for proficiency in the tech stack itself is not high. It is not like algorithm competitions, where you need to master syntax rules and underlying principles thoroughly and apply them skillfully in different scenarios. The minimum requirement for Vibecoding has shifted from “being able to write” to “being able to understand.” This is also one of the most controversial points. But for common application-layer development, this is indeed the case.

Here I want to share a prompt I designed when learning Node.js. It reflects my methodology for collaborative learning with AI:

> "Please play the role of a full-stack expert with 20 years of experience, as a master, and explain the technical details of backend Node.js development to me in detail and in plain language, from beginner level to gradual mastery. Your single reply should be as short as possible, explaining only one or two knowledge points, so that I can immediately ask follow-up questions."

The brilliance of this prompt is that, through “playing an expert” and “limiting the length of a single reply,” it transforms AI from an “information repository” that might dump an encyclopedia at any time into a “private tutor” who knows how to guide step by step and teach according to aptitude. This “step-by-step learning” perfectly solves beginners’ fear when facing a massive knowledge system. However, this learning method varies from person to person, and different Prompts need to be designed according to specific needs.

As learning deepened, I gradually discovered that **in the code AI wrote, syntax appeared that I had never seen before**—`async/await`, arrow functions, destructuring assignment, template literals. These advanced ES6 features looked like hieroglyphs to me at the time. But it was precisely this “not understanding” that drove me to actively study the ES6 specification and understand the essence of asynchronous programming. I realized a key principle: **AI’s output must be fully understood by the developer. Code you do not understand must never be used directly. This is a safety bottom line and also an opportunity to learn.**

This is the third core principle of Vibecoding: **humans are decision-makers, AI is the executor.**

Vibecoding is not “AI writes code for you,” but “you tell AI what to write, and AI writes it for you.” Throughout backend development, AI helped me write a lot of code—controllers, service layers, middleware—but every key decision was made by me: How many levels should forum comment nesting be limited to? Where is the boundary of administrator permissions? Should cloud drive file deletion be physical deletion or soft deletion? AI cannot answer these questions for me, because they have no standard answers; they can only be judged based on an understanding of the club’s actual needs.

AI is my hand, but the brain must be my own.


## My Vibecoding Workflow: A Five-Step Closed Loop

After long-term practical exploration, my Vibecoding workflow can be roughly summarized into five steps. It was not learned from some online tutorial, but naturally precipitated through countless cycles of “falling into a pit → reflecting → optimizing.” Now I present it completely, hoping to inspire developers also on the Vibecoding path.

### Step One: Requirement Breakdown—Turning “What I Want” into “What to Do”

This is the most easily overlooked yet most critical step in the entire process.

When I say “I want to add a pinning feature to the forum,” AI can immediately write a piece of code. But does this code really meet my needs? Is pinning global or specific to a board? Do pinned posts need a visual marker? Who has permission to pin—administrators or moderators? What is the pin duration?

AI will not proactively ask these questions—it will only give you a “standard answer” based on the most common design. If you do not break down requirements and directly merge AI’s code, you will definitely find various mismatches with expectations later, then revise repeatedly, with extremely low efficiency.

So before each development session, I first break down requirements in my notes into several elements: **who the target users are, what the core operation is, what boundary conditions exist, and where the interaction points with the existing system are.** This breakdown process itself is a deep sorting-out of business logic. It lets me, before conversing with AI, already have a clear understanding of what to do.

### Step Two: Prompt Design—Translating “What to Do” into Instructions AI Can Understand

After requirement breakdown is complete, the next step is designing the Prompt. This is not simply writing “help me implement XXX,” but needs to include several key elements:

- **Role setting**: Tell AI who it is now—for example, “You are a full-stack development expert maintaining a Vue 3 + Express club website project.”
- **Task description**: Precisely explain what feature is to be completed, what the inputs and outputs are.
- **Constraints**: Tech stack limitations (Composition API, ES6 modules), code conventions (CSS variables, parameterized queries), file paths, comments that need to be preserved, etc.
- **Context materials**: Reference Skills files or specific code file paths so AI has something to consult.

A good Prompt is like a concise technical specification. It lets AI know where the boundaries are and reduces the risk brought by “free improvisation.”

### Step Three: AI Generation and Human Review—Let AI Run, but Keep Your Hands on the Wheel

After AI generates code, I do not directly run it to see the result. I do three things:

**Read it through**: Understand AI’s logic and ensure there are no obvious errors. This depends on the “syntax-level judgment” mentioned earlier.

**Check boundary conditions**: This is where AI most easily makes mistakes. What if the input is empty? What if permissions are insufficient? What if the network is abnormal? AI often omits these scenarios when generating.

**Verify compatibility with existing code**: Is the API path correct? Do field names match the database? Does the Pinia store method already exist? AI cannot automatically perceive these, so you must check them.

In this step, I intentionally raise AI’s awareness of self-review. For more critical parts, I specify a question checklist based on the specific feature being implemented, such as the previously mentioned: “Is the API path correct? Do field names match the database?” and other questions, letting AI conduct detailed review aimed at high-risk areas, reducing the cost of later bug fixing and troubleshooting.

I also have another trick, which can be summarized as “the player is blind, the spectator sees clearly.” For code review, sometimes letting AI inspect code it just wrote may cause it to overlook potential issues. At such times, I may choose to open a new conversation, paste the code into a conversation without Context, and imply in the Prompt that “this code has potential vulnerabilities,” making AI examine the problem more carefully, then copy the inspection report back for efficient repair. Of course, this method feels somewhat “mystical” intuitively, but it does have some effect; you can decide for yourself whether to use it.

### Step Four: Debugging Feedback—Turn AI’s Mistakes into Its Learning Materials

When I find a problem with AI-generated code, I do not quietly fix it myself. I feed the error message, stack trace, comparison between expected behavior and actual behavior back to AI completely, and then let it correct itself.

This not only fixes the current bug, but more importantly **lets AI accumulate knowledge about this project in the same conversation context**. Next time a similar problem occurs, it will not make the same mistake again. This “debugging as teaching” approach is the key to Vibecoding efficiency.

### Step Five: Experience Precipitation—Turn One-Off Experience into Reusable Rules

When a problem appears repeatedly, or a design decision is worth recording, I write it into the Skills system.

For example, AI once repeatedly deleted my comments when modifying code. I wrote “preserve existing comments” into the “pitfall iron rules” of SKILL.md. From then on, every new conversation AI knew this rule, and similar problems never appeared again.

This step is the most easily overlooked link in the Vibecoding workflow, but it is precisely what determines whether your collaboration efficiency grows “linearly” or “exponentially.” Spending five extra minutes recording after each pitfall saves countless fifty-minute repeated debugging sessions in the future.

### Complete Diagram of the Five-Step Closed Loop

Connecting the five steps above, you will see a clear closed loop:

```
Requirement Breakdown (Human) → Prompt Design (Human) → AI Generates Code (Machine) → Human Review and Debugging (Human) → Experience Precipitation (Human→Skill)
     ↑                                                                                    ↓
     └────────────────────────── Next task automatically loads Skill, efficiency improves ────────────────────────────┘
```

The core idea of this closed loop is: **human energy is always invested in the most creative links—requirement understanding, solution decisions, quality control—while AI is responsible for accelerating repetitive, mechanical execution work**. The two each perform their roles, forming a positive cycle.

This is also why I believe Vibecoding will not make developers lazy—on the contrary, it forces you to maintain clear judgment in every interaction with AI, because you are fully responsible for the final result. AI will not bear any responsibility for you; all it can do is make your hands faster and give your brain more time to think about truly important questions.


## The Twists and Turns of the Database: From “It Runs, That’s Enough” to “Boundary Condition Awareness”

If you ask me what gave me the biggest headache in full-stack development, I would answer without hesitation: databases.

At the beginning of the project, choosing MySQL was a reasonable long-term decision. But when deploying in the school computer lab, I suffered a harsh reality check: the lab computers did not have the VC++ runtime installed, so the MySQL service could not start; and after the computers restarted, the system would be restored, so even if it was installed, it could not persist.

This constraint forced out a “temporary solution”—switching to SQLite. SQLite is an embedded file-based database that requires no installation or configuration, stores data as a single file, and only needs file read/write permissions to run. It perfectly solved the urgent need that “the lab demo must run.”

But SQLite has its ceiling: weak concurrent write capability (file-level locking), no support for MySQL-style user-level permission management, and differences in data types from MySQL. Considering the long-term development of the club website, after the demo I switched the database back to MySQL.

This “MySQL → SQLite → MySQL” switching process looked like a detour, but was actually a valuable learning experience. It made me deeply understand that **there is no absolutely correct technology choice, only the “most suitable” one relative to constraints**. When making technical decisions, you must clarify what the current constraints are and what costs are acceptable. This is engineering judgment that cannot be learned from any textbook.

Database switching was only the beginning of the challenge. What truly left a deep mark on me was the Chinese filename garbling problem.

After users uploaded files with Chinese names, the frontend displayed garbled text. Investigation revealed that the problem lay in the Windows operating system environment: the filename received by the Multer middleware was transmitted in GBK encoding, while Node.js processes strings in UTF-8 by default. The inconsistency caused character parsing errors. I wrote a dedicated transcoding module that treated the string as latin1 encoding to restore the original byte sequence, then redecoded it as UTF-8. At that moment, I finally understood why textbooks say, “The only lesson humanity has learned from history is that humanity learns no lessons.” Even in 2026, we are still fighting to the death with encoding problems. Without experiencing the torture of GBK vs UTF-8 once, you never know your true level.

This problem made me complete a review from **operating system layer → network transmission layer → application layer → database layer**. AI could help me locate the problem (“use iconv-lite for transcoding”), but truly understanding why transcoding is needed—how encoding is passed and converted across layers—that process was the key to technical growth.

There is another design that left a deep impression on me: the choice of foreign key constraints. When deleting a user, posts and files need different handling strategies. For the `posts` table, I set `ON DELETE CASCADE`, because posts are personal expressions of the user, and without the author there is no meaning in keeping them; for the `files` table, I set `ON DELETE SET NULL`, because files in the public cloud drive belong to departmental resources and should not disappear just because one person leaves.

This was not taught by AI, nor written in textbooks. It was a judgment made based on an understanding of the club’s actual business. **AI can help you write SQL, but it will not make business decisions for you.**

These database-level twists and turns ultimately condensed into the fourth core principle of Vibecoding: **true growth is not in the code, but in cognition**.

Every bug is a lesson, and every data migration is a training session in systems thinking. From “it works, that’s enough” to “boundary condition awareness,” from “feature implementation” to “data flow design”—these cognitive leaps are the most valuable gains in the Vibecoding process. The code was written by AI, but the growth is my own.


## Requirement Breakdown and Prompt Design

In my five-step workflow, the first two steps are “Requirement Breakdown” and “Prompt Design.” They connect end to end in a complete chain—the result of requirement breakdown directly transforms into the skeleton of the Prompt. Whether these two steps are done well often determines the quality of the final delivery more than subsequent code review. So I am expanding them separately in more detail.

### Requirement Breakdown: The Questions AI Will Not Ask for You, You Must Ask Yourself

One of the most common Vibecoding misconceptions is: throwing the vague thought in your head directly at AI and expecting it to produce a complete solution.

“I want a user ban feature.”

Fine, AI may immediately generate a set of code for you. But it will not proactively ask you:
- Who is being banned? Is it banning login, banning posting, or banning access to the cloud drive?
- Is the ban temporary? Is it permanent, or does it automatically lift after 24 hours?
- Who executes the ban? Administrators? Moderators? Can moderators ban people in their own boards, or only administrators?
- What does a banned user see? Does the login page say “Account disabled,” or does posting say “You have been muted”?

These questions are not AI’s fault—without your business context, it does not know how your website operates. But if you do not think through these questions first, the code AI generates is a half-finished product that “looks runnable but leaks everywhere.” Later you will spend several times as long patching it up, and every patch may introduce new bugs.

So before each development session, I first break down requirements in my notes into several elements. These elements come directly from the business itself and do not require any Prompt engineering tricks:

1.  **Who are the target users**: Who will use this feature? Administrators? Moderators? Ordinary users?
2.  **What is the core operation**: What action does the user need to complete? What are the inputs? What are the outputs?
3.  **What are the boundary conditions**: Under what circumstances is the operation rejected? Under what circumstances does the behavior change?
4.  **Where are the interaction points with the existing system**: Which tables need to be changed? Which existing APIs need to be called? Which frontend pages are affected?

Taking the “user ban feature” as an example, it can be broken down like this:

-   **Target users**: Administrators (site-wide bans), moderators (only boards they manage)
-   **Core operation**: Administrator selects user → selects ban type (account / posting / cloud drive) → selects duration → executes. Unbanning works the same way.
-   **Boundary conditions**: A user who is already banned is banned again, update the time; automatically lift after expiration; moderators cannot ban administrators; cannot ban oneself.
-   **Interaction points**: Add a record to the `bans` table; add ban-check middleware in `userController.js`; add a management interface in `adminController.vue`; add ban validation to login and posting APIs.

I did not use any “Prompt template”; I was just answering the most basic question: **What exactly should this feature do?** This helps me write a clear Prompt.

### Prompt Design: Translating Business Language into a “Cyber Contract” AI Can Execute

After requirement breakdown is complete, Prompt design becomes natural. Because the most core information—who, does what, where the boundaries are—is already clear. What you need to do is organize this information in a way AI can precisely understand.

Here I want to convey an important idea: **Prompt writing relies on natural language; there is no need to deliberately learn “Prompt syntax” or “template frameworks.”** You do not need to take a course, memorize formulas, or learn advanced terminology. If you can explain requirements clearly to a colleague, you can write a good Prompt for AI. This ability is naturally polished in real development—write more, and you will know what information AI needs and what words are redundant.

Below is a real Prompt example, from my actual conversation when developing the “user ban feature”:

> You are a full-stack development expert maintaining a Vue 3 + Express + MySQL club website project. Now we need to implement a “user ban feature.” The specific requirements are as follows:
>
> **Feature Overview**:
> Administrators can ban users in the admin panel, supporting three ban types: account ban (prohibit login), posting mute (prohibit posting and commenting), and cloud drive disable (prohibit access to the cloud drive). Bans support setting an expiration time and automatically lift after expiration. Administrators can also manually unban early.
>
> **Technical Constraints**:
> - Frontend: Vue 3 + Composition API (`<script setup>`), styles use project global CSS variables.
> - Backend: Express + ES6 modules, database queries use parameterization to prevent SQL injection.
> - Database: There is already a `bans` table (fields: `id`, `user_id`, `type`, `banned_until`, `created_by`).
> - Ban checking is implemented through middleware and called in pre-validation for posting, commenting, cloud drive access, and other APIs.
>
> **Deliverables**:
> 1. Backend: Ban/unban API endpoints (`POST /admin/ban`, `POST /admin/unban`).
> 2. Backend: Ban-check middleware.
> 3. Frontend: Ban operation interface in the admin panel (added in `adminController.vue`).
> 4. Frontend: Prompts for banned users (on the login page, post button, and cloud drive entrance).
>
> Please first give the database fields that need to be added or modified (if any), then gradually implement the four parts above. Give one part at a time, and wait for my confirmation before continuing.

This Prompt looks long, but when broken down it contains five key elements:

1.  **Role setting** (You are a full-stack development expert…): Let AI know what identity to think with.
2.  **Feature description** (supports three ban types…): Directly transformed from the requirement breakdown notes.
3.  **Technical constraints** (Vue 3 + Composition API…): Write the project’s technical conventions clearly to reduce AI’s free improvisation. This part has already been precipitated in the Skills system, so in actual writing it usually only needs one sentence: “Follow the SKILL.md conventions.”
4.  **Delivery boundary** (backend API + middleware + frontend interface): Clarify what AI needs to produce and the scope of production.
5.  **Interaction rhythm** (give one part at a time, wait for my confirmation before continuing): Control AI’s output granularity to avoid generating too much at once and making review difficult.

This writing style is relatively comprehensive, but since a project generally proceeds within a single conversation context, in actual development the more fundamental **project background, technical constraints, and role setting** are usually already included in the Context, so there is no need to repeat them.

The above writing style is one of my Prompt design styles. It is built on the premise that you have a comprehensive understanding of the project’s technical principles and have conducted deep analysis of the project.

I also have another more “aggressive” writing style:

> Task: Add an entry point for viewing other users’ information to the forum module (post authors and repliers in post lists/details).
> 
> Requirements:
> 1. Change the username area to “avatar + username”; clicking it navigates via route parameters to that user’s userInfo.vue page.
> 2. Department field handling: Map database raw names (such as "soft") to readable Chinese names (such as “Software Department”); internal members (including administrators) all apply this mapping, while external personnel display “External Personnel” and have no background color.
> 3. Preserve the already implemented exclusive color identifiers for administrators and moderators; the forum area uses these colors independently and does not apply the font color logic set for usernames in MainLayout.
> 
> Please first organize the above design plan, assess implementation difficulty and considerations. No need to write code; inform me after confirming.

This writing style does not require describing the specific operation flow to AI in detail. Instead, it lets AI first perform a simple task design based on the project Context and the given Prompt. It places higher demands on the model’s own capabilities and project stability.

### Polish in Practice, Not Recite from Books

When I first started using Vibecoding, I also made the mistake of writing Prompts too casually. “Help me write a login API”—and then AI returned a “three-no product” with no password encryption, no Token expiration mechanism, and no error handling. The problem was not AI; it was that I did not explain clearly.

Later I gradually developed a habit: before writing each Prompt, first run through in my head “what exactly should this feature do, and where are the boundaries.” This habit was not learned from tutorials, but naturally polished through repeated pitfalls—when you get an unwanted implementation for the third time because your Prompt was vague, next time you know what information to add.

So, if you are learning Vibecoding, my advice is: **do not treat Prompt as a skill that requires deliberate learning. It is your language, your logic, your understanding of requirements. Write more, and you will naturally become good at it.** What truly requires deliberate practice is not Prompt writing technique, but the thinking mode of requirement breakdown—how to think clearly enough about “what I want” before writing the Prompt.


## The Skills System: Vibecoding’s Ultimate Weapon

When the project entered the middle and later stages, a new problem appeared.

My codebase had expanded to dozens of files, and because of various debugging and feedback, the web conversations were extremely messy and cluttered. To start a new conversation, I needed to explain the tech stack, naming conventions, and project structure to AI, and also upload core files so AI could understand the context. This was simply a black hole of productivity. Worse, AI would also “forget”—as the conversation grew longer, it could not remember rules set early on and began making various low-level mistakes.

For example: AI would delete my carefully written comments without authorization when modifying code; AI would name variables in snake_case, breaking the unified camelCase convention; AI would hard-code color values when modifying styles, ignoring the CSS design token system I had already established. More seriously, AI might forget that JavaScript should use ES6 conventions and write me a CommonJS version.

These problems made me realize: **the highest level of managing AI is not writing it a longer Prompt every time, but preparing an onboarding manual for it that it will never forget.**

This is the background behind the birth of the Skills system. It is a “cyber constitution” that prevents AI from freely improvising based on feeling.

Following the Claude Code conventions, I created a `skills/` directory in the project root. This directory contains:

- **SKILL.md**: The core skill file. It includes the tech stack, naming conventions, design principles, pitfall records, and most importantly—**Vibecoding operating iron rules**. For example, “preserve existing comments,” “must ask when uncertain,” “multiple modifications in the same file must be integrated,” etc.
- **references/**: Reference documents. Including database table structure quick reference, API endpoint list, UI design specifications, common error repair guide, key technical decision records, project status dashboard, etc.
- **scripts/**: Executable scripts. Including database migration scripts, quick initialization scripts, etc.
- **assets/templates/**: Code templates. Skeleton templates for Vue components, backend Services, and Pinia Stores, ensuring that new files generated by AI have a consistent format.

With the Skills system, every new conversation only needs me to say, “Follow the SKILL.md conventions,” and AI instantly recovers all key memories. It knows the project uses Vue 3 + Composition API, knows CSS must use global variables, knows comment nesting is limited to two levels, and knows administrator usernames are displayed in purple.

This is not just an efficiency improvement, but a qualitative change in collaboration mode. Skills turn AI from a “temp worker in successive conversations” into a “long-term partner who has mastered the project’s full background.”

This is the fifth core principle of Vibecoding, and the one I consider most important: **establish rules for AI instead of repeating yourself every time.**

The essence of Skills is to precipitate the experience gained after each pitfall into persistent conventions. AI forgets, but files do not. This ability to “encode experience into rules” cannot be learned in traditional programming education; it is a new ability derived from the AI era—how to manage an Agent’s behavioral boundaries.

During development, I also discovered several micro-techniques for improving collaboration efficiency:

- **Multiple modifications in the same file must be integrated**: Let AI complete all modifications to a file at once, rather than changing line by line. This can speed up the Agent’s work.
- **Must ask when uncertain**: Clearly stipulate in SKILL.md that AI must proactively ask about any uncertain parameters, field names, or route paths, rather than making assumptions. This rule can minimize bugs caused by AI “acting on its own” and reduce the cost of subsequent repairs.
- **Code files must be annotated with paths**: When creating a new file, write a comment on the first line declaring the file path (such as `// src/api/forum.js`). This method is somewhat redundant in “ancient programming,” but in Vibecoding it helps developers and AI clarify code files and reduces the possibility of errors.


## Make Good Use of Git for Version Control

After discussing Skills, I also want to emphasize another thing that is equally important but completely different in nature—**Git version control.**

If Skills are compared to “an ex ante agreement to prevent AI from making mistakes,” then Git is your “ex post insurance so you are not afraid of AI making mistakes.” One manages “doing it right,” the other manages “fault tolerance”; neither can be missing.

**What is Git?** Simply put, it is a version control system. You can understand it as a “time machine”—every time you actively save (commit), Git takes a snapshot of the current project state. After that, no matter how much you modify the code, even beyond recognition, you can return to any snapshot at any time.

In traditional development, Git is mainly used for multi-person collaboration: you change yours, I change mine, and finally merge. But in the Vibecoding scenario, Git has a more urgent use for me—**it is used to fight against AI’s “unpredictability.”**

I have encountered many situations like this: when AI modifies a feature, it “conveniently” modifies another unrelated piece of code; AI confidently generates a whole set of “optimization plans,” and after merging, the project directly fails to run; more extreme, once an Agent nearly deleted the entire route configuration file while cleaning up redundant code—if I had not discovered and stopped it in time, it would have been a disaster.

My workflow habit is this: before letting AI make relatively large-scale changes, I first commit the current state—even if the code is not perfect, even if the feature is not finished. After that, no matter what AI changes or how much it changes, I am not afraid. Because I know that with one command, everything can return to the origin.

You may think this is very basic, but from my observation, many developers just starting with Vibecoding overlook exactly this. They treat AI as a “reversible operation,” thinking, “Anyway, it can change it back.” But reality is that AI sometimes does not remember what the previous code looked like; its context contains only the current state. Once it overwrites correct code with incorrect code, do you expect it to restore it by itself? It will regenerate it—most likely still wrong, because the context that caused it to make the mistake has not changed at all.

So my advice is very pragmatic: **use Git to replace AI’s “memory,” and use commit to replace AI’s “promises.”** The specific operations do not need to be fancy—`git add .`, `git commit -m "backup before revision"`, then let AI work. If the result is satisfactory, commit a new one; if not, `git reset --hard` back and try another path.

In the development of my club website, Git’s rollback capability saved me from many large-scale reworks. The most typical was a database refactor—AI modified many backend files at once, and when I tested, login was completely broken. After troubleshooting for ten minutes with no clue, I decisively `git reset` back to the version before the migration, then had AI modify step by step, module by module, submitting only after each step passed testing. If I had not had Git that time, just locating the problem might have consumed a long time.

**Vibecoding lowers the threshold for writing code, but it does not lower the speed of making mistakes.** Git is a reliable line of defense when facing this “rapid mistake-making.” It does not require you to be very experienced; it only requires you to develop a good habit: **before AI starts working, press save first.**


## Large Models and Workflows: Vibecoding’s Dual Foundation

If Vibecoding is compared to building a house, then **large models are the concrete of the foundation, and the development process is the way bricks are stacked upward**. Together they determine how high and how fast your building can be built.

### Choosing a Large Model: Intelligence Determines the Ceiling

In Vibecoding practice, one unavoidable fact is: **the code capability of the large model itself directly determines the ceiling of your collaboration with AI**. This is not a gap that Prompt engineering can make up for—just as no matter how good you are at communication, you cannot make an intern write architect-level code.

This view may make some Vibecoding optimists uncomfortable. After all, we often hear people say, “Prompt design is more important than model selection,” or “Use the Skill system well, and any model can produce work.” These statements have their truth—good Prompts and Skills can indeed significantly improve the output quality of any model. But they ignore a basic premise: **the quality of the tool itself determines how much effect your optimization can produce**. A family sedan tuned to perfection cannot beat an untuned race car on a track. The same Prompt given to different models may produce vastly different code quality—this is why many people who try Vibecoding reach completely opposite conclusions: some think “AI is amazing,” others think “AI is an idiot.” Both may be right, **because they are not using models at the same “intelligence” level at all**.

To more intuitively understand the impact of model capability differences on Vibecoding, I have fictionalized three representative models, summarizing based on my hands-on experience with mainstream models on the market. Their capability gradient is roughly as follows:

**Model A (representing the world’s top closed-source models)**: Has an extremely long context memory window and can load the codebase of an entire medium-to-large project at once. In complex system design, it can accurately understand cross-file dependencies, and the code it generates has systematic consideration in security, performance optimization, and boundary condition handling. It can even proactively point out potential problems in your existing architecture without explicit instructions. This level of model is like hiring a professional architect to sit next to you—it can not only write code, but also help you make technical decisions.

**Model B (representing first-tier mainline models)**: Context length is medium-to-upper, capable of covering several core module files in a project. Under clear requirements, code quality is reliable and logic is clear, but cross-module design occasionally shows inconsistency. It is more like a senior developer—solid ability, but needs you to give clear direction, and is not very likely to proactively question your architectural choices. For most daily development tasks, this model is completely sufficient, and its cost-effectiveness is often the highest.

**Model C (representing lightweight models with weaker performance)**: Limited context window, usually only able to handle the content of the current file. It performs well on simple independent features, such as writing a utility function, changing styles, or generating a regular expression. But once multi-file collaboration or complex business logic is involved, it begins to “freestyle”—hallucinations, omitted boundary conditions, and even forgetting constraints you just confirmed a few turns earlier. This model is like an intern: enthusiastic and fast, but you have to watch it, or it may turn a simple problem into a complex accident.

The capability differences among these three models are immediately visible in actual Vibecoding. Taking the “user ban feature” in my club website project as an example: I used Model A to design the entire ban system—it automatically considered ban types (account ban, posting mute, cloud drive disable), valid duration (scheduled lift or permanent), unban mechanism, and interaction with the admin panel. The entire plan from data structure to API endpoints flowed in one go, with almost no major revisions needed. Using Model B for the same task, code quality was reliable but required me to break down requirements more clearly step by step; it was less likely to proactively consider boundary scenarios like “scheduled unban.” When using Model C, I had to describe each small feature point separately; with slightly more complex logic combinations, it began “fabricating” nonexistent APIs or database fields.

So, if you want to seriously use Vibecoding to build a project that can be maintained long-term, **model selection itself is one of the most important technical decisions**. It is not a question of “which model is best”—because different models have their own advantages on different tasks—but rather **whether the “intelligence level” you need matches the complexity of the current task**. Choose the right model, and you get twice the result with half the effort; choose the wrong model, and no matter how much you optimize the Prompt, you are chopping a tree with a dull axe—you can cut it down, but it will exhaust you. Of course, cost is also an indispensable consideration. Generally speaking, the more powerful the large model, the higher the Token price. This needs comprehensive consideration based on actual circumstances.

### The Evolution of Development Workflow: From “Cyber Brick Moving” to “Cyber Colleague”

Large models are the engine, and the development workflow is the gearbox. With the same horsepower, driving on the highway in first gear versus cruising in fifth gear feels completely different.

**Stage One: Copy-paste on the web page**. This is the primitive society form of Vibecoding. The process is simple: open the AI web page → describe requirements → AI generates code → manually copy → switch back to IDE → paste → save → discover a missing import → switch back to the web page → supplement the Prompt → copy and paste again. Some developers jokingly call this mode “**cyber brick moving**”—you are not programming, but acting as a “human data bus” between AI and the IDE. It is not entirely without merit: for one-off tasks, independent scripts, and algorithm problems, this mode has the lowest threshold and fastest onboarding. But once it involves **multi-file, long-cycle, repeatedly iterated real projects**, it becomes a black hole of productivity. More fatally, web-based AI knows nothing about your project structure, and every new conversation requires re-uploading core files as “memory anchors,” and this “anchor” must be manually maintained by you.

**Stage Two: Fully automatic Agent**. The next stage of Vibecoding is Agent mode. The core difference between an Agent and web-based AI is: **it is no longer a passive “autocomplete plugin,” but an independent developer with environmental awareness, autonomous planning, tool calling, and self-correction capabilities**. It can traverse directories, locate files, execute tests, and fix errors by itself. You no longer need to manually move code; you only need to describe requirements in natural language, and it can complete the entire process from code generation to file writing. The improvement in development efficiency is by orders of magnitude.

If we give the Agent a “persona,” it is like “a senior colleague sitting inside your computer doing work for you”—you assign the task, it works on its own, and you do not need to watch every step. But Agent mode also has thresholds: **you need to understand what it is doing, you need to be able to review its output, and you need to correct it in time when it “goes off track.”** An Agent does not mean you can let go completely; it means you shift your energy from “how to move bricks” to “where to build the building.” Looking back at my club website project, I experienced the complete evolution from web page to Agent—in the early stage of the project I used the web page, and with few files it was manageable; after the codebase expanded, efficiency collapsed, and I decisively switched to Agent mode. In hindsight, this was one of the most critical efficiency turning points in the entire development process.


## A Record of Troubleshooting a “Paranormal Event”

I once encountered an extremely eerie problem: during the testing phase after I added the username-change feature, I changed my username successfully, logged out, then entered the new username and the original password and clicked login. The moment the login button was pressed, the page quickly reverted to the logged-out state. The whole process was as fast as an illusion.

Strangely, accounts that had never changed their usernames were completely normal.

I continuously switched between the web page and terminal to ask two different AIs, and the diagnoses I got were all over the place: Token expired? Route guard misjudgment? Pinia state pollution? CORS? Each AI “thought deeply” for five minutes and swore it had found the root cause. I tried their solutions one by one—none worked.

In the end, I had to resort to the most primitive method: open the browser F12, insert one `console.log` after another, print out every step of state change, and feed it to AI for analysis. After dozens of rounds, the truth finally came out—the problem lay in the JWT payload encoding. JWT uses Base64URL encoding (including `-` and `_`, without padding `=`), but the browser’s native `atob()` function only recognizes standard Base64. After modifying the username, certain character sequences happened to appear in the new Token, causing `atob()` decoding to fail and triggering the forced logout logic in `catch`. Next, I will tell you in the most blunt, most realistic, least roundabout, most hardcore, most refreshing, least drawn-out, most heart-piercing, most unsparing, most direct language: **The key was changed, but the lock was not.**

From discovering the problem to solving it, the whole process took nearly an hour. And this was just a small feature—username modification.

This experience taught me a profound lesson: **do not harbor too many illusions about AI programming.** It can help you write beautiful code frameworks and efficiently complete tasks under clear guidance, but when facing bugs with coherent logic, bizarre behavior, and hidden root causes, AI often falls into a state of **"Talking nonsense in a serious manner"**—the solutions it gives all look right, but none solve your problem.

This touches on an easily overlooked boundary of Vibecoding: **human subjective initiative.** You think you are using an omnipotent programming assistant, but in fact you need a self that understands technology and can troubleshoot. Of course, for debugging and troubleshooting tasks, you can also do it by connecting to MCP. Some professional development MCPs provide interfaces for obtaining browser console information, and perhaps can also query debugging information.


## Vibecoding’s Applicable Boundaries and Risks

After the club website project ran smoothly, I began to seriously think about a question that had previously been covered up by excitement: **What exactly is Vibecoding suitable for? What is it not suitable for?**

**Suitable scenarios, personally tested and effective:**

First, **small products and simple features from zero to one**. These have clear requirements but limited resources, no one looks at your architecture, and it works if it runs. Vibecoding is extremely efficient in this “from nothing to something” stage, because AI excels at “generation.”

Second, **full-stack JavaScript projects with a unified tech stack**. When choosing the stack, I accidentally chose the most AI-friendly route—frontend and backend in the same language. This means AI does not need to switch context between syntaxes of different languages, and generation consistency is noticeably higher. If it were Python backend + React frontend, AI’s error frequency would probably double.

Third, **personal or small-team non-critical business systems**. If the club website goes down, people will at most complain a little; if cloud drive files are lost, they can be uploaded again. This kind of “high fault tolerance” scenario is Vibecoding’s comfort zone. You allow it to make mistakes because the cost is controllable.

**Unsuitable scenarios, which I have not personally stepped into, but can judge by common sense:**

First, **projects with complex core business logic and extremely low fault tolerance** (such as financial trading, medical data, autonomous driving control). This is not a question of AI code quality, but a question of **responsibility attribution**—when AI-generated code has a bug under a boundary condition and causes real financial loss, who bears it? I do not think a “developer” can confidently say, “AI wrote it, I did not know.” A court will not accept that defense. In such environments, code written by AI at the very least needs strict human review.

Second, **projects requiring extreme performance optimization**. AI-generated code is becoming increasingly reliable in “correctness,” but remains mediocre in “efficiency.” It can write a sorting function, but is less likely to consider CPU cache hit rate; it can write a SQL query, but is less likely to ponder index pushdown. These details are currently beyond AI, and by the time you learn to teach it optimization step by step, you might as well write it yourself.

Third, **large projects with long maintenance cycles**. I have deeply felt this. The club website has only been built for a few months, but the AI-generated parts of the codebase have already begun to show problems: variable naming is not semantic enough, functions are bloated, and necessary abstraction layers are missing. In the short term, efficiency is extremely high; in the long term, the interest on technical debt slowly accumulates. If your project is going to run for more than two years, it is best to establish strict human code review and refactoring rhythm early, rather than relying on AI to continuously output.

**Several risks worth expanding on:**

**Risk One: The hidden nature of security vulnerabilities.** AI will not proactively remind you that “this API has no rate limiting,” “this file upload does not validate MIME type,” or “this password reset logic has a user enumeration risk.” It can write functionally complete code, but its security awareness is not high. During development, if I had not seen related discussions while looking up materials one time, the club website login API might still have no anti-brute-force measures at all.

**Risk Two: AI’s “overconfident” output.** When your code does not run and you give AI the error message, it will quickly give you a “fix.” But the JWT Base64URL troubleshooting experience mentioned earlier made me understand—there is no positive correlation between the speed at which AI gives solutions and their reliability. It can give five seemingly reasonable diagnoses within five minutes, but the real problem may be in the sixth direction. AI rarely proactively says “I am not sure,” and this confidence is extremely likely to mislead beginners.

**Risk Three: Weakening of judgment.** This is what I worry about most. When you get used to “saying one sentence and AI completes 80% for you,” you will imperceptibly let that 20% of judgment atrophy too. Just as people who are used to calculators have weaker mental arithmetic—this is not an intelligence problem, but a transfer of muscle memory. In the later stage of the project, I discovered a dangerous tendency in myself: after encountering a bug, my first reaction was no longer “let me look at the code logic,” but “let me paste the error to AI.” Once this habit solidifies, my debugging ability will degenerate.

**So, how do you judge whether a project is suitable for Vibecoding?**

1. **Is the cost of failure controllable?** If this system crashes, is the loss time or money? Is it embarrassment or legal liability? The cost of trial and error depends on you personally.
2. **How long is the maintenance cycle?** If the project has a short lifecycle (such as a temporary event website or competition Demo), Vibecoding is extremely cost-effective. If the project needs to iterate continuously for several years, you must invest extra manpower in architecture design and code review.
3. **Are you personally capable of completing the project independently?** This is a counterintuitive standard—**only when you are capable of writing this project without AI are you suitable for using AI to write it.** Otherwise, you are walking a tightrope. The reason my club website project ultimately did not spiral out of control is that during development I gradually filled in the entire cognitive chain from frontend to backend. If I had never understood what AI was writing from beginning to end, the project would have collapsed sooner or later.


## From “Using AI” to “Collaborating with AI”: Vibecoding’s Cognitive Leap

Looking back at the entire development journey, I found that the most profound transformation was not technical, but my cognition of “programming” itself.

In traditional programming education, we start from “Hello World,” learn syntax, algorithms, and design patterns, and only then can we do projects. This is a linear process of “learn first, then use.”

But in Vibecoding mode, this process is completely reversed. I “use first, then learn”—first generate runnable code through AI, then learn technical details through debugging and understanding. This learning method may be harmful to beginners (it is easy to skip fundamentals), but for people with a solid programming foundation and clear project goals, the efficiency is astonishing.

However, there is a key point that is easily overlooked: **“use first, then learn” is not “learn only once,” but a spiraling cognitive cycle**. When you first use AI to get a feature running, you are forced to understand its logic during debugging; when you encounter a similar requirement next time, you can already judge from the principle level whether AI’s solution is reasonable. This cycle of “practice → cognition → practice again” embeds learning into the deepest part of real combat, maximizing the efficiency of knowledge transformation. It is not a shortcut that skips fundamentals, but rather lets fundamentals be mastered at the moment they are most needed—this is precisely what the traditional “learn first, then use” model struggles to achieve.

But there is a boundary that must be made clear: **Vibecoding’s efficiency improvement is built on the premise that the developer already possesses “judgment.”** This judgment contains at least two levels.

The first level is **syntax-level judgment**—being able to read code and knowing the basic concepts of variables, functions, loops, and asynchrony. Without this level, you cannot even judge whether AI-generated code is correct. This is the minimum threshold, and a threshold anyone must cross on their own before touching Vibecoding. In the project, I encountered countless times when AI-generated code seemed runnable but actually hid logic holes—if I had not mastered basic JavaScript syntax in advance, these holes would have been buried like landmines at the bottom of the entire project, only to explode suddenly late one night.

The second level is **system-level judgment**—understanding how data flows between frontend and backend, the basic principles of HTTP, and how database CRUD operations work. This level determines whether you can only “modify code” or can “design systems.” In the development of the club website, when AI suggested executing multiple database queries simultaneously in one API, the reason I could judge whether the solution was reasonable was that I understood the working principles of database connection pools and the performance characteristics of concurrent requests. This is not something AI can judge for you—it depends entirely on the depth of your cognition of how systems operate.

For this reason, I remain vigilant against the rhetoric that casually advocates “zero foundation can also do full-stack development.” **Vibecoding is indeed a trend of the times, but you must not blindly follow it and directly start AI programming without any technical foundation.** Admittedly, for some small features and small components, the threshold is indeed extremely low—it has basically become a universal skill. Because code written this way does not need to consider subsequent maintenance or project stability; it only needs to “run.” But what truly differentiates developers is precisely the pursuit of complex requirements, high durability, and stable, mature projects.

Someone on social media bragged: “I did not write a single line of code, but I commanded an AI army.” However, the fact is that this “developer” knew nothing about the technical details of the open-source project and was completely an outsider. He handed over project development entirely to AI, ultimately causing AI to submit a large number of invalid contributions to the open-source community beyond his control. Even if some PRs were successfully merged, the gains did not outweigh the losses. To become a developer, you must first be responsible for the project. If you know nothing about what AI is doing and what features it is writing, it is somewhat ridiculous—even dangerous.

This case reveals a deeper pattern. The more AI is used, the greater the code output, but if the developer’s judgment does not grow in sync, technical debt will also accumulate exponentially. This is not a problem of Vibecoding, but a paradox existing in any automation tool—the more powerful the tool, the higher the user’s ability to control it must be, because the cost of error is amplified. It is like giving a person who just got a driver’s license an F1 race car: speed increases, but the probability of hitting the wall skyrockets.

More importantly, Vibecoding taught me how to collaborate with another intelligent entity. This is not simply “issue command → receive result,” but a cooperative relationship requiring continuous optimization of communication protocols. The essence of the Skills system is a carefully designed “human-AI collaboration protocol”—it defines the boundaries, conventions, and expectations of both sides, turning collaboration from a random, temporary state into a reusable, iterable stable mode. During project development, I also increasingly realized that you and AI are not boss and subordinate, but collaborators on the same team. As a designer, you can share your code debugging experience with AI, and you can also brainstorm with AI to gain more project design inspiration.

I gradually understood a deeper truth: **truly efficient Vibecoding is not about making AI infinitely powerful, but about making humans infinitely clear.** When you must describe requirements precisely to AI, you are forced to think more deeply about business logic. When AI makes mistakes, you are forced to analyze root causes. This process inversely shapes your technical thinking—you are no longer just a code writer, but a system designer, a rule maker, a quality gatekeeper.

This is also why I am not worried that AI will make programmers unemployed. Not out of optimism, but based on the essence of software engineering. **As long as the core challenge of software engineering remains “transforming vague human requirements into precise machine instructions,” humans are needed to bear responsibility.** AI can optimize any step in this process—write faster, check more comprehensively, modify more accurately—but it cannot replace the key step: the power of decision. Because the power of decision means responsibility, and responsibility can only be borne by humans. AI can help you write functions, but cannot judge how users will actually feedback in a production environment; AI can help you change styles, but does not know whether this color fits the club’s culture and aesthetics; AI can generate ten different technical solutions, but cannot decide for you which one best fits the current constraints and long-term goals.

This is the core principle of collaborating with AI in Vibecoding: **humans are responsible for decisions, AI improves efficiency in execution.** AI is your hand, but the brain must be your own. If you do not even know what you are doing, then no matter how powerful AI is, it is just an engine accelerating your mistakes.


## Epilogue: What Vibecoding Taught Me

Today, this club website project is already quite mature. In daily development, I serve as architect and tester. I discover requirements during website testing, translate requirements into natural language, describe detailed feature designs in natural language to the Agent for programming, then I immediately test, give the Agent instant feedback on problems and fix them. This workflow greatly improves my development efficiency.

But for me, the value of this project goes far beyond that.

It transformed me from a novice who could only program into a developer capable of independently designing, developing, and deploying a complete web application. It made me understand in practice the technical principles of frontend-backend connection. It taught me how to manage my energy, how to collaborate efficiently with AI, and how to precipitate the experience of every pitfall into reusable rules.

More importantly, it showed me the infinite possibilities of human-AI collaboration.

Vibecoding is reshaping the way software is developed, but it is not magic, nor is it omnipotent. It is a methodology that can be learned, optimized, and shared. The original intention of writing this article is to hope that more beginners like me can take fewer detours and find the correct posture for collaborating with AI more quickly.

If this article allows you to remember only one sentence, it is: **proceed from reality in everything, and adapt to circumstances.**

— A novice developer’s humble opinion_20260729.md.