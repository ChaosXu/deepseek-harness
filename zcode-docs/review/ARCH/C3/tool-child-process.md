# 组件 ⑦ 工具执行子进程（子进程）

**本组件没有 dsh 模块**：⑦ 是 harness 进程（①③④）为执行工具而 spawn 的目标程序，其可执行文件属于本地 OS 生态、用户配置或外部系统，不是 dsh 代码。模块依赖图因此不存在；下表列出目标程序的种类与 spawn 它们的模块（模块图见 `dsh-host-process.md`）。

| ⑦ 中的目标程序 | spawn 它的模块（在 ①③④ 内） | 驱动方式 |
|---|---|---|
| bash 命令与进程树 | `dsh-bash-sandbox` / `dsh-bash-local`（经 `dsh-subprocess-local`） | pipe、进程组、超时/取消 |
| PTY shell（持久终端） | `dsh-terminal-bash` | PTY |
| 语言服务器（LSP） | `dsh-lsp-stdio` | JSON-RPC over stdio |
| 用户 hooks 脚本 | `dsh-hooks-claude-code` / `dsh-hooks-codex` | 按 hooks.json 约定执行，检查退出码 |
| MCP server（stdio 形态） | `dsh-mcp-client`（`StdioClientTransport`） | MCP 协议 over stdio |
| 外部 agent CLI（codex app-server / Claude Code） | `dsh-subagent-codex` / `dsh-subagent-claude-code` | 各自的 stdio 协议 |
| 被沙箱限制的命令 | `dsh-sandbox-local` → 组件 ⑥ landlock-run → exec | ⑥ exec 后的目标进程即属 ⑦ |
