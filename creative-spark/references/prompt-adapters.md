# Prompt Adapters

How to adapt Creative Spark §6 prompts to different kinds of generative tools. Tools change quickly: treat everything here as patterns, and verify parameters and syntax against the tool's current documentation. Never state that a syntax works in a specific tool unless its documentation supports it.

Contents: 1. Identify the tool type · 2. Image prompts · 3. Video prompts · 4. Music & audio prompts · 5. 3D & code generation · 6. Consistency techniques · 7. Reference translation · 8. Correction moves · 9. Reference-image & image-to-image workflows · 10. Batch prompting for variant sets

---

## 1. Identify the tool type first

| Tool type | How it tends to read prompts | Write |
|---|---|---|
| Natural-language image models (instruction-following) | Full sentences, relationships, text rendering | Descriptive paragraph: subject → setting → composition → light → mood → format |
| Keyword-oriented diffusion setups | Comma-separated descriptors; some support weights and negative prompts | Ordered keyword chain, most important first; negatives in the separate field if supported |
| Text/image-to-video models | Subject, action, camera, duration; often one shot per generation | One shot per prompt, explicit camera move and start → end state |
| Music/audio generators | Genre, mood, tempo, instrumentation, structure, vocal style; may take lyrics | Descriptor block + structure tags if the tool documents them |
| LLM code generation (for creative coding) | Specifications | Precise spec: library, canvas size, behavior, parameters, constraints |

If the user does not name a tool, give a natural-language version and a compact keyword version.

Language: write prompts in English by default because many generators handle it most reliably; switch when the user asks or the tool clearly supports their language. Keep on-image text in the audience's language.

---

## 2. Image prompts

**Natural-language template**
```
[Creative intent in a clause]. [Subject with 2–3 defining specifics] [doing action] in [environment with time and weather].
Composition: [shot size / framing], [perspective or lens feel], focal point on [x], [negative space location for text if needed].
Lighting: [source, direction, quality, color temperature].
Materials and texture: [...].
Palette: [dominant], [secondary], [accent on focal point].
Mood: [one or two precise words].
Medium/finish: [photograph, gouache illustration, risograph print, clay render…]. Aspect ratio [x:y].
```

**Keyword template**
```
[subject + defining traits], [action], [environment], [composition], [lens/perspective], [lighting], [palette], [materials], [medium/finish], [mood]
Negative (only if supported): [specific unwanted elements]
```

**Rules:** subject first; one lighting setup; no contradictory descriptors (e.g., "minimalist, highly detailed busy scene"); negatives name concrete things (extra fingers, watermark, text artifacts) rather than vague "bad quality".

---

## 3. Video prompts

One prompt = one shot. For sequences, write a shot list (medium-playbooks §1) and one prompt per shot.

```
Shot [ID] · [duration] · [aspect ratio]
[Shot size] of [subject with locked traits] [specific action with start and end state], in [environment].
Camera: [move], [speed], [start framing] → [end framing].
Lighting & mood: [...]. Palette: [...].
Motion notes: [what must stay still, what moves, physical realism needs].
Continuity: [locks copied verbatim from the continuity bible].
```

**Rules:** one primary camera move per shot; describe physical action concretely ("pours slowly until the cup is two-thirds full"); keep the character description identical word-for-word across shots; plan transitions in the edit, not inside a single generation; if the tool accepts a reference image or first frame, generate a hero still first and reuse it.

---

## 4. Music & audio prompts

```
[Genre/subgenre blend], [mood arc], [tempo BPM range], [instrumentation: lead, rhythm, texture], [vocal: none / style and language], [production character: lo-fi, polished, roomy, intimate], [structure: intro–verse–chorus… or 'loopable 30 s bed'], [duration].
```
For sound design: list layers (ambience, foley, designed hits) with timings.

**Rules:** describe sound qualities, not artist names; never request existing lyrics or melodies; original lyrics are fine; state the licensing caveat for commercial use according to the tool's terms (user verifies).

---

## 5. 3D and code generation

- 3D generators: specify object, real-world scale, topology needs (game-ready low-poly vs. hero), material style, and output format the pipeline needs — verify supported formats.
- Creative coding: specify library and version range, canvas or viewport behavior, frame-rate target, interactions, exposed parameters, and accessibility (pause control, reduced motion).

---

## 6. Consistency techniques (multi-asset projects)

1. **Locked descriptor block:** a fixed 1–3 sentence description of each character/product, pasted identically into every prompt.
2. **Hero-first pipeline:** generate and approve one hero image; use it as reference input for later assets where the tool supports reference or image-to-image/video.
3. **Seeds / style settings:** reuse only where the tool documents them; note that seeds rarely guarantee consistency across different prompts.
4. **Palette and light lock:** same hex palette and lighting sentence across a series.
5. **Post-production unification:** consistent color grade, type, and grain applied in editing fixes residual drift.

---

## 7. Translating references safely

When the user cites a living artist, studio, film, or brand style, extract transferable qualities and prompt those instead:

| Dimension | Ask yourself | Example translation |
|---|---|---|
| Era & technique | When and how was it made? | "1970s offset print with slight misregistration" |
| Shape & line | Geometric, organic, thick, delicate? | "chunky rounded shapes, uniform thick outlines" |
| Color | Limited, saturated, muted, complementary? | "three-color palette: tomato red, cream, deep teal" |
| Light | Flat, chiaroscuro, neon, natural? | "soft overcast light, low contrast" |
| Composition | Symmetric, off-center, dense, sparse? | "strict symmetry, subject at center, wide margins" |
| Texture | Grain, paper, brush, plastic, film? | "visible paper grain and dry-brush edges" |

The result should evoke a broad aesthetic family, not replicate one creator's signature.

---

## 8. Correction moves when output drifts

| Symptom | Fix |
|---|---|
| Wrong focal subject | Move subject to the first clause; remove competing nouns |
| Muddy, busy image | Cut descriptors by half; specify negative space |
| Flat lighting | Name source, direction, and hardness explicitly |
| Character changes between shots | Paste the locked descriptor verbatim; use a reference image if supported |
| Garbled text in image | Shorten text, quote it exactly, or add text in post |
| Generic look | Replace mood adjectives with specific materials, era, and lens choices |
| Camera ignores instruction (video) | One move only; state start and end framing; shorten duration |

---

## 9. Reference-image & image-to-image workflows

When the tool supports an input reference image (style transfer, character/product consistency, pose/composition guides, first-frame-to-video), write prompts that *describe what should change*, not the whole scene from scratch:

1. **Style/palette reference:** name what to take (palette, brushwork, grain, lighting quality) and what to leave (do not re-describe the whole composition if the reference already fixes it).
2. **Character/product reference:** state what must stay identical (the locked descriptor block, §6) and only prompt the new action/environment/composition around it.
3. **Pose/composition reference (e.g., a sketch or pose map):** describe subject and style; let the reference carry structure, and say so explicitly if the tool expects that division of labor.
4. **First-frame-to-video:** generate and approve the hero still first, then prompt only the motion, camera, and duration for the clip — the still already answers subject/light/palette.
5. **Strength/influence settings:** if the tool exposes a reference-strength or denoise-strength parameter, note that higher values preserve more of the reference and lower values let the prompt override more — verify the exact scale and direction in the tool's own documentation, since conventions differ by tool.

**Rules:** never assume a reference-image feature exists without checking the session's actual available tools (§8 of SKILL.md); if no such feature is available, fall back to the Locked descriptor block technique (§6.1) in text only, and say that's what you're doing.

---

## 10. Batch prompting for variant sets

Pairs with SKILL.md §16 (Rapid Variant & Batch Generation). When asked for many prompt variants at once:

1. Write the **shared block** once — everything that must not change across the set (subject identity, palette, format, aspect ratio).
2. For each variant, write only the **delta**: the one or two things that differ (hook framing, action, lighting mood, camera angle) per the Variant Matrix axes chosen upstream.
3. Number variants to match their matrix cell (e.g., `V-Hook2xTone1`) so the user can trace which axis combination produced which result.
4. Keep every variant's delta genuinely different along the chosen axes — a batch where every "variant" only swaps an adjective fails the Variant Matrix's purpose (SKILL.md §16.1) and wastes a generation budget.
5. If the tool supports seeds and the goal is to isolate the effect of the prompt change alone, hold the seed constant across the set and say so; if the goal is maximum diversity, vary it and say that instead.
