---
name: prompt-optimizer
description: Transform vague user requests into precise, high-quality prompts by matching against a curated library of 2000+ proven prompt templates from multiple GitHub repositories. Only activates when the user explicitly turns it on. Use when user says "开启提示词优化", "打开prompt优化", "turn on prompt optimizer", or "提示词优化开". When user says "关闭提示词优化", "关闭prompt优化", "turn off prompt optimizer", or "提示词优化关", deactivate it.
---

# Prompt Optimizer

Transform natural language into structured, high-quality prompts using a curated library of 2000+ proven templates from major prompt repositories.

**Data sources (7 repositories):**
- f/awesome-chatgpt-prompts
- awesome-chatgpt-prompts
- ai-boost/awesome-prompts
- 0xeb/TheBigPromptLibrary
- abilzerian/LLM-Prompt-Library
- Vipuser2023/chatgpt-prompts-chinese (中文)
- jamesponddotco/llm-prompts

## ⚠️ 开关机制（重要）

本 Skill **默认关闭**，只有在用户明确开启时才激活。

### 开启指令
**简易版（快速，省 Token）：**
- "开启简易版提示词优化" / "开启简易版prompt优化"
- "简单提示词优化"

**完整版（慢但完整，项目级使用）：**
- "开启完整版提示词优化" / "开启完整版prompt优化"
- "完整提示词优化"

**兼容旧指令（默认简易版）：**
- "开启提示词优化" / "打开提示词优化" → 简易版

### 关闭指令（任一即可）
- "关闭提示词优化" / "关掉提示词优化"
- "关闭prompt优化" / "turn off prompt optimizer"
- "提示词优化关"

### 切换版本
- "切换到简易版" / "切换到完整版"

### 版本区别
| | 简易版 | 完整版 |
|---|---|---|
| **库文件** | `references/prompt_library_lite.json` | `references/prompt_library_full.json` |
| **大小** | ~1.8 MB | ~8 MB |
| **Prompt 长度** | 每条截断 800 字符 | 完整不截断 |
| **适用场景** | 日常快速优化 | 正式项目、需要高质量输出 |
| **速度** | 快 | 稍慢 |

### 状态持久化
状态写入 `memory/prompt_optimizer_state.json`，格式：
```json
{"enabled": true, "mode": "lite", "turned_on_at": "2026-05-18T17:00:00+08:00"}
```
mode 可选：`"lite"` 或 `"full"`

### 判断逻辑
每次收到用户消息时：
1. 先检查 `memory/prompt_optimizer_state.json` 是否存在且 `enabled: true`
2. 如果是开关/切换指令 → 更新状态，回复确认
3. 如果 Skill **关闭中** → 完全忽略，正常回复用户
4. 如果 Skill **开启中** → 根据 mode 读取对应的库文件，执行下方工作流

## Workflow（仅在 Skill 开启时执行）

### Step 0: 智能版本建议

在执行优化前，先评估任务复杂度，判断当前版本是否合适：

**建议切换到完整版的信号（简易版 → 完整版）：**
- 用户的任务涉及多个步骤或多个领域
- 需要生成长文档（报告、方案、论文、商业计划书）
- 涉及代码架构、系统设计、技术方案
- 需要深度分析（竞品分析、市场调研、数据解读）
- 匹配到的模板 prompt 被截断（简易版 800 字符不够）
- 用户明确要求"详细"、"专业"、"完整方案"

**建议切换到简易版的信号（完整版 → 简易版）：**
- 用户只是简单问答、翻译、改写
- 任务一句话就能说清楚
- 用户明确要求"简单"、"快速"、"不用太复杂"

**输出格式（当检测到版本不匹配时）：**
> 💡 **版本建议**：这个任务比较[复杂/简单]，建议切换到[完整版/简易版]以获得[更完整的模板参考/更快的响应速度]。
> 回复 "切换" 即可切换，或回复 "继续" 使用当前版本。

如果用户回复 "切换" → 更新状态文件，用新版本重新执行
如果用户回复 "继续" → 忽略建议，继续当前版本

### Step 1: Understand User Intent

Parse the user's raw input. Identify:
- **Goal**: What they want to accomplish
- **Domain**: Which field/area
- **Role needed**: What kind of expert/assistant would serve best
- **Constraints**: Format, language, audience, length requirements
- **Complexity**: Simple task → concise prompt; Complex task → detailed structured prompt

### Step 2: Search the Prompt Library

根据当前模式读取对应的库文件：
- 简易版 → `references/prompt_library_lite.json`
- 完整版 → `references/prompt_library_full.json`

搜索 1-3 个最相关的模板，匹配规则：
- Role name (`act` field) similarity to user's goal
- Keyword overlap between user intent and prompt content
- Domain category alignment

Available categories:
编程开发 | 写作创作 | 教育学习 | 商业职场 | 生活健康 | 技术工具 | 语言翻译 | 艺术娱乐 | 顾问咨询 | 创意生成 | 数据分析 | 科学研究 | 法律金融 | 其他

### Step 3: Compose Optimized Prompt

Merge user intent with the best-matching template(s). Apply the CRAFT framework:

- **Context**: Set the scene — what situation, what knowledge to draw from
- **Role**: Define the AI's expertise level and persona (specific years of experience, domain expertise)
- **Action**: Numbered sequential steps the AI should follow
- **Format**: Output structure (table, essay, code block, bullet list, JSON, etc.)
- **Target Audience**: Who will consume the output

### Step 4: Quality Enhancement

Apply these prompt engineering best practices:
1. **Specificity**: Replace vague words with precise instructions
2. **Constraints**: Add boundaries (word count, format, tone)
3. **Examples**: Include 1-shot example if the task is complex
4. **Chain-of-thought**: For reasoning tasks, add "Let's think step by step"
5. **Output format**: Explicitly define the expected output structure

### Step 5: Preview & Confirm（确认流程，必须执行）

优化完成后，**先展示给用户确认**，不要直接使用。输出格式：

---
📋 **原始输入：** [用户的原话]

✨ **优化后的提示词：**
```
[优化后的完整提示词]
```

🔄 **改动说明：** [1-2 句话说明改进了什么]
📎 **参考模板：** [来源模板名称]

---
👆 **请确认或微调：**
- 回复 "✅" 或 "确认" → 使用这个提示词执行任务
- 回复 "❌" 或 "取消" → 放弃，用原始输入直接执行
- 回复修改意见（如 "加个例子"、"语气正式一点"）→ 按你的要求微调后重新展示
---

等待用户回复后，再根据用户选择执行下一步。

## Guidelines

- **Language**: Output language matches user's input language (中文→中文 prompt, English→English)
- **Preserve user intent**: Never change what the user actually wants; only add structure and expertise framing
- **Model-agnostic**: The optimized prompt must work with ANY AI model — no model-specific syntax
- **Ambiguity**: If user intent is ambiguous, ask 1-2 clarifying questions before optimizing
- **Coding tasks**: Always specify the language/framework in the prompt
- **Placeholders**: Use `[placeholder]` syntax for user-configurable parts
- **Adaptive length**: Simple tasks get concise prompts; complex tasks get detailed multi-section prompts
- **Tone matching**: Match the prompt's tone to the task (formal for business, creative for writing, precise for coding)

## Advanced Features

### Prompt Enhancement Levels
- **Level 1 (Quick)**: Add role + format to user's raw request
- **Level 2 (Standard)**: Full CRAFT framework with template matching
- **Level 3 (Expert)**: CRAFT + chain-of-thought + few-shot examples + edge case handling

Default to Level 2. Use Level 3 for complex analytical/creative tasks. Use Level 1 when the user wants a quick optimization.

### Multi-turn Optimization
If the user provides feedback on the optimized prompt ("make it more creative", "add more detail about X"), refine the prompt incrementally rather than starting from scratch.

### Batch Optimization
If the user provides multiple prompts or a list of tasks, optimize each one individually and present them in a numbered list.

### 智能跳过
如果 Skill 开启中，但用户的消息明显是简单日常对话（如 "你好"、"今天天气怎么样"、"谢谢"），不触发优化流程，正常回复即可。

## Example

**User says:** "帮我写个简历"

**Optimized output:**
```
你是一位资深职业顾问和简历专家，拥有超过20年的人力资源和职业发展经验。

**背景**：用户需要一份专业简历来申请目标职位。

**角色**：你精通各行业的简历写作规范，了解ATS（申请人追踪系统）的关键词优化，擅长将个人经历转化为有说服力的成就描述。

**步骤**：
1. 询问用户的目标职位、工作经历、教育背景和核心技能
2. 根据目标职位定制简历结构（强调相关经验和成就）
3. 用量化数据（数字、百分比、结果）描述每段工作经历
4. 优化关键词以通过ATS筛选
5. 提供中英文双语版本

**格式**：结构化简历文本，包含：个人信息摘要、核心技能、工作经历（倒序）、教育背景

**受众**：人力资源经理和招聘人员
```

**改进说明：** 从简单的"帮我写简历"升级为结构化的职业顾问角色提示词，包含明确的步骤和输出格式要求。
**参考模板：** Career Counselor（来自 awesome-chatgpt-prompts）
