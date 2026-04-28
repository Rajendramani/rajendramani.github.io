# Rajendramani's Notes

Personal blog powered by Jekyll + GitHub Pages.

## 🚀 Quick Setup (One Time)

```bash
# 1. Create repo on GitHub: rajendtamani.github.io
# 2. Clone and copy these files
git clone https://github.com/rajendtamani/rajendtamani.github.io.git
cp -r blog/* rajendtamani.github.io/
cd rajendtamani.github.io
git add .
git commit -m "Initial blog setup"
git push

# 3. Go to GitHub → Settings → Pages → Source: main branch
# 4. Wait 2 minutes → visit https://rajendtamani.github.io
```

## ✍️ How to Post (Just 3 Steps)

### 1. Create a Markdown file

Put it in the right folder:

| Content Type | Folder     | Example Filename                          |
|-------------|------------|-------------------------------------------|
| Tech Notes  | `_notes/`  | `2026-04-28-jslt-null-handling.md`        |
| Thoughts    | `_posts/`  | `2026-04-28-done-is-better-than-perfect.md`|
| DIY         | `_diy/`    | `2026-04-28-obsidian-setup.md`            |

### 2. Add front matter at the top

```yaml
---
title: "Your Post Title"
date: 2026-04-28
description: "One line summary"
---

Your content in Markdown here...
```

### 3. Push to GitHub

```bash
git add .
git commit -m "New post: your title"
git push
```

That's it! Site updates in ~2 minutes.

## 📁 Folder Structure

```
rajendtamani.github.io/
├── _config.yml          # Site settings (edit title, description)
├── _layouts/
│   ├── default.html     # Base layout
│   └── post.html        # Article layout
├── _notes/              # ← Drop technical notes here
├── _posts/              # ← Drop thoughts here
├── _diy/                # ← Drop DIY projects here
├── images/              # ← Drop images here
├── index.md             # Home page (auto-generated list)
├── notes.md             # Notes filter page
├── thoughts.md          # Thoughts filter page
├── diy.md               # DIY filter page
└── about.md             # About page (edit this!)
```

## 🖼️ Adding Images

```markdown
![Description](/images/my-screenshot.png)
```

Put image files in the `images/` folder.

## 💡 Tips

- **Obsidian integration**: Point your Obsidian vault to this repo folder. Use the Obsidian Git plugin for auto-push.
- **Tamil + English**: Write freely in code-mixed style — Markdown handles Unicode perfectly.
- **Code blocks**: Use triple backticks with language name for syntax highlighting.
- **Draft posts**: Add `published: false` in front matter to hide a post.
- **Dark mode**: Site automatically adapts to reader's system preference.

## 🔧 Local Preview (Optional)

```bash
# Install Ruby, then:
bundle install
bundle exec jekyll serve
# Open http://localhost:4000
```
