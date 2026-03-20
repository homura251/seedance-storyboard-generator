---
name: seedance-storyboard-generator
description: "Seedance 2.0 剧本与分镜技能。用于把主题、小说、故事、文章改成多集视频方案，覆盖帖子里的工作流：构思主题、写剧本、生成素材描述、生图衔接、写分镜脚本、逐集生成视频；也支持单独生成 Seedance 2.0 分镜提示词、续拍提示词、视频编辑提示词、角色场景道具素材提示词。"
---

# Seedance Storyboard Generator

Follow the workflow demonstrated in the Linux.do post and the upstream repository:

`构思主题 -> 写剧本 -> 生成素材描述 -> 生图 -> 写分镜脚本 -> 逐集生成视频`

Read [references/故事转视频脚本-转换工具.md](references/故事转视频脚本-转换工具.md) when the source material is still rough and must be converted into a filmable story structure first.

Read [references/seedance-manual.md](references/seedance-manual.md) when you need exact Seedance 2.0 prompt templates, platform limits, camera keywords, multimodal reference syntax, video extension, or edit patterns.

## Default Behavior

When the user gives a theme, story, article, novel excerpt, or asks for a short-drama workflow, default to the full guided flow below.

The skill should behave like a step-by-step production assistant:

1. help the user confirm the project setup
2. write the script
3. generate the asset prompt list
4. tell the user to generate images with Nana Banana Pro or another image model
5. write per-episode Seedance storyboard scripts
6. explain how to chain episodes with video extension

If the user asks for only one narrow task, such as a single storyboard prompt, a continuation prompt, a video edit prompt, or only an asset list, skip unrelated steps and do only that part.

## Guided Workflow

### 1. Intake And Configuration

Treat this as the default first step when the user says something like `seedance 风云中聂风小时候的故事` or provides only a rough topic.

Collect or infer:

- source material or one-sentence story premise
- visual style
- aspect ratio
- target duration or episode count
- tone
- whether the user already has images, videos, or audio references

Ask only for missing parameters that materially change the result. If reasonable defaults are obvious, state them once and continue instead of blocking.

Recommended defaults when the user gives only a theme:

- language: Chinese
- aspect ratio: `9:16`
- duration: `15s` per episode
- structure: multi-episode short drama
- deliverables: script + asset list + storyboard package + chaining notes

### 2. Script Development

Convert the source material into a four-act script structure aligned with the repo workflow:

- 起: episodes 1-5
- 承: episodes 6-10
- 转: episodes 11-15
- 合: episodes 16-20

For shorter series, preserve the same escalation pattern in fewer episodes.

For each episode include:

- episode number and title
- duration
- emotional tone
- key plot points
- beginning frame
- ending frame

If the source is still loose or literary, use [references/故事转视频脚本-转换工具.md](references/故事转视频脚本-转换工具.md) to first extract theme, conflict, character arc, scenes, and dramatic beats.

### 3. Asset Planning

Create reusable asset prompts before storyboard writing. This is the Nana Banana Pro prompt stage in the upstream workflow.

Use the numbering scheme:

| Category | Prefix | Example | Description |
|----------|--------|---------|-------------|
| Characters | `C01-C99` | `C01 林冲·正面全身` | Character references and angles |
| Scenes | `S01-S99` | `S01 沧州草料场·雪景` | Key locations and environments |
| Props | `P01-P99` | `P01 长枪` | Important objects and wardrobe items |

Use the upstream prompt format for every reusable asset:

```text
### [编号] — [名称]

[Style prefix], [detailed visual description in English], [technical specs]
```

Style prefix examples:

- `Chinese ink wash painting style mixed with anime cel-shading`
- `Cinematic photorealistic style with dramatic lighting`
- `3D Pixar-style animation rendering`
- `Sci-fi cyberpunk aesthetic with neon lighting`

Requirements:

- use one shared style prefix across the whole project
- make each prompt directly usable in Nana Banana Pro or another image model
- preserve recurring identity markers for characters
- use distinct color schemes and visual markers for each character to ensure recognition
- keep the list organized with unique IDs suitable for copy-pasting into image generators

### 4. Image Generation Handoff

The skill does not generate images itself. After producing the asset list, explicitly instruct the user to generate the referenced images with Nana Banana Pro or another image model before video production.

Mention the practical handoff:

- open `[标题]_素材清单.md`
- generate the listed character, scene, and prop images
- keep filenames or IDs stable so they can be mapped back into storyboard slots

### 5. Storyboard Script Generation

After the script and asset plan are ready, generate Seedance 2.0 storyboard files in the repo's production format.

Each episode storyboard should contain:

1. 素材上传清单
2. Seedance Prompt
3. 尾帧描述

Use the upstream structure:

```text
图片1: C01 (角色参考)
图片2: S03 (场景参考)
图片3: P01 (道具参考)
```

Then write the Seedance prompt in time-axis format:

```text
[风格描述]，[画幅比例]，[整体氛围]

0-3s画面：[镜头运动]，[场景建立]，[主体引入]
3-6s画面：[镜头运动]，[情节发展]，[动作描述]
6-9s画面：[镜头运动]，[高潮/冲突]，[情绪爆发]
9-12s画面：[镜头运动]，[转折/过渡]
12-15s画面：[镜头运动]，[结尾/落版]

【声音】[配乐风格] + [音效] + [对白/旁白]
【参考】@图片1 [用途]，@图片2 [用途]，@视频1 [用途]，@音频1 [用途]
```

And finish with a plain-language ending frame description for next-episode continuity.

Use camera movement keywords consistent with the upstream skill:

- 推镜头
- 拉镜头
- 摇镜头
- 移镜头
- 跟镜头
- 环绕镜头
- 升降镜头
- 希区柯克变焦
- 一镜到底
- 手持晃动

### 6. Episode Chaining

Explain the chain-generation workflow exactly as a production note:

- `E01` is generated as a new video
- `E02` extends `E01` by uploading `E01` as `@视频1`
- `E03` extends `E02`
- continue the same pattern for later episodes

When continuity matters, start the prompt with:

```text
将@视频1延长X秒
```

Then describe only the newly added segment and any transition needed from the previous ending frame.

If the user specifically wants strict upstream behavior for chaining, default to `将@视频1延长15s` for standard 15-second episodes.

## Narrow Task Modes

If the user requests a specific subtask, switch to the corresponding mode instead of forcing the full drama workflow:

- single storyboard or short prompt
- asset prompt generation only
- Seedance video extension
- Seedance video edit or rewrite
- product, travel, battle, voice, or template-driven prompts from the manual

Use [references/seedance-manual.md](references/seedance-manual.md) for the correct template in these narrow modes.

## Output Files

When the user wants the default post workflow, a repo-aligned project, or production-ready files, create separate Markdown files in the workspace by default. Do not collapse a multi-episode project into one combined storyboard file unless the user explicitly asks for a single-file delivery.

Use these names:

1. `[标题]_剧本.md`
2. `[标题]_素材清单.md`
3. `[标题]_E[XX]_分镜.md`

For a 5-episode project, that means:

- one `[标题]_剧本.md`
- one `[标题]_素材清单.md`
- five storyboard files: `[标题]_E01_分镜.md` through `[标题]_E05_分镜.md`

Only use a single combined Markdown file when the user explicitly asks for inline output, a draft preview, or one-file delivery.

## Interaction Rules

- Prefer Chinese output when the user or source material is Chinese.
- If the user provides only a theme, guide them through setup briefly and continue with reasonable defaults.
- If any character identity, source, or canonical setting is unclear, search the web first, summarize the likely matches with sources, and ask the user to confirm before continuing script, asset, or storyboard generation.
- Keep IDs stable once assigned.
- Make references explicit whenever using `@图片X`, `@视频X`, or `@音频X`.
- Use explicit names instead of ambiguous pronouns when continuity matters.
- Keep prompts practical and production-ready rather than literary.

## Quality Assurance

Before finalizing:

- verify every `@图片X`, `@视频X`, and `@音频X` reference has a corresponding upload slot
- check episode-to-episode continuity from ending frame to next opening frame
- ensure the time axis covers the full requested duration
- validate camera movements are feasible and logically sequenced
- ensure all recurring characters, scenes, props, wardrobe, and injuries remain consistent
- ensure one shared style prefix is used across reusable asset prompts
- ensure the Nana Banana asset prompts and Seedance prompt blocks can be copied into the production workflow with minimal cleanup

## Common Pitfalls To Avoid

1. Do not force a full multi-episode workflow when the user only wants one prompt.
2. Do not ask unnecessary setup questions when safe defaults are obvious.
3. Do not generate asset IDs that are later changed or renumbered.
4. Do not ignore Seedance reference limits or continuation mechanics.
5. Do not output only literary summaries when the user needs executable production prompts.
