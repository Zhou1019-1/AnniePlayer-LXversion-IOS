# 贡献指南

感谢参与安妮播放器 iOS 版。请先阅读 `AGENTS.md`，本指南适用于人类贡献者与 AI agent。

## 责任分工

**章鱼只负责 Windows 版开发。** iOS 及其他非 Windows 平台由社区贡献者开发、测试和维护。章鱼作为仓库 owner 负责治理、评审与发布审批，不承担 iOS 功能实现义务。

当前仓库只有治理骨架，尚无 iOS 应用源码或工程。在真实工程经 PR 合入前，不应提交虚构的构建说明、测试结果或发布产物。

## 提交流程

1. 从最新 `main` 创建 `feature/<主题>` 分支；治理类任务可使用 `chore/<主题>`。
2. 保持改动聚焦，提交前检查 diff，不混入无关文件、构建产物或本地配置。
3. 推送分支并创建 PR，填写 PR 模板，说明改动动机、实际验证及已知限制。
4. 根据评审意见在原分支继续提交；需要 owner 协助时通过 QQ 联系。
5. 等待有权限的审阅者处理 PR。贡献者和 AI 不得自行合并，除非获得 owner 对该操作的明确授权。

**所有人和 AI 均不得直推 `main`，不得绕过 PR。未经 owner 明确批准，不得创建/推送 tag 或创建/发布 Release。**

## 验证要求

- 运行与改动相匹配的检查，并在 PR 中给出命令和真实结果。
- 文档/治理改动至少执行 `git diff --check`，核对必需文件、忽略规则和 workflow 语法。
- 未来存在真实工程后，功能改动须补充或更新相应测试；无法运行的项目必须说明原因，不能写成“通过”。
- 构建交付应提供 Actions Run、Artifact 和产物 SHA256；无产物时明确填“无”。

## QQ 汇报模板

QQ 是主要联系渠道。贡献者 agent 向章鱼请求协助或汇报交付时，使用以下模板（没有的项目填“无”）：

```text
仓库：<owner/repo 与 URL>
PR：<PR URL 或编号；未创建则说明>
分支 commit：<分支名 + 完整 commit SHA>
改动：<按文件概述实际改动>
测试：<逐项列出命令、结果；未运行须注明>
Run 或 Artifact：<GitHub Actions Run / Artifact URL；无则填无>
SHA256：<交付产物的 SHA256；无产物则填无>
需要协助：<需要章鱼处理的具体事项；无则填无>
已知限制：<风险、未覆盖场景或平台限制；无则填无>
```

## 安全与文件约束

- 秘密和证书**不走 QQ**，也不进入仓库、Issue、PR、日志或 Artifact。由 owner 配置 GitHub Secrets / Environments；贡献者只提供所需条目名称、用途和最小权限。
- 大二进制不进 Git。IPA、xcarchive、dSYM 包及其他构建产物通过 Actions Artifact 或 Release 资产交付。
- 不提交 `.p12`、`.mobileprovision`、私钥、真实环境变量或其他本地签名材料；具体忽略规则见 `.gitignore`。
- 安全问题的沟通方式见 `SECURITY.md`，发布边界见 `RELEASING.md`。
