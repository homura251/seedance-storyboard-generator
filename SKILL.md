---
name: seedance-storyboard-generator
description: "Seedance 2.0 剧本与分镜技能。用于把主题、故事、小说、文章、角色设定或短视频创意转成剧本、素材清单、分镜提示词、续拍提示词和视频编辑提示词。用户要求按 Seedance 工作流生产、生成 Nana Banana 素材提示词、拆分分集、做续拍延长，或只有粗略题材需要先确认制作参数时使用。"
---

# Seedance Storyboard Generator

Follow the production order:

`Confirm Production Parameters -> 写剧本 -> 生成素材描述 -> 生图 -> 写分镜脚本 -> 逐集生成视频`

Read [references/production-parameters.md](references/production-parameters.md) first when the user provides only a rough theme, story, article, novel excerpt, or asks for the default end-to-end workflow.

Read [references/production-workflow.md](references/production-workflow.md) when you need the detailed production steps, storyboard structure, narrow-task handling, output-file rules, or QA checklist.

Read [references/故事转视频脚本-转换工具.md](references/故事转视频脚本-转换工具.md) when the source material is literary, loose, or not yet in a filmable dramatic structure.

Read [references/seedance-manual.md](references/seedance-manual.md) when you need exact Seedance 2.0 templates, camera keywords, multimodal reference syntax, duration limits, continuation syntax, or edit patterns.

## Default Behavior

Treat this skill as a step-by-step production assistant.

When the user gives only a theme, concept, rough story, or asks for a short-drama package, default to the full workflow:

1. Confirm Production Parameters
2. write the script
3. generate the reusable asset prompt list
4. hand off image generation
5. write per-episode Seedance storyboard files
6. explain episode chaining or continuation

If the user asks for only one narrow task, do only that task and skip unrelated phases.

## Confirm Production Parameters

Make this the mandatory first step for the default workflow.

Before writing the script, asset prompts, or storyboard files:

1. identify the source type and story scope
2. extract the protagonist, conflict, setting, and desired deliverables
3. confirm or infer the production parameters
4. state the resolved parameters once, then keep them stable across every downstream output

The minimum production parameters are:

1. visual style
2. duration and episode count
3. target platform and aspect ratio
4. tone

If the user does not provide enough information, ask only for parameters that would materially change the production result. If safe defaults are obvious, state them and continue.

Default assumptions for rough prompts:

- language: Chinese
- aspect ratio: `9:16`
- duration: `15s` per episode
- structure: multi-episode short drama
- deliverables: script + asset list + storyboard package + chaining notes

## Core Rules

- Prefer Chinese output when the user or source material is Chinese.
- If any character identity, source, or canonical setting is unclear, browse reliable web sources before continuing and ask the user to confirm the match.
- For character names, run a separate web search for the official English name before using it in Nana Banana prompts.
- If no reliable English name is found, mark it as unknown and ask the user to confirm instead of inventing one.
- In Nana Banana character prompts, always use the explicit character name; never replace it with a vague role label.
- Keep asset IDs stable once assigned.
- Keep every `@图片X`, `@视频X`, and `@音频X` reference explicit and traceable.
- Keep prompts practical and production-ready rather than literary.
