---
name: gzh_markdown
description: >
  Automatically generates Chinese WeChat public account (公众号) markdown articles from code scripts or tutorial content.
  Use when the user wants to convert technical tutorial material into formatted WeChat articles, providing: (1) a previous article to learn writing style, (2) the current content/script to convert, and (3) a next content/script for the preview section.
  Typical trigger phrases: "生成公众号markdown", "写推文", "生成推文", "公众号文章", "gzh_markdown".
---

# WeChat Public Account Markdown Generator (公众号 Markdown 生成器)

Generate WeChat public account markdown articles from code scripts or tutorial content.

## Workflow

### 1. Receive Three Inputs

- **上次推文** (Previous article): A WeChat URL or local text file. Learn the writing framework, tone, and formatting style.
- **本次推文** (Current content): The main script or content file to convert into a markdown article.
- **下次推文** (Next content): The script or content for the next issue. Extract key topics for "下期预告".

### 2. Analyze Writing Style from Previous Article

Extract:

- **Structure**: 简介 → Step 1..N → 下期预告 → 参考文献
- **Tone**: Conversational, tutorial-style Chinese with emoji decorations
- **Formatting patterns**:
  - Steps numbered with Chinese numerals + emoji
  - Code blocks use ` ``` ` — **never `<pre>` tags** (WeChat corrupts them)
  - Key concepts highlighted: `<span style="color:#C0482C;font-weight:bold;">text</span>`
  - Tips/warnings with `⚠️`, concepts with `💡` `🔍` `🎯`
  - Citations: `Author et al. (Year)` inline, numbered list in 参考文献

### 3. Generate Markdown Article

#### Mandatory Formatting Rules

1. **Headers**: ALL section headers use `**<span style="font-size:22px">标题</span>**` — bold, 22pt.
2. **Code Blocks**: ALL code in ` ``` ` blocks. **Never `<pre>`**.
3. **Key Content Highlighting**: `<span style="color:#C0482C;font-weight:bold;">text</span>` for important concepts.

#### Section Structure

**Title**: `**<span style="font-size:22px">系列名N：English subtitle</span>**`

**简介**:
- `📖 上期回顾：` recap previous article
- Describe this issue's content
- Explain key technical concepts with citations
- Call-to-action: `✉️ 关注本公众号，后台发送关键词"...N"`

**Steps**:
- `**<span style="font-size:22px">📦 一、标题</span>**`
- Prose description + ` ``` ` code + technical explanations
- Detailed explanation for complex concepts, skip simple ones
- Separate steps with `---`
- 4-7 steps per article

**下期预告**:
- `**<span style="font-size:22px">🔜 下期预告</span>**`
- Brief `✅` bullet points from next content
- End: `👉 关注更新，不迷路`

**参考文献**:
- `**<span style="font-size:22px">📚 参考文献</span>**`
- Numbered: `Author, I., et al. (Year). Title. Journal, Volume(Issue), Pages.`

### 4. Output

Save as `推文_第N期.md`.

## Style Quick Reference

| Element | Format |
|---------|--------|
| Code | ` ``` ` blocks (never `<pre>`) |
| Header | `**<span style="font-size:22px">text</span>**` |
| Highlight | `<span style="color:#C0482C;font-weight:bold;">text</span>` |
| Citations | `Author et al. (Year)` inline |

### Emojis

📦🗺️🌎🎲⚙️💾📊🔮 steps | 📖 review | 🎯💡🔍 concept | ⚠️ warning | 🔜 next | 📚 refs | ✉️ CTA | ✅ list
