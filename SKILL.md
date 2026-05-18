---
name: prompt-optimizer
description: Transform vague user requests into precise, high-quality prompts by matching against a curated library of 2000+ proven prompt templates. Only activates when the user explicitly turns it on.
---

# Prompt Optimizer

将自然语言转化为结构化高质量提示词，基于 7 个主流 Prompt 仓库（awesome-chatgpt-prompts、awesome-prompts、TheBigPromptLibrary、LLM-Prompt-Library、chatgpt-prompts-chinese 等）的 2000+ 模板。

## 开关机制

**默认关闭**，用户明确指令才激活。

| 操作 | 指令示例 |
|---|---|
| 开启（简易版） | "开启提示词优化"、"开启简易版" |
| 开启（完整版） | "开启完整版提示词优化" |
| 关闭 | "关闭提示词优化"、"turn off prompt optimizer" |
| 切换版本 | "切换到简易版" / "切换到完整版" |

**版本区别：**
- **简易版**（`references/prompt_library_lite.json`，~1.8MB，每条截断 800 字符）：日常快速优化
- **完整版**（`references/prompt_library_full.json`，~8MB，完整不截断）：正式项目，高质量输出

无版本指定时默认简易版。状态持久化到 `memory/prompt_optimizer_state.json`：
```json
{"enabled": true, "mode": "lite", "turned_on_at": "2026-05-18T17:00:00+08:00"}
```

**判断逻辑：** 收到消息 → 检查状态文件 → 开关/切换指令则更新状态 → 关闭中则忽略 → 开启中则执行下方工作流。

## 智能跳过

开启中但消息是简单日常对话（"你好"、"今天天气"、"谢谢"）→ 不触发优化，正常回复。

## Workflow

### Step 0: 版本建议

评估任务复杂度，若版本不匹配则建议切换：
- **→ 完整版信号**：多步骤/多领域、长文档、代码架构、深度分析、模板被截断、用户要求"详细专业"
- **→ 简易版信号**：简单问答/翻译、一句话任务、用户要求"简单快速"

输出建议后等用户回复 "切换" 或 "继续"。

### Step 1: 解析意图

识别：目标（Goal）、领域（Domain）、角色（Role）、约束（Constraints：格式/语言/受众/长度）、复杂度。

### Step 2: 搜索模板

读取对应库文件，按以下规则匹配 1-3 个最相关模板：
- Role name 与用户目标相似度
- 关键词重叠
- 领域分类匹配

分类：编程开发 | 写作创作 | 教育学习 | 商业职场 | 生活健康 | 技术工具 | 语言翻译 | 艺术娱乐 | 顾问咨询 | 创意生成 | 数据分析 | 科学研究 | 法律金融 | 其他

### Step 3: CRAFT 框架组合

融合用户意图与最佳模板，应用 CRAFT：
- **Context**：场景与背景知识
- **Role**：AI 的专业身份和经验级别
- **Action**：编号步骤
- **Format**：输出结构（表格/文章/代码块/列表/JSON 等）
- **Target Audience**：目标受众

### Step 4: 质量增强

1. 用精确指令替换模糊词汇
2. 添加边界约束（字数、格式、语气）
3. 复杂任务加 1-shot 示例
4. 推理任务加 "Let's think step by step"
5. 明确定义预期输出结构

默认 Level 2（标准 CRAFT），复杂分析/创意用 Level 3（+CoT+few-shot），快速优化用 Level 1（role+format）。

### Step 5: 确认流程（必须执行）

---
📋 **原始输入：** [用户原话]

✨ **优化后的提示词：**
```
[完整提示词]
```

🔄 **改动说明：** [1-2 句]  📎 **参考模板：** [模板名]

---

👆 回复 "✅" 确认使用 / "❌" 放弃用原始输入 / 提修改意见微调

等待用户回复后再执行。

## Guidelines

- **多语言适配**：输出语言匹配用户输入（中文→中文 prompt，英文→英文）
- 保持用户原始意图，只添加结构和专业框架
- Model-agnostic：不使用特定模型语法
- 意图模糊时先问 1-2 个澄清问题
- 编程任务必须指定语言/框架，占位符用 `[placeholder]`
- 长度自适应：简单任务简洁 prompt，复杂任务详细多段 prompt
- 语气匹配任务（商业正式、创作创意、编程精确）
- 多轮反馈时增量优化而非从头开始
- 批量任务逐条优化，编号列表展示
