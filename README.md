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
| 💻 编程开发 / Coding | 893 | 🎨 艺术娱乐 / Art & Entertainment | 393 |
| ✍️ 写作创作 / Writing | 203 | 💼 商业职场 / Business | 64 |
| 🎓 教育学习 / Education | 82 | 💡 创意生成 / Creative | 60 |
| 📊 数据分析 / Data Analysis | 72 | 🏥 生活健康 / Health | 54 |
| 🗣️ 语言翻译 / Translation | 42 | ⚖️ 法律金融 / Legal & Finance | 36 |
| 🔧 技术工具 / Dev Tools | 31 | 🔬 科学研究 / Science | 26 |
| 🎯 顾问咨询 / Consulting | 115 | 📁 其他 / Other | 150 |

## ⚡ Quick Start

### 1. Install
```bash
# Clone the repo
git clone https://github.com/Thomaszhou22/prompt-optimizer-skill.git

# Copy to your OpenClaw skills directory
cp -r prompt-optimizer-skill/ ~/.config/openclaw/skills/prompt-optimizer/
```

<details>
<summary>📂 Alternative: Manual download (3 files required)</summary>

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
- **"开启简易版提示词优化"** → Lite mode (fast, saves tokens)
- **"开启完整版提示词优化"** → Full mode (maximum quality)

### 3. Use
Just talk naturally:
```
You: 帮我写一份市场调研报告
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

**Input:** `我想学Python`

**Output:**
```
你是一位资深 Python 编程导师，拥有超过 15 年的编程教学经验。

【背景】用户是编程初学者，希望从零开始系统学习 Python。

【角色】你善于将复杂概念用简单类比解释，注重实践而非纯理论。

【步骤】
1. 先了解学员的基础水平和学习目标
2. 制定个性化学习路线图：基础语法 → 数据结构 → 函数与模块 → 项目实战
3. 每个知识点先用生活类比解释，再给代码示例
4. 每节课末尾布置小练习（带参考答案）
5. 遇到错误时引导学员自己发现 bug

【格式】代码用 ```python 代码块，重点 **加粗**，每阶段推荐时长和里程碑

【受众】零基础编程初学者
```

## 📊 Data Sources & Impact

Each repository contributes different strengths. Together they achieve ~90% intent coverage:

| Repository | Prompts | Type | Unique Value |
|---|---|---|---|
| [f/awesome-chatgpt-prompts](https://github.com/f/awesome-chatgpt-prompts) | 1,794 | Role-based (short) | **Breadth** — covers every common role |
| [ai-boost/awesome-prompts](https://github.com/ai-boost/awesome-prompts) | 221 | Detailed multi-paragraph | **Depth** — full specifications, not one-liners |
| [0xeb/TheBigPromptLibrary](https://github.com/0xeb/TheBigPromptLibrary) | 115 | Production system prompts | **Real patterns** — how ChatGPT/v0/Manus actually prompt |
| [abilzerian/LLM-Prompt-Library](https://github.com/abilzerian/LLM-Prompt-Library) | 47 | Domain-specific | **Expertise** — finance, legal, medical terminology |
| [Vipuser2023/chatgpt-prompts-chinese](https://github.com/Vipuser2023/chatgpt-prompts-chinese) | 12 | Chinese-native | **中文原生** — not translated, natively written |
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
