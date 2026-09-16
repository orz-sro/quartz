# Obsidian 备份配置完整记录

## Git 基础概念

### 仓库（Repository）

本地文件夹执行 `git init` 后就变成一个 git 仓库，git 会在里面创建 `.git` 文件夹来追踪所有变更。

### Remote（远程地址）

git 通过 remote 知道要把代码推到哪里。用 `git remote add origin <url>` 绑定远程仓库地址，之后所有 push 都往这个地址推。

查看当前绑定的远程地址：
```
git remote -v
```

### 分支（Branch）

代码的不同版本线。GitHub 默认分支叫 `main`，本地 git 默认分支叫 `master`，两者不一致会导致推送后页面显示为空。

### 身份认证

GitHub 不允许用账号密码推送，需要用 Personal Access Token（PAT）。Token 存在 Windows 凭据管理器里，推送时自动调用，不需要每次手动输入。

### .gitignore

告诉 git 哪些文件不需要追踪。写在 `.gitignore` 文件里的路径或文件类型会被忽略，不会被提交和推送。

### 常用命令
```
git init                        # 初始化仓库
git add .                       # 把所有变更加入暂存区
git commit -m "备注"            # 提交变更
git push -u origin master       # 推送到远程
git log --oneline               # 查看提交历史
git status                      # 查看当前状态
git remote -v                   # 查看远程地址
git ls-files                    # 查看被追踪的文件
```

---

## 本次配置完整流程

### 1. 创建 GitHub 仓库
在 GitHub 新建私有仓库 `obsidan_backup`。

### 2. 本地初始化
在 Obsidian 库文件夹（`D:\Desktop\数一\我对学习的思考`）执行：
```
git init
git remote add origin https://github.com/orz-sro/obsidan_backup.git
```

### 3. 配置 .gitignore
排除大文件，避免超出 GitHub 限制。在库根目录新建 `.gitignore` 文件，写入：
```
# Obsidian 配置和缓存
.obsidian/workspace.json
.obsidian/workspace-mobile.json
.obsidian/plugins/
.obsidian/themes/
.obsidian/hotkeys.json
.obsidian/app.json
.obsidian/appearance.json

# 大文件
*.mp4
*.exe
image/
政治/徐涛讲义/00.配课书籍/
.git/

# 系统文件
.DS_Store
Thumbs.db
```

### 4. 提交并推送
```
git add .
git commit -m "initial commit"
git push -u origin master
```

### 5. 配置代理（国内必须）
国内直连 GitHub 不稳定，需要开梯子并配置 git 走代理：
```
git config --global http.proxy http://127.0.0.1:10808
```
端口号根据自己的代理软件设置，常见的是 7890 或 10808。

---

## 常见问题

### 推送后 GitHub 显示为空

原因：本地分支是 `master`，GitHub 默认分支是 `main`，不匹配。
解决：推送时指定分支映射：
```
git push -u origin master:main
```

### RPC failed / Connection was reset

原因：文件太大或网络中断。
解决：
1. 检查有没有大文件混入，用 `.gitignore` 排除
2. 开梯子并配置代理

### index.lock 文件存在

原因：上一个 git 进程异常退出留下锁文件。
解决：
```
del .git\index.lock
```
如果提示被占用就重启电脑。

### Everything up-to-date 但远程是空的
原因：之前推送的分支名和 GitHub 默认分支不一致，内容推上去了但不在默认分支上。
解决：到 GitHub Settings → Branches 把默认分支改成实际推上去的分支名。

---

## Git 插件自动备份

### 安装

Obsidian 设置 → 第三方插件 → 关闭安全模式 → 搜索 **Obsidian Git** → 安装并启用

### 关键设置

- **Auto commit interval**：5（每5分钟自动提交）
- **自动推送间隔**：5（每5分钟自动推送到 GitHub）
- **自动拉取间隔**：可按需设置
- **配置账户**: `git config --global credential.https://github.com.username orz-sro`
- **检验结果**：`git config --global --list | findstr credential`

### 工作原理

插件直接读取 Obsidian 库文件夹里已有的 git 配置，不需要额外设置仓库地址，自动提交和推送所有变更。

### 手动推送

侧边栏点击 ↑ 箭头可立即推送，不用等自动间隔。

### 注意

推送时梯子必须开着，否则连接不上 GitHub。

