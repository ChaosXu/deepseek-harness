# C3 — Component（每个 C2 进程组件内部的模块与依赖）

按 C4 方法论：C3 组件 = C2 容器（进程），**一个组件一个 `<组件名>.md`**。每个文件内按依赖类型分**三张图**：dependencies（运行时依赖）、peerDependencies（同进程服务契约——Cordis 的服务关系走 peer）、devDependencies（开发期依赖）；边 A --> B = A 依赖 B；只画组合行 → 第一层直接依赖，第一层节点不再向下展开。

| 文件 | C2 组件 | 模块来源 | 规模（deps/peers/devs，模块·边） |
|---|---|---|---|
| [dsh-host-process.md](dsh-host-process.md) | ① dsh 宿主进程（主；web/headless 两形态各三图） | profile 组合行（dsh-base + dsh-web-app / dsh-headless patch）+ 启动器 `@deepseek-ai/dsh` | web 130·168 / 129·577 / 133·574；headless 106·117 / 113·489 / 121·504 |
| [browser-spa.md](browser-spa.md) | ② 浏览器进程（主） | web profile 的 client 组合行（dsh-client-\* 等）+ `dsh-web-frontend` | 50·33 / 70·295 / 75·277 |
| [acp-server.md](acp-server.md) | ③ ACP Server（主/子） | `examples/acp-agent/cordis.yml` 组合行 | 28·19 / 68·187 / 74·219 |
| [sdk-server.md](sdk-server.md) | ④ SDK Server（主/子） | `examples/jsonrpc-agent/cordis.yml`（与 Python 捆绑 runtime 同源） | 17·12 / 63·128 / 69·149 |
| [python-sdk.md](python-sdk.md) | ⑤ Python SDK（主） | Python 模块（`deepseek_harness` 5 个 + runtime 载体） | 6 模块（单图） |
| [landlock-run.md](landlock-run.md) | ⑥ landlock-run（子） | C 编译单元 + JS 入口包 + 平台预编译包 | 单图 |
| [tool-child-process.md](tool-child-process.md) | ⑦ 工具执行子进程（子） | **无 dsh 模块**——目标程序非 dsh 代码；表格列出种类与 spawn 方 | — |

## 图的生成口径

- **模块**：进程的组合行（cordis yml/patch 中的插件包）**及其第一层直接依赖**，按 dependencies / peerDependencies / devDependencies 分三张图（边只从组合行出发，第一层节点不再向下展开）。外部 npm 依赖不画。
- **图内无分组**：节点与依赖边平铺（渲染限制）。
- **省略项（仅 devs 图）**：全员开发期框架依赖 `cordis` / `dsh-invariants` / `cordis-plugin-loader` / `cordis-plugin-include`——无结构信息。
- **终端节点**：`dsh-base` / `dsh-web-app` / `dsh-headless`（纯配置组合层，不展开）。
- **跨进程剪枝**：npm 依赖会跨进程面（如 api-gateway 依赖 client-connection），已按进程剪枝——① 的图不含 client 家族与对侧 bundle，② 的图不含 host 家族；被剪的模块在对应进程自己的文件里。
- **组合但禁用的行**：平台条件禁用（如非 Windows 下的 pwsh 行）仍画出——行在组合中存在，仅运行时禁用。
