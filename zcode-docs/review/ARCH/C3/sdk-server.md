# 组件 ④ SDK Server（Node runtime）进程（主/子）

模块 = `examples/jsonrpc-agent/cordis.yml` 组合行（与 Python SDK 捆绑 runtime 的 `runtime/cordis.yml` 同源）**及其第一层直接依赖**：`dsh-sdk-jsonrpc-server` 协议服务端 + `dsh-agent-spine-demo` 拉入 agent 脊柱 + llm/bash/fs 行。按依赖类型分三张图；边 A --> B 表示 A 依赖 B；只画一层。

## dependencies（运行时依赖）（17 模块 / 12 依赖边）

```mermaid
flowchart LR
  m_dsh-agent-spine-demo["dsh-agent-spine-demo"]
  m_dsh-bash-local["dsh-bash-local"]
  m_dsh-compaction-basic["dsh-compaction-basic"]
  m_dsh-fs-local["dsh-fs-local"]
  m_dsh-fs-observation-policy["dsh-fs-observation-policy"]
  m_dsh-llm-deepseek["dsh-llm-deepseek"]
  m_dsh-sdk-jsonrpc-server["dsh-sdk-jsonrpc-server"]
  m_dsh-session-checkpoint-policy["dsh-session-checkpoint-policy"]
  m_dsh-session-persistence-jsonl["dsh-session-persistence-jsonl"]
  m_dsh-subagent["dsh-subagent"]
  m_dsh-subagent-spawn-in-process["dsh-subagent-spawn-in-process"]
  m_dsh-subprocess-local["dsh-subprocess-local"]
  m_dsh-token-meter["dsh-token-meter"]
  m_dsh-tool-fs["dsh-tool-fs"]
  m_dsh-tool-subagent["dsh-tool-subagent"]
  m_dsh-tool-todo["dsh-tool-todo"]
  m_schemastery["schemastery"]
  m_dsh-sdk-jsonrpc-server --> m_schemastery
  m_dsh-llm-deepseek --> m_schemastery
  m_dsh-bash-local --> m_schemastery
  m_dsh-agent-spine-demo --> m_schemastery
  m_dsh-session-persistence-jsonl --> m_schemastery
  m_dsh-subagent-spawn-in-process --> m_schemastery
  m_dsh-tool-subagent --> m_schemastery
  m_dsh-tool-todo --> m_schemastery
  m_dsh-fs-local --> m_schemastery
  m_dsh-tool-fs --> m_schemastery
  m_dsh-token-meter --> m_schemastery
  m_dsh-compaction-basic --> m_schemastery
```

## peerDependencies（同进程服务契约）（63 模块 / 128 依赖边）

```mermaid
flowchart LR
  m_cordis["cordis"]
  m_cordis-plugin-timer["cordis-plugin-timer"]
  m_dsh-agent["dsh-agent"]
  m_dsh-agent-instructions["dsh-agent-instructions"]
  m_dsh-agent-loop["dsh-agent-loop"]
  m_dsh-agent-presets["dsh-agent-presets"]
  m_dsh-agent-spine-demo["dsh-agent-spine-demo"]
  m_dsh-anonymous-user-id["dsh-anonymous-user-id"]
  m_dsh-attachment["dsh-attachment"]
  m_dsh-bash-local["dsh-bash-local"]
  m_dsh-brand["dsh-brand"]
  m_dsh-commands["dsh-commands"]
  m_dsh-compaction["dsh-compaction"]
  m_dsh-compaction-basic["dsh-compaction-basic"]
  m_dsh-compaction-tool-result-pruner["dsh-compaction-tool-result-pruner"]
  m_dsh-credentials["dsh-credentials"]
  m_dsh-fs["dsh-fs"]
  m_dsh-fs-local["dsh-fs-local"]
  m_dsh-fs-observation-policy["dsh-fs-observation-policy"]
  m_dsh-goal["dsh-goal"]
  m_dsh-goal-round-driver["dsh-goal-round-driver"]
  m_dsh-home-paths["dsh-home-paths"]
  m_dsh-invariants["dsh-invariants"]
  m_dsh-jobs["dsh-jobs"]
  m_dsh-jobs-local["dsh-jobs-local"]
  m_dsh-launch-environment["dsh-launch-environment"]
  m_dsh-llm["dsh-llm"]
  m_dsh-llm-deepseek["dsh-llm-deepseek"]
  m_dsh-llm-retry["dsh-llm-retry"]
  m_dsh-sandbox["dsh-sandbox"]
  m_dsh-sandbox-policy["dsh-sandbox-policy"]
  m_dsh-scope["dsh-scope"]
  m_dsh-sdk-jsonrpc-server["dsh-sdk-jsonrpc-server"]
  m_dsh-sdk-protocol["dsh-sdk-protocol"]
  m_dsh-session["dsh-session"]
  m_dsh-session-checkpoint-policy["dsh-session-checkpoint-policy"]
  m_dsh-session-persistence["dsh-session-persistence"]
  m_dsh-session-persistence-jsonl["dsh-session-persistence-jsonl"]
  m_dsh-session-projection["dsh-session-projection"]
  m_dsh-session-projection-cache["dsh-session-projection-cache"]
  m_dsh-session-title["dsh-session-title"]
  m_dsh-settings["dsh-settings"]
  m_dsh-shell["dsh-shell"]
  m_dsh-shell-env["dsh-shell-env"]
  m_dsh-skill["dsh-skill"]
  m_dsh-skill-filesystem["dsh-skill-filesystem"]
  m_dsh-subagent["dsh-subagent"]
  m_dsh-subagent-in-process-driver["dsh-subagent-in-process-driver"]
  m_dsh-subagent-spawn-in-process["dsh-subagent-spawn-in-process"]
  m_dsh-subprocess["dsh-subprocess"]
  m_dsh-subprocess-local["dsh-subprocess-local"]
  m_dsh-system-prompt["dsh-system-prompt"]
  m_dsh-timeout["dsh-timeout"]
  m_dsh-token-meter["dsh-token-meter"]
  m_dsh-tool-bash["dsh-tool-bash"]
  m_dsh-tool-fs["dsh-tool-fs"]
  m_dsh-tool-goal["dsh-tool-goal"]
  m_dsh-tool-jobs["dsh-tool-jobs"]
  m_dsh-tool-skill["dsh-tool-skill"]
  m_dsh-tool-subagent["dsh-tool-subagent"]
  m_dsh-tool-todo["dsh-tool-todo"]
  m_dsh-tools["dsh-tools"]
  m_dsh-user-approval["dsh-user-approval"]
  m_dsh-sdk-jsonrpc-server --> m_dsh-agent
  m_dsh-sdk-jsonrpc-server --> m_dsh-invariants
  m_dsh-sdk-jsonrpc-server --> m_dsh-llm
  m_dsh-sdk-jsonrpc-server --> m_dsh-llm-deepseek
  m_dsh-sdk-jsonrpc-server --> m_dsh-scope
  m_dsh-sdk-jsonrpc-server --> m_dsh-sdk-protocol
  m_dsh-sdk-jsonrpc-server --> m_dsh-session
  m_dsh-sdk-jsonrpc-server --> m_dsh-subagent
  m_dsh-sdk-jsonrpc-server --> m_cordis
  m_dsh-llm-deepseek --> m_dsh-credentials
  m_dsh-llm-deepseek --> m_dsh-launch-environment
  m_dsh-llm-deepseek --> m_dsh-invariants
  m_dsh-llm-deepseek --> m_dsh-llm
  m_dsh-llm-deepseek --> m_dsh-settings
  m_dsh-llm-deepseek --> m_dsh-timeout
  m_dsh-llm-deepseek --> m_dsh-anonymous-user-id
  m_dsh-llm-deepseek --> m_cordis
  m_dsh-subprocess-local --> m_dsh-invariants
  m_dsh-subprocess-local --> m_dsh-subprocess
  m_dsh-subprocess-local --> m_dsh-timeout
  m_dsh-subprocess-local --> m_cordis
  m_dsh-bash-local --> m_dsh-shell
  m_dsh-bash-local --> m_dsh-invariants
  m_dsh-bash-local --> m_dsh-subprocess
  m_dsh-bash-local --> m_dsh-timeout
  m_dsh-bash-local --> m_cordis
  m_dsh-bash-local --> m_dsh-settings
  m_dsh-agent-spine-demo --> m_cordis-plugin-timer
  m_dsh-agent-spine-demo --> m_dsh-agent
  m_dsh-agent-spine-demo --> m_dsh-agent-loop
  m_dsh-agent-spine-demo --> m_dsh-goal
  m_dsh-agent-spine-demo --> m_dsh-goal-round-driver
  m_dsh-agent-spine-demo --> m_dsh-invariants
  m_dsh-agent-spine-demo --> m_dsh-llm
  m_dsh-agent-spine-demo --> m_dsh-home-paths
  m_dsh-agent-spine-demo --> m_dsh-llm-retry
  m_dsh-agent-spine-demo --> m_dsh-scope
  m_dsh-agent-spine-demo --> m_dsh-session
  m_dsh-agent-spine-demo --> m_dsh-session-title
  m_dsh-agent-spine-demo --> m_dsh-skill
  m_dsh-agent-spine-demo --> m_dsh-skill-filesystem
  m_dsh-agent-spine-demo --> m_dsh-system-prompt
  m_dsh-agent-spine-demo --> m_dsh-jobs-local
  m_dsh-agent-spine-demo --> m_dsh-shell-env
  m_dsh-agent-spine-demo --> m_dsh-tool-bash
  m_dsh-agent-spine-demo --> m_dsh-tool-goal
  m_dsh-agent-spine-demo --> m_dsh-tool-skill
  m_dsh-agent-spine-demo --> m_dsh-tool-jobs
  m_dsh-agent-spine-demo --> m_dsh-tools
  m_dsh-agent-spine-demo --> m_dsh-agent-instructions
  m_dsh-agent-spine-demo --> m_cordis
  m_dsh-session-persistence-jsonl --> m_dsh-invariants
  m_dsh-session-persistence-jsonl --> m_dsh-session
  m_dsh-session-persistence-jsonl --> m_dsh-session-persistence
  m_dsh-session-persistence-jsonl --> m_cordis
  m_dsh-session-checkpoint-policy --> m_dsh-agent
  m_dsh-session-checkpoint-policy --> m_dsh-invariants
  m_dsh-session-checkpoint-policy --> m_dsh-llm
  m_dsh-session-checkpoint-policy --> m_dsh-session
  m_dsh-session-checkpoint-policy --> m_dsh-session-persistence
  m_dsh-session-checkpoint-policy --> m_dsh-tools
  m_dsh-session-checkpoint-policy --> m_cordis
  m_dsh-subagent --> m_dsh-agent
  m_dsh-subagent --> m_dsh-agent-presets
  m_dsh-subagent --> m_dsh-brand
  m_dsh-subagent --> m_dsh-invariants
  m_dsh-subagent --> m_dsh-llm
  m_dsh-subagent --> m_dsh-sandbox
  m_dsh-subagent --> m_dsh-sandbox-policy
  m_dsh-subagent --> m_dsh-scope
  m_dsh-subagent --> m_dsh-session
  m_dsh-subagent --> m_dsh-session-persistence
  m_dsh-subagent --> m_dsh-session-projection
  m_dsh-subagent --> m_dsh-session-projection-cache
  m_dsh-subagent --> m_dsh-jobs
  m_dsh-subagent --> m_dsh-tools
  m_dsh-subagent --> m_dsh-user-approval
  m_dsh-subagent --> m_cordis
  m_dsh-subagent-spawn-in-process --> m_dsh-invariants
  m_dsh-subagent-spawn-in-process --> m_dsh-subagent
  m_dsh-subagent-spawn-in-process --> m_dsh-subagent-in-process-driver
  m_dsh-subagent-spawn-in-process --> m_cordis
  m_dsh-tool-subagent --> m_dsh-agent
  m_dsh-tool-subagent --> m_dsh-invariants
  m_dsh-tool-subagent --> m_dsh-llm
  m_dsh-tool-subagent --> m_dsh-subagent
  m_dsh-tool-subagent --> m_dsh-system-prompt
  m_dsh-tool-subagent --> m_dsh-jobs
  m_dsh-tool-subagent --> m_dsh-tools
  m_dsh-tool-subagent --> m_cordis
  m_dsh-tool-todo --> m_dsh-agent
  m_dsh-tool-todo --> m_dsh-invariants
  m_dsh-tool-todo --> m_dsh-session
  m_dsh-tool-todo --> m_dsh-session-projection
  m_dsh-tool-todo --> m_dsh-tools
  m_dsh-tool-todo --> m_cordis
  m_dsh-fs-local --> m_dsh-fs
  m_dsh-fs-local --> m_dsh-invariants
  m_dsh-fs-local --> m_cordis
  m_dsh-fs-observation-policy --> m_dsh-fs
  m_dsh-fs-observation-policy --> m_dsh-invariants
  m_dsh-fs-observation-policy --> m_cordis
  m_dsh-tool-fs --> m_dsh-attachment
  m_dsh-tool-fs --> m_dsh-fs
  m_dsh-tool-fs --> m_dsh-invariants
  m_dsh-tool-fs --> m_dsh-llm
  m_dsh-tool-fs --> m_dsh-sandbox
  m_dsh-tool-fs --> m_dsh-sandbox-policy
  m_dsh-tool-fs --> m_dsh-session
  m_dsh-tool-fs --> m_dsh-system-prompt
  m_dsh-tool-fs --> m_dsh-tools
  m_dsh-tool-fs --> m_dsh-user-approval
  m_dsh-tool-fs --> m_cordis
  m_dsh-token-meter --> m_dsh-compaction
  m_dsh-token-meter --> m_dsh-invariants
  m_dsh-token-meter --> m_dsh-llm
  m_dsh-token-meter --> m_dsh-session
  m_dsh-token-meter --> m_dsh-session-projection
  m_dsh-token-meter --> m_cordis
  m_dsh-compaction-basic --> m_dsh-agent
  m_dsh-compaction-basic --> m_dsh-compaction
  m_dsh-compaction-basic --> m_dsh-commands
  m_dsh-compaction-basic --> m_dsh-invariants
  m_dsh-compaction-basic --> m_dsh-llm
  m_dsh-compaction-basic --> m_dsh-session
  m_dsh-compaction-basic --> m_dsh-token-meter
  m_dsh-compaction-basic --> m_dsh-compaction-tool-result-pruner
  m_dsh-compaction-basic --> m_cordis
```

## devDependencies（开发期依赖；全员开发期框架依赖 cordis / dsh-invariants / cordis-plugin-loader / cordis-plugin-include 为省略项）（69 模块 / 149 依赖边）

```mermaid
flowchart LR
  m_cordis-plugin-timer["cordis-plugin-timer"]
  m_dsh-agent["dsh-agent"]
  m_dsh-agent-instructions["dsh-agent-instructions"]
  m_dsh-agent-loop["dsh-agent-loop"]
  m_dsh-agent-loop-testkit["dsh-agent-loop-testkit"]
  m_dsh-agent-presets["dsh-agent-presets"]
  m_dsh-agent-spine-demo["dsh-agent-spine-demo"]
  m_dsh-anonymous-user-id["dsh-anonymous-user-id"]
  m_dsh-attachment["dsh-attachment"]
  m_dsh-bash-local["dsh-bash-local"]
  m_dsh-bash-sandbox["dsh-bash-sandbox"]
  m_dsh-brand["dsh-brand"]
  m_dsh-commands["dsh-commands"]
  m_dsh-compaction["dsh-compaction"]
  m_dsh-compaction-basic["dsh-compaction-basic"]
  m_dsh-compaction-tool-result-pruner["dsh-compaction-tool-result-pruner"]
  m_dsh-credentials["dsh-credentials"]
  m_dsh-fs["dsh-fs"]
  m_dsh-fs-local["dsh-fs-local"]
  m_dsh-fs-observation-policy["dsh-fs-observation-policy"]
  m_dsh-fs-sandbox["dsh-fs-sandbox"]
  m_dsh-goal["dsh-goal"]
  m_dsh-goal-round-driver["dsh-goal-round-driver"]
  m_dsh-home-paths["dsh-home-paths"]
  m_dsh-jobs["dsh-jobs"]
  m_dsh-jobs-local["dsh-jobs-local"]
  m_dsh-launch-environment["dsh-launch-environment"]
  m_dsh-llm["dsh-llm"]
  m_dsh-llm-deepseek["dsh-llm-deepseek"]
  m_dsh-llm-retry["dsh-llm-retry"]
  m_dsh-loader-smoke["dsh-loader-smoke"]
  m_dsh-sandbox["dsh-sandbox"]
  m_dsh-sandbox-local["dsh-sandbox-local"]
  m_dsh-sandbox-policy["dsh-sandbox-policy"]
  m_dsh-scope["dsh-scope"]
  m_dsh-sdk-jsonrpc-server["dsh-sdk-jsonrpc-server"]
  m_dsh-sdk-protocol["dsh-sdk-protocol"]
  m_dsh-session["dsh-session"]
  m_dsh-session-checkpoint-policy["dsh-session-checkpoint-policy"]
  m_dsh-session-persistence["dsh-session-persistence"]
  m_dsh-session-persistence-jsonl["dsh-session-persistence-jsonl"]
  m_dsh-session-projection["dsh-session-projection"]
  m_dsh-session-projection-cache["dsh-session-projection-cache"]
  m_dsh-session-title["dsh-session-title"]
  m_dsh-settings["dsh-settings"]
  m_dsh-shell["dsh-shell"]
  m_dsh-shell-env["dsh-shell-env"]
  m_dsh-skill["dsh-skill"]
  m_dsh-skill-filesystem["dsh-skill-filesystem"]
  m_dsh-storage["dsh-storage"]
  m_dsh-storage-domain["dsh-storage-domain"]
  m_dsh-subagent["dsh-subagent"]
  m_dsh-subagent-in-process-driver["dsh-subagent-in-process-driver"]
  m_dsh-subagent-spawn-in-process["dsh-subagent-spawn-in-process"]
  m_dsh-subprocess["dsh-subprocess"]
  m_dsh-subprocess-local["dsh-subprocess-local"]
  m_dsh-system-prompt["dsh-system-prompt"]
  m_dsh-timeout["dsh-timeout"]
  m_dsh-token-meter["dsh-token-meter"]
  m_dsh-tool-bash["dsh-tool-bash"]
  m_dsh-tool-fs["dsh-tool-fs"]
  m_dsh-tool-goal["dsh-tool-goal"]
  m_dsh-tool-jobs["dsh-tool-jobs"]
  m_dsh-tool-skill["dsh-tool-skill"]
  m_dsh-tool-subagent["dsh-tool-subagent"]
  m_dsh-tool-todo["dsh-tool-todo"]
  m_dsh-tools["dsh-tools"]
  m_dsh-user-approval["dsh-user-approval"]
  m_dsh-user-questions["dsh-user-questions"]
  m_dsh-sdk-jsonrpc-server --> m_dsh-agent
  m_dsh-sdk-jsonrpc-server --> m_dsh-agent-spine-demo
  m_dsh-sdk-jsonrpc-server --> m_dsh-llm
  m_dsh-sdk-jsonrpc-server --> m_dsh-llm-deepseek
  m_dsh-sdk-jsonrpc-server --> m_dsh-scope
  m_dsh-sdk-jsonrpc-server --> m_dsh-sdk-protocol
  m_dsh-sdk-jsonrpc-server --> m_dsh-session
  m_dsh-sdk-jsonrpc-server --> m_dsh-session-persistence-jsonl
  m_dsh-sdk-jsonrpc-server --> m_dsh-subagent
  m_dsh-llm-deepseek --> m_dsh-credentials
  m_dsh-llm-deepseek --> m_dsh-launch-environment
  m_dsh-llm-deepseek --> m_dsh-llm
  m_dsh-llm-deepseek --> m_dsh-settings
  m_dsh-llm-deepseek --> m_dsh-timeout
  m_dsh-llm-deepseek --> m_dsh-anonymous-user-id
  m_dsh-subprocess-local --> m_dsh-loader-smoke
  m_dsh-subprocess-local --> m_dsh-subprocess
  m_dsh-subprocess-local --> m_dsh-timeout
  m_dsh-bash-local --> m_dsh-shell
  m_dsh-bash-local --> m_dsh-subprocess
  m_dsh-bash-local --> m_dsh-subprocess-local
  m_dsh-bash-local --> m_dsh-timeout
  m_dsh-bash-local --> m_dsh-settings
  m_dsh-agent-spine-demo --> m_cordis-plugin-timer
  m_dsh-agent-spine-demo --> m_dsh-agent
  m_dsh-agent-spine-demo --> m_dsh-agent-loop
  m_dsh-agent-spine-demo --> m_dsh-shell-env
  m_dsh-agent-spine-demo --> m_dsh-bash-local
  m_dsh-agent-spine-demo --> m_dsh-bash-sandbox
  m_dsh-agent-spine-demo --> m_dsh-fs-local
  m_dsh-agent-spine-demo --> m_dsh-fs-observation-policy
  m_dsh-agent-spine-demo --> m_dsh-fs-sandbox
  m_dsh-agent-spine-demo --> m_dsh-goal
  m_dsh-agent-spine-demo --> m_dsh-goal-round-driver
  m_dsh-agent-spine-demo --> m_dsh-llm
  m_dsh-agent-spine-demo --> m_dsh-home-paths
  m_dsh-agent-spine-demo --> m_dsh-llm-retry
  m_dsh-agent-spine-demo --> m_dsh-subprocess-local
  m_dsh-agent-spine-demo --> m_dsh-sandbox-local
  m_dsh-agent-spine-demo --> m_dsh-sandbox-policy
  m_dsh-agent-spine-demo --> m_dsh-scope
  m_dsh-agent-spine-demo --> m_dsh-session
  m_dsh-agent-spine-demo --> m_dsh-session-title
  m_dsh-agent-spine-demo --> m_dsh-skill
  m_dsh-agent-spine-demo --> m_dsh-skill-filesystem
  m_dsh-agent-spine-demo --> m_dsh-system-prompt
  m_dsh-agent-spine-demo --> m_dsh-jobs
  m_dsh-agent-spine-demo --> m_dsh-jobs-local
  m_dsh-agent-spine-demo --> m_dsh-tool-bash
  m_dsh-agent-spine-demo --> m_dsh-tool-fs
  m_dsh-agent-spine-demo --> m_dsh-tool-goal
  m_dsh-agent-spine-demo --> m_dsh-tool-skill
  m_dsh-agent-spine-demo --> m_dsh-tool-jobs
  m_dsh-agent-spine-demo --> m_dsh-tools
  m_dsh-agent-spine-demo --> m_dsh-agent-instructions
  m_dsh-session-persistence-jsonl --> m_dsh-session
  m_dsh-session-persistence-jsonl --> m_dsh-session-persistence
  m_dsh-session-checkpoint-policy --> m_dsh-agent
  m_dsh-session-checkpoint-policy --> m_dsh-agent-loop
  m_dsh-session-checkpoint-policy --> m_dsh-agent-loop-testkit
  m_dsh-session-checkpoint-policy --> m_dsh-llm
  m_dsh-session-checkpoint-policy --> m_dsh-session
  m_dsh-session-checkpoint-policy --> m_dsh-session-persistence
  m_dsh-session-checkpoint-policy --> m_dsh-session-persistence-jsonl
  m_dsh-session-checkpoint-policy --> m_dsh-system-prompt
  m_dsh-session-checkpoint-policy --> m_dsh-tools
  m_dsh-subagent --> m_dsh-agent
  m_dsh-subagent --> m_dsh-agent-presets
  m_dsh-subagent --> m_dsh-brand
  m_dsh-subagent --> m_dsh-llm
  m_dsh-subagent --> m_dsh-sandbox
  m_dsh-subagent --> m_dsh-sandbox-policy
  m_dsh-subagent --> m_dsh-scope
  m_dsh-subagent --> m_dsh-session
  m_dsh-subagent --> m_dsh-session-persistence
  m_dsh-subagent --> m_dsh-session-projection
  m_dsh-subagent --> m_dsh-session-projection-cache
  m_dsh-subagent --> m_dsh-storage
  m_dsh-subagent --> m_dsh-storage-domain
  m_dsh-subagent --> m_dsh-jobs
  m_dsh-subagent --> m_dsh-tools
  m_dsh-subagent --> m_dsh-user-approval
  m_dsh-subagent-spawn-in-process --> m_dsh-agent
  m_dsh-subagent-spawn-in-process --> m_dsh-agent-loop
  m_dsh-subagent-spawn-in-process --> m_dsh-agent-loop-testkit
  m_dsh-subagent-spawn-in-process --> m_dsh-bash-local
  m_dsh-subagent-spawn-in-process --> m_dsh-subprocess-local
  m_dsh-subagent-spawn-in-process --> m_dsh-llm
  m_dsh-subagent-spawn-in-process --> m_dsh-llm-deepseek
  m_dsh-subagent-spawn-in-process --> m_dsh-session
  m_dsh-subagent-spawn-in-process --> m_dsh-subagent
  m_dsh-subagent-spawn-in-process --> m_dsh-subagent-in-process-driver
  m_dsh-subagent-spawn-in-process --> m_dsh-tool-bash
  m_dsh-subagent-spawn-in-process --> m_dsh-tool-subagent
  m_dsh-tool-subagent --> m_dsh-agent
  m_dsh-tool-subagent --> m_dsh-llm
  m_dsh-tool-subagent --> m_dsh-session
  m_dsh-tool-subagent --> m_dsh-session-persistence
  m_dsh-tool-subagent --> m_dsh-session-persistence-jsonl
  m_dsh-tool-subagent --> m_dsh-subagent
  m_dsh-tool-subagent --> m_dsh-subagent-spawn-in-process
  m_dsh-tool-subagent --> m_dsh-system-prompt
  m_dsh-tool-subagent --> m_dsh-jobs
  m_dsh-tool-subagent --> m_dsh-jobs-local
  m_dsh-tool-subagent --> m_dsh-tool-jobs
  m_dsh-tool-subagent --> m_dsh-tools
  m_dsh-tool-todo --> m_dsh-agent
  m_dsh-tool-todo --> m_dsh-agent-loop
  m_dsh-tool-todo --> m_dsh-agent-loop-testkit
  m_dsh-tool-todo --> m_dsh-llm
  m_dsh-tool-todo --> m_dsh-session
  m_dsh-tool-todo --> m_dsh-session-projection
  m_dsh-tool-todo --> m_dsh-system-prompt
  m_dsh-tool-todo --> m_dsh-tools
  m_dsh-tool-todo --> m_dsh-user-questions
  m_dsh-fs-local --> m_dsh-fs
  m_dsh-fs-local --> m_dsh-llm
  m_dsh-fs-observation-policy --> m_dsh-fs
  m_dsh-fs-observation-policy --> m_dsh-llm
  m_dsh-tool-fs --> m_dsh-agent
  m_dsh-tool-fs --> m_dsh-agent-loop
  m_dsh-tool-fs --> m_dsh-agent-loop-testkit
  m_dsh-tool-fs --> m_dsh-attachment
  m_dsh-tool-fs --> m_dsh-fs
  m_dsh-tool-fs --> m_dsh-fs-local
  m_dsh-tool-fs --> m_dsh-fs-observation-policy
  m_dsh-tool-fs --> m_dsh-llm
  m_dsh-tool-fs --> m_dsh-llm-deepseek
  m_dsh-tool-fs --> m_dsh-sandbox
  m_dsh-tool-fs --> m_dsh-sandbox-policy
  m_dsh-tool-fs --> m_dsh-session
  m_dsh-tool-fs --> m_dsh-system-prompt
  m_dsh-tool-fs --> m_dsh-tools
  m_dsh-tool-fs --> m_dsh-user-approval
  m_dsh-token-meter --> m_dsh-compaction
  m_dsh-token-meter --> m_dsh-llm
  m_dsh-token-meter --> m_dsh-session
  m_dsh-token-meter --> m_dsh-session-projection
  m_dsh-compaction-basic --> m_dsh-agent
  m_dsh-compaction-basic --> m_dsh-agent-loop
  m_dsh-compaction-basic --> m_dsh-agent-loop-testkit
  m_dsh-compaction-basic --> m_dsh-compaction
  m_dsh-compaction-basic --> m_dsh-commands
  m_dsh-compaction-basic --> m_dsh-llm
  m_dsh-compaction-basic --> m_dsh-llm-retry
  m_dsh-compaction-basic --> m_dsh-session
  m_dsh-compaction-basic --> m_dsh-token-meter
  m_dsh-compaction-basic --> m_dsh-compaction-tool-result-pruner
  m_dsh-compaction-basic --> m_dsh-tools
```
