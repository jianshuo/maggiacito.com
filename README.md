# Maggiacito

[maggiacito.com](https://maggiacito.com) —— 一个 Hugo 静态博客,托管在 GitHub Pages,
push 到 `main` 自动构建上线(见 `.github/workflows/deploy.yml`)。

写文章不用进任何后台、不用记 Hugo 命令——用 **`wjs-publishing-hugo`** 这个 Claude Code 技能,
跟 Claude 说一句话就能新增/编辑文章、管理类目、传图、发布。

## 一、安装技能(一次性)

**最简单——直接跟 Claude Code(或 Codex)说一句话:**

> 安装 https://github.com/jianshuo/claude-skills/tree/main/wjs-publishing-hugo

它会把这个技能拉到你的技能目录(Claude Code 在 `~/.claude/skills/`,Codex 在
`~/.agents/skills/`)。装好后**新开一个会话**,技能就会出现在列表里。

<details>
<summary>手动安装(可选,不想让 AI 代劳时用)</summary>

```bash
mkdir -p ~/.claude/skills && cd ~/.claude/skills
git clone --depth 1 --filter=blob:none --sparse \
  https://github.com/jianshuo/claude-skills.git _tmp-skills
cd _tmp-skills && git sparse-checkout set wjs-publishing-hugo
mv wjs-publishing-hugo ~/.claude/skills/
cd .. && rm -rf _tmp-skills
chmod +x ~/.claude/skills/wjs-publishing-hugo/scripts/*
```
</details>

## 二、用它改文章

在**本仓库根目录**(`maggiacito.com/`)启动 Claude Code,直接说人话即可:

| 你说 | 它做 |
|---|---|
| 「发一篇博客,讲 XXX,放进『知天命』类目」 | 起草/润色 → 生成 `content/posts/*.md`(front matter 自动按本站格式)→ 让你确认 → 发布上线 |
| 「把《标题》那篇改一下,结尾加一段」 | 改对应 markdown,更新 `lastmod`,发布 |
| 「现在有哪些类目?」 | 列出所有类目和篇数 |
| 「把『旧类目』合并到『新类目』」 | 批量改所有文章的 `categories`,发布 |
| 「给这篇配张题图」 | 生成/放图到 `static/uploads/`,插进正文 |
| 「删掉《标题》那篇」 | 删除并下线 |

也可以触发 `/wjs-publishing-hugo`。发布前它会让你确认,确认后 `git push` 自动部署,
几分钟后上线 `https://maggiacito.com/`。

## 三、本地预览(可选)

```bash
hugo server -D     # 打开 http://localhost:1313 看效果
```

## 仓库结构

```
content/posts/      文章(每篇一个 .md)
static/uploads/     文章配图(新图放这里)
static/wp-content/  从 WordPress 迁移来的历史图片(勿动)
layouts/            Hugo 模板
hugo.toml           站点配置(类目 taxonomy、菜单等)
.github/workflows/  deploy.yml(构建部署)+ feedback.yml(站内反馈闭环)
```

技能本身的完整说明见
[claude-skills/wjs-publishing-hugo](https://github.com/jianshuo/claude-skills/tree/main/wjs-publishing-hugo)。
