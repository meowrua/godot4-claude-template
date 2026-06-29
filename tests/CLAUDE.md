# Tests Directory

测试套件。使用 GUT (Godot Unit Testing) 框架。

## 目录结构

```
tests/
├── unit/             # 单元测试
├── integration/      # 集成测试
├── performance/      # 性能测试
└── playtest/         # 游玩测试脚本
```

## 测试框架

- **GUT**: Godot 原生单元测试框架
- 通过 `/test-setup` skill 可自动搭建测试框架和 CI 管道
- 通过 `/test-helpers` 生成引擎专用测试辅助库

## 运行测试

在 Godot 编辑器中通过 GUT 面板运行，或使用命令行：

```bash
godot --headless -s addons/gut/gut_cmdln.gd -gdir=res://tests/unit
```
