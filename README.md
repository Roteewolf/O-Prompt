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

## 3. Confirmed Effective Keywords

| Keyword | Purpose | LLM Compatibility |
|---------|---------|--------------------|
| `DO` | Include / enforce | ✅ Excellent |
| `DO NOT` | Strict exclusion | ✅ Excellent (better than `NOT`) |
| `MUST` | Hard requirement | ✅ |
| `Use_Data_Sample_Keyword` | sampling control | ✅ |
| `Remember` | Contextual memory | ✅ |
| `Output_Format` | Response structure control | ✅ |
| `if_`, `if_condition` | Conditional logic | ✅ |
| `return_`, `return_if` | Logic result mapping | ✅ |
| `Persona` | Role-based instruction anchor | ✅ |
| `style` | Output texture control | ✅ |
| `tone` | Emotional nuance | ✅ |
| `Attention` | Focus priming signal | ✅ (partially model-dependent) |

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

## 8. License and Attribution

✅ Document maintained by **[Rotee]** — original creator of O-Prompt.
For license or usage inquiries, please cite or link back to the original repository.

