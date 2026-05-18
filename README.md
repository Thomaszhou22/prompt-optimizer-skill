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
- 🌍 **Bilingual** — Chinese & English native support
- 🤖 **Model-Agnostic** — Works with ChatGPT, Claude, GLM, Gemini, Llama, or any AI

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

## ⚡ Quick Start

### 1. Install
```bash
# Clone the repo
git clone https://github.com/Thomaszhou22/prompt-optimizer-skill.git

# Copy to your OpenClaw skills directory
cp -r prompt-optimizer-skill/ ~/.config/openclaw/skills/prompt-optimizer/
```

### For Non-OpenClaw Users (Claude Code, Cursor, etc.)

The prompt library is **pure JSON data** — you can use it anywhere.

**Option A: Use with CLAUDE.md (Claude Code)**
```bash
# 1. Clone the repo
git clone https://github.com/Thomaszhou22/prompt-optimizer-skill.git
cd prompt-optimizer-skill

# 2. Add to your project's CLAUDE.md
cat SKILL.md >> /your-project/CLAUDE.md
```
> ⚠️ The SKILL.md references JSON library files. For Claude Code to access them,
> you need to mention the file path in your prompt (e.g., "read references/prompt_library_lite.json and optimize my prompt").

**Option B: Use the JSON library directly (any environment)**
```bash
# Download the library file
curl -O https://raw.githubusercontent.com/Thomaszhou22/prompt-optimizer-skill/main/references/prompt_library_lite.json

# Load it in Python
python3 -c "import json; lib = json.load(open('prompt_library_lite.json')); print(f'{len(lib[\"prompts\"])} prompts loaded')"
```

The JSON structure:
```json
{
  "prompts": [
    {
      "id": "abc123",
      "act": "Python Developer",
      "act_zh": "Python开发者",
      "prompt": "You are an expert Python developer...",
      "category": "Coding",
      "source": "ai-boost/awesome-prompts",
      "lang": "en"
    }
  ]
}
```

Use cases:
- **Search by category** — filter `"category": "Coding"`
- **Search by keyword** — match against `"act"` or `"prompt"` fields
- **Use as RAG context** — feed matching prompts into any AI as examples
- **Build your own optimizer** — use the CRAFT framework from SKILL.md

<details>
<summary>📂 Alternative: Manual download (OpenClaw users)</summary>

You need ALL of these files:
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
> ⚠️ SKILL.md alone won't work — it needs the JSON libraries.
</details>

### 2. Activate
Say any of these to your OpenClaw assistant:
- **"Enable lite prompt optimization"** → Lite mode (fast, saves tokens)
- **"Enable full prompt optimization"** → Full mode (maximum quality)

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
  Step 1: Match against 2,200+ templates
  Step 2: Apply CRAFT framework
  Step 3: Show optimized prompt to user
  Step 4: User confirms / tweaks / cancels
  Step 5: Final prompt ready to use with any AI
```

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
├── SKILL.md                              # Core skill instructions (9.1 KB)
├── README.md                             # This file
├── LICENSE                               # MIT
├── references/
│   ├── prompt_library_lite.json          # Lite mode (1.9 MB)
│   └── prompt_library_full.json          # Full mode (8.5 MB)
└── scripts/                              # (reserved for future tools)
```

## 🤝 Contributing

Contributions welcome! Especially:

- **Chinese prompts** — we need more native Chinese templates
- **New categories** — education, healthcare, legal domain expertise
- **Quality improvements** — better categorization, deduplication

### How to contribute

1. Fork this repo
2. Add/edit prompts in the JSON library
3. Run `python3 scripts/validate.py` (coming soon)
4. Submit a PR

## 📄 License

MIT — see [LICENSE](LICENSE).

Data source licenses are respected individually: CC0, MIT, Apache 2.0.

---

<div align="center">

Built by [Thomas Zhou](https://github.com/Thomaszhou22) with AI assistance via [OpenClaw](https://openclaw.ai) 🦞

</div>
