# 民商事谈案方案（client-pitch）

一个面向**中国大陆民商事争议解决律师**的 Agent Skill，用于根据案件材料和客户目标，整理案件判断、设计可行的处理路径，并形成适合与客户沟通的谈案方案。

它关注的不只是“能否起诉”，还包括：**为什么选择这条路径、律师具体做什么、客户需要配合什么，以及方案何时需要调整**。

> 本项目是辅助律师开展案件分析与客户沟通的工作流指令，不是法律意见的自动核验工具，也不替代执业律师对事实、证据及现行法律的独立判断。

## 适用场景

- **初次接案与谈案**：根据客户陈述和现有材料，形成便于沟通的初步处理建议。
- **诉讼服务方案**：围绕争议焦点、主要证据和对方抗辩，明确诉前、诉中、诉后的律师工作。
- **多路径选择**：比较起诉、协商和解、分期履行等具有实际选择意义的路线，说明优先顺序和切换条件。
- **方案精简**：按要求提供适合微信沟通的简版谈案方案。

例如，可用于民间借贷、买卖合同、建设工程及公司商事争议等民商事案件。具体分析仍取决于输入事实、证据及可核验的规则。

## 核心工作方式

1. **先核实决策信息**：梳理客户身份与目标、争议关系、关键金额、已有证据、主要抗辩以及可执行财产线索；区分已获材料支持的事实、客户陈述和待核事项。
2. **再选择处理路径**：根据现有材料选择一条优先路线；如确有不同可行路径，则比较其适用条件、证据把握、时间、费用和风险，不为凑方案数量而机械拆分。
3. **按阶段安排律师工作**：从诉前、诉中、诉后三个阶段说明拟开展的事项，重点写清“做什么、为什么重要、交付什么”。
4. **形成客户能看懂的方案**：突出建议、主要风险、客户配合事项和下一步行动，避免将谈案材料写成冗长的法条罗列。

Skill 的完整指令见 [`skills/client-pitch/SKILL.md`](skills/client-pitch/SKILL.md)。

## 安装与调用

各平台使用同一份 [`SKILL.md`](skills/client-pitch/SKILL.md)。它包含技能名称、适用范围和工作指令，可以独立使用，无需脚本或 API 密钥。`agents/openai.yaml` 用于 Codex 界面展示。[Agent Skills 格式规范](https://agentskills.io/specification)

### 腾讯 WorkBuddy

在 GitHub 打开 [`SKILL.md`](skills/client-pitch/SKILL.md) 并下载原始文件。在 WorkBuddy 的技能页面依次选择「添加技能」和「上传技能」，上传下载的 `SKILL.md`。导入后，从聊天里的已安装技能列表选中 `client-pitch`，再提供案情和客户目标。[WorkBuddy 安装文档](https://intl.cloud.tencent.com/zh/document/product/1316/84503) · [上传格式示例](https://main.qcloudimg.com/raw/document/product/pdf/862_129183_cn.pdf#page=5)

### Codex

将项目发布到 GitHub 后，在 **Codex 聊天窗口**输入（不是在 Mac 终端输入）：

```text
用 $skill-installer 安装 https://github.com/yyovo1219/civil-litigation-strategy-skill/tree/main/skills/client-pitch
```

示例链接对应 `yyovo1219/civil-litigation-strategy-skill` 的 `main` 分支。**请先确认链接能打开仓库中的 `skills/client-pitch` 目录。** 如果实际仓库或分支不同，请打开对应目录并复制地址栏中的链接。

安装完成后，在 Codex 对话中输入 `$client-pitch` 并提供案情。若当前会话未显示该 Skill，打开新的 Codex 会话再试。

### Claude Code

将 `SKILL.md` 保存为 `~/.claude/skills/client-pitch/SKILL.md`，然后在 Claude Code 中输入 `/client-pitch`。如果只想在一个项目内使用，可放到项目的 `.claude/skills/client-pitch/SKILL.md`。[Claude Code 技能文档](https://code.claude.com/docs/en/skills)

### Kimi Code CLI

将 `SKILL.md` 保存为 `~/.agents/skills/client-pitch/SKILL.md`，然后在 Kimi Code CLI 中输入 `/skill:client-pitch`。[Kimi Code CLI 技能文档](https://www.kimi.com/code/docs/kimi-code-cli/customization/skills.html)

## 使用示例

以下均为**虚构情境**。先按平台说明调用技能，再发送示例中的案情和要求。

### 示例一：单方案——买卖合同货款追收

> 为供货商客户写一份谈案方案。现有对账单显示欠款90万元，之后收到两笔回款共15万元；买方仍在营业，客户希望尽快收款。请依据现有材料提出优先处理路径，明确仍需补充的证据，并按诉前、诉中、诉后说明律师工作。

### 示例二：多方案——立即起诉还是协商分期

> 比较“立即起诉”和“限期协商分期”两条路线。买方承认尚欠60万元，提出分四期支付，但没有提供担保。请比较两条路线的适用条件、证据把握、时间和回款风险，明确优先建议、第一步行动及切换条件。

**预期的方案组织方式**（具体内容随案件和用户要求调整）：案件判断 → 处理路径 → 诉前／诉中／诉后工作 → 风险与客户配合 → 最终建议。它不是固定模板，实际输出以案情和指令为准。

## 仓库结构

```text
.
├── README.md
└── skills/
    └── client-pitch/
        ├── SKILL.md
        └── agents/
            └── openai.yaml
```

## 使用提示

- **保护隐私**：在公开展示、分享或提交演示材料前，对当事人身份信息、联系方式、银行账户、商业秘密等进行脱敏；不要将真实案件材料直接放入公开仓库。
- **核验法律依据**：具体法条、裁判规则、程序期限、费用标准等应以现行权威来源为准；没有检索条件时，不应将未经核实的信息当作已核验结论。
- **保留专业判断**：本 Skill 提供工作流和文稿辅助。胜诉、保全和实际回款受个案事实及程序进展影响，立案、保全申请等事项由律师按案情办理。
