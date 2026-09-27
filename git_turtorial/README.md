# IceCream Arm Git 协作指南

[返回项目首页](../README.md) · [查看远端分支](https://github.com/EdieMaxie/icecream_arm/branches) · [发起 Pull Request](https://github.com/EdieMaxie/icecream_arm/compare)

当前远端以 `main` 为集成分支，另有 `feature/head`、`feature/motor_driver` 和三个 `feature/raspberryPi-*` 分支。**没有 `develop` 分支**；旧文档中先合入 `develop` 的步骤不适用。

## 新改动怎么推送

```bash
git switch main
git pull --ff-only origin main
git switch -c feature/my-change  # 修复可用 fix/my-bug

# 修改并完成对应验证后
git status
git add <相关文件>
git commit -m "简要说明本次改动"
git push -u origin feature/my-change
```

在 GitHub 上由该分支向 `main` 发起 [Pull Request](https://github.com/EdieMaxie/icecream_arm/compare)。PR 写清改动范围、运行或测试方法、结果；涉及 PC/Pi/STM32 通信时，补充两端分支或提交、协议版本与实机验证结果。审查并验证后合入 `main`。

## 分支使用规则

- `main`：集成入口。只接收已审查、已验证的 PR；发布前确认 README 与实际代码相符。
- 现有 `feature/*`：保留各自开发历史。改动前先看对应分支 README 和与 `main` 的差异，不直接混合多个设备分支。
- 新 `feature/*`、`fix/*`：从最新 `main` 拉取，围绕单一改动，完成后提 PR。
- 不向共享分支强制推送；不要提交令牌、密码、机器专属配置、日志或构建产物。硬件参数与标定文件需要明确适用设备。

常用检查：`git status` 查看工作区；`git branch -r` 查看远端分支；`git diff --check` 检查空白错误；`git fetch origin` 后用 `git log --oneline main..origin/<分支>` 查看待集成提交。
