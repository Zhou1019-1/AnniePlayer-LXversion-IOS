# 构建与发布约定

## 当前状态

本仓库尚无真实 iOS 应用工程，因此**当前不可构建、不可签名、不可发布**。

`.github/workflows/build_release.yml` 和 `.github/workflows/delivery.yml` 是手动触发且明确失败的占位保护，用于防止把空仓库包装成成功的构建或交付。它们不会编译源码、生成 Artifact、创建 tag 或 Release，也不代表已具备 CI/CD 能力。不得绕过该保护伪造构建结果。

## 真实工程落地后的目标流程

以下流程只有在真实 iOS 工程、可复现构建与对应测试已通过 PR 合入后才适用。新增或修改 workflow 本身也必须经过 PR 评审。

### 1. PR 无签名构建

- 对代码 PR 执行可复现的**无签名构建**与测试，不使用 Apple 发布证书、私钥或生产签名配置。
- PR（尤其是 fork PR）不得读取发布用 GitHub Secrets / Environments。
- 构建成功后上传明确标注为无签名的 Artifact，并记录 commit SHA、Actions Run URL 和每个产物的 SHA256。
- PR 构建只用于评审和验证，不创建 tag，不创建 Release，不向用户冒充正式版本。

### 2. 受控生成 Draft Release

- 发布准备必须先经 PR 审阅，并获得 owner 对本次发布操作的明确批准。
- 经批准的受控流程方可使用 owner 配置的 GitHub Secrets / Environments 处理签名材料；秘密和证书不得经 QQ 或 Git 传递。
- 流程核验源码 commit、构建与测试结果、产物及 SHA256 后，只创建 **Draft Release**，不得自动公开。
- 贡献者与 AI 不得擅自创建或推送 tag、创建 Release；Draft 阶段也不等于已发布。

### 3. owner 最终发布

- 由 owner 最终核对版本、变更说明、来源 commit、Artifact、SHA256、签名与测试结果。
- 只有 owner 可以决定是否将 Draft Release 转为公开发布；其他贡献者和 AI 不得代替执行或宣布发布。
- 若任何检查不一致，保持 Draft 或取消本次发布，回到 feature 分支通过新 PR 修正，不直推 `main` 补救。
