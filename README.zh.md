<div align="center">

# 🪞 QBE 镜像仓库

**[QBE](https://c9x.me/compile/) 的非官方自动同步 GitHub 镜像**

Quentin Carayol 开发的小型可嵌入编译器后端 —
*"以 10% 的代码量，达到先进编译器 70% 的性能。"*

[![同步状态](https://github.com/azhzx/qbe_lastest_mirror/actions/workflows/mirror.yml/badge.svg)](https://github.com/azhzx/qbe_lastest_mirror/actions/workflows/mirror.yml)
[![最新标签](https://img.shields.io/github/v/tag/azhzx/qbe_lastest_mirror?label=%E6%9C%80%E6%96%B0%E6%A0%87%E7%AD%BE&sort=semver)](https://github.com/azhzx/qbe_lastest_mirror/tags)
[![许可证](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/azhzx/qbe_lastest_mirror/blob/master/LICENSE)
[![上游](https://img.shields.io/badge/%E4%B8%8A%E6%B8%B8-c9x.me-orange)](https://c9x.me/compile/)

[English](README.md) · 简体中文

</div>

---

## ✨ 为什么有这个镜像

QBE 官方仓库只提供 **git 协议**（`git://c9x.me/qbe.git`），部分网络、代理和 CI 环境会封锁 9418 端口。本仓库把它以 HTTPS 方式重新发布在 GitHub 上，并**每天自动与上游同步一次**，让你可以像普通 GitHub 项目一样 clone、钉版本、引入构建。

> QBE 是一个用纯 C 编写的小型可嵌入编译器后端，目标架构为 amd64、arm64 和 rv64。

## 📦 使用方法

> [!IMPORTANT]
> 默认分支 `main` 只存放镜像元数据。**代码在 `master` 分支和各 release 标签上。**

```sh
# 同步最新上游代码
git clone -b master https://github.com/azhzx/qbe_lastest_mirror.git

# 锁定某个发布版本
git clone -b v1.3 --depth 1 https://github.com/azhzx/qbe_lastest_mirror.git
```

或在已有仓库中作为远程源使用：

```sh
git remote add qbe https://github.com/azhzx/qbe_lastest_mirror.git
git fetch qbe --tags
```

按上游文档构建：

```sh
make
make test   # 可选
```

## 🗂 仓库结构

| 引用 | 内容 |
| --- | --- |
| `main` | 仅镜像元数据（本 README + 同步 workflow），**不是**上游代码 |
| `master` | 上游默认分支，每次同步 force-push 覆盖 |
| `dev` · `loopopt` | 上游开发分支 |
| `v1.0` … `v1.3` | 上游发布标签 |

## ⚙️ 同步机制

一个 [GitHub Actions workflow](.github/workflows/mirror.yml) 完成全部工作：

- 🕐 每天约**北京时间 05:17** 运行（cron `17 21 * * *` UTC）— 定时任务可能有几分钟延迟，属正常现象
- 🔄 裸克隆 `git://c9x.me/qbe.git` 并 force-push **全部分支和标签**，忠实跟随上游——包括上游强推回滚历史的情况
- 🔘 可随时手动触发：[Actions 页面](https://github.com/azhzx/qbe_lastest_mirror/actions/workflows/mirror.yml)或 `gh workflow run mirror.yml`
- 💓 若上游长期无提交，会在 `main` 上补一个空 "keepalive" 提交，防止 GitHub 因 60 天无活动自动停用定时任务

## 📌 注意事项

- **这是只读镜像。** Bug 反馈和补丁请提交给上游 — QBE **仅接受邮件补丁**（见[官网](https://c9x.me/compile/)），在本仓库开 issue 无法自动转发。
- QBE 采用 MIT 许可，版权归上游作者所有。本镜像与 QBE 官方项目无隶属关系。
- 同步正确性逐引用核对：每次同步后，本仓库每个分支/标签与上游 SHA 完全一致。

---

<div align="center">

[English](README.md) · 简体中文

**QBE** © Quentin Carayol · 镜像由 [@azhzx](https://github.com/azhzx) 维护

</div>
