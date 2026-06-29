# Assets Directory

游戏资源文件。

## 目录结构

```
assets/
├── art/          # 美术资源（纹理、模型、精灵、材质）
├── audio/        # 音频资源（音乐、音效、环境音）
├── vfx/          # 视觉特效（粒子、着色器特效）
├── shaders/      # 自定义着色器文件（.gdshader）
└── data/         # 游戏数据文件（JSON、CSV 配置表）
```

## 资源管理

- 使用 Godot 的原生格式优先（.tscn、.tres、.gdshader）
- 大型二进制资源（.png、.wav、.fbx）建议配合 Git LFS 使用
- 通过 `godot-mcp-enhanced` MCP 工具可让 Claude Code 直接导入和管理资源
