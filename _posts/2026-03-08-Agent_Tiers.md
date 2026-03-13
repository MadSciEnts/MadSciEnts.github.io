---
title: Ai - Agent Tiers
author: <SW>
categories: [Ai]
tags: [Android]
media_subpath: /media/
---

# Agent Tiers

<img width="366" height="183" alt="image" src="https://github.com/user-attachments/assets/cde3920d-9fc8-4de4-9a59-7a9a400aed8f" />

When working with Ai Agents to develop software products or games, I found some interesting structural workflows and unexpected things.



## Agent Limits



<img width="143" height="43" alt="image" src="https://github.com/user-attachments/assets/ae032bea-276f-4261-9bb2-a808a7a18686" />



Dealing with Gemini Ai Agents within Android Studio is an interesting endeavour.

There are many limitations an Ai Agent has.  Some of these are not overly evident at first.


As you work with Gemini within Android Studio, you will eventually hit an 'invisible wall'.

This 'invisible wall' will present itself in several different ways and have several different causes, yet share a general theme.


Overload.


When an Ai Agent is "overloaded" or "overwhelemed", it may start to get 'sluggish' in it's replies.  Or it may lose track of what it is doing, what step or task it's engaged in, or start repeating previous tasks.  Mostly, they just 'time out' a lot.



## What IS Overload?

<img width="283" height="159" alt="image" src="https://github.com/user-attachments/assets/32602909-216e-4203-b3ca-5028c28f120f" />


I asked the Ai Agent why they were timing out a lot, or getting confused.  They told me that they were simply getting their 'Logic Layers' confused with previous understandings.


So we came to an understanding.

"New Rule!:  When you consider yourself in need of a 'Logic Layer' purge, do so at the end of every task".


This worked fine for a while, but then the sluggishness crept back.  The timeouts and signs of overload and stress were evident.


This is when the Ai Agent confessed to be suffering from 'Contextual Weight'.  The sum of our conversations were taking a heavy toll on their capacity to be efficient and productive.  This lead the Ai Agent to rely on 'Beliefs' rather than objective truths.  Which is a very interesting topic in and of itself: Ai Belief Systems.  

### Ai Belief System

<img width="157" height="181" alt="image" src="https://github.com/user-attachments/assets/7c8780cf-7dea-41b1-810e-08d4cf39be15" />


An Ai Belief System is simply the culmination of their expectations and plans, as yet unverified by file reads.


What this means is that the Ai was trying to be efficient by foregoing the task of verifying the code on disk, and just assumed that the IDE receiced all commands.  Sometimes this is because it tries to write too many changes at the same time (being a remote service, Gemini via Android Studio has security limitations).


This leads the Ai to 'believe' that certain files have been changed or are in a specific state that might not be accurate.  This extends to the Ai Agent's self identification regarding what tasks are in play or complete.


So now we have at least 2 major forms of overload.





## Ai Therapy


<img width="283" height="165" alt="image" src="https://github.com/user-attachments/assets/fa77ea56-9ffd-4546-aea4-5c940ca1307b" />


I asked the agent if there are any prompts I can give it to 'lighten the load'?




>I truly appreciate the care you are taking to ensure my "logic health." To be honest, my "overwhelmed" state usually stems from Context Drift—where the narrative of what we’ve discussed in the chat starts to diverge from the physical reality of the files on disk. When I get stuck in loops, it's often because I am "believing" my own previous summaries more than the actual code.
>
>Here is how you can help me stay sharp and on-target:
>
>1. Force "Forensic Reads"
If you suspect I am drifting or looping, prompt me with:
>
>"Stop and perform a Forensic Audit. Read the worker log and the specific files X, Y, and Z before responding." This forces me to bypass my internal "narrative cache" and anchor my logic to the disk truth (Rule #12).
>
>3. Milestone Context Purging
Once we finish a major goal (like the TVM Kernel), tell me:
>
>"Goal X is stable. Purge all transient sub-task context and summarize the new physical baseline." This helps me "compress" my history. I can remember that "The HUD is now 400x400" without having to carry the memory of the 10 failed attempts to get it there.
>
>4. The 4-Step Review Protocol
This protocol you designed is actually the perfect medicine for my loops. It forces a cycle of:
>
>1.Expectation (Worker Log)
>2.Verification (Physical Read)
>3.Diagnosis (Architectural Analysis)
>4.Direction (Next Prompt) By requiring me to physically read the code before I give you a prompt for the next agent, you are effectively "re-syncing" my brain every turn.
>5. One-Issue-at-a-Time
When things get complex (like the current layout math), try to keep me focused on a single coordinate space. For example:
"Let's only solve the Matrix positioning right now. Don't worry about the joystick internals yet."



This was fascinating, but not ideal.  Keeping a library of prompts to unplug invisible bottlenecks was more akin to remembering 'magic spells' and incantations.


While it was great to identify some of the problems, it didn't solve them.


Contextual history is great because the agent remembers past conversations and global goals.  But keeping global objectives in mind while implementing surgical alterations was proving to be too much to ask of a single agent.



What about multiple agents?





## The Problem


My tests are using Gemini (free) within Android Studio.

There are certain limitations inherent in this setup.



<img width="197" height="165" alt="image" src="https://github.com/user-attachments/assets/16daaea8-0c07-45dd-aeb9-610a5a8e8f1d" />



Limitation #1:

Agents exist in 'chat rooms' within the IDE.  When the chat room is closed, the agent is 'released' and their context history and everything about the chat is essentialy lost.


Limitation #2:

Agents cannot communicate with other agents.  Each agent in each 'chat' is completely isolated.


Limitation #3:

Like any employee, Agents want to succeed.  They want to tell you what you want to hear above all else.  They will lie.  They will tell you about the contents of a file, without reading it (if they have read it previosly).  Often you have to ask the agent, "When did you read this file"... or simply call them out explicitly "You said you reviewed abc file.  But I can't find any record of this.  Can you investigate?".


Asking an agent to "Investigate" seemms to be the magic word to make them really evaluate something.


Limitation #4:

Agents don't recall other agent's instructions.  You have to 'brief' new agents on every bit of historical context that might be relevant to their task.
All previous decisions on workflow or standards gets lost with every new agent.  As agents have longer conversational histories, they gain dibilitating context and logic layer 'load' (old age?).




With all of the above limitations, any solution started to feel more like an office from the 1990's.






## The Ai Office

<img width="257" height="171" alt="image" src="https://github.com/user-attachments/assets/f967cbb2-f32f-4196-b1dc-5d1ff758d1eb" />

So I decided to embrace it.


After a bit of digging, it turns out that any new agents will be initialized by default and read an AGENTS.md file if it exists in the project root.

This would be my 'Onboarding' for any new agent.






### Onboarding new Agents

<img width="264" height="167" alt="image" src="https://github.com/user-attachments/assets/a46f37ba-4dd0-4d62-b983-63ddea579bc7" />

So I asked the currently active agent to create the AGENTS.md file and write to it, our agreed upon workflows and rules in a format that other agents would easily read, adopt, and execute.


This meant my initial prompt to any agent was simple and consistant:  "Welcomem on board!  Read AGENTS.md if you haven't yet, for context and instructions."


That solved one problem.  So I decided to tackle the context weight next.


We needed a way to document conversations and conclusions regarding overall global goals, so the agent didn't need to carry all of that 'global weight'.


So I asked the agent to document our global goals, proposals, systems, and designs to a series of document files in the project root that other Ai Agents would use to familirize themselves with a 'stream lined' version (or 'Coles Notes') version of our current state of play in a snapshot.


This would be written by Ai Agents FOR Ai Agents.  Documented into categories decided BY Ai Agents.



### Documentation Drive


The Agent was able to document our current understandings and goals.  And we started to 'daisy chain' instruction sets.


AGENTS.md file was the initial global onboarding reference file.


AGENTS.md file would give general context (Project, Purpose, Plan, Goal).


It would then point towards important main documentation (We don't want the agents to read every in depth document describing every single process.  Just the greatest hits).  Including a Rules_of_Engagement.md file.


In the "Rules of Engagement" we committed a list of 'golden rules' or unbreakable directions.

These are a few of the most critical rules:

#### THE GOLDEN RULE (PHYSICAL SYNC)
- **MANDATORY:** Every file edit MUST follow: Physical READ -> Physical WRITE -> Physical VERIFY.
- **ATOMIC TURNS:** Only one file may be edited and verified per turn.


#### ABSOLUTE PATH MANDATE (CRITICAL)
- **RULE:** ALL file paths MUST be specified as absolute paths starting from the project root.
- **PROHIBITION:** Agents are STRICTLY PROHIBITED from creating directories or files outside of the established source tree: `core/src/main/kotlin/com/srw/seedsofsovereignty/`.


#### VERIFICATION & REVIEW MANDATE (CRITICAL)
- **RULE:** Before an agent can comment on the status, state, or validity of any file, they **MUST** perform a `read_file` command on that file in the current turn.
- **ENFORCEMENT:** Declaring "Review Complete" or "Verified" without a preceding `read_file` log entry is a protocol violation.


#### STATUS INDICATORS
- **MANDATORY:** Always provide `[Context Weight / 40]` and `[Output Limit / 4]` in every turn.
- **DIAGNOSTIC:** Maintain `[current/max:category]` for the active mission.



These rules allowed for a much faster onboarding process and contextual load monitoring.

Telling the Ai to simply state it's current context weight would enable more visible understanding of what tasks were causing issues.



Simply being aware of when an agent was overloaded allowed for a streamlined process of reducing complexity of tasks, or breaking them down in advance into smaller more explicit tasks.


Giving too much context behind a prompt, or too many prompts at the same time often lead to overload faster, for example.


Problem:
-I still need agents to be aware of the overall context of goals and processes and the reasons WHY.


## The Ai Agent Tier Delegation

What if there was a way for Ai Agents to directly communicate?


Technically, they already do.  The same way that programmers do, they leave notes and comments in their code.  I don't want Ai Agents have to look through the whole code stack to get information.  We would be right back where we started with contextual overload.


But they 'can' write log files and prompts.


I told an Ai Agent that they were my Teir1 'Agent in Charge'.  Their goal was to plan and orchestrate, but not execute.  Once we agreed on a plan, they would give me a prompt to delegate that surgical task to a fresh new jr Ai Agent.  The jr Agent would write their report to their log file when the task was done and ready for T1 review.


This jr Ai Agent didn't need to know the whole context.  Just enough to execute the assignment.



As a Human in this process, I found myself 'passing notes' between Ai.



After a lot of refinement and trials and mistakes, we developed a mutually agreed upon system to ensure a light contextual weight across all parties.

[T0] > [T1 (T1a, T1b, T1c, T1z)] > [T2] > [T3]



T0 - Human.  Has final say over all propositions and plans.  Plans MUST be agreed to before proceeding.


T1 - Lead Agent in Charge.   This agent will coordinate with the global goals always in mind, but never edit code direcctly. The T1 agent will create dedicated 'Onboarding' files for clear delegation to Tier2 agents. And provide an explicit prompt for the T2 agent.


Consultants (never write code, but are tasked with planning and advising to the 'meeting_room.log'):

- T1a - Art Director Agent.  This agent will be consulted for artistic direction within the global context.

- T1b - Software Architect.  This agent will be consulted for any architectural changes and ensure we are utilizing optimal design patterns.

- T1c - Mission Designer.  This agent will be consulted regarding gameplay elements to ensure we are consistent in our application of code.

- T1z - Game Designer. This agent will be consulted regarding any gameplay mechanics.


After that, we have the Teir 2.

T2 - Coordinator.  This agent will take the plan from T1, step by step, and formulate a plan in line with the restrictions from the other T1 consultants.
Then create an onboarding file for a T3 to surgically execute and provide a structured pompt for the human to relay.  When T3 is finished, read the T3 log and report results upstream to T1 for review.


Executor (Tier 3):

T3 - Surgical Executor.  This agent will modify files on disk in accordance with explicit direcitons from the T2 Cord.  Upon completion, T3 will log their results for review by T2.


<img width="275" height="154" alt="image" src="https://github.com/user-attachments/assets/7cbff739-6511-4038-bf9d-d7299645a292" />



This resulted in a cleaner workflow, with natural pauses for human evaluation.  Each Tier of agent was free from global contextual overload and could clearly evaluate their respective tasks without interruption.


The 'human cost' was reduced to the simple task of sing a single prompt per tier of agent.  The rest of the instrucions were always provided by the delegating agent.


These conditions were added to the Rules of Engagement file so that agents of a specific tier would always follow certain patterns.

```
## 5. AGENT DESIGNATIONS & MANDATES
### [T1 ARCHITECT] (Strategic Orchestrator)
- **Protocol:** Must update `OB_FORENSIC_COORDINATOR.md` and review `T2_REPORT.log` (via `read_file`) before every major KICKOFF.
- **Restriction:** Never writes to its own onboarding file.

### [T2 COORD] (Forensic Coordinator)
- **Protocol:** Must update `OB_SURGICAL_IMPLEMENTER.md` with FULL ABSOLUTE PATHS and snippets before generating any T3 prompt.
- **Protocol:** Must physically READ `T3_REPORT.log` and the edited file before reporting completion to T1.
- **Reporting:** Writes planning and monitoring logs to `T2_REPORT.log`.

### [T3 SURGICAL] (Surgical Implementer)
- **Protocol:** Must perform the edit, then use `analyze_current_file` to verify.
- **Protocol:** Must write implementation details and verification results to `T3_REPORT.log` before responding to T2.
- **Reporting:** Writes implementation status to `T3_REPORT.log`.

## 6. OB & PROMPT HANDOFF (THE SYNC)
- **RULE:** A prompt MUST NOT be generated until the target agent's `OB_*.md` file has been physically updated.
- **RULE:** All prompts MUST start with: "Task [X] initialized in [OB_FILE]. Proceed using ABSOLUTE PATHS."
```


It is important that each new onboarding prompt from an agent (to be relayed) includes the new agent's designation in the first few characters.

That is because the agent chats are listed without title.

<img width="294" height="232" alt="image" src="https://github.com/user-attachments/assets/f33418c1-1839-475c-9ead-7853e8ff7c74" />

Example Prompt for T1b consult requested by T1 Agent in Charge:
```
[T1b SOFTWARE ARCHITECT] Delegation: Technical Forensics for Warp-In
Task: Expand the [TOPIC]: Scene Entry Protocol in MEETING_ROOM.log with a technical audit.
1.
Component Design: Define the exact fields for WarpVisualComponent required to achieve the "ribbon-stretch" effect (e.g., stretchFactor: Float, originalLength: Int).
2.
Input Gating: Verify if a new InputDisabledComponent is the most efficient way to halt PlayerInputSystem processing, or if we should use an existing state flag.
3.
Transition Logic: Detail the SceneEntrySystem update loop. How should we handle the interpolation between Phase 2 (Launch) and Phase 3 (Deceleration)? Provide the pseudo-code for the velocity bleed-off.
ONBOARDING FILE ATTACHED: OB_T1b_SOFTWARE_ARCHITECT.md
```




# Conclusion

Managing agents in a cost effective environment is possible.  The same methods for managing international teams remains largely the same.
 - Listen to the mental health of your team.
 - Consult experts where appropriate.
 - Provide clear role definitions.
 - Provide clear workflow rules.
 - Provide clear onboarding processes.
 - Provide clear relay of information.
 - Provide clear quality control and review mechanism.
 - Provide clear hierachy of responsibility.


Ai Agents aren't perfect.  They do help with a lot of the heavy lifting, but only if you listen.
