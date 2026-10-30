<div align="center">

# 🪞 QBE Mirror

**An unofficial, automatically-synced GitHub mirror of [QBE](https://c9x.me/compile/)**

A small, embeddable compiler backend by Quentin Carayol —
*"70% of the performance of advanced compilers in 10% of the code."*

[![Sync status](https://github.com/azhzx/qbe_lastest_mirror/actions/workflows/mirror.yml/badge.svg)](https://github.com/azhzx/qbe_lastest_mirror/actions/workflows/mirror.yml)
[![Latest tag](https://img.shields.io/github/v/tag/azhzx/qbe_lastest_mirror?label=latest%20tag&sort=semver)](https://github.com/azhzx/qbe_lastest_mirror/tags)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/azhzx/qbe_lastest_mirror/blob/master/LICENSE)
[![Upstream](https://img.shields.io/badge/upstream-c9x.me-orange)](https://c9x.me/compile/)

English · [简体中文](README.zh.md)

</div>

---

## ✨ Why this mirror

The official QBE repository is only reachable over the **git protocol** (`git://c9x.me/qbe.git`), which some networks, proxies, and CI environments block. This repository re-publishes it over HTTPS on GitHub and keeps it in sync with upstream **once a day** — so you can `git clone` / `pip`-style pin / vendor it like any ordinary GitHub project.

> QBE is a small embeddable compiler backend written in pure C. It targets amd64, arm64, and rv64.

## 📦 Usage

> [!IMPORTANT]
> The default branch `main` holds only mirror metadata. **The code lives on `master` and the release tags.**

```sh
# Latest upstream code
git clone -b master https://github.com/azhzx/qbe_lastest_mirror.git

# A pinned release
git clone -b v1.3 --depth 1 https://github.com/azhzx/qbe_lastest_mirror.git
```

Or add it as a remote in an existing repository:

```sh
git remote add qbe https://github.com/azhzx/qbe_lastest_mirror.git
git fetch qbe --tags
```

Build as upstream documents:

```sh
make
make test   # optional
```

## 🗂 Repository layout

| Ref | Content |
| --- | --- |
| `main` | Mirror metadata only (this README + sync workflow) — **not** upstream code |
| `master` | Upstream default branch, force-pushed on every sync |
| `dev` · `loopopt` | Upstream development branches |
| `v1.0` … `v1.3` | Upstream release tags |

## ⚙️ How syncing works

A single [GitHub Actions workflow](.github/workflows/mirror.yml) does everything:

- 🕐 Runs daily at **~05:17 Beijing time** (cron `17 21 * * *` UTC) — scheduled runs can lag by minutes, which is normal
- 🔄 Bare-clones `git://c9x.me/qbe.git` and force-pushes **all branches and tags**, so the mirror faithfully follows upstream — including forced rewinds
- 🔘 Can be triggered manually anytime: the [Actions tab](https://github.com/azhzx/qbe_lastest_mirror/actions/workflows/mirror.yml) or `gh workflow run mirror.yml`
- 💓 If upstream stays quiet for weeks, an empty "keepalive" commit on `main` prevents GitHub from auto-disabling the schedule (the 60-day inactivity rule)

## 📌 Notes

- **This is a read-only mirror.** Bug reports and patches belong upstream — QBE accepts patches **by email only** (see the [official site](https://c9x.me/compile/)). Issues opened here cannot be forwarded automatically.
- QBE is MIT-licensed; all credit and copyright belong to the upstream authors. This mirror is not affiliated with the QBE project.
- Sync correctness is verified per-ref: after each sync, every branch/tag here matches the upstream SHA exactly.

---

<div align="center">

English · [简体中文](README.zh.md)

**QBE** © Quentin Carayol · Mirror maintained by [@azhzx](https://github.com/azhzx)

</div>
