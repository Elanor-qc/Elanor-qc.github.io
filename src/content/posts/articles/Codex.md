---
title: "Codex 备忘"
description: "Codex是我最好的工作搭子ヾ(≧▽≦*)o"
pubDatetime: 2026-08-10T18:00:00+08:00
tags:
  - Note
  - Tech
featured: false
draft: false
---

# Codex CLI 一页速记

## 终端命令

| 命令                                 | 用途                         |
| ---------------------------------- | -------------------------- |
| `codex`                            | 启动交互式 Codex                |
| `codex "任务"`                       | 启动并直接发送任务                  |
| `codex -m <model>`                 | 指定模型启动                     |
| `codex -C <dir>`                   | 指定工作目录                     |
| `codex --search`                   | 开启实时 Web 搜索                |
| `codex resume`                     | 打开历史会话选择器                  |
| `codex resume --last`              | 继续当前目录最近会话                 |
| `codex resume --all`               | 查找所有目录的历史会话                |
| `codex resume <id/名称>`             | 继续指定会话                     |
| `codex fork`                       | 从历史会话创建分支                  |
| `codex exec "任务"` / `codex e "任务"` | 非交互执行，适合脚本/CI              |
| `codex review`                     | 非交互代码 Review               |
| `codex doctor`                     | 检查安装 / 配置 / Auth / Git 等问题 |
| `codex update`                     | 更新 Codex CLI               |
| `codex login` / `codex logout`     | 登录 / 登出                    |
| `codex mcp`                        | 管理 MCP Server              |
| `codex completion`                 | 生成 shell 自动补全              |

### 常用启动参数

```bash
codex -m <model>           # 指定模型
codex -C ./project         # 指定目录
codex -s read-only         # 只读 sandbox
codex -s workspace-write   # 允许修改工作区
codex --search             # 实时联网搜索
codex -i screenshot.png    # 携带图片
codex -c key=value         # 临时覆盖 config.toml
```

---

## 会话内 `/` 命令

| 命令                      | 用途                        |
| ----------------------- | ------------------------- |
| `/model`                | ⭐ 切换模型 / reasoning effort |
| `/reasoning`            | 调整推理强度                    |
| `/fast`                 | 开关 Fast 模式（模型支持时）         |
| `/status`               | ⭐ 查看模型、上下文、权限、Token 等     |
| `/permissions`          | ⭐ 修改执行/文件访问权限             |
| `/plan`                 | ⭐ 进入 Plan 模式，先规划再执行       |
| `/review`               | ⭐ Review 当前代码改动           |
| `/diff`                 | ⭐ 查看 Git diff             |
| `/compact`              | ⭐ 压缩长对话，释放 context        |
| `/resume`               | ⭐ 切换/恢复历史会话               |
| `/fork`                 | 从当前会话分叉新会话                |
| `/new`                  | 新建干净会话                    |
| `/clear`                | 清屏并开启新 Chat               |
| `/rename`               | 给当前会话改名                   |
| `/goal`                 | 设置/查看/暂停/恢复长期目标           |
| `/agent` / `/subagents` | 查看、切换子 Agent              |
| `/ps`                   | 查看后台终端任务                  |
| `/stop`                 | 停止后台终端任务                  |
| `/mcp`                  | 查看 MCP 工具状态               |
| `/skills`               | 浏览/使用 Skills              |
| `/apps`                 | 浏览 Apps / Connectors      |
| `/init`                 | 创建 `AGENTS.md`            |
| `/mention`              | 添加文件/目录到上下文               |
| `/copy`                 | 复制上一条 Codex 输出            |
| `/side` / `/btw`        | 临时旁路提问，不打断主会话             |
| `/experimental`         | 管理实验功能                    |
| `/exit` / `/quit`       | 退出 Codex                  |

---

## 键盘 / 输入快捷方式

```text
@文件名       搜索文件并加入上下文
!命令         直接执行本地 shell 命令
Ctrl+R        搜索历史 Prompt
Ctrl+O        复制最近一次 Codex 输出
Tab           Codex 工作时排队下一条指令
Enter         Codex 工作时插入新指令
Esc Esc       编辑上一条消息并从那里 Fork
Ctrl+C        退出
```

---

## 最常用工作流

```bash
# 进入项目
cd my-project
codex

# 继续上次工作
codex resume --last

# 指定目录直接启动
codex -C ~/code/my-project

# 一次性让 Codex 完成任务
codex e "运行测试，定位失败原因并给出修复方案"
```

```text
/model        → 选模型
/plan         → 复杂任务先规划
/permissions  → 调权限
/diff         → 看改了什么
/review       → 做一次代码审查
/compact      → 对话太长时压缩
/status       → 随时检查当前状态
```

> ⚠️ `--yolo` / `--dangerously-bypass-approvals-and-sandbox` 会绕过审批和 sandbox，除非运行在额外隔离的环境中，否则不建议使用。
