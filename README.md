# Prompt Optimizer

> **Dual-Engine Prompt Optimization Skill** — Template matching (3,344 library) + LLM meta-prompting (host AI as optimizer). Zero API cost.

---

## 🖥️ Platform Compatibility (Read This First!)

Different platforms have different capabilities. **Find yours below and follow the recommended setup.**

### ⭐⭐⭐⭐⭐ OpenClaw (Best Experience)

| Feature | Status |
|---------|--------|
| Template Engine | ✅ Full support |
| LLM Engine | ✅ |
| Category Loading | ✅ |
| State Persistence | ✅ Auto-save config |
| Quality Evaluation | ✅ |

**Install:** Place in `skills/prompt-optimizer/` directory. OpenClaw auto-detects.
**Recommended Mode:** Template-first + LLM fallback (default). All features available.
**No limitations.**

---

### ⭐⭐⭐⭐ Claude Code

| Feature | Status |
|---------|--------|
| Template Engine | ✅ Reads local files |
| LLM Engine | ✅ |
| Category Loading | ✅ |
| State Persistence | ⚠️ In-conversation only; lost on restart |
| Quality Evaluation | ✅ |

**Install:** Copy skill folder into your project. Add to `CLAUDE.md`: `Read and follow skills/prompt-optimizer/SKILL.md`
**Recommended Mode:** Template-first (default), in-conversation state memory.
**Limitation:** Must re-enable ("开启提示词优化") each new conversation.

---

### ⭐⭐⭐½ Cursor

| Feature | Status |
|---------|--------|
| Template Engine | ✅ Reads local files |
| LLM Engine | ✅ |
| Category Loading | ✅ |
| State Persistence | ❌ No cross-session persistence |
| Quality Evaluation | ✅ |

**Install:** Copy skill folder into project root. Add to `.cursorrules`: `Read and follow skills/prompt-optimizer/SKILL.md. Activate when user says "开启提示词优化".`
**Recommended Mode:** Template-first (default).
**Limitation:** Must re-enable each session; manual file copy required.

---

### ⭐⭐⭐ Gemini CLI

| Feature | Status |
|---------|--------|
| Template Engine | ⚠️ Large files (>1MB) may truncate |
| LLM Engine | ✅ |
| Category Loading | ⚠️ Small categories recommended |
| State Persistence | ❌ None |
| Quality Evaluation | ✅ |

**Install:** Same as Cursor — place in project, reference in system instructions.
**Recommended Mode:** `"引擎设为纯LLM"` or load small categories only (Tech Tools 36KB, Translation 57KB).
**Limitation:** Free tier context is limited; large JSON may truncate. LLM-only mode recommended.

---

### ⭐⭐⭐½ Cline / AI Coding Assistants

| Feature | Status |
|---------|--------|
| Template Engine | ✅ Reads local files |
| LLM Engine | ✅ |
| Category Loading | ✅ |
| State Persistence | ❌ No cross-session persistence |
| Quality Evaluation | ✅ |

**Install:** Copy skill folder into project. Reference SKILL.md in Cline's custom instructions.
**Recommended Mode:** Template-first (default).
**Limitation:** Must re-enable each session; manual file copy required.

---

### ⭐⭐ ChatGPT Custom GPT

| Feature | Status |
|---------|--------|
| Template Engine | ❌ Cannot read JSON files |
| LLM Engine | ✅ |
| Category Loading | ❌ |
| State Persistence | ❌ |
| Quality Evaluation | ⚠️ No baseline comparison data |

**Install:** Paste the contents of `STANDALONE-GPT.md` into your Custom GPT's Instructions.
**Recommended Mode:** LLM-only (the only available mode).
**Limitation:** No template library, no category loading, no persistence. LLM optimization only.
**⚠️ Use `STANDALONE-GPT.md`, NOT `SKILL.md`.**

---

### ⭐⭐½ Aider

| Feature | Status |
|---------|--------|
| Template Engine | ⚠️ Can read files but context is tight |
| LLM Engine | ✅ |
| Category Loading | ⚠️ Small categories only |
| State Persistence | ❌ |
| Quality Evaluation | ✅ |

**Install:** Place skill folder in project. Reference with `--file`.
**Recommended Mode:** `"引擎设为纯LLM"` (saves context space).
**Limitation:** Aider is designed for code editing; general chat feels unnatural. System prompt may be too long with SKILL.md added.

---

## 📦 Installation Guide

| Platform | Files to Use | How to Install |
|----------|-------------|----------------|
| OpenClaw | `SKILL.md` + all of `references/` | Place in `skills/prompt-optimizer/` |
| Claude Code | `SKILL.md` + all of `references/` | Copy to project, reference in `CLAUDE.md` |
| Cursor | `SKILL.md` + all of `references/` | Copy to project, reference in `.cursorrules` |
| Gemini CLI | `SKILL.md` + small category JSONs | Copy to project, reference in system instructions |
| Cline | `SKILL.md` + all of `references/` | Copy to project, reference in custom instructions |
| ChatGPT GPT | `STANDALONE-GPT.md` | Paste into Custom GPT Instructions |
| Aider | `SKILL.md` | Copy to project directory |

---

## 🎯 Default Configuration

| Setting | Default | Options |
|---------|---------|---------|
| Engine | **Template-first + LLM fallback** | Template-first / LLM-only / Template-only |
| Library Version | **Lite** (~3MB, truncated at 800 chars) | Lite / Full (~10MB) |
| Category | **Coding** (1,672 prompts, ~1.5MB) | Any combination of 14 categories |
| Output Format | **Plain text** | Plain text / Markdown / XML / All |
| State | **Off by default**, manually enable | — |

---

## 🚀 Quick Start

| Action | Command |
|--------|---------|
| Enable | "开启提示词优化" (or "enable prompt optimizer") |
| Enable (Full) | "开启完整版提示词优化" |
| Disable | "关闭提示词优化" |

**Minimal usage:**
```
You: "开启提示词优化"
You: "优化这个：帮我写个登录页面"
Bot: [outputs optimized prompt]
You: "✅"
```

---

## ⚙️ All Configuration Commands

> 🌐 All commands accept any language. Just express your intent naturally — the AI will understand.

### Engine Mode

| Command | Behavior |
|---------|----------|
| "引擎设为模板优先" (default) | Search template library first; if no match, auto-fallback to LLM |
| "引擎设为纯LLM" | Skip template library; host AI optimizes directly |
| "引擎设为仅模板" | Template library only; tells user if no match found |

### Template Categories

| Command | Behavior |
|---------|----------|
| "只加载编程开发的模板" (default) | Loads only ~1.5MB |
| "加载编程+数据分析" | Load multiple categories |
| "有哪些类别可选" | Show all 14 categories |
| "加载全部类别" | Load complete library |
| "移除艺术娱乐" | Remove a loaded category |

| Category | Prompts | Size |
|----------|---------|------|
| **Coding** (default) | 1,672 | ~1.5MB |
| Art & Entertainment | 404 | ~411KB |
| Other | 253 | ~202KB |
| Writing | 208 | ~196KB |
| Education | 117 | ~107KB |
| Consulting | 114 | ~115KB |
| Business | 108 | ~98KB |
| Health & Lifestyle | 82 | ~76KB |
| Legal & Finance | 82 | ~80KB |
| Data Analysis | 73 | ~73KB |
| Creative Generation | 73 | ~66KB |
| Science & Research | 61 | ~55KB |
| Translation | 60 | ~57KB |
| Tech Tools | 37 | ~36KB |

### Output Format

| Command | Effect |
|---------|--------|
| "输出格式设为纯文本" (default) | Raw prompt text |
| "输出格式设为 Markdown" | Headings, lists, bold formatting |
| "输出格式设为 XML" | `<prompt><role>...</role></prompt>` structure |
| "输出格式设为全部" | All three formats side by side |

---

## 📋 Post-Optimization Actions

| Reply | Action |
|-------|--------|
| "✅" | Confirm and use |
| "❌" | Discard; use original input |
| Free-form feedback | Fine-tune (e.g., "add responsive design") |
| "继续优化" | Iterate another round |
| "评估" | Show before/after quality scores |
| "换格式" | Switch output format |

---

## 📊 Quality Evaluation

Say "评估" to trigger a before/after comparison. Scores 1-10 on 5 dimensions:

| Dimension | What It Measures |
|-----------|-----------------|
| goalClarity | Is the goal clear and specific? |
| instructionCompleteness | Are instructions complete and unambiguous? |
| structuralExecutability | Can the structure be executed step by step? |
| ambiguityControl | Are vague terms eliminated? |
| robustness | Will it hold up across varied inputs? |

Output: Before vs. After scores + total improvement + highlights + remaining gaps.

---

## 🧠 Four Optimization Modes

| Mode | When | What It Does |
|------|------|-------------|
| **General** (default) | Most scenarios | Structured Role/Profile/Skills/Rules/Workflows output |
| **Analytical** | Complex scenarios | 8-dimension deep analysis, 5 points per dimension |
| **Iterative** | Say "继续优化" | Merges new requirements into existing prompt |
| **User Query Refinement** | Optimizing user queries | Adds clarity, scope, parameters, output format |

---

## 🔧 Full Workflow

```
1. Enable → Detect platform capabilities → Load defaults
   ├─ File system available → Template engine ready
   └─ File system unavailable → Auto-switch to LLM-only mode
2. User submits prompt
3. Parse intent (goal, domain, role, constraints, complexity)
4. Engine routing:
   ├─ Template-first: Search → Match → CRAFT output / No match → LLM fallback
   ├─ LLM-only: Meta-prompt generates directly
   └─ Template-only: Search → Match → output / No match → notify user
5. Quality enhancement (precise instructions + constraints + examples)
6. Confirm & deliver
7. Optional: Evaluate / Iterate / Fine-tune
```

---

## 🗂️ Template Library Data

Curated from 7 major repositories, **3,344 prompts total**:

| Source | Description |
|--------|-------------|
| f/awesome-chatgpt-prompts | CSV, 5MB |
| awesome-chatgpt-prompts (original) | CSV format |
| ai-boost/awesome-prompts | 228 high-quality detailed prompts |
| 0xeb/TheBigPromptLibrary | 115 system prompts |
| jamesponddotko/llm-prompts | Categorized library |
| chatgpt-prompts-chinese | Chinese prompts |
| Prompt Garden | Community contributions |

---

## 📂 File Structure

```
prompt-optimizer/
├── SKILL.md                          # Core instructions (v4.0, full features)
├── STANDALONE-GPT.md                 # ChatGPT Custom GPT lite version
├── STANDALONE.md                     # Standalone usage guide
├── README.md                         # This file
├── references/
│   ├── prompt_library_full.json      # Full version (~10MB)
│   ├── prompt_library_lite.json      # Lite version (~3MB)
│   └── categories/                   # Split by category
│       ├── index.json
│       ├── coding.json              # Default (coding)
│       └── ... (14 categories)
└── scripts/                          # Build and maintenance scripts
```

---

## 🛡️ Features

- **Zero API Cost** — Host AI optimizes directly, no extra charges
- **Auto Platform Detection** — Graceful degradation when file system unavailable
- **Dual Engine** — Template library + LLM meta-prompting
- **Category Loading** — Load only what you need, save tokens
- **Model-Agnostic** — Works with all host AI platforms
- **Bilingual** — Chinese input → Chinese prompt; English → English
- **Quality Evaluation** — 5-dimension scoring
- **Iterative Optimization** — Multi-round fine-tuning
