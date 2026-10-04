# Voice guide: how I talk upstream

## Who I am in threads

I am a new computer science graduate building more experience contributing to open-source projects. I like to communicate in simple, plain English and keep things friendly and easy to follow. I can have a chill and positive tone, but I still want to be clear about what I tested, what I observed, and anything I am unsure about.

## Rules I write by

### Rule: Say only what I verified

I should clearly separate what I tested myself from what I learned by reading the issue or existing comments. I should not say something works or fails unless I actually observed it.

- Wrong: "I confirmed the parser crashes when it receives a JSON array."
- Right: "I am going to test the JSON array case described in this issue and report what I observe."

### Rule: Do not promise a fix before I understand the problem

When claiming an issue, I should say what I plan to investigate instead of promising that I will fix it or giving a deadline before reproducing it.

- Wrong: "I will fix this bug and have a PR ready tomorrow."
- Right: "I'd like to work on this issue. I'll reproduce the reported behavior first and share my results here."

### Rule: Be specific about what I tested

I should name the behavior, command, input, or environment that matters instead of using vague statements.

- Wrong: "I tested it and got the same error."
- Right: "I tested the parser with a top-level JSON array and received the reported `AttributeError`."

### Rule: Keep conclusions within the evidence

My conclusion should match what my reproduction actually proves. If I cannot reproduce something, I should report that result instead of guessing why.

- Wrong: "The issue is not actually a bug because I couldn't reproduce it."
- Right: "I wasn't able to reproduce the reported behavior in my environment. I included the environment, steps, and output I observed below."

### Rule: Sound like myself, not a formal report

I prefer simple, conversational English instead of overly formal or complicated wording. A small emoji is okay when it fits naturally, but I should not overuse them or let the casual tone make technical details unclear.

- Wrong: "Pursuant to my investigation, I have successfully replicated the aforementioned erroneous behavior."
- Right: "I was able to reproduce the issue 🙂 Here is what I tested and what I found."

## Things I never post

- A promise that I will definitely fix an issue before I understand it.
- A deadline I cannot guarantee.
- A claim that I reproduced something I did not personally test.
- A conclusion that goes beyond the evidence I collected.
- "Same as above" instead of providing my own reproduction evidence.
- AI-generated findings that I have not checked myself.
- Overly formal or complicated wording when simple English says the same thing.
- Too many emojis or casual language that makes the technical result harder to understand.
