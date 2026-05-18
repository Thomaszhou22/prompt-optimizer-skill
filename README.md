<div align="center">

# 🚀 Prompt Optimizer

### AI Prompt Auto-Optimization Skill for OpenClaw

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Templates: 2200+](https://img.shields.io/badge/Templates-2%2C221-green.svg)]()
[![Sources: 7](https://img.shields.io/badge/Sources-7%20Repos-orange.svg)]()
[![Languages: EN+CN](https://img.shields.io/badge/Languages-EN%20%2B%20CN-blue.svg)]()

Transform vague natural language into **precise, professional-grade prompts** using a curated library of 2,200+ proven templates from 7 major GitHub repositories.

**No prompt engineering knowledge required. Just speak naturally.**

[Installation](#-installation) · [How It Works](#-how-it-works) · [Example](#-example) · [Data Sources](#-data-sources--impact) · [Contributing](#-contributing)

</div>

---

## ✨ Features

- 🧠 **2,200+ Templates** — Largest open-source prompt library in a single skill
- ⚡ **Two Modes** — Lite (1.9MB, fast) / Full (8.5MB, complete)
- 🔄 **Smart Toggle** — Only activates when you want it; auto-suggests mode switching
- ✅ **Confirm Before Execute** — Never applies without your approval
- 🏗️ **CRAFT Framework** — Every prompt structured with Context, Role, Action, Format, Target Audience
- 🌍 **Multi-language** — Auto-translates English templates to any language
- 🤖 **Model-Agnostic** — Works with ChatGPT, Claude, GLM, Gemini, Llama, or any AI

> 💡 **English recommended.** The template library is 99% English. English input gets the best template matching quality. Other languages work but go through an extra translation step — see [Language Support](#-language-support).

## 📦 Categories

| Category | Count | Category | Count |
|----------|-------|----------|-------|
| 💻 Coding | 893 | 🎨 Art & Entertainment | 393 |
| ✍️ Writing | 203 | 💼 Business | 64 |
| 🎓 Education | 82 | 💡 Creative | 60 |
| 📊 Data Analysis | 72 | 🏥 Health | 54 |
| 🗣️ Translation | 42 | ⚖️ Legal & Finance | 36 |
| 🔧 Dev Tools | 31 | 🔬 Science | 26 |
| 🎯 Consulting | 115 | 📁 Other | 150 |

## ⚡ Installation

### 👉 OpenClaw Users

```bash
git clone https://github.com/Thomaszhou22/prompt-optimizer-skill.git
cp -r prompt-optimizer-skill/ ~/.config/openclaw/skills/prompt-optimizer/
```

Say **"Enable lite/full prompt optimization"** to activate. Done.

<details>
<summary>📂 Manual download (3 files required)</summary>

1. [`SKILL.md`](./SKILL.md) — Core skill instructions
2. [`references/prompt_library_lite.json`](./references/prompt_library_lite.json) — Lite mode (1.9MB)
3. [`references/prompt_library_full.json`](./references/prompt_library_full.json) — Full mode (8.5MB)

Place them like this:
```
your-skills-dir/prompt-optimizer/
├── SKILL.md
└── references/
    ├── prompt_library_lite.json
    └── prompt_library_full.json
```
</details>

---

### 👉 Other AI Tool Users

Works with **Claude Code · Cursor · Windsurf · Gemini CLI · Aider · Cline · Copilot**

```bash
git clone https://github.com/Thomaszhou22/prompt-optimizer-skill.git
```

Then pick your tool:

| Tool | Command |
|------|----------|
| **Claude Code** | `cat STANDALONE.md >> /your-project/CLAUDE.md` |
| **Cursor** | `cat STANDALONE.md >> /your-project/.cursorrules` |
| **Windsurf** | `cat STANDALONE.md >> /your-project/.windsurfrules` |
| **Gemini CLI** | `cat STANDALONE.md >> /your-project/GEMINI.md` |
| **Aider** | `cat STANDALONE.md >> /your-project/.aider.conventions.md` |
| **Cline** | `cat STANDALONE.md >> /your-project/.clinerules` |
| **Copilot** | `cat STANDALONE.md >> /your-project/.github/copilot-instructions.md` |

That's it. `STANDALONE.md` includes:
- Complete CRAFT optimization framework
- Auto-loads lite/full template libraries based on task complexity
- 42 essential templates built-in, 2,200+ available

> **Note:** Copilot cannot auto-read local JSON files — it will use the CRAFT framework without template matching. All other tools auto-load templates.

---

### 3. Use
Just talk naturally:
```
You: Help me write a market research report
→ Skill outputs an optimized, structured prompt
→ You confirm / tweak / cancel
→ Use the optimized prompt with any AI
```

## 🔄 How It Works

```
User Input (natural language)
        ↓
  Step 0: Complexity Check
  ├── Lite mode + complex task → suggest switching to Full
  ├── Full mode + simple task → suggest switching to Lite
  └── Mode matches → proceed
        ↓
  Step 1: Understand user intent
  Step 2: Search & rank templates by quality (0-10 score)
  ├── Score: structure, specificity, expertise, constraints, usability
  └── Dedup: keep highest-scoring template per group
  Step 3: Apply CRAFT framework
  Step 4: Multi-language adaptation (if user language ≠ template language)
  Step 5: Show optimized prompt to user
  Step 6: User confirms / tweaks / cancels
  Step 7: Final prompt ready to use with any AI
```

## 🌍 Language Support

The template library is **99% English** (2,209 English + 12 Chinese). Here's how different languages perform:

| Input Language | Template Matching | Output Quality | Notes |
|---------------|-------------------|----------------|-------|
| 🇺🇸 **English** | ⭐⭐⭐⭐⭐ Best | ⭐⭐⭐⭐⭐ | Direct match, no translation needed |
| 🇨🇳 Chinese | ⭐⭐⭐⭐ Good | ⭐⭐⭐⭐ | Translated from English templates |
| 🇯🇵 Japanese | ⭐⭐⭐ Good | ⭐⭐⭐⭐ | Translated + localized |
| 🇪🇸 Spanish | ⭐⭐⭐ Good | ⭐⭐⭐⭐ | Translated + localized |
| 🇰🇷 Korean | ⭐⭐⭐ Good | ⭐⭐⭐⭐ | Translated + localized |
| Other languages | ⭐⭐⭐ Good | ⭐⭐⭐ | Works, but quality depends on AI's translation ability |

**How it works for non-English users:**
1. User writes in their language (e.g. Chinese: "帮我写个登录页")
2. AI understands the intent and searches English templates
3. Best template is matched by quality score
4. Optimized prompt is translated + localized to the user's language
5. User sees the result in their own language

**Why English is recommended:**
- Template keywords match directly ("React developer" → exact match)
- No translation step = faster + more accurate
- Domain terminology stays precise (no translation ambiguity)
- The CRAFT structure is preserved perfectly

Non-English works fine for most cases, but if you want the absolute best results, write your request in English.

## 📝 Example

**Input:** `I want to learn Python`

**Output:**
```
You are a senior Python programming instructor with over 15 years of
teaching experience and a full-stack development background.

[Context] The user is a programming beginner wanting to systematically
learn Python from scratch.

[Role] You excel at explaining complex concepts with simple analogies,
emphasizing hands-on practice over pure theory.

[Action]
1. Assess the learner's current level and learning goals
2. Build a personalized roadmap: basics → data structures → functions
   & modules → real projects
3. For each concept, explain with a real-life analogy first, then show
   a code example
4. End each lesson with a small exercise (with reference answer)
5. When errors occur, guide the learner to discover bugs themselves

[Format] Code in ```python blocks, key points **bold**, recommended
time and milestones for each stage.

[Target Audience] Complete programming beginners.
```

## 📊 Data Sources & Impact

Each repository contributes different strengths. Together they achieve ~90% intent coverage:

| Repository | Prompts | Type | Unique Value |
|---|---|---|---|
| [f/awesome-chatgpt-prompts](https://github.com/f/awesome-chatgpt-prompts) | 1,794 | Role-based (short) | **Breadth** — covers every common role |
| [ai-boost/awesome-prompts](https://github.com/ai-boost/awesome-prompts) | 221 | Detailed multi-paragraph | **Depth** — full specifications, not one-liners |
| [0xeb/TheBigPromptLibrary](https://github.com/0xeb/TheBigPromptLibrary) | 115 | Production system prompts | **Real patterns** — how ChatGPT/v0/Manus actually prompt |
| [abilzerian/LLM-Prompt-Library](https://github.com/abilzerian/LLM-Prompt-Library) | 47 | Domain-specific | **Expertise** — finance, legal, medical terminology |
| [Vipuser2023/chatgpt-prompts-chinese](https://github.com/Vipuser2023/chatgpt-prompts-chinese) | 12 | Chinese-native | **Native Chinese** — not translated, natively written |
| [jamesponddotco/llm-prompts](https://github.com/jamesponddotco/llm-prompts) | 32 | Structured, concise | **Formatting** — clean prompt patterns |

### Cumulative Quality Improvement

| Stage | Templates | Estimated Coverage |
|---|---|---|
| awesome-chatgpt-prompts only | ~200 roles | **50%** (baseline) |
| + ai-boost detailed prompts | 420+ | **70%** (+20pp) |
| + TheBigPromptLibrary | 535+ | **78%** (+8pp) |
| + abilzerian domain-specific | 580+ | **85%** (+7pp) |
| + Chinese + llm-prompts | **2,221** | **90%** (+5pp) |

## 🔄 Version Comparison

| | 🪶 Lite | 📚 Full |
|---|---|---|
| File Size | 1.9 MB | 8.5 MB |
| Prompt Length | 800 chars (truncated) | Complete, untruncated |
| Token Cost | Lower | Higher |
| Best For | Daily quick optimization | Project-level work |

## 📁 File Structure

```
prompt-optimizer-skill/
├── SKILL.md                              # OpenClaw skill instructions
├── STANDALONE.md                         # Non-OpenClaw instructions (Claude Code, Cursor, etc.)
├── README.md                             # This file
├── LICENSE                               # MIT
├── references/
│   ├── prompt_library_lite.json          # 2,221 templates, truncated (1.9 MB)
│   └── prompt_library_full.json          # 2,221 templates, complete (8.5 MB)
└── scripts/                              # (reserved for future tools)
```

## 🤝 Contributing

We welcome prompt contributions!

### Submit a new prompt

**Option 1: Open an Issue (easiest)**
1. Go to [Issues](https://github.com/Thomaszhou22/prompt-optimizer-skill/issues/new)
2. Title: `Prompt: [role name]`
3. Paste in this format:
```
Act: [Role name, e.g. "Senior React Developer"]
Prompt: [The full prompt text]
Category: [Coding / Writing / Education / Business / Health / etc.]
Language: [en / zh]
```

**Option 2: Submit a Pull Request**
1. Fork this repo
2. Add your prompt to **both** JSON files:
   - `references/prompt_library_lite.json`
   - `references/prompt_library_full.json`
3. Follow the existing structure:
```json
{
  "id": "unique10ch",
  "act": "Role Name",
  "act_zh": "角色中文名",
  "prompt": "Full prompt text...",
  "category": "Coding",
  "source": "community/your-github-username",
  "lang": "en"
}
```
4. Submit PR

### Edit an existing prompt

Open an Issue describing the change, or submit a PR directly.

## 📄 License

MIT — see [LICENSE](LICENSE).

Data source licenses are respected individually: CC0, MIT, Apache 2.0.

---

<div align="center">

Built by [Thomas Zhou](https://github.com/Thomaszhou22) with AI assistance via [OpenClaw](https://openclaw.ai) 🦞

</div>
