<div align="center">

# 🧠 Prompt Engineering — The Basics

### A practical, no-fluff guide to writing prompts that actually get you what you want

![Level](https://img.shields.io/badge/level-beginner-brightgreen?style=flat-square)
![Topic](https://img.shields.io/badge/topic-prompt%20engineering-blueviolet?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)

</div>
https://www.aishort.top/en/
---

## 📖 What is prompt engineering?

Prompt engineering is the practice of **designing the input you give an AI model** so it
reliably produces the output you actually want. The model hasn't changed between a bad
result and a great one — usually the instructions have.

Think of it less like "magic words" and more like **writing a clear brief for a very
capable, very literal new hire**: the more precisely you describe the task, the context,
and what "good" looks like, the better the result.

---

## 📂 Table of Contents

| Section | What you'll learn |
|---|---|
| [🎯 Core Principles](#-core-principles) | The mindset behind every good prompt |
| [🧩 Core Techniques](#-core-techniques) | Concrete methods you can apply today |
| [🏗️ Anatomy of a Great Prompt](#️-anatomy-of-a-great-prompt) | The building blocks, assembled |
| [❌ Common Mistakes](#-common-mistakes) | What quietly ruins results |
| [🔁 Iterating on Prompts](#-iterating-on-prompts) | Treating prompts like code |
| [📋 Quick Reference Cheat Sheet](#-quick-reference-cheat-sheet) | The one-page summary |

---

## 🎯 Core Principles

<details>
<summary><b>1. Be clear and specific</b></summary>

Vague instructions get vague answers. Instead of guessing what you meant, spell it out:
audience, tone, length, format, constraints. If a human intern would need to ask a
clarifying question, the model probably does too.

> ❌ "Write about dogs"
> ✅ "Write a 150-word paragraph for a children's science blog explaining why dogs have a
> better sense of smell than humans. Keep the tone playful and avoid jargon."

</details>

<details>
<summary><b>2. Give context, not just instructions</b></summary>

Tell the model *why* it's doing the task, *who* the output is for, and *what happens
next* with the result. Context lets the model make good judgment calls on the details
you didn't specify.

</details>

<details>
<summary><b>3. Show, don't just tell (use examples)</b></summary>

One or two examples of the input/output pattern you want ("few-shot" prompting) is often
worth several paragraphs of description. Models are excellent pattern-matchers.

</details>

<details>
<summary><b>4. Let the model think before it answers</b></summary>

For anything involving reasoning, math, or multi-step logic, explicitly asking the model
to reason step-by-step before giving a final answer improves accuracy dramatically. This
is often called **chain-of-thought prompting**.

</details>

<details>
<summary><b>5. Positive instructions beat negative ones</b></summary>

Telling a model what *to do* is more reliable than telling it what *not to do*. If you
must forbid something, pair it with the correct alternative.

> ❌ "Don't use markdown."
> ✅ "Write in plain prose paragraphs, no headers or bullet points."

</details>

<details>
<summary><b>6. Iterate — the first prompt is a draft</b></summary>

Nobody writes the perfect prompt on the first try. Treat prompting as a short feedback
loop: run it, look at what went wrong, adjust one variable, run again.

</details>

---

## 🧩 Core Techniques

<details>
<summary><b>Zero-shot prompting</b></summary>

Just ask directly, with no examples — relying on the model's existing knowledge.

```text
Summarize the following article in three bullet points.
```

Best for: simple, well-understood tasks where the format is obvious.

</details>

<details>
<summary><b>Few-shot prompting</b></summary>

Provide 2–5 examples of the input → output pattern before your real request. Great for
enforcing a specific style, structure, or edge-case handling.

```text
Convert each product description into a one-line tagline.

Description: A backpack with a built-in solar charger.
Tagline: "Never run out of power, wherever the trail takes you."

Description: A water bottle that keeps drinks cold for 24 hours.
Tagline: "Ice cold, all day long."

Description: A running shoe with responsive foam cushioning.
Tagline:
```

</details>

<details>
<summary><b>Chain-of-thought (CoT) prompting</b></summary>

Ask the model to reason through the problem step by step before giving the final answer.
Useful for math, logic, multi-step analysis, or anything where jumping straight to a
conclusion causes errors.

```text
A store had 120 apples. They sold 35% on Monday and 20 more on Tuesday.
How many apples are left? Think step by step, then give the final answer.
```

</details>

<details>
<summary><b>Role / persona prompting</b></summary>

Assigning a role focuses the model's tone, vocabulary, and priorities.

```text
You are a senior backend engineer doing a code review. Be direct and specific
about bugs, but keep the tone constructive.
```

</details>

<details>
<summary><b>Delimiters and structure</b></summary>

Use clear separators (triple quotes, XML tags, headers, code fences) to mark where
instructions end and content begins. This prevents the model from confusing your
instructions with the data you're asking it to process.

```text
Summarize the text between the <article> tags in two sentences.

<article>
...paste article here...
</article>
```

</details>

<details>
<summary><b>Specifying output format</b></summary>

If you need JSON, a table, a specific word count, or a particular structure — say so
explicitly, and ideally show the exact shape you want.

```text
Return the result as JSON with exactly these keys: "title", "summary", "tags" (an array).
```

</details>

<details>
<summary><b>Constraining scope</b></summary>

Tell the model what's in bounds and what isn't, especially for research or analysis
tasks, to prevent it from wandering or padding the answer.

```text
Only use information from the provided document. If the answer isn't in the
document, say "Not found in the source" instead of guessing.
```

</details>

<details>
<summary><b>Self-critique / refinement loop</b></summary>

Ask the model to draft an answer, then critique and improve its own draft against a
checklist. This catches errors a single pass misses.

```text
First, write a draft response. Then review your draft against these criteria:
accuracy, conciseness, and tone. Revise if needed, and give me only the final version.
```

</details>

---

## 🏗️ Anatomy of a Great Prompt

A strong prompt usually combines several of these pieces — not all are needed every
time, but this is a good default order:

1. **Role** — who the model should act as (optional, but helps set tone/expertise)
2. **Task** — the specific thing you want done, stated as an action
3. **Context** — background info, audience, purpose
4. **Constraints** — length, tone, format, things to avoid
5. **Examples** — sample input/output if the pattern is non-obvious
6. **Output format** — the exact shape of the answer you want

```text
You are a technical writer. [Role]

Write a short troubleshooting guide for a "Wi-Fi won't connect" issue on a
home router. [Task]

The audience is non-technical home users who just want their internet
working again. [Context]

Keep it under 200 words, use numbered steps, and avoid jargon like "DHCP"
or "SSID" — use plain descriptions instead. [Constraints]

Format the response as a numbered list with a one-line title. [Output format]
```

---

## ❌ Common Mistakes

| Mistake | Why it hurts | Fix |
|---|---|---|
| Being vague ("make it better") | Model has to guess what "better" means | Define the specific dimensions: clearer, shorter, more formal, etc. |
| Overloading one prompt with 10 unrelated asks | Model prioritizes inconsistently, quality drops | Split into separate prompts or a clear numbered list |
| Only saying what *not* to do | Leaves a gap where the model doesn't know what's correct | Pair negative instructions with the positive alternative |
| No examples for a stylistic or structural task | Model falls back to generic defaults | Add 1–2 examples of the pattern you want |
| Never iterating | First attempt is rarely optimal | Treat prompting as a loop: run → diagnose → adjust → rerun |
| Burying the real ask in a wall of text | Key instruction gets lost or deprioritized | Put the core task early and use structure (headers, lists, delimiters) |

---

## 🔁 Iterating on Prompts

Prompting is closer to debugging code than writing an essay. A simple loop:

1. **Run** the prompt and read the output critically.
2. **Diagnose**: is the problem missing context, unclear instructions, wrong format, or
   a reasoning gap?
3. **Change one thing** at a time — add an example, tighten a constraint, reorder
   sections — so you know what actually fixed it.
4. **Re-run** and compare.
5. Once it's reliable, **save the prompt** as a reusable template for next time.

---

## 📋 Quick Reference Cheat Sheet

- ✅ Say exactly what you want, including format and length
- ✅ Give the "why" and the audience, not just the task
- ✅ Show an example when the pattern isn't obvious
- ✅ Ask for step-by-step reasoning on anything logic-heavy
- ✅ Use delimiters to separate instructions from content
- ✅ Phrase constraints as what *to* do, not just what to avoid
- ✅ Iterate — refine one variable at a time
- ❌ Don't assume the model knows unstated context
- ❌ Don't cram unrelated requests into a single prompt
- ❌ Don't skip the output format if it matters

---

## 📄 License

Shared under the MIT License — free to use, remix, and share.
