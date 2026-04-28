---
title: "Obsidian → GitHub Pages Auto-Publish Setup"
date: 2026-04-20
category: diy
description: "Obsidian-ல எழுதுனா automatic-ஆ blog-ல publish ஆகுற workflow"
---

## Goal

Obsidian-ல note எழுது → save பண்ணு → automatic-ஆ GitHub Pages-ல publish ஆகணும்.

## Setup

1. Obsidian vault-ஐ blog repo folder-ல point பண்ணு
2. Obsidian Git plugin install பண்ணு
3. Auto-commit interval set பண்ணு (every 30 min)

## Folder Mapping

```
Obsidian Vault/
├── _notes/          ← Technical notes
├── _posts/          ← Thoughts  
├── _diy/            ← DIY projects
└── images/          ← Screenshots, photos
```

## Result

Note எழுதி save பண்ணா, 30 நிமிடத்துல site-ல live ஆகிடும்!
