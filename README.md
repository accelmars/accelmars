## AccelMars

**Rust-native infrastructure for AI-era work.**

I build the systems that let one founder plus an AI workforce operate at the scale that used to
take a team. Most of that machinery is private. What follows is what is published, and what you
can actually do with it today.

### Published here

| Repository | What it is | Status |
|---|---|---|
| [**anchor**](https://github.com/accelmars/anchor) | `mv` for Markdown workspaces — move a file, and the links pointing at it follow. Rust CLI. | `v2.1.0` · Apache-2.0 |
| [**os-env**](https://github.com/accelmars/os-env) | The env-var contract engines read at startup. Small support crate; published because `anchor` depends on it. | `v0.3.1` · Apache-2.0 |
| [**mind-template**](https://github.com/accelmars/mind-template) | Continuity across AI sessions in plain Markdown — a protocol a fresh AI can pick up without a recap. Template — click *Use this template*. | `v2.0.0` · Apache-2.0 |
| [**.github**](https://github.com/accelmars/.github) | Account-wide contribution, conduct, security and support defaults. | — |

Neither Rust crate is on crates.io. Install `anchor` from source, pinned to a release:

```sh
cargo install --git https://github.com/accelmars/anchor --tag accelmars-anchor-v2.1.0
```

### What is not here

Most AccelMars engines are private. Whether a given engine is published is a deliberate decision
made one engine at a time — there is no blanket promise that more will follow, and no timeline.
If a repository is not listed above, it is not public.

### The company

AccelMars is building an AI-era company operating system and is **not open for sale** — no general
availability, no paying customers. [accelmars.com](https://accelmars.com) is the front door;
[`llms.txt`](https://accelmars.com/llms.txt) is the machine-readable version of the same posture.

📍 Ho Chi Minh City, Vietnam · ✉️ hello@accelmars.com

---

<sub>AccelMars Co., Ltd.</sub>
