# Project Skill Autolearn

[English](README.md) | [中文](README.zh-CN.md)

`project-skill-autolearn` 是一个全局 Claude Code Skill，用来把当前项目里可复用的流程沉淀成项目本地、带索引、按需加载的 Skill。

它适合保存项目特定的调试路径、验证流程、恢复步骤，或者可以脚本化的小型重复检查。目标是让这些知识在当前项目中可复用、可共享，但不会在每次请求中都被加载。

## 为什么需要它

项目工作经常会暴露一些有用流程，但这些流程又太项目化，不适合变成全局 Skill：

- 调试某个不稳定子系统
- 从已知的 codegen 失败中恢复
- 验证某类高风险改动
- 确认生成文件真正来自哪里
- 把重复的人工检查包装成脚本

这个 Skill 会把这些流程保存在当前仓库里，并用 `SkillsDs.md` 建立索引。后续 Agent 只在需要时扫描索引，然后加载一个匹配的 `SKILL.md`。

## 会创建什么

直接调用后，它会先初始化当前项目：

```text
<project>/
  .claude/
    skills/
  SkillsDs.md
```

如果某个流程通过门槛判断，它会创建项目本地 Skill：

```text
<project>/
  .claude/
    skills/
      <project-skill-name>/
        SKILL.md
        scripts/        # 可选，仅脚本型 Skill 需要
  SkillsDs.md
```

全局 Skill 只提供学习流程，真正学到的流程留在各自项目里。

## 会保存什么

候选内容必须是项目本地的、条件式的、有证据验证的、未来可复用的、具体可执行的、安全可记录的，并且没有被项目说明、`SkillsDs.md` 或已有 Skill 覆盖。

适合保存：

- 当前项目特有的调试 playbook
- 针对某类变更的验证流程
- 和当前仓库绑定的 codegen 恢复流程
- 可以安全验证的小型自动化脚本
- 未来 Agent 可能再次犯错的纠正假设

不适合保存：

- 一次性任务结果
- 原始日志、堆栈、临时快照
- 泛泛的工程建议
- 应该写在项目说明里的宽泛硬规则
- 密钥、私有日志、客户数据或敏感信息

## 脚本型 Skill

有些 Skill 可以包含代码。如果某个流程稳定、重复、机械、容易手动做错，`project-skill-autolearn` 可以把它包装成：

```text
.claude/skills/<skill-name>/
  SKILL.md
  scripts/
    <script-file>
```

脚本负责自动化易错部分，`SKILL.md` 仍然负责说明什么时候用、如何运行、验证什么、如何理解结果。

## Token 模型

这个 Skill 使用渐进加载：

- frontmatter 用于发现
- 主 `SKILL.md` 只保留核心 review loop
- 模板和脚本型 Skill 规则放在 `references/`
- 只有需要时才读取 reference

当前大致体量：

| 文件 | 词数 |
| --- | ---: |
| `SKILL.md` | ~640 |
| `references/project-index-template.md` | ~160 |
| `references/project-skill-template.md` | ~220 |
| `references/scripted-skills.md` | ~310 |

直接调用时加载主 Skill。创建索引、新 Skill 或脚本型 Skill 时，只加载对应 reference。

## 安装为 Claude Code marketplace

在 Claude Code 中添加 marketplace：

```text
/plugin marketplace add YOUR_NAME/project-skill-autolearn
```

安装插件：

```text
/plugin install project-skill-autolearn@project-skill-autolearn
```

检查是否可用：

```text
/skills
```

通过 marketplace 安装的插件 Skill 通常带命名空间，直接调用一般使用：

```text
/project-skill-autolearn:project-skill-autolearn
```

## 手动安装

克隆仓库：

```bash
git clone https://github.com/YOUR_NAME/project-skill-autolearn.git
```

复制 standalone Skill：

```bash
mkdir -p ~/.claude/skills
cp -R project-skill-autolearn/.claude/skills/project-skill-autolearn ~/.claude/skills/
```

Windows PowerShell：

```powershell
git clone https://github.com/YOUR_NAME/project-skill-autolearn.git
New-Item -ItemType Directory -Force "$HOME\.claude\skills" | Out-Null
Copy-Item -Recurse ".\project-skill-autolearn\.claude\skills\project-skill-autolearn" "$HOME\.claude\skills\project-skill-autolearn"
```

重启 Claude Code，或运行 `/skills` 检查。

## 使用方式

直接调用：

```text
/project-skill-autolearn:project-skill-autolearn
```

也可以自然语言调用：

```text
Use project-skill-autolearn to review this session and preserve any reusable conditional workflow.
```

直接调用后，它应该在当前对话中保持激活，并在非平凡任务的最终回复前做 review。

## 仓库结构

```text
.claude-plugin/marketplace.json
plugins/project-skill-autolearn/
  .claude-plugin/plugin.json
  skills/project-skill-autolearn/
    SKILL.md
    references/
.claude/skills/project-skill-autolearn/
  SKILL.md
  references/
skills/project-skill-autolearn/
  SKILL.md
  references/
```

- `plugins/project-skill-autolearn/` 用于 marketplace 安装。
- `.claude/skills/project-skill-autolearn/` 是 standalone 手动安装副本。
- `skills/project-skill-autolearn/` 兼容使用普通 `skills/` 目录的 Agent。

编辑时需要保持三份 Skill 目录同步，包括 `SKILL.md` 和 `references/`。

## 验证

验证 marketplace 结构：

```text
/plugin validate .
```

或者在有 Claude Code 的 shell 中运行：

```bash
claude plugin validate .
```

## 参考

- [Claude Code plugin marketplaces](https://docs.claude.com/en/docs/claude-code/plugin-marketplaces)
- [Claude Code skills](https://docs.claude.com/en/docs/claude-code/skills)

## 许可证

MIT
