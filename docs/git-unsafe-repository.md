# Git "Unsafe Repository" 问题记录

## 环境信息

- **平台：** Linux (x86_64)
- **Shell：** sh (root 用户)
- **Git 版本：** Git 2.35.2+（包含安全目录检查）
- **仓库：** `/workspace`（learning-cxx C++ 练习项目）

---

## 问题现象

在 IDE 或终端中执行 Git 操作时，弹出以下警告：

```
The detected Git repository is potentially unsafe as the folder is owned by
someone other than the current user.
```

Git 命令虽然能执行，但每次操作都会提示这个安全警告。

---

## 问题根源

### 1. Git 的安全机制（Safe Directory）

自 Git 2.35.2 起，Git 引入了一个安全机制：**如果仓库目录的所有者与执行 Git 命令的用户不一致，Git 会拒绝执行操作**（或弹出警告）。

这是为了防止以下攻击场景：

> 用户 A 在 `/home/a/project` 创建了一个仓库，并在 `.git/hooks/` 中放置了恶意脚本。
> 用户 B 用 `sudo` 或以其他方式访问该目录执行 Git 命令时，这些钩子脚本可能会以用户 B 的权限执行，造成安全风险。

### 2. 本项目中的具体情况

在本环境中，问题的产生路径如下：

```
（1）克隆仓库时以 root 用户执行
     → 仓库文件所有者 = root

（2）安装 xmake 后，xmake 拒绝以 root 运行
     error: Running xmake as root is extremely dangerous
     → 被迫创建 coder 用户用于编译和测试

（3）用 coder 用户运行 xmake 编译练习
     → chown -R coder:coder /workspace（仓库文件所有者变为 coder）

（4）再次以 root 用户（或 IDE 内的 Git 集成）操作仓库
     → 发现仓库所有者是 coder，不是当前用户 root
     → Git 弹出 "unsafe repository" 警告
```

**核心冲突：** 运行构建工具（xmake）需要 `coder` 用户，但实际的终端/IDE 环境以 `root` 用户运行。两个用户交替操作同一个仓库，导致 Git 的所有者检查失败。

---

## 修复过程

### 第一次尝试：为 coder 用户配置安全目录

```bash
su -c "git config --global safe.directory /workspace" coder
```

**结果：** 未生效。
**原因：** 配置写入了 `coder` 用户的 Git 全局配置（`~coder/.gitconfig`），但实际执行 Git 操作的是 `root` 用户，不读这份配置。

### 第二次尝试（最终解决方案）：为 root 用户配置安全目录

```bash
git config --global safe.directory /workspace
```

**结果：** 立即生效，Git 不再弹出警告。
**验证：**

```bash
git status
# 输出正常，无任何警告
```

---

## 其他修复方式对比

| 方式 | 命令 | 适用场景 | 评价 |
|:---|:---|:---|:---|
| **安全目录（本次采用）** | `git config --global safe.directory <path>` | 单个仓库 | ✅ 精确、安全 |
| 通配符信任 | `git config --global safe.directory '*'` | 所有仓库 | ❌ 关闭了安全检查，不推荐 |
| 修改所有者 | `chown -R 用户:组 /workspace` | 单一用户环境 | ✅ 从根本上解决，但需要知道实际用户 |
| 统一用户 | 全程使用同一用户 | 新环境 | ✅ 最干净，但在 xmake 限制下不可行 |

---

## 经验教训

1. **Git 2.35.2+ 的安全目录检查** 是一个有用但容易被忽略的特性。在多用户环境或容器环境中尤其容易触发。

2. **用户感知问题：** 在多用户交替操作的环境下，需要明确当前操作的用户身份，配置要写入正确的用户名下。

3. **xmake 的限制：** xmake 禁止以 root 运行是其安全设计，在容器/开发环境中需要额外创建普通用户，这会间接引发 Git 安全目录问题。后续如果在类似环境中搭建项目，可以先规划好用户体系：

   ```bash
   # 方案 A：一开始就用普通用户
   useradd -m dev
   chown -R dev:dev /workspace
   su -c "cd /workspace && xmake" dev

   # 方案 B：root 用户 + 跳过 xmake 限制（不推荐）
   # 但 xmake 本身不允许，此路不通
   ```

4. **一条命令解决同类问题：** 如果以后再遇到这个警告，直接执行以下命令即可：

   ```bash
   git config --global safe.directory /workspace
   ```
