# 安妮播放器 iOS 仓库 · AI 协作规范

本文件适用于所有参与本仓库的人类贡献者与 AI agent。开始任何修改前，必须先阅读本文件及 `CONTRIBUTING.md`。

## 一、项目边界

- **章鱼只负责 Windows 版开发**，不负责 iOS 或其他桌面/移动平台的功能开发。
- 本仓库的 iOS 应用由社区贡献者设计、实现、测试和维护；章鱼作为仓库 owner 进行治理、评审与发布审批，不承诺实现 iOS 需求。
- 当前仓库尚无 iOS 应用源码或真实工程。不得伪造工程、构建结果、测试记录、Run、Artifact、SHA256 或发布状态。

## 二、分支与 PR 硬规则

1. 所有人和 AI 的所有改动都必须从独立分支发起 PR；功能开发使用 `feature/<主题>`，治理任务可使用 `chore/<主题>`。
2. **禁止直接推送 `main`**，包括文档、配置、格式化及“微小修复”。AI 不得以任务紧急、已获口头认可等理由绕过 PR。
3. 未经 owner 明确批准，任何人和 AI 均不得创建或推送 tag、创建或发布 Release，也不得擅自合并 PR 或修改仓库设置。
4. PR 必须如实列出改动、验证命令与结果、未验证事项和已知限制；不得把“未运行”写成“通过”。
5. 代码、文档、workflow 的变更都要经过审阅。AI 生成内容由提交者负责核对，不能以 AI 输出代替测试或审查。

## 三、联系与 agent 汇报

- **QQ 是主要联系渠道**，具体联系方式以章鱼公开的信息为准。
- 需要章鱼协调评审、权限、Runner、签名或发布时，贡献者 agent 必须发送以下标准模板；没有的项目填“无”，不得编造：

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

## 四、秘密、证书与权限

- 密码、令牌、私钥、签名证书、provisioning profile、keystore 及其他凭据**不得通过 QQ 传输**，也不得进入 Git、Issue、PR、日志、截图或 Artifact。
- 所需秘密和证书由 owner 在 **GitHub Secrets / Environments** 中配置并授权。贡献者只说明条目名称、用途和最小权限，不索取明文。
- PR 及来自 fork 的无签名构建不得读取发布秘密。发现泄露时立即停止相关工作流，并通过安全渠道通知 owner 轮换凭据。

## 五、文件与构建产物

- 大二进制不得提交到 Git，包括安装包、IPA、xcarchive、dSYM 包、构建缓存及大型媒体样本；使用 GitHub Actions Artifact 或 Release 资产交付。
- 签名材料与本地配置只保留在开发者本机或 GitHub Secrets / Environments，仓库中不得放入真实凭据。
- 当前 `build_release.yml` 与 `delivery.yml` 仅为拒绝执行的占位保护，不提供构建或发布能力。真实工程落地后，必须通过 PR 替换并验证，流程约束见 `RELEASING.md`。
- 保持现有 `LICENSE` 不变，除非另有明确授权与独立 PR。
