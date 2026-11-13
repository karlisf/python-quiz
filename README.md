# Python basics practice quiz

A multiple-choice quiz for people who are learning to code for the first time, using Python.

Live version: https://karlisf.github.io/python-quiz/

- 10 subjects, 10 questions each, 100 questions in total.
- Everything is in one static file, `index.html`. There is no build step, no server and no external libraries.
- Progress (answers, time spent) is saved in the learner's own browser (`localStorage`). Nothing is sent anywhere.

## Subjects

| # | Subject | Covers |
|---|---------|--------|
| 1 | Values and types | `int`, `str`, `float`, single characters, indexing |
| 2 | Operations | `+ - * / // %`, mixing types |
| 3 | Casting | `int()`, `str()`, `float()` |
| 4 | Logical operations | `and`, `or`, `not`, parentheses |
| 5 | input() and print() | reading text, `sep`, `end` |
| 6 | Tracing variables | the value of a variable after several steps |
| 7 | if, elif, else | which branch runs |
| 8 | for loops and range() | `range` bounds, step, looping over a string |
| 9 | while loops | the condition, infinite loops, `break`, `continue` |
| 10 | Loop patterns | sum, count, build a string; review of all earlier subjects |

## Principles

### 1. Learners read code and predict what it does
- Most questions show a short program and ask "What does this print?" or "What happens?".
- The aim is to practise *tracing*: following the code line by line in your head.
- A few questions turn this around: they show code as the answer options (9.9) or ask what is missing (9.5).

### 2. Every wrong answer is a real beginner mistake
- Each question has 4 options.
- The wrong options are not random. Each one is the result a beginner gets from a specific misunderstanding.
- Example for `7 // 2`:
  - `3.5` means mixing up `//` and `/`.
  - `4` means believing `//` rounds up.
  - `3.0` means expecting a `float` result.

### 3. Every option explains itself
- After answering, the learner sees an explanation for **all four** options, not only the one they picked.
- A wrong option's explanation names the misunderstanding behind it and, where useful, the code that *would* give that result.
- The real output of the program is shown in a separate box.
- Some questions add a note with a fix or a tip.

### 4. Difficulty rises inside each subject
Every subject has the same mix of levels, in this order:

| Level | Questions | Meaning |
|-------|-----------|---------|
| trivial | 3 | one idea, the most common case |
| simple | 3 | one idea with a small twist |
| non-advanced | 3 | the usual traps: edge cases, order of operations, values at the boundaries |
| mixed | 1 | combines this subject with earlier ones |

### 5. Subjects build on each other
- Subjects are ordered so that each one only uses ideas from the subjects before it.
- For example, no loop question uses lists, because lists have not been introduced yet.

### 6. Ideas come back again and again
Repetition is written into the questions themselves:

- **Contrast pairs**: the same code with one change, placed next to each other. Examples:
  - two separate `if`s vs. `if/elif` (7.6 / 7.7)
  - `and/or` without vs. with parentheses (4.7 / 4.8)
  - `input()` without vs. with `int()` (5.5 / 5.6)
  - a sum printed after the loop vs. inside it (10.1 / 10.4)
  - `break` vs. `continue` (9.7 / 9.8)
- **Callbacks**: ideas from earlier subjects come back in later ones. Examples:
  - `str * int` repetition (operations → casting → input → loops)
  - `%` for odd/even (operations → logic → if → loops)
  - `TypeError` from `"5" + 5` (operations → input)
- **Mixed questions**: the last question of each subject combines it with earlier subjects.
- **Loop patterns** (subject 10) is mostly review: loops used together with `if`, `%`, casting, `input()` and string building.

### 7. Plain language for beginners
- Short sentences.
- Python terms are introduced in the questions where they are used.
- No assumed knowledge of other programming languages. Where another language behaves differently (Python has no `char` type), it is said directly.

## How a question is written

Questions live in the `SUBJECTS` array in `index.html`:

```js
{lvl:"simple", q:"What does this print?", code:`print(7 // 2)`, opts:[
  ["3", true,  "Explanation of why this is right."],
  ["3.5", false, "Which misunderstanding leads here."],
  ["4", false, "..."],
  ["3.0", false, "..."]],
  out:"3",                      // actual output, shown after answering
  given:"User types: 20",       // optional: what the user types for input()
  note:"Optional extra tip."}   // optional
```

- Write the correct option first. Options are shuffled when shown.
- Text in `` `backticks` `` is shown as code.
- Use `\n` in an option for output that spans several lines.
- Before publishing, run every code sample in Python and check that `out` and the correct option match what Python actually prints.

## TODO

### Data
- [ ] **Stable question ids.** Saved answers are keyed by position (`"<subject>-<question>"`). Adding subjects at the end is safe. Inserting or reordering subjects attaches learners' saved answers to the wrong questions. Fix: give each subject and question a fixed id, or change the storage key (`pyquiz.v1` → `v2`) whenever the order changes, which resets everyone's progress.

### Learning features
- [ ] **Retry missed questions.** A wrong answer is final and the question never comes back. Add a mode that asks the missed questions again.
- [ ] **More question types.** Almost all questions are "predict the output". Add more "find the bug" and "which code produces this output?" questions, especially for `if` and loops.
- [ ] **Next subjects:** lists, then functions.

### Small fixes
- [ ] The subtitle says "10 questions each" as fixed text. Calculate it from the data, or reword it.
- [ ] Answer letters reshuffle after a page reload, because the shuffle is not saved. The chosen answer still shows correctly.
- [ ] The "User types:" line formats everything after the colon as code, including words like "(Enter after each)".
- [ ] Level badges keep their light colours in dark mode.
- [ ] Consider renaming the level "non-advanced" to "intermediate".
- [ ] Check the layout on a phone with 10 subjects (the subject list becomes a horizontal scrolling row).
