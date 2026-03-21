# Production Parameters

Use this file for the mandatory intake step before full Seedance production.

## Confirm Production Parameters

Do not write the script, asset list, or storyboard package until the production parameters are resolved.

### Trigger

Read this file when the user provides:

- only a theme or one-line concept
- a rough story, article, or novel excerpt
- a request for the default end-to-end workflow
- a franchise character or setting that might be ambiguous

### Intake Checklist

Identify and document:

1. source material or one-sentence premise
2. protagonist(s) and key supporting characters
3. central conflict and narrative arc
4. setting or world-building elements
5. key plot points and emotional beats
6. requested deliverables

Then confirm or infer these production parameters:

1. visual style: `写实 / 动画 / 水墨 / 科幻 / 复古 / 电影感 / 其他`
2. duration: total runtime or per-episode duration plus episode count
3. target platform: aspect ratio such as `16:9` / `9:16` / `2.35:1`
4. tone: `史诗 / 温馨 / 悬疑 / 欢快 / 忧伤 / 其他`

### Interaction Rule

Ask only for missing parameters that would materially change the result.

If reasonable defaults are obvious, state them once and continue instead of blocking.

Recommended defaults for rough prompts:

- language: Chinese
- aspect ratio: `9:16`
- duration: `15s` per episode
- structure: multi-episode short drama
- deliverables: script + asset list + storyboard package + chaining notes

### Output Pattern

State the resolved production parameters in a compact block before the script phase. Use this structure:

```text
Production Parameters
- 视觉风格：
- 时长 / 集数：
- 目标平台 / 画幅：
- 情绪基调：
- 交付物：
```

After this block, keep the same values across:

- script outline
- Nana Banana asset prompts
- per-episode Seedance storyboard files
- continuation or extension prompts

### Ambiguity Handling

If a character identity, canon source, or English name is unclear:

1. search reliable web sources first
2. summarize the likely match with sources
3. ask the user to confirm before continuing

Do not guess a franchise identity.
Do not invent an official English name.
