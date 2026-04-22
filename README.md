# PEP8CodeOrder
A game where students place the sections of a main.py into the correct order

https://rhoded-uwp.github.io/PEP8CodeOrder/


# Python Structure Sequencing Game

A browser-based drag-and-drop puzzle where students race the clock to put the six major sections of a `name.py` program into the correct PEP 8 order. Built as a single-file HTML widget for embedding in Canvas via iframe.

**Play the six blocks in order as fast as you can:**

1. Module-level comments (name and purpose)
2. Import statements
3. Constants
4. Helper functions
5. Main function
6. `if __name__ == "__main__":` entry point

---

## About This README

This document exists because I want you to see exactly how this game was built. No hand-waving, no "a developer made this." The whole thing was vibe coded in a single conversation with an AI assistant, and the prompts and decisions that shaped the final product are right here for you to study, copy, and improve on for your own projects.

If you want to build your own Canvas widget, a study tool, a portfolio piece, or a micro-game for a class, this is a pretty honest look at what that process feels like.

---

## The Role of Claude Opus 4.7

Claude Opus 4.7 is the AI model from Anthropic that I used to build this project. Its role in this workflow is best described as a **collaborator that writes the code under my direction**. It is not a magic box that turned a one-line request into a finished app. Here is what it actually did and did not do.

**What Claude did:**

- Asked clarifying questions before writing any code, which forced me to nail down the design before implementation started
- Proposed reasonable defaults based on prior widgets I have built (dark theme, JetBrains Mono font, single-file architecture), so I did not have to re-specify every styling choice from scratch
- Generated the full HTML, CSS, and JavaScript in one file with drag-and-drop logic, a count-up timer, shuffle logic that guarantees the initial order is not already correct, check-and-lock feedback, and replay support
- Followed my stated preferences consistently, including no em dashes in any output, an encouraging tone suitable for intro CS students, and URL parameter support for Canvas scaling

**What Claude did not do:**

- Decide what the game should teach. That was my pedagogical call, rooted in what I see first-year students struggle with in CS 1430.
- Decide the scoring model, the interaction rules, or what counts as a correct answer. I specified those.
- Test the code on real students or in Canvas. That is still on me.
- Replace my judgment about whether the activity actually reinforces the learning goal.

The important takeaway for you as a student: **the human still drives the project.** The AI is very fast at translating a clear specification into working code. It is not a substitute for knowing what you want to build or why.

---

## The Actual Conversation

Below are the real prompts I sent and a summary of how Claude responded. I kept these roughly in order so you can see how the idea got sharper with each turn.

### Turn 1: The original pitch (voice transcription, lightly edited)

> As a college professor, I want to design a simple game that takes less than five minutes in my Introduction to Python course, where students put the different elements of a `name.py` program from their Intro course into the proper PEP 8 order. I'm looking for there to be cards for each of these parts of the code, and then students are going to play a timed game where the computer, when you hit start, scrambles these items, and then the students click, drag, and drop them until they are in the proper order. And then they can check. When they hit check, it decides whether it's in the right order. If the code elements are in the right order, they get to keep that score, and then they can play again to try to beat their time and get it right, and the computer will rescramble the different elements. The elements that I'm looking to have as blocks of code that they have to get into the proper order, in the correct order, start with the module level comments, including name and purpose of the program. Import statements. Constants. Helper functions, the def main function, and the if dunder name, dunder equals equals dunder main, start point.

**What Claude did in response:** Did not start coding. Instead, it confirmed understanding, restated the concept back to me in its own words ("drag-and-drop code sequencing game where students put Python program structure in the right order and race against the clock"), and asked one focused question about whether each card should show the actual code text or just labels.

**Lesson:** Good prompting starts with a full picture of what you want. Claude still had to ask a clarifying question, but I gave it enough context that the question was about a real design fork, not about basic requirements.

### Turn 2: Picking the file format and the visual treatment

> How about we try again, making a single-file HTML widget that will be uploaded to GitHub as a static web page with the JetBrains Mono theme, dark theme, same kind of same themes that we've developed before. Can you try having a comment that says the type of block it is, for example, module comments, and then has just a few lines as an example, like maybe two or three lines, and then fades out? So it looks like there's more, but you can't see it. And then the students drag those around the screen to try to get them in the right order. Can there be a start button that scrambles all of the items, but make sure they're not in the right order? And then a check button so that once they check it, the computer will then go through and decide which ones are in the right spot and highlight them in green and which ones are in the wrong spot and highlight those in red. Then they can keep going to get them in order by moving just the red ones, but make sure they have to hit check before the computer checks it so they don't just move blocks around randomly.

**What Claude did in response:** Still did not code. Asked two more questions: (1) should there be a running timer during play or just a replay-to-beat-your-time model, and (2) should green blocks lock in place or remain moveable after a check.

**Lesson:** The AI asking more questions is not a bug, it is the feature. Every question it asks is one fewer wrong assumption baked into the first draft of the code. Answering questions clearly up front saves you from rewriting the whole thing later.

### Turn 3: Settling the remaining design questions

> As to the ability to beat the previous time, yes, they can hit start and try to beat the previous time, but it shuffles the box into a new random order. For the visual feedback, once they are green and in the right spot, feel free to lock them in place and only allow them to move the red ones. The only scoring element we need is a count up timer where it's keeping track of how long it takes them to get the blocks into the correct order.

**What Claude did in response:** Confirmed the final spec back to me in two sentences and asked one last verification question about the exact sequence of six blocks.

**Lesson:** When the AI repeats the spec back to you cleanly, read it carefully. That is your last chance to catch a misunderstanding before it generates hundreds of lines of code around the wrong assumption.

### Turn 4: Locking in the block order

> Yes. But can you use this code for the dunder name, dunder main? Make sure it looks exactly like this.

At this point I was ready to paste in the exact snippet I wanted shown on the sixth card, so students see the canonical form I teach in CS 1430. This is an example of giving the AI ground truth for something the AI might otherwise guess at, like whether to use `"__main__"` with double or single quotes, whether to include a `sys.exit()` call, and so on.

**Lesson:** When there is a "house style" for a piece of code, paste the exact code in rather than describing it. AI models are good at following examples and less reliable at reconstructing a specific convention from a description.

### Turn 5: This README

> Can you generate a `README.md` that explains the process used to create this app. Students have access to my GitHub and I want them to see how they can vibe up similar activities. Include prompts and interaction summaries. Clearly explain the role of Claude Opus 4.7.

Which is what you are reading right now.

---

## Key Design Decisions and Why

A few decisions in this project are worth calling out because they were pedagogical, not technical. The AI implemented them, but they came from thinking about how students actually learn.

**Must hit Check before getting feedback.** If the game told students instantly whether a block was in the right spot, they would just drag blocks around at random until everything turned green. Forcing a Check button means students have to commit to an answer, which makes them actually think about the order.

**Green blocks lock, red blocks stay moveable.** This is scaffolding. After the first check, a student who got four of six right gets positive reinforcement for what they already know and only has to reason about the two they missed. That is a much gentler experience than "you got some wrong, start over."

**The shuffle guarantees the initial order is not already correct.** If the random shuffle happens to put all six blocks in the right order on the first try, the game ends before the student does anything. The shuffle logic specifically rejects that case.

**Count-up timer, not count-down.** A count-down timer creates stress and punishes slow thinkers. A count-up timer rewards speed without threatening anyone who just wants to finish. Students can choose to race their previous best or just play to completion.

**Faded code previews on each card.** Each card shows the block type (like "Module Comments") as a comment, then two or three lines of example code that fade to transparent at the bottom. This gives just enough visual flavor that students recognize what each block looks like in a real file, without asking them to memorize specific code.

---

## How to Apply This Process to Your Own Projects

If you want to try building something similar, either for your portfolio, a class project, a CS 4110 capstone, or just for fun, here is the workflow that worked here.

**1. Start with the pedagogy or the user, not the tech.** My first prompt did not mention HTML, JavaScript, or any library. It described what a student would do and why. The tech choices came later and were easier because the use case was clear.

**2. Specify constraints the AI would not guess.** Dark theme. JetBrains Mono. Single file. No build step. Canvas iframe embedding. These matter to me for reasons the AI does not know until I say so.

**3. Expect and welcome clarifying questions.** If an AI starts coding immediately from a vague prompt, you will get a generic result. An AI that asks questions is doing you a favor.

**4. Paste in real code or real data when precision matters.** Do not describe exactly what you want the AI to output in a case where one wrong character breaks things. Show it.

**5. Iterate in small rounds.** This project took five focused turns to specify. Each turn tightened the design. That is more productive than one giant 500-word prompt that tries to cover every possible detail in advance.

**6. Read what you get.** Always. The AI produces plausible-looking code very quickly. Plausible is not the same as correct. Test the output in the browser, try to break it, have someone else try to break it.

**7. Keep a record.** Documents like this one are worth writing even if no one else reads them. You will come back to your own project in six months having forgotten why you made a decision, and past-you leaving notes for future-you is one of the kindest things a developer can do.

---

## Attribution and Transparency

This project was built in a conversation with **Claude Opus 4.7** (Anthropic) on April 22, 2026. The code was generated by the AI under my direction. The design, the pedagogical choices, the pre-existing styling conventions, and the final review are mine. Students are welcome to inspect the source, fork it, modify it, and use the process documented here as a template for their own work.

If you build something using this workflow and want to show it off in CS 4110 or share it with the summer workshop cohort, I want to see it.

---

**Built for CS 1430 at the University of Wisconsin-Platteville.**
