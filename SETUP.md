# Setup Guide — SurvivalGame Template

本指南覆盖从 `git clone` 到完整可运行开发环境的全部步骤。

## 前置条件

| 工具 | 用途 | 安装方式 |
|------|------|----------|
| **Git** | 版本控制 | [git-scm.com](https://git-scm.com/) |
| **Godot 4.7+** | 游戏引擎 | [godotengine.org](https://godotengine.org/download/) |
| **Python 3.10+** | MCP 服务器运行环境 | [python.org](https://www.python.org/) |
| **uv** (Python 包管理器) | MCP 服务器依赖管理 | `winget install astral-sh.uv` 或 `pip install uv` |
| **Claude Code** | AI 代理 CLI | `npm install -g @anthropic-ai/claude-code` |
| **jq** (推荐) | Hook 脚本 JSON 解析 | `winget install jqlang.jq` |
| **VS Code** (推荐) | IDE，搭配 Claude Code 扩展 | [code.visualstudio.com](https://code.visualstudio.com/) |

> **Windows 用户注意**: Git for Windows 自带 Git Bash，所有 hook 脚本依赖 `bash` 命令。确保安装 Git 时勾选 "Git Bash" 组件。

## 1. 克隆项目

```bash
git clone https://github.com/<your-org>/<your-repo>.git my-game
cd my-game
```

## 2. 安装 Python MCP 服务器

Godot MCP Enhanced 使用 Python MCP 服务器桥接 Claude Code 与 Godot 编辑器：

```bash
cd python

# 创建虚拟环境并安装依赖
uv venv
uv pip install -e .

# 验证安装
python test_connection.py

cd ..
```

> `.venv/` 目录已在 `.gitignore` 中排除，不会提交到仓库。

## 3. 配置 Godot MCP Enhanced

### 3.1 Godot 编辑器端

1. 用 Godot 4.7 打开项目
2. 确认 `addons/godot_mcp_enhanced/` 插件已启用（项目设置 → 插件）
3. 检查 `godot_mcp_config.json` 中的端口配置（默认 3571/3572）
4. 运行项目（F5）或保持编辑器运行状态

### 3.2 Claude Code 端

MCP 服务器配置已在 `.claude/mcp.json` 中预设：

```json
{
  "mcpServers": {
    "godot-mcp-enhanced": {
      "command": "uv",
      "args": [
        "--directory", "e:/develop/project/survival_game/python",
        "run", "mcp-server"
      ],
      "env": {
        "GODOT_HOST": "127.0.0.1",
        "GDAI_MCP_SERVER_PORT": "3571"
      }
    }
  }
}
```

> **重要**: 如果你克隆到的目录路径不同，请更新 `.claude/mcp.json` 中 `--directory` 参数为你的实际路径。

### 3.3 验证 MCP 连接

启动 Claude Code 后，检查 MCP 服务器状态：

```bash
# 在 Claude Code 会话中
/mcp-status
```

你应该看到 `godot-mcp-enhanced` 处于 connected 状态。

## 4. 首次启动 Claude Code Game Studios

```bash
# 在项目根目录启动 Claude Code
claude
```

进入会话后，运行引导命令：

```
/start
```

CCGS 会检测你的项目阶段并引导你完成后续设置：
- 如果你的项目是**全新空白项目** → 运行 `/brainstorm` 生成游戏概念
- 如果你**已有游戏概念** → 运行 `/setup-engine godot 4.7` 配置引擎
- 如果你**已有代码和文档** → 运行 `/project-stage-detect` 分析当前状态

## 5. 引擎配置

如果 `/start` 没有自动配置引擎，手动运行：

```
/setup-engine godot 4.7
```

这会：
- 更新 `.claude/docs/technical-preferences.md` 中的引擎、语言、命名约定
- 配置引擎版本参考文档
- 设置正确的 Godot 专项代理路由

## 6. 个人偏好配置（可选）

```bash
# 创建个人偏好文件（不会提交到 git）
cp .claude/docs/CLAUDE-local-template.md CLAUDE.local.md

# 创建个人权限覆盖（不会提交到 git）
# 参考 .claude/docs/settings-local-template.md 中的 JSON 示例手动创建 .claude/settings.local.json
```

编辑这些文件以匹配你的：
- 模型偏好（Opus / Sonnet / Haiku）
- 权限偏好
- 通信风格
- 本地环境变量

## 7. 验证安装

运行以下命令检查一切就绪：

```bash
# 环境检查
git --version
python --version
uv --version
godot --version

# Hook 工具检查
bash --version
jq --version      # 可选

# 启动 Claude Code 并运行诊断
claude
/help
```

## 项目结构概览

```
.
├── CLAUDE.md                    # 主配置文件（AI 代理入口）
├── SETUP.md                     # 本文件
├── .claude/
│   ├── agents/                  # 49 个专项代理定义
│   ├── skills/                  # 73 个 / 命令工作流
│   ├── hooks/                   # 12 个自动化验证脚本
│   ├── rules/                   # 11 个路径级编码规范
│   ├── docs/                    # 工作室架构文档
│   ├── settings.json            # Claude Code 项目设置
│   └── mcp.json                 # MCP 服务器连接配置
├── src/                         # 游戏源码
├── assets/                      # 游戏资源（美术、音频、着色器）
├── design/                      # 游戏设计文档
├── docs/                        # 技术文档、架构决策记录
│   └── engine-reference/        # 版本锁定的引擎 API 快照
├── tests/                       # 测试套件
├── prototypes/                  # 一次性原型
├── production/                  # Sprint、里程碑、发布管理
├── python/                      # Godot MCP Enhanced Python 服务器
├── godot_mcp_config.json        # Godot 端 MCP 配置
└── project.godot                # Godot 引擎项目文件
```

## 常见问题

### MCP 服务器连接失败

1. 确保 Godot 编辑器正在运行且项目已加载
2. 检查 `godot_mcp_config.json` 中端口是否正确（默认 3571）
3. 检查 `.claude/mcp.json` 中 `--directory` 路径是否正确
4. 运行 `python/test_connection.py` 测试连接
5. 确认 `python/.venv/` 已创建且依赖已安装

### Hook 脚本不执行

- Windows: 确保 Git Bash 在 PATH 中（`bash --version` 可执行）
- 如果缺少 `jq`，hook 会静默跳过验证（不会报错），但建议安装
- 检查 `.claude/settings.json` 中的 hook 配置

### Godot 版本太新

如果 Godot 版本高于 4.7，`/setup-engine` 会自动检测并获取最新文档。你也可以手动更新 `docs/engine-reference/godot/VERSION.md`。

### 导入的项目资源缺失

- `*.import` 文件由 Godot 自动生成，已在 `.gitignore` 中排除
- 首次打开项目时 Godot 会自动重新导入所有资源
- 不要提交 `.godot/` 目录内容
