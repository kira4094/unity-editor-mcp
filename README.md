# Unity Editor MCP

[English](README.md) | **中文**

## 概述

Unity Editor MCP 是一个基于 Model Context Protocol (MCP) 的 Unity 编辑器集成工具，让 AI 助手（如 Claude Code）能够直接操控 Unity Editor，实现自动化游戏开发。

## 特性

- **70+ 工具**，覆盖 13 个类别，用于 Unity Editor 自动化
- **GameObject 管理** — 创建、查找、修改、删除，支持完整层级控制
- **组件系统** — 添加、移除、修改组件及属性
- **场景管理** — 创建、加载、保存、列出场景，支持 Build Settings 集成
- **场景分析** — 深度检查、组件分析、性能指标
- **资源管理** — 创建和修改 Prefab、材质、脚本
- **UI 自动化** — 查找、点击 UI 元素
- **输入模拟** — 模拟键盘、鼠标、游戏手柄、触摸输入
- **Play Mode 控制** — 播放、暂停、停止
- **C# 脚本编辑** — 内置 Roslyn LSP，支持符号搜索、引用查找、结构编辑
- **控制台** — 读取日志、清除、编译状态监控

---

## 🔧 本分支的改动

本分支（`packages`）基于上游 [akiojin/unity-editor-mcp](https://github.com/akiojin/unity-editor-mcp) 进行了以下兼容性修改：

### 1. Unity 版本兼容（2023.2）
- 将 `package.json` 中的 `"unity": "6000.0"` 修改为 `"2023.2"`
- 修复了 Unity 2023.x 中不存在的 Rigidbody API：
  - `linearDamping` → `drag`
  - `angularDamping` → `angularDrag`

### 2. 依赖版本调整
- `com.unity.inputsystem`: `1.14.2` → `1.8.2`
- `com.unity.recorder`: `4.0.0` → `5.0.0`

> 注意：`main` 分支保持与上游同步，仅 `packages` 分支包含上述改动。

---

## 📦 安装方法

### 1. 在 Unity 项目中添加包

**Unity Package Manager → + → Add package from git URL：**

```
https://github.com/kira4094/unity-editor-mcp.git?path=UnityEditorMCP/Packages/unity-editor-mcp#packages
```

> 末尾的 `#packages` 指定使用本分支。

### 2. 安装 MCP 服务器（Node.js）

全局安装：
```bash
npm install -g @akiojin/unity-editor-mcp
```

或用 npx 直接运行：
```bash
npx @akiojin/unity-editor-mcp@latest
```

### 3. 配置 Claude Code

在 CC-Switch 或 `.claude.json` 中添加：

```json
{
  "mcpServers": {
    "unity-editor": {
      "type": "stdio",
      "command": "cmd",
      "args": ["/c", "npx", "-y", "@akiojin/unity-editor-mcp@latest"]
    }
  }
}
```

### 4. 验证连接

确保 Unity Editor 处于打开状态，然后在 Claude Code 中测试：
```
/mcp reconnect unity-editor
```

成功后会显示 `Reconnected to unity-editor.`

---

## 🚀 常用工具示例

| 工具 | 用途 |
|------|------|
| `ping` | 测试连接 |
| `get_scene_info` | 获取当前场景信息 |
| `get_hierarchy` | 获取场景层级结构 |
| `create_gameobject` | 创建 GameObject |
| `modify_component` | 修改组件属性 |
| `load_scene` | 加载场景 |
| `play_game` / `stop_game` | 播放/停止 |
| `capture_screenshot` | 截取编辑器画面 |
| `read_console` | 读取控制台日志 |
| `script_search` | 搜索 C# 脚本符号 |

---

## 许可证

MIT License
