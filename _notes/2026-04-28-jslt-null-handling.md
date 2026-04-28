---
title: "JSLT-ல Null Values Handle பண்றது எப்படி"
date: 2026-04-28
category: notes
description: "JSLT payload transformation-ல null value issues debug பண்ண கற்றுக்கொண்டது"
---

## Problem

XSLT-லிருந்து JSLT-க்கு migration பண்ணும் போது, null values array-ல வந்தா output corrupt ஆகுது.

## Root Cause

JSLT-ல XSLT மாதிரி automatic null filtering கிடையாது. Explicitly handle பண்ணணும்.

```json
// ❌ This passes nulls through
[for (.items) .]

// ✅ Filter nulls explicitly  
[for (.items) . if (. != null)]
```

## Key Learnings

- JSLT-ல comment syntax கிடையாது — `//` வேலை செய்யாது
- Array output-ல null filter always add பண்ணு
- Test with empty payload — edge cases catch ஆகும்

## References

- [JSLT Documentation](https://github.com/schibsted/jslt)
