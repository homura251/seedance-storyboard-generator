---
name: seedance-storyboard-generator
description: Generate Seedance 2.0 scripts, episode outlines, asset prompts, storyboard prompts, and multimodal extend/edit prompts from novels, articles, outlines, existing scripts, images, videos, or audio. Use when Codex needs to adapt story material into short-form video packages, create Nana Banana Pro character or scene prompts, plan multi-episode continuity, or write Seedance prompts that use @图片X, @视频X, @音频X references.
---

# Seedance Storyboard Generator

Turn source material into a production-ready Seedance package.

Read [references/story-adaptation-guide.md](references/story-adaptation-guide.md) when you need the repo-aligned adaptation workflow, file naming, asset numbering, and continuity checklist.

Read [references/seedance-manual.md](references/seedance-manual.md) when you need:
- exact Seedance prompt templates
- platform limits
- camera keyword patterns
- extend, edit, voice, music, or multimodal reference examples

## Work In This Order

1. Classify the request.
   Sort the task into one of these modes:
   - story adaptation into a multi-episode series
   - single storyboard or short prompt
   - asset prompt generation for Nana Banana Pro or another image model
   - Seedance video extension
   - Seedance video edit or rewrite
   - voice, music, product, travel, battle, or other template-driven prompt writing

2. Confirm production parameters.
   Capture source material, language, style, aspect ratio, total runtime or episode count, target platform, tone, and any available references.
   For story adaptation, default to 15 seconds per episode unless the user says otherwise.
   Ask only for missing parameters that materially change the output. Otherwise make a conservative assumption and state it once at the top.

3. Build the narrative scaffold before drafting shots.
   For long-form adaptation, write a compact story bible and then a four-act structure:
   - 起: episodes 1-5
   - 承: episodes 6-10
   - 转: episodes 11-15
   - 合: episodes 16-20
   If the requested series is shorter, preserve the same escalation shape in fewer episodes.
   Extract the core premise, theme, major beats, character roster, relationship map, setting rules, and continuity constraints.
   Assign stable IDs for reusable assets before writing prompts.

4. Plan reusable assets.
   Use the repo's asset numbering scheme:
   - characters: `C01-C99`
   - scenes: `S01-S99`
   - props: `P01-P99`
   For each recurring asset, write a reusable generation prompt that keeps appearance stable across the whole project.
   Apply one shared style prefix to every asset prompt so the visual language stays coherent.

5. Break the material into episodes and scenes.
   Optimize for short-form retention: immediate setup, escalating conflict, clean emotional turn, and a hook or cliffhanger at the end.
   Keep each episode visually actionable. If a scene cannot be shot cleanly, split it.

6. Write Seedance storyboards in the repo's production format.
   For each episode, produce:
   - a material upload list
   - a Seedance prompt in time-axis format
   - an ending frame description
   Use 0-3s, 3-6s, 6-9s, 9-12s, 12-15s blocks unless the user asks for another duration.
   Each time block should specify picture content, camera movement, and audio cues.

7. Handle continuation and edit workflows explicitly.
   For episode chaining or continuation, start with `将@视频1延长Xs` and describe only the newly added segment.
   For edits, state what to preserve, what to modify, and what to overturn or replace.
   When using references, explain the purpose of each `@图片X`, `@视频X`, or `@音频X`.

8. Package the result for direct use.
   Deliver clean Markdown with stable naming and IDs throughout.
   If the user asks for files, use the repo-aligned names:
   - `[标题]_剧本.md`
   - `[标题]_素材清单.md`
   - `[标题]_E[XX]_分镜.md`

## Output Rules

- Prefer Chinese output when the user or source is Chinese; otherwise match the user's language.
- Use explicit names instead of ambiguous pronouns whenever continuity matters.
- Keep each prompt focused on one episode, one shot, or one reusable asset.
- Make cross-shot dependencies explicit. If a shot extends or references an earlier image or video, state exactly what is being reused.
- Surface assumptions in a short block at the top instead of hiding them in the prose.
- Respect platform limits from the manual: images, videos, audio, and duration constraints.

## Default Deliverables

Produce these sections unless the user asks for a narrower output:

1. Project assumptions
2. Story bible
3. Four-act script or sequence outline
4. Asset prompt library
5. Episode storyboard package
6. Continuity checklist
7. Usage notes for Seedance references when helpful

## Adaptation Heuristics

- Compress exposition into visuals, behavior, and conflict.
- Favor high-contrast beats that read within a few seconds.
- End episodes on a reveal, reversal, decision, threat, or emotional break.
- Reuse locations and props strategically so the production plan stays coherent.
- When adapting long text, summarize narrative function first and only then write prompts.
- Track beginning and ending frames so adjacent episodes can connect cleanly.
- If a user already has generated assets, prefer reusing them instead of inventing replacements.

## Quality Bar

- Every episode has a clear dramatic question.
- Every time slice has a visual purpose.
- Every recurring subject keeps stable identity markers.
- Every referenced asset exists in the asset list.
- Every prompt can be copied into a generation workflow with minimal cleanup.
- No section contradicts the story bible or the prior ending frame.

## Avoid

- Writing only a literary synopsis when the user needs production prompts
- Letting wardrobe, age, hairstyle, or setting drift between shots
- Using generic filler like "cinematic", "masterpiece", or "best quality" without actionable detail
- Mixing multiple unrelated shots into one prompt unless the user explicitly wants montage handling
- Exceeding reference limits without warning the user
- Ignoring sensitive-word risk when the prompt contains violence, named IP characters, or ambiguous flagged phrasing
