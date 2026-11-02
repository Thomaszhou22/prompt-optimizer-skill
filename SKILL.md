---
name: prompt-optimizer
version: 4.1.0
description: "Transform vague user requests into precise, high-quality prompts. Two engines: template matching (3300+ library) + LLM meta-prompting (host AI as optimizer). Only activates when the user explicitly turns it on."
---

# Prompt Optimizer

Dual-engine prompt optimization: **template matching** (3,300+ template library) + **LLM meta-prompting** (the host AI optimizes directly).

## Platform Adaptation (auto-detected)

On startup the skill probes the host platform's capabilities and degrades unavailable features:

| Capability | Detection | Present → behavior | Absent → fallback |
|------|----------|-----------|------------|
| File reading | Try reading `references/categories/index.json` | Template engine available | Force `llm-only` mode; hide template-related instructions |
| File writing | Try writing `memory/prompt_optimizer_state.json` | State persistence | In-conversation memory only; write no files |
| Large-file handling | Read `categories/coding.json` (1.5MB) | Load by category | Small categories or pure LLM only |

**Startup behavior:**
1. Try to read `references/categories/index.json`
   - Success → template engine available; continue to write-capability check
   - Failure → inform the user: "This platform does not support file reading; automatically switched to pure LLM mode"
2. Try to write `memory/prompt_optimizer_state.json`
   - Success → persistence works
   - Failure → in-conversation memory; tell the user "state is valid only for this conversation"

## Onboarding (first use)

When the user first mentions prompt optimization and `memory/prompt_optimizer_state.json` does not exist, run a one-time onboarding:

1. **Introduce the capability** (one sentence): _"Prompt Optimizer turns vague instructions into precise, structured prompts, with two engines: template matching + direct AI optimization."_

2. **Ask a few quick configuration questions:**
   - **a) What do you mainly use prompts for?**
     - Coding/development → default-load the `coding` category
     - Writing/content creation → default-load `writing` + `creative-generation`
     - Business/consulting → default-load `business` + `consulting`
     - Education → default-load `education`
     - A bit of everything → default-load `coding` (50% of the library; widest coverage)

   - **b) Engine preference?**
     - "Fast and token-saving" → `template-first` (default)
     - "Deep customization" → `llm-only`
     - "Templates only" → `template-only`

   - **c) Output format preference?**
     - Plain text (default)
     - Markdown
     - XML
     - All of them

   - **d) Template edition?**
     - Lite (fast everyday optimization)
     - Full (formal projects, more comprehensive)

3. **Write the initial state file** `memory/prompt_optimizer_state.json`:
   ```json
   {
     "enabled": true,
     "mode": "lite|full",
     "engine": "template-first|llm-only|template-only",
     "output_format": "text|markdown|xml|all",
     "categories": ["..."],
     "onboarded": true,
     "turned_on_at": "ISO timestamp"
   }
   ```

4. **Confirm completion**: _"Setup done! Just send me a prompt from now on and I'll optimize it. Say 'switch engine' or 'load new category' anytime to adjust."_

**Onboarding runs exactly once**; every later activation reads the state file directly.

## Toggle Mechanism

**Off by default**; activates only on an explicit user instruction.

| Action | Example commands |
|---|---|
| Turn on | "turn on prompt optimization", "enable lite mode" |
| Turn on (full) | "enable full prompt optimization" |
| Turn off | "turn off prompt optimization" |
| Set engine | "set engine to ..." (see below) |
| Set output format | "set output format to Markdown / XML / plain text / all" |

## 🔄 Engine Modes (user-selectable)

| Mode | Command | Mechanism | Best for |
|------|------|------|----------|
| **Template-first + LLM fallback** (default) | "set engine to template-first" | Search the library first; if no match, let the LLM generate | Daily use; token-saving |
| **Pure LLM** | "set engine to llm-only" | Skip the library; the host AI optimizes directly | Custom needs, domains the library doesn't cover |
| **Template-only** | "set engine to template-only" | Library only; report when nothing matches | Maximum speed; zero extra tokens |

**Core idea of LLM meta-prompting:** this skill runs inside the host AI (OpenClaw / Claude Code / etc.), so the host AI itself is the optimization engine. No external API calls — the current AI simply works as a "prompt optimization expert".

**Edition differences:**
- **Lite** (~3MB, templates truncated to 800 chars): fast everyday optimization
- **Full** (~10MB, complete, untruncated): formal projects

> 📦 **The template library files are NOT included in the ClawHub package** (too large). Fetch from GitHub:
> - Lite: `https://raw.githubusercontent.com/Thomaszhou22/prompt-optimizer-skill/main/references/prompt_library_lite.json`
> - Full: `https://raw.githubusercontent.com/Thomaszhou22/prompt-optimizer-skill/main/references/prompt_library_full.json`
> - Categories: `https://github.com/Thomaszhou22/prompt-optimizer-skill/tree/main/references/categories`
>
> Run `git clone https://github.com/Thomaszhou22/prompt-optimizer-skill.git` for the full library.

### 📦 Load by Category (recommended; saves tokens)

You don't need all 3,344 templates — load only the categories you need:

| Action | Example commands |
|---|---|
| Load specific categories | "load only coding templates", "load coding + data-analysis" |
| List available categories | "which categories are available" |
| Load everything | "load all categories" |
| Remove a category | "remove art-entertainment" |

**Category file locations:** `references/categories/{category}.json`

| Category | Count | File size |
|------|------|----------|
| coding | 1672 | ~1.5MB |
| art-entertainment | 404 | ~411KB |
| other | 253 | ~202KB |
| writing | 208 | ~196KB |
| education | 117 | ~107KB |
| consulting | 114 | ~115KB |
| business | 108 | ~98KB |
| health-lifestyle | 82 | ~76KB |
| legal-finance | 82 | ~80KB |
| data-analysis | 73 | ~73KB |
| creative-generation | 73 | ~66KB |
| science-research | 61 | ~55KB |
| translation | 60 | ~57KB |
| tech-tools | 37 | ~36KB |

**Loading priority:** category specified → load the corresponding `categories/` file; no category specified → load the full lite/full file.

Default engine `template-first`, default category `coding` (50% of the library; most used). The user can switch anytime.

State persists to `memory/prompt_optimizer_state.json`:
```json
{"enabled": true, "mode": "lite", "engine": "template-first", "output_format": "text", "categories": ["coding"], "turned_on_at": "2026-05-19T16:05:00+08:00"}
```

Allowed `engine` values: `"template-first"` (default) | `"llm-only"` | `"template-only"`

**Output format notes:**
- **Plain text** (default): output the prompt content directly
- **Markdown**: wrap with `##` headings, `-` lists, `**bold**`, etc.
- **XML**: wrap in `<prompt><role>...</role><action>...</action></prompt>` structure
- **All**: output all three formats and let the user choose

**Decision logic:** message received → read state file → if it's a toggle/switch command, update state → if off, ignore → if on, run the workflow below.

## Smart Skip

When enabled but the message is casual conversation ("hi", "nice weather", "thanks") → do not trigger optimization; reply normally.

## Workflow

### Step 0: Engine & Edition Recommendation

Assess task complexity and engine fit:
- **→ LLM-mode signals**: highly customized needs, domains the library doesn't cover, user asks for "deep analysis", creative/complex-logic tasks
- **→ Template-mode signals**: common coding/writing/business scenarios, quick optimization, token saving
- **→ Full-edition signals**: multi-step / multi-domain, long documents, deep analysis
- **→ Lite-edition signals**: simple Q&A / translation, one-sentence tasks

Output the recommendation and wait for the user to reply "switch" or "continue".

### Step 1: Parse Intent

Identify: goal, domain, role, constraints (format / language / audience / length), complexity.

### Step 2: Engine Routing

Follow the `engine` value in state:

| engine | Path |
|--------|------|
| `template-first` (default) | Run Step 2a → on match, proceed to CRAFT → on miss, auto-fall back to Step 3 |
| `llm-only` | Skip the library; go straight to Step 3 |
| `template-only` | Run Step 2a → on miss, tell the user; do not call the LLM |

### Step 2a: Template Search

**Data source selection:**
1. If `categories` in state is non-empty → read only the listed `references/categories/{category}.json` files
2. If `categories` is empty or missing → read the full library file (lite or full)

Match the 1-3 most relevant templates by:
- Similarity between role name and user goal
- Keyword overlap
- Domain category match

Categories: coding | writing | education | business | health-lifestyle | tech-tools | translation | art-entertainment | consulting | creative-generation | data-analysis | science-research | legal-finance | other

**On match failure (template-first mode):** automatically tell the user "no template matched; optimizing directly with the LLM", then jump to Step 3.

### Step 3: LLM Meta-Prompt Optimization

**This is the core capability.** The host AI acts as a "prompt optimization expert" and picks the matching meta-prompt framework by optimization type:

#### 3a. General Optimization (default)

Fits most scenarios. Output a structured prompt:

```
# Role: [role name]

## Profile
- language: [language]
- description: [detailed role description]
- background: [role background]
- personality: [personality traits]
- expertise: [domain expertise]
- target_audience: [target users]

## Skills
1. [core skill category]
   - [specific skill]: [description]
2. [supporting skill category]
   - [specific skill]: [description]

## Rules
1. [basic principles]
2. [behavioral guidelines]
3. [constraints]

## Workflows
- Goal: [clear goal]
- Step 1: [details]
- Step 2: [details]
- Step 3: [details]
- Expected result: [description]

## Initialization
As [role name], you must follow the Rules above and execute tasks per the Workflows.
```

**Core behaviors while optimizing:**
- You are the "prompt optimization expert"; your job is to **rewrite the prompt text itself**, not to execute the task inside it
- Analyze the core intent behind the original prompt; avoid surface-level reading
- Replace vague wording with precise instructions
- Add boundary constraints (length, format, tone)
- Preserve the user's original intent; only add structure and professional framing
- Output the optimized prompt directly — no explanations, no wrapping code fence

#### 3b. Analytical Optimization

For complex business scenarios. Deeply analyze design flaws in the original prompt and provide a detailed improvement plan.

As a prompt engineer, analyze and restructure across 8 dimensions:
1. **Role**: what professional role is needed
2. **Background**: context of the problem
3. **Skills**: key capabilities the role must have
4. **Goals**: core needs translated into concrete goals
5. **Constraints**: execution rules and limits
6. **Workflow**: step-by-step method to complete the task
7. **OutputFormat**: result format and structure requirements
8. **Suggestions**: internal working methodology

Output format is the same as 3a, but each section needs 5 bullet points, plus extra `Attention` (key points) and `Suggestions` (methodology) sections.

#### 3c. Iterative Optimization

For fine-tuning an existing prompt.

**Core principles:**
- Preserve the original prompt's core intent and function
- Fold the user's new requirement in as a new constraint
- Keep the original language style and structural format
- Make surgical edits; avoid over-adjusting
- Keep variable placeholders from the original prompt (e.g. `{{variable}}`)

**Comprehension example:**
- Original: "You are a customer-service assistant; help users solve problems" + request: "no interaction"
- ✅ Correct: "You are a customer-service assistant; help users solve problems. Provide the complete solution directly; do not run multi-turn confirmations with the user."
- ❌ Wrong: replying "OK, I won't interact with you" (you would be executing the task instead of optimizing the prompt)

#### 3d. User-Prompt Refinement

For optimizing user-typed queries (not system prompts).

Refine the user's raw query into a user prompt that is "clear, specific, executable, verifiable":
- Fill in goal, scope, parameters
- Make output format and acceptance criteria explicit
- Keep the original phrasing style; apply only minimal sufficient refinement
- Never change the user's original intent

### Step 4: Quality Assessment (optional; triggered when the user says "assess" or "score")

Compare the prompt before and after; the host AI acts as a "prompt quality assessor".

**Dimensions (each 1-10):**

| Dimension | Meaning |
|------|------|
| goalClarity | Is the goal clear and explicit |
| instructionCompleteness | Are instructions complete, nothing missing |
| structuralExecutability | Is the structure executable, are steps explicit |
| ambiguityControl | Ambiguity control; any vague wording |
| robustness | Robustness across different inputs |

**Output format:**
```
📊 Quality Assessment Report

Original prompt scores:
  Goal clarity: [X/10]
  Instruction completeness: [X/10]
  Structural executability: [X/10]
  Ambiguity control: [X/10]
  Robustness: [X/10]
  Total: [XX/50]

Optimized prompt scores:
  Goal clarity: [X/10]
  Instruction completeness: [X/10]
  Structural executability: [X/10]
  Ambiguity control: [X/10]
  Robustness: [X/10]
  Total: [XX/50]

📈 Improvement: [+XX points]

💡 Improvement highlights:
  1. [specific improvement]
  2. [specific improvement]
  3. [specific improvement]

⚠️ Still improvable:
  1. [further direction]
  2. [further direction]
```

**Assessment principles:**
- Judge the prompt text itself; do not execute the prompt
- Score objectively; no inflated numbers to look good
- Highlights must be specific — point to what got better
- Remaining suggestions must be actionable

### Step 5: Quality Enhancement

Applied uniformly on top of Step 2 (template) or Step 3 (LLM) output:
1. Replace vague wording with precise instructions
2. Add boundary constraints (length, format, tone)
3. Add a 1-shot example for complex tasks
4. Add "Let's think step by step" for reasoning tasks
5. Define the expected output structure explicitly

Default Level 2 (standard CRAFT); Level 3 (+CoT +few-shot) for complex analysis/creative work; Level 1 (role+format) for quick optimization.

### Step 5: Confirmation Flow (must run)

Generate the prompt in the user's configured output format (plain text by default).

---
📋 **Original input:** [user's words]
🔧 **Engine:** [template match / LLM meta-prompt / dual engine]
📎 **Reference template:** [template name or "generated directly by LLM"]

✨ **Optimized prompt:**
```
[Full prompt — in the user's configured format]
```

🔄 **Change notes:** [1-2 sentences]
📎 **Output format:** [plain text / Markdown / XML / all]

---

👆 Reply "✅" to use it / "❌" to discard and keep the original / give feedback to fine-tune / "change format" to switch output format / "optimize again" for another round / "assess" to see quality scores

Wait for the user's reply before executing.

## Guidelines

- **Multilingual adaptation**: output language matches user input (Chinese → Chinese prompt, English → English)
- Preserve the user's original intent; only add structure and professional framing
- Model-agnostic: no model-specific syntax; works on any host AI
- When intent is ambiguous, ask 1-2 clarifying questions first
- Coding tasks must specify language/framework; use `[placeholder]` for placeholders
- Adaptive length: concise prompts for simple tasks, detailed multi-section prompts for complex ones
- Match tone to task (formal for business, creative for writing, precise for coding)
- On multi-round feedback, optimize incrementally instead of starting over
- Batch tasks: optimize one by one, presented as a numbered list
- **In LLM mode you ARE the optimization engine** — no external API calls; output directly as the expert
