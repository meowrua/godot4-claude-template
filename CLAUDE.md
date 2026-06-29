# Claude Code Game Studios -- SurvivalGame

独立游戏开发模板，通过 49 个协调的 Claude Code 子代理管理。
每个代理负责特定领域，确保关注点分离和代码质量。

> **刚克隆本项目？** 请阅读 [SETUP.md](SETUP.md) 获取完整的环境搭建指南。

## 技术栈

- **引擎**: Godot 4.7
- **语言**: GDScript
- **物理**: Jolt Physics 3D
- **渲染**: Direct3D 12（Windows），Forward+
- **MCP 集成**: [Godot MCP Enhanced](https://github.com/IvanPck/godot-mcp-enhanced)（端口 3571/3572）
- **版本控制**: Git，基于主干开发

## 项目结构

@.claude/docs/directory-structure.md

## 环境搭建

@SETUP.md

## 引擎版本参考

@docs/engine-reference/godot/VERSION.md

## 技术偏好

@.claude/docs/technical-preferences.md

## 协调规则

@.claude/docs/coordination-rules.md

## 协作协议

**用户驱动的协作，而非自主执行。**
每个任务遵循：**提问 -> 选项 -> 决策 -> 草稿 -> 批准**

- 代理在调用 Write/Edit 工具前必须询问"我可以将此内容写入 [文件路径] 吗？"
- 代理在请求批准前必须展示草稿或摘要
- 多文件修改需要明确批准整个变更集
- 未经用户指示不得提交

详见 `docs/COLLABORATIVE-DESIGN-PRINCIPLE.md` 获取完整协议和示例。

## 编码标准

@.claude/docs/coding-standards.md

## 上下文管理

@.claude/docs/context-management.md

## Godot MCP Enhanced 集成

本项目预配置了 Godot MCP Enhanced，使 Claude Code 能够直接操作 Godot 编辑器。

### 架构概览

```
Claude Code → .claude/mcp.json → Python MCP 服务器 (uv) → Godot 编辑器 (:3571)
```

### 连接配置

- **MCP 服务器配置**: [.claude/mcp.json](.claude/mcp.json)
- **Godot 端配置**: [godot_mcp_config.json](godot_mcp_config.json)
- **Python 服务器**: [python/mcp_server.py](python/mcp_server.py)
- **MCP 服务器端口**: `GDAI_MCP_SERVER_PORT=3571`
- **运行时桥接端口**: `GDAI_RUNTIME_SERVER_PORT=3572`

### 可用功能

通过 `godot-mcp-enhanced` MCP 工具，Claude Code 可以：

- **场景操作**: 创建/打开/保存场景，添加/删除/移动节点，修改节点属性
- **资源管理**: 导入资源，创建材质/着色器，管理文件系统
- **脚本编辑**: 创建/修改 GDScript 文件，附加脚本到节点
- **调试支持**: 获取错误日志，截图（自动/手动），性能分析
- **编辑器控制**: 运行/停止项目，切换场景，获取当前选中节点

### 自动截图配置

根据 `godot_mcp_config.json`，以下情况会自动截图：
- 场景切换时（`SCREENSHOT_ON_SCENE_CHANGE: true`）
- 错误发生时（`SCREENSHOT_ON_ERROR: true`）
- AI 请求时（`AUTO_SCREENSHOT: true`）

### 故障排除

详见 [SETUP.md](SETUP.md) 中的"常见问题"章节。

## Godot 专项代理

处理引擎相关任务时，优先使用以下专项代理：
- `godot-specialist` — 通用 Godot 4 架构和最佳实践
- `godot-gdscript-specialist` — GDScript 编码、模式、优化
- `godot-shader-specialist` — 可视着色器和着色器代码
- `godot-csharp-specialist` — C# Godot 集成（按需）
- `godot-gdextension-specialist` — 原生 GDExtension 开发
