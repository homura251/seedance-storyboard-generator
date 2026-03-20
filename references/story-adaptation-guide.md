# Story Adaptation Guide

Use this file when the user wants the repo's standard story-to-video workflow rather than a one-off prompt.

## Contents

1. Pipeline
2. Output files
3. Asset numbering
4. Episode package
5. Continuity checks
6. Common pitfalls

## Pipeline

Follow the same high-level flow used in the repository:

`构思主题 -> 写剧本 -> 生成素材描述 -> 生图 -> 写分镜脚本 -> 逐集生成视频`

For Codex, map that flow to:

1. Story analysis and theme confirmation
2. Four-act script structure
3. Asset planning and prompt writing
4. Episode storyboard generation
5. Continuity and reference QA

## Output Files

When the user wants project files, use these names:

- `[标题]_剧本.md`
- `[标题]_素材清单.md`
- `[标题]_E01_分镜.md`
- `[标题]_E02_分镜.md`

For a combined storyboard delivery, note clearly that multiple episodes were merged into one Markdown file.

## Asset Numbering

Use the repo's numbering scheme:

| Prefix | Range | Type | Example |
|---|---|---|---|
| `C` | `C01-C99` | character | `C01 林冲·正面全身` |
| `S` | `S01-S99` | scene | `S01 沧州草料场·雪景` |
| `P` | `P01-P99` | prop | `P01 长枪` |

Keep IDs stable once assigned. Do not renumber assets between episodes unless the user explicitly wants a reset.

## Episode Package

Each episode storyboard should contain three sections.

### 1. 素材清单

List the uploaded references in slot order.

Example:

```markdown
| 素材槽 | 文件 | 说明 |
|---|---|---|
| 图片1 | C01 | 角色一致性参考 |
| 图片2 | S01 | 场景背景参考 |
| 图片3 | P01 | 道具参考 |
```

### 2. Seedance Prompt

Use a time-axis format.

Default pattern:

```markdown
[风格描述]，[画幅比例]，[整体氛围]

0-3秒画面：[镜头运动]，[场景建立]，[主体引入]
3-6秒画面：[镜头运动]，[情节发展]，[动作描述]
6-9秒画面：[镜头运动]，[高潮/冲突]，[情绪爆发]
9-12秒画面：[镜头运动]，[转折/过渡]
12-15秒画面：[镜头运动]，[结尾/落版]

【声音】[配乐风格] + [音效] + [对白/旁白]
【参考】@图片1 [用途]，@图片2 [用途]，@视频1 [用途]
```

For episode 2 and later, use video extension when continuity matters:

```markdown
将@视频1延长15s
```

Then describe only the new time segment and any required transition.

### 3. 尾帧描述

Record the final frame in plain language so the next episode can open from it.

## Continuity Checks

Before finishing, verify:

- every `@图片X` points to a listed asset
- every episode covers the full requested duration
- the ending frame of episode N can plausibly become the opening frame of episode N+1
- character appearance, wardrobe, injuries, and props remain consistent
- a shared style prefix is used across all image-generation prompts
- the reference count stays within Seedance limits

## Common Pitfalls

- Sensitive-word failures are opaque; if the user reports repeated rejection, suggest binary-searching the prompt and swapping risky wording.
- Overly long prompts reduce instruction-following stability; compress non-essential wording before adding more detail.
- Seedance editing is limited; if one short interval is wrong, the user may need to regenerate the whole clip.
- Day-night or weather transitions often need an explicit transition sentence instead of assuming the model will infer it.
