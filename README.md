# Godot 游戏开发模板

> 预配置 Claude Code Game Studios + Godot MCP Enhanced 的 Godot 4.7 项目模板，克隆即可使用。

---

## 这是什么？

一个**开箱即用**的 Godot 4.7 项目模板，预配置了：

- 🤖 **Claude Code Game Studios** — 49 个 AI 专项代理、70+ 工作流命令、自动化验证钩子
- 🔧 **Godot MCP Enhanced** — Claude Code 直接操控 Godot 编辑器（场景、资源、脚本、调试）
- 🎮 **Godot 4.7** — Jolt Physics 3D、Direct3D 12 渲染、Forward+

## 前置条件

| 工具 | 用途 |
|------|------|
| [Godot 4.7+](https://godotengine.org/download/) | 游戏引擎 |
| [Python 3.10+](https://www.python.org/) | MCP 服务器运行环境 |
| [uv](https://docs.astral.sh/uv/) | Python 包管理器 |
| [Git](https://git-scm.com/) | 版本控制 |

## 快速开始

```bash
# 1. 克隆模板
git clone https://github.com/<your-org>/<repo-name>.git my-game
cd my-game

# 2. 安装 Python MCP 服务器
cd python
uv venv
uv pip install -e .
python test_connection.py
cd ..

# 3. 用 Godot 4.7 打开项目（确认 addons/godot_mcp_enhanced 插件已启用）

# 4. 启动 Claude Code
claude

# 5. 在 Claude Code 会话中
/start
```

## 项目结构

```
├── CLAUDE.md                    # 主配置（AI 代理入口）
├── SETUP.md                     # 详细环境搭建指南
├── README.md                    # 本文件
├── LICENSE                      # MIT 许可证
├── .claude/                     # 代理定义、技能、钩子、规则、文档
│   ├── agents/                  # 49 个专项代理定义
│   ├── skills/                  # 70+ 个工作流命令
│   ├── hooks/                   # 自动化验证脚本
│   ├── rules/                   # 路径级编码规范
│   └── docs/                    # 工作室架构文档
├── src/                         # 游戏源码
├── assets/                      # 游戏资源（美术、音频、着色器、数据）
├── design/                      # 游戏设计文档
├── docs/                        # 技术文档
│   └── engine-reference/        # 版本锁定的引擎 API 快照
├── tests/                       # 测试套件
├── prototypes/                  # 一次性原型
├── production/                  # 项目管理和状态文件
├── python/                      # Godot MCP Enhanced Python 服务器
└── project.godot                # Godot 引擎项目文件
```

## 克隆后需要修改

| 文件 | 修改内容 |
|------|----------|
| `project.godot` | 修改 `config/name` 为你的游戏名 |
| `.claude/mcp.json` | 更新 `--directory` 为你的实际路径 |
| `.claude/docs/technical-preferences.md` | 配置目标平台、帧率、输入方式等 |
| `CLAUDE.local.md`（新建） | 个人偏好（不会被 git 跟踪） |

## 使用方式

```bash
/start          # 检测项目阶段，引导后续设置
/brainstorm     # 生成游戏概念
/setup-engine   # 配置引擎偏好
```

每个任务遵循协作协议：**提问 → 选项 → 决策 → 草稿 → 批准**。AI 代理会在修改文件前请求确认，不会自主提交。

## 许可证

[MIT](LICENSE) — 你可以自由使用、修改和分发此模板。
