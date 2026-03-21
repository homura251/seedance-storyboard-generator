# Production Workflow

Use this file for the detailed Seedance production process after production parameters are resolved.

## Workflow

### 1. Script Development

Convert the source into a four-act short-drama structure aligned with the repo workflow:

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

If the source is still loose or literary, read [故事转视频脚本-转换工具.md](故事转视频脚本-转换工具.md) first.

### 2. Asset Planning

Create reusable asset prompts before storyboard writing.

Use the ID system:

- Characters: `C01-C99`
- Scenes: `S01-S99`
- Props: `P01-P99`

Use this prompt structure:

```text
### [编号] — [名称]

[Style prefix], [detailed visual description in English], [technical specs]
```

Requirements:

- use one shared style prefix across the whole project
- make each prompt directly usable in Nana Banana Pro or another image model
- explicitly name each character in character prompts
- include both Chinese and official English names when a reliable English name exists
- preserve recurring identity markers, wardrobe, and color cues
- keep IDs stable for downstream storyboard mapping

### 3. Image Generation Handoff

The skill does not generate images itself.

After producing the asset list, tell the user to:

1. open `[标题]_素材清单.md`
2. generate the listed character, scene, and prop images with Nana Banana Pro or another image model
3. keep filenames or IDs stable for storyboard mapping

### 4. Storyboard Script Generation

Each episode storyboard should contain:

1. 素材上传清单
2. Seedance Prompt
3. 尾帧描述

Use explicit upload slots such as:

```text
图片1: C01 (角色参考)
图片2: S03 (场景参考)
图片3: P01 (道具参考)
```

Then write the Seedance prompt in a time-axis block:

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

Finish with a plain-language ending-frame description for next-episode continuity.

Prefer these camera movement keywords:

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

### 5. Episode Chaining

Explain chaining as a production note:

- `E01` is generated as a new video
- `E02` extends `E01` by uploading `E01` as `@视频1`
- `E03` extends `E02`
- continue the same pattern for later episodes

When continuity matters, start with:

```text
将@视频1延长X秒
```

Then describe only the newly added segment and the transition from the previous ending frame.

If the user wants strict standard behavior, default to `将@视频1延长15s`.

## Narrow Task Modes

If the user requests only one subtask, switch to that mode instead of forcing the full workflow:

- single storyboard or short prompt
- asset prompt generation only
- Seedance video extension
- Seedance video edit or rewrite
- product, travel, battle, voice, or template-driven prompts from the manual

Read [seedance-manual.md](seedance-manual.md) for exact templates in these cases.

## Output Files

For repo-aligned or production-ready delivery, create separate Markdown files by default:

1. `[标题]_剧本.md`
2. `[标题]_素材清单.md`
3. `[标题]_E[XX]_分镜.md`

Use a single combined file only when the user explicitly asks for inline output, a draft preview, or one-file delivery.

## QA Checklist

Before finalizing:

- verify every `@图片X`, `@视频X`, and `@音频X` reference has a corresponding upload slot
- check episode-to-episode continuity from ending frame to next opening frame
- ensure the time axis covers the full requested duration
- validate camera movements are feasible and logically sequenced
- keep recurring characters, scenes, props, wardrobe, and injuries consistent
- keep one shared style prefix across reusable asset prompts
- ensure every Nana Banana character prompt includes the explicit character name and official English name when available
- ensure the asset prompts and Seedance prompt blocks are copy-ready with minimal cleanup

## Common Pitfalls

- do not skip Confirm Production Parameters for the default workflow
- do not force a full multi-episode workflow when the user wants only one prompt
- do not ask unnecessary setup questions when safe defaults are obvious
- do not renumber asset IDs after using them downstream
- do not ignore Seedance continuation mechanics or reference-slot limits
- do not return literary summaries when the user needs executable production prompts
