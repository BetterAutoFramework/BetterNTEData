# BetterNTEData

[BetterNTE](https://github.com/BetterAutoFramework/BetterNTE) 的运行时数据仓库，包含脚本、触发器、模板图片和插件。

作为 git submodule 引入主仓库：

```bash
git submodule update --init
```

## 目录结构

```
data/
  main/                    # 主数据目录
    scripts/               # 自动化脚本
      fishing_assist_v2/   # 钓鱼辅助
      cafe_income/         # 咖啡馆收益
      make_coffee/         # 制作咖啡
      lib/                 # 公共库
      anti_detect/         # 防检测
      ...
    triggers/              # 触发器（每帧检测）
      auto_skip/           # 自动跳过剧情/传送确认
      ...
  plugins/                 # 插件
    nte/                   # NTE 插件清单
    test-js-plugin/        # JS 测试插件
    test-wasm-plugin/      # WASM 测试插件
    test-ffi-plugin/       # FFI 测试插件
  local/                   # 用户本地数据（不提交，运行时生成）
```

## 脚本结构

每个脚本/触发器目录包含：

- `manifest.json` — 清单文件，定义名称、版本、权限、参数 schema 等
- `main.js` — 入口脚本
- `templates/` — 模板图片（`.png`）及其匹配参数（`.json`）

### manifest.json 示例

```json
{
  "schema_version": 1,
  "name": "fishing_assist_v2",
  "display_name": "钓鱼辅助V2",
  "version": "1.1.4",
  "type": "solo_task",
  "entry": "main.js",
  "permissions": ["screenshot", "template_match", "click", "keyboard", "ocr"],
  "params_schema": { ... }
}
```

### 脚本类型

| type | 说明 |
|------|------|
| `solo_task` | 独立任务脚本 |
| `trigger` | 触发器，每帧检测并自动响应 |

## 插件结构

插件目录包含 `manifest.json` 和入口文件。支持三种类型：

| type | 入口 | 说明 |
|------|------|------|
| `js` | `index.js` | QuickJS 隔离运行时 |
| `wasm` | `plugin.wasm` | WebAssembly 插件 |
| `ffi` | `plugin.so`/`.dll` | 原生动态库（C ABI） |

## 许可证

参见 [LICENSE](LICENSE)。
