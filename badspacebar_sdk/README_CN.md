# badspacebar/sdk 中文索引

这个文件夹来自 GitHub 仓库：
https://github.com/badspacebar/sdk

## 这是什么

这是 Hanbot Lua 脚本开发资料仓库，主要包含：

1. 离线 SDK 文档
2. IDE 类型提示/自动补全文件
3. 开源 Hanbot 示例脚本

它不是完整平台本体，也不是直接加载的 AIO 合集。它更像是“写 Hanbot 脚本的说明书 + 示例库”。

## 目录说明

- `index.html`
  - 文档首页，可以直接双击用浏览器打开。

- `docs\`
  - 离线文档页面。
  - 重点看：
    - `docs\modules.html`：预测、走砍、目标选择等模块。
    - `docs\globals.html`：全局变量和函数。
    - `docs\objects.html`：英雄、小兵、技能等对象。
    - `docs\examples.html`：基础写法示例。
    - `docs\best-practices.html`：推荐写法。

- `ide-helper\`
  - Lua 编辑器补全/类型提示用。
  - 写脚本时可以给 VSCode/IDE 做提示参考。

- `opensource\`
  - 开源 Hanbot 脚本示例。
  - 重点看：
    - `hello world`：最简单入口。
    - `menu example`：菜单写法。
    - `beasty syndra`：技能逻辑/预测示例。
    - `gagong riven`：英雄脚本结构示例。
    - `DivineLib`：公共库参考。

## 写 Hanbot 平台/合集时怎么用

推荐顺序：

1. 先看 `index.html` 或 `docs\index.html`，确认 API 总览。
2. 看 `docs\modules.html`，重点理解：
   - `module.internal('pred')`
   - `module.internal('orb')`
   - `module.internal('TS')`
   - `player:castSpell(...)`
3. 看 `opensource\menu example`，学菜单结构。
4. 看 `opensource\beasty syndra` 和 `opensource\gagong riven`，学真实英雄脚本结构。
5. 再把这些封装成自己的平台目录：
   - `core`：加载器、日志、模式判断
   - `sdk`：pred/orb/target/spell 封装
   - `champions`：每个英雄自己的 combo/menu/spells

## 和其他资料的关系

- `KleeAIO123/HanbotSDK`
  - 更偏 SDK/API 示例和文档整理。

- `DancingLeaf123/yeahbot`
  - 更偏真实脚本源码参考。

- `badspacebar/sdk`
  - 更完整：有离线文档、IDE helper、开源示例。

三者合起来，足够搭一个 Hanbot AIO 平台骨架，并按英雄写合集逻辑。
