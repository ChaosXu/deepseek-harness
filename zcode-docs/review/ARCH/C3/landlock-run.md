# 组件 ⑥ landlock-run 子进程（子进程）

模块 = `native/landlock-run`（C11，静态 musl）的编译/分发单元。边 A --> B 表示 A 依赖 B。

```mermaid
flowchart LR
  MAIN["packages/entry/src/main.c<br/>（唯一编译单元：raw Landlock UAPI，<br/>self-restrict-then-exec，fail-closed）"]
  UAPI["Linux Landlock UAPI 头<br/>（linux/landlock.h，内核 ≥5.13）"]
  MUSL["musl 静态 libc"]
  ENTRY["@deepseek-ai/node-addon-landlock-run<br/>（JS 入口包，argv 包装接口）"]
  X64["linux-x64 平台包<br/>（预编译二进制）"]
  ARM["linux-arm64 平台包<br/>（预编译二进制）"]

  MAIN --> UAPI
  MAIN --> MUSL
  ENTRY --> X64
  ENTRY --> ARM
  X64 & ARM -.->|"同一 main.c 的构建产物"| MAIN
```

说明：由 ①③④ 的 `dsh-sandbox-local`（Linux 后端链 bwrap → landlock 的后备 rung）作为 argv 包装器 spawn；exec 后即成为被限制的 ⑦ 目标进程（PID 不变，权限已收窄）。
