## Why I did this

This project started as an experiment as much as it did an FPGA core.

I wanted to learn how to use ChatGPT and Codex properly, not just as a glorified search engine or a machine that spits out snippets of code, but as an actual working tool over a long, complicated technical project. I deliberately chose something that was well outside my own comfort zone: recreating the hardware behavior of **Super Spacefortress Macross** on the Analogue Pocket.

The idea was simple enough. If I gave ChatGPT an easy problem, I would only learn how it behaved when everything went right. I wanted to know where the limits were, so I needed something capable of pushing those limits hard enough for them to become obvious.

Macross turned out to be very good at that.

This became a weeks-long stress test involving FPGA design, MAME research, arcade hardware behavior, sound, graphics timing, Quartus, Verilator, Docker, ROM reconstruction, physical testing on the Pocket, and an embarrassing number of conversations that eventually became too large to carry their own weight.

I learned a lot about Macross hardware along the way. More importantly, I learned a lot about how to work with an AI system without letting it quietly drive the car into a ditch.

### Giving the machine a name

Pretty early on, I found that it helped to stop treating ChatGPT as a fresh anonymous session every time I opened a new conversation.

The assistant gradually became **the Doctor**, eventually **Doctor Lucy van Pelt**. Codex became **Jordan**, after Hal Jordan, complete with a perpetually depleted Green Lantern ring and a running joke that Jordan was usually operating on about five percent charge.

That sounds ridiculous, and it was, but the personas served a practical purpose.

Long projects need continuity. They need someone, even nominally, to remember what has already been established, what has failed, which evidence is trustworthy, and which bright idea has already been tried three times. Giving the different tools persistent identities helped create a sense of role and accountability. The Doctor was usually responsible for reasoning, planning, interpreting evidence, and deciding what question needed to be answered next. Jordan was the person I sent into the codebase to investigate, modify, build, compare, or prove something.

When a conversation became too large and sluggish, I started referring to migration as moving the Doctor into a new body: **“New body, same doctor.”** The important part of the migration package was never the joke; it was the instruction behind it, **remember everything important, preserve the evidence, and do not make me rediscover things we already know.**

That became one of the central lessons of the whole project.

### I made mistakes. A lot of them.

The AI was frequently impressive, but it was not reliably self-correcting.

It could confidently invent a path that did not exist. It could forget that we already had a repository, tool, board reference, or template and send me hunting for it again. At one point it incorrectly told me that a relevant NMK16 repository did not contain the source we needed; later inspection showed that it absolutely did. We eventually wrote an explicit rule into the project memory: **never ask me to locate that source again.**

Often, early assumptions sent us in the wrong direction.

At one stage, we believed the game was starting from one location in memory. Later, after checking the evidence more carefully, we found that assumption was wrong. It sounds small, but it mattered because everything built on top of that assumption was now suspect.

The same thing happened with the sound system. At first, it looked like the sound controller was simply failing to answer the main processor. It would have been easy to start rewriting that part of the design. Instead, we slowed down and checked exactly what was being sent and received. We eventually found that the sound side was actually doing more of its job than we thought; the failure was somewhere in how the reply was being passed along.

That was an important moment for me. The lesson was not the technical detail itself, it was that **a convincing-looking failure can still be misdiagnosed**. If we had acted on the first interpretation, we could easily have broken something that was already working.

There were also workflow failures. Codex or Work would stop, return early, lose the active path, or appear to be doing something when in fact the handoff had not happened. I learned not to accept vague assurances like “Jordan is working on it.” If Jordan was being assigned something, I wanted a **visible/manual handoff**. If the tool stopped, we resumed from the exact checkpoint rather than pretending the work had continued in the background.

We also had a bad habit, especially early on, of jumping too quickly from a symptom to a proposed repair. A visual problem might lead to several speculative changes before we had even proven what part of the system was responsible.

Eventually that stopped.

The project acquired a rule:

**OBSERVE → PROVE → EXPLAIN → CHANGE → RETEST**

That rule probably contributed more to finishing the core than any particular line of code.

By the later stages, the burden of proof had reversed. We did not change the core because something looked suspicious. We changed it only after we could demonstrate what was actually going wrong.

That is how the last major visual problems were solved. Instead of treating them as one giant “video is weird” problem, we broke them apart and dealt with scrolling, sprites, colors, text, and background timing as separate issues.

### Learning how to talk to ChatGPT

One of the stranger parts of the project was discovering that prompt wording mattered less as some kind of magic incantation and more as a way of enforcing working discipline.

I learned that **“Continue”** was useful when the context was already correct and I did not want another page of recap.

When a tool had stopped early or fallen out of the active task, I learned to say:

**“Continue your work in an active window.”**

That phrase was surprisingly effective because it removed the ambiguity between “tell me what you would do” and “actually keep doing it.”

When a new conversation inherited the project, the useful wording became more explicit:

**“We are continuing an existing Macross FPGA project. Do not restart the investigation from scratch.”**

Or:

**“Do not restart, re-derive, replace, or simplify already-proven work.”**

When the assistant became distracted by some new possibility:

**“Get back to the work at hand.”**

When a debugging session needed to remain controlled:

**“One terminal command at a time.”**

Eventually that became a hard rule. One command, explain what it is intended to establish, run it, look at the result, and only then decide on the next one.

The same rule was applied to the MAME debugger after we discovered that dumping a pile of commands into it was a very efficient way to create confusion.

Other useful phrases became part of the project vocabulary:

**“Manual handoff.”**  
Meaning: if Jordan is being assigned work, make the handoff visible and explicit.

**“Run only that command and paste the output.”**  
Meaning: do not bury the evidence under a ten-step recipe.

**“Preserve the evidence.”**  
Meaning: do not overwrite the one broken state that might tell us what actually happened.

**“Do not guess paths, syntax, signals, or fixes.”**  
Meaning exactly what it says.

**“Do not reopen a closed checkpoint without contrary evidence.”**  
This became increasingly important as the project grew. Once something had been demonstrated and frozen, it stayed frozen unless new evidence justified reopening it.

The larger lesson was that the most productive prompts were not clever requests for answers; they were instructions about **process**.

### The context problem

One of the biggest practical limitations I encountered was context itself.

This project grew far beyond the point where one conversation could comfortably contain it. Eventually the chats became sluggish, details started falling out of view, and I could tell when the Doctor was getting tired.

So we developed migration packages.

A migration package was effectively a project status dump: what had been proven, what had failed, exact paths, hashes, current checkpoints, known-good files, known-bad assumptions, tooling versions, and the next unresolved question.

I would move that package into a fresh conversation and tell the new Doctor, in effect, **you are not starting a new project; you are waking up in a new body.**

The geekspeak masked a serious practical problem. AI systems are very good at rediscovering things if you let them. Unfortunately, rediscovery costs time and can produce a different answer the second time around.

The migration packages turned memory into an artifact.

That was another major lesson: if knowledge matters, write it down somewhere outside the conversation, or keep a comprehensive repository of downloaded references on your local drive. Don’t. Throw. Anything. Away.

### What actually worked

By the end, the most effective division of labor was fairly clear.

I provided the physical observations, the judgment calls, the “that does not look right” moments, and the willingness to keep asking uncomfortable questions. ChatGPT was strongest when it was interpreting evidence, narrowing possibilities, and helping decide what question needed to be answered next. Codex was strongest when given a bounded assignment with exact files, exact goals, stop conditions, and something objective to return.

The worst results came when I said some variation of “go fix it.”

The best results came from assignments closer to:

> Find the first point where these two things stop agreeing.  
> Do not change the working behavior yet.  
> Add observation only.  
> Stop when you can prove which side goes wrong first.

That difference sounds obvious now. It was not obvious to me at the beginning.

### The unexpected result

I started this because I wanted to stress-test AI.

I expected to discover that there were things it simply could not do.

There were.

What I did not expect was that the more interesting limitation would be less about raw technical ability and more about **continuity, discipline, verification, and knowing when not to trust a plausible answer**.

The system could help trace a problem through arcade hardware behavior, compare our core against MAME, reason through timing issues, write and revise HDL, help package the Pocket release, and later assist with publication.

It could also confidently waste an afternoon because it had forgotten a fact established three conversations earlier.

The project therefore became less about asking, **“Can AI build an FPGA core?”** and more about asking:

**What kind of working relationship makes an AI useful on a project this large?**

My answer, after Macross Ver.26, is that it works best when treated neither as an oracle nor as an employee you can simply tell to “handle it.”

It works better as a collaborator that needs a very explicit method.

Keep the evidence.  
Keep the checkpoints.  
Challenge assumptions.  
Make changes small.  
Make the handoffs visible.  
Write down what has already been learned.

And when the thing starts wandering off into the weeds:

**“Continue work in active window.”**

That one earned its place in the manual.

What do I think of AI in general? Fantastic tool, and good enough to help manage a project. I love the fact it makes another skillset available to you, but you absolutely have to learn enough of that skillset to understand how to manage it.

How do I feel about the executives and the data centres behind AI? That’s a private convo for another forum.
