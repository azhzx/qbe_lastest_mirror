# qbe_lastest_mirror

[QBE](https://c9x.me/compile/)（Quentin Carayol 开发的小型编译器后端）的**每日自动镜像**。

QBE 官方仓库托管在 c9x.me（`git://c9x.me/qbe.git`），仅提供 git 协议。本仓库由 GitHub Actions 每天自动从上游同步一次，方便直接从 GitHub clone 和引用。

## 使用

- **代码在 `master` 分支和各 release tag 上**（与上游保持一致，force-push 同步）
- `main` 分支只存放镜像元数据（README + 同步 workflow），不是代码分支

```sh
# 克隆最新代码
git clone https://github.com/azhzx/qbe_lastest_mirror.git
cd qbe_lastest_mirror

# 或克隆指定 release
git clone -b v1.2 --depth 1 https://github.com/azhzx/qbe_lastest_mirror.git
```

## 同步机制

- [.github/workflows/mirror.yml](.github/workflows/mirror.yml) 每天约 **北京时间 05:17**（UTC 21:17）运行：从上游拉取全部分支和 tag，force-push 到本仓库
- GitHub 定时任务可能有几分钟到几十分钟的延迟；也可在 Actions 页面手动触发（`workflow_dispatch`）
- 若上游长期无提交，workflow 会定期在 `main` 上补一个空提交，防止 GitHub 因 60 天无活动自动停用定时任务

## 注意

- 这是**只读镜像**：bug 报告和补丁请发往上游邮件列表（见 [QBE 官网](https://c9x.me/compile/)），c9x.me 仅接受邮件补丁
- QBE 采用 MIT 许可，镜像保留原版权声明，权利归上游作者所有
