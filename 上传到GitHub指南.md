# 上传到 GitHub 指南（3 分钟搞定）

压缩包解开后，你会得到这个文件夹：

```
dji-action-photo-lab/
├── index.html        ← 整个工作站（双击就能用）
├── README.md         ← 仓库首页说明（GitHub 会自动展示）
├── 上传到GitHub指南.md  ← 本文件
└── assets/           ← README 里用的 3 张配图
```

---

## 方法一：GitHub 网页拖拽上传（最简单，不用装任何东西）

1. 登录 <https://github.com>，右上角点 **+ → New repository**
2. 仓库名填 `dji-action-photo-lab`，勾选 **Add a README file** 可以不勾（我们已有 README）
3. 选 **Private**（先私有更保险；想公开随时在 Settings → General → Change visibility → Public 改）
4. 点 **Create repository**
5. 进入仓库页面，点 **Add file → Upload files**
6. 把解压出来的 `index.html`、`README.md`、`上传到GitHub指南.md` 和 **`assets` 文件夹**（整个文件夹一起拖）拖到浏览器里
7. 下方填一句提交说明，例如 `init: DJI Action 摄影工作站`，点 **Commit changes**

### 顺便开一个网页版（推荐）

1. 仓库顶部 **Settings** → 左侧 **Pages**
2. Source 选 **Deploy from a branch**，Branch 选 `main`、目录选 `/ (root)`，点 **Save**
3. 等 1–2 分钟，页面会出现访问地址：
   `https://你的用户名.github.io/dji-action-photo-lab/`

这就是一个可以直接发给同事的在线版，和本地双击打开的效果完全一样。

---

## 方法二：本地 git 推送（保留提交历史，以后方便更新）

在解压出来的文件夹里打开 PowerShell / Git Bash，依次执行：

```bash
cd dji-action-photo-lab
git init
git add .
git commit -m "init: DJI Action 摄影工作站"
git branch -M main
git remote add origin https://github.com/你的用户名/dji-action-photo-lab.git
git push -u origin main
```

推送时提示要登录：

- **Username**：填你的 GitHub 用户名
- **Password**：填 **Personal Access Token**（不是登录密码）
  - 生成地址：<https://github.com/settings/tokens> → **Generate new token (classic)** → 勾选 `repo` → Generate → 复制那串 `ghp_...`
  - 粘贴时终端不会显示任何字符，属于正常现象，粘贴完直接回车

如果推送时提示 `fatal: could not read Username`，说明凭据没配好，可以改用下面任一方式：

- 用 SSH：先 `ssh-keygen -t ed25519 -C "你的邮箱"`，再把 `C:\Users\你的用户名\.ssh\id_ed25519.pub` 的内容粘贴到 GitHub → Settings → SSH and GPG keys → New SSH key，然后
  `git remote set-url origin git@github.com:你的用户名/dji-action-photo-lab.git` 再 push
- 或者在电脑上安装 [GitHub CLI](https://cli.github.com/) 后执行 `gh auth login`，再 `gh repo create dji-action-photo-lab --private --source . --push`

---

## 常见问题

- **改了代码怎么更新？** 本地改完 `index.html`，在方法二的目录里执行 `git add .`、`git commit -m "描述"`、`git push`，GitHub 和 Pages 会自动更新。
- **图片显示不出来？** 演示素材用的是 Unsplash 在线图，需要联网；断网时会自动显示内置占位图，页面功能不受影响。
- **会不会泄露我的隐私？** 作品、分镜、器材清单都只存在你自己浏览器的 localStorage 里，不会传到 GitHub。
- **想改成公开？** 仓库 Settings → General → Danger Zone → Change visibility → Change to public。

