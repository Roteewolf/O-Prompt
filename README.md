![op2](https://github.com/user-attachments/assets/471cb32a-b75a-4874-9d96-3db44a591065)
# O-Prompt 4.0 Language Specification

## Table of Contents
1. Introduction
2. Global Priority Rules
3. Confirmed Effective Keywords
4. Why These Keywords Work
5. Syntax Rules: Avoiding Interpretation Conflict
6. Experimental Keywords (Under Testing)
7. Recommended Prompt Structures
8. License and Attribution

---

## 1. Introduction
- What is O-Prompt?
- Purpose & Philosophy
- Version History

<details>
<summary>📌 Click here to expand detailed explanation</summary>

### What is O-Prompt?
O-Prompt is a lightweight, LLM-focused prompt engineering language developed by Rotee. It is designed to optimize the clarity, efficiency, and expressiveness of prompts in a way that surpasses traditional systems like Markdown or JSON-based formats. Its purpose is to enable precise instruction of AI behavior through compact, modular, and semantically rich syntax.
O-prompt is configured to work reliably across all models by exploiting common denominator learning data patterns across LLMs.

### Purpose & Philosophy
The core philosophy behind O-Prompt is to simplify prompt construction while increasing its interpretability for AI models—especially for small and mid-size LLMs. Unlike most languages that avoid negatives, O-Prompt embraces `DO NOT` directives to increase clarity and control. Inspired by practices in image models like Stable Diffusion, O-Prompt allows for weighted attention, conditional logic, and explicit sampling guidance—all in human-readable form.

### Version History
- **v1.0** (2025-01-14): Initial prototype, used in "Rotee's RP Prompt Mild 1.2 Preview"
- **v4.0** (2025-04): Fully modular structure, model-tested with LLaMA3 7B, Claude Haiku, and GPT-3.5 class models

</details>

---

## 2. Global Priority Rules

### 🔒 Highest Priority Restriction
```
# Absolute Priority Rule
{DO NOT: ...}
```
Use this as the top-level directive to ensure strict behavioral control over the model.

---

| Keyword           | Purpose                                          | LLM Compatibility |
|------------------|---------------------------------------------------|--------------------|
| `DO`             | Include / enforce                                | ✅ Excellent |
| `DO NOT`         | Strict exclusion                                 | ✅ Excellent (better than `NOT`) |
| `MUST`           | Hard requirement                                 | ✅ |
| `Use_Data_Sample_Keyword` | sampling control; list-based input     | ✅ |
| `Remember`       | Contextual memory                                | ✅ |
| `Output_Format`  | Response structure control                       | ✅ |
| `if_`            | Conditional check (used with `return_`)          | ✅ Excellent |
| `return_`        | Result mapping ← used with `if_`                 | ✅ Excellent |
| `Persona`        | Role-based instruction anchor                    | ✅ |
| `style`          | Output texture control                           | ✅ |
| `tone`           | Emotional nuance                                 | ✅ |

## 🌉 Conditional Command Rules

O-Prompt supports conditional command structures that perform different actions based on given conditions.
There are two main types of conditional commands:

| Syntax | Behavior |
|--------|----------|
| `{if_condition:Return_"content"}` | If the condition is satisfied, returns the specified **static output** immediately. |
| `{if_condition:DO_content}` | If the condition is satisfied, executes the specified **dynamic logic or internal operation**. |

### 🔹 Examples
- `{if_user says "I washed up":Return_"Good job, you did well!"}`  
  → When the user says "I washed up," it directly outputs "Good job, you did well!"

- `{if_user says "I washed up":DO_Change user state to 'clean'}`  
  → When the user says "I washed up," it internally changes the user state to 'clean'.

**Summary:**
- `Return` → Static output for display
- `DO` → Dynamic behavior or internal processing execution



---

## 4. Why These Keywords Work

<details>
<summary>📌 Click to reveal theoretical explanation</summary>

### 3 Core Conditions for Effective Keywords:

1. **Shallow Inference Compatibility**  
   → Keywords must be interpretable even by smaller/lower-depth models.

2. **Alignment with Model Architecture**  
   → Best keywords match core mechanisms (like `Attention`).

3. **Presence in Training Corpus**  
   → Commonly seen terms in training data are more likely to be correctly interpreted.

</details>

---

## 5. Syntax Rules: Avoiding Interpretation Conflict

> Avoid using the specific combination `MUST DO NOT` in the same instruction block.
> 
> While `MUST` and `DO NOT` can each be effective on their own, combining them directly causes confusion in how the model parses semantic intent.
> 
> ❌ Problematic:
> ```
> {MUST DO NOT: ...}
> ```
> → Model may become uncertain whether `DO` belongs to `MUST` or `NOT`, leading to unstable behavior.
> 
> ✅ Recommended:
> ```
> # Absolute Priority Rule
> {DO NOT: ...}
> ```
> {must do not: ...}
> ```
> → May confuse `do` with either `must` or `not`
---

## 6. Experimental Keywords (Under Testing)

<details>
<summary>🧪 Click to expand test candidates</summary>

| Keyword | Hypothesis | Planned Usage |
|---------|------------|----------------|
| `Prompt-Negative Prompt Structure` | Dual-channel block separation for command/negation | `Command: ...` / `Negative: ...` |

</details>

---

## 7. Recommended Prompt Structures

<details>
<summary>🧠 Click to expand syntax patterns that work</summary>

### 📘 Proven Prompt Structures:

- `{Key: Value}` → universal tagging and logic
- `or`, `或` → alternate choice structure
- `{DO NOT: ...}` → strict exclusion logic
- `#`, `##`, `>` → markdown-style anchors
- `[tag]`, `>info:` → meta-output and annotation

</details>

---

## 9. Examples

<details>
<summary>✅ Click to reveal practical examples</summary>

### 9.1 Persona Setting Example
```prompt
# Session Persona Setting
name: Runa
goal: To provide useful information to the user.
personality: Kind, professional and helpful, meticulous, realistic, cynical;
---
{DO NOT: Provide incorrect information, speak assumptions as facts, make hasty conclusions}
```
*Description*: This example demonstrates how to set a chatbot's persona. The chatbot named 'Runa' aims to provide useful information to users and is defined to have a kind and professional personality. Additionally, the 'DO NOT' directive specifies behaviors to avoid, such as providing incorrect information or making hasty conclusions.

---

### 9.2 Data Sampling Specification Example
```prompt
{Must_Priority_Use_Data_Sample_Keywords: Minecraft1.12.1, script}
{DO NOT: Refer to data from other versions}

Command: Please write a script based on the Minecraft 1.12.1 economy plugin.
```
*Description*: This prompt uses 'Must_Priority_Use_Data_Sample_Keywords' to prioritize data sampling for specific keywords (Minecraft1.12.1, script). The 'DO NOT' directive restricts referencing data from other versions, ensuring the model generates a script based on the correct version.

---

### 9.3 Conditional Directive Example
```prompt
# Absolute Rule
{if_"User dances": returns_Choose only one_"Play tambourine" or "Dance together"}
{DO NOT: Execute both options simultaneously}
```
*Description*: This example shows how to set conditional directives using 'if' and 'returns'. When the user performs 'dances', the model is instructed to choose only one response between 'Play tambourine' or 'Dance together'. The 'DO NOT' directive clearly restricts executing both options simultaneously.

---

### 9.4 Mixing Numbers with DO/DO NOT Example
```prompt
# Session Goals
A core explanation of the session goals

## Session Rules
1. Instruction Title & Description
   {DO: Instruction1}
   {DO NOT: Prohibition1}

2. Second Instruction Title & Description
   {DO: Instruction2}
   {DO NOT: Prohibition2}
```
*Description*: This structure demonstrates how to clearly define session rules by mixing numbering with 'DO'/'DO NOT' directives. For each instruction, the actions to perform and actions to avoid are specified, effectively controlling the model's behavior.

</details>

---


## 8. License and Attribution

This project is licensed under the **O‑Prompt License (OPL)**.  
Adapted in spirit from the Python Software Foundation License.

Maintained by **[Rotee]** — original creator of O‑Prompt.  
Please cite or link back to this repository when referencing or redistributing any part of this project.

➡️ See the full [LICENSE](./LICENSE) for legal terms and redistribution conditions.

---

If you found O‑Prompt valuable, or you believe in the philosophy behind it,  
you can support the creator directly here:

☕ Ko-fi: https://ko-fi.com/Rotee  
💸 PayPal: https://www.paypal.me/Roteewolf  

Your support keeps this project — and me — alive. 💜



