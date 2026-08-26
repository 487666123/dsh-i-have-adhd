# dsh-i-have-adhd

[DeepSeek Harness (DSH)](https://github.com/search?q=deepseek+harness) 的 ADHD 友好输出塑形：一个系统提示词区段改变助手的回复方式——行动先行、编号步骤、具体时间估算、零客套——附带可随时开关、重启保持的控制工具。

灵感来自 [ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd)（MIT）。本包的规则文本是为 DSH 全新重写的原创表达，详见 [THIRD-PARTY-NOTICES.md](./THIRD-PARTY-NOTICES.md)。

## 改变什么

| 之前 | 之后 |
| --- | --- |
| "好问题！让我想想。你的鉴权流程有好几个环节：中间件、令牌校验，还有……希望能帮到你！" | "运行 `npm install jsonwebtoken@latest`，然后改 `src/auth.ts:42`。1. 打开文件 2. 替换 `verifyToken` 3. 跑测试。下一步：贴出第一条失败日志。" |

## 工作原理

- 一个系统提示词区段（`dsh-i-have-adhd`，order 50——排在 persona 之后、工具指引之前）在模式开启时进入每个模型步。
- 三个零参数 agent 工具控制它：
  - `adhd_on` —— 本会话开启并持久化（标志文件在 `$DSH_HOME/dsh-i-have-adhd/`）
  - `adhd_off` —— 关闭并清除标志
  - `adhd_status` —— 报告状态、开启时间、重启是否恢复
- 持久化标志在启动时自动恢复模式。
- 区段通过 systemPrompt 服务注册，开关在下一个模型步立即生效——不用重启会话，不用刷新页面。

## 使用

安装后对话里直接说：

```text
adhd mode on      → 模型调用 adhd_on，回复立即切换形态
adhd mode off     → 恢复默认风格，标志清除
```

也可以随时查询状态，或自己增删标志文件：
`$DSH_HOME/dsh-i-have-adhd/always-on`（默认 `~/.dsh/dsh-i-have-adhd/always-on`）。

## 规则集

十条规则，按可略读方式分组——全文见 [`dsh/rules.js`](./dsh/rules.js)：

**形态**：首行即行动 · 步骤编号 · 收尾给一个下一步 · 支线靠边
**状态**：每轮复述进度 · 时间估算用真实单位 · 让成果可见
**语气**：错误只陈述事实 · 列表不超过五条 · 不说客套话

明确的覆盖规则：harness 规则优先于本模式；"explain" 请求保留形态但放开深度；破坏性操作仍然先确认；连续三轮调试失败就停下来问一个诊断性问题，而不是继续改代码。

## 安装

```sh
dsh plugin --profile <你的-profile> add dsh-i-have-adhd
```

## 许可证

MIT。第三方声明：概念与名称源自 ayghri/i-have-adhd（MIT），其许可文本完整保留于 [THIRD-PARTY-NOTICES.md](./THIRD-PARTY-NOTICES.md)。
