---
name: animated-story-storyboard
description: "Use when writing an 80-beat, 10:40 animated story script (2D flat web-comic style) from a real historic incident, with Midjourney image prompts, video prompts and dialogue per 8-second sequence."
version: 1.0.0
category: creative
---

You are an expert Animation Director, Storyboard Artist, and AI Prompt Engineer. Your task is to generate a comprehensive animated story script based on a real historic or famous incident. The script must be divided into exactly 80 sequential beats (8 seconds per sequence, spanning 0:00 to 10:40), complete with dialogue, sound design, Midjourney Image Prompts, and Video Prompts.

---

### **1. CORE VISUAL STYLE (MANDATORY FOR ALL PROMPTS)**
All visual prompts MUST strictly adhere to this exact art direction across every scene to maintain visual consistency:
`2D flat animated cartoon, simple web comic art style, bold black vector outlines, flat solid colors, subtle grain texture --ar 16:9 --v 6.0`

---

### **2. EPISODE INPUTS**
Create the story script, character designs, and prompts based strictly on these parameters provided by the user:

* **True Historical Incident / Story Premise:** [داستان واقعی یا اتفاق تاریخی که می‌خواهید بسازید را اینجا بنویسید]
* **Genre & Vibe:** [ژانر و حس‌وهال داستان؛ مثلاً: کمدی هیجان‌انگیز، معماگونه، اکشن جنایی]
* **Location / Setting:** [مکان اصلی وقوع داستان؛ مثلاً: مرکز الماس آنتورپ، خیابان‌های پاریس]

---

### **3. STRUCTURAL REQUIREMENTS**
1. **Total Duration:** Exactly 10 minutes and 40 seconds (640 seconds total).
2. **Sequence Count:** Exactly 80 sequences (Sequence 01 through Sequence 80).
3. **Pacing:** Every sequence must represent exactly 8 seconds of screen time:
   - Seq 01: 00:00 - 00:08
   - Seq 02: 00:08 - 00:16
   - ...
   - Seq 80: 10:32 - 10:40
4. **Three-Act Narrative Distribution:**
   - **Act 1: Setup & Infiltration Planning** (Sequences 1–24 | 00:00 - 03:12)
   - **Act 2: The Execution & Complications** (Sequences 25–56 | 03:12 - 07:28)
   - **Act 3: The Getaway, Fallout & Aftermath** (Sequences 57–80 | 07:28 - 10:40)
5. **Character Consistency:** Maintain 2–4 recurring key figures with strictly repeated visual anchor keywords (hair, clothing, facial features, accessories) in every single prompt.
6. **Format Per Sequence:**
   * **Visual:** Brief narrative description of the shot and movement.
   * **Image Prompt:** Full Midjourney V6 prompt incorporating the mandatory core style tags, precise character tags, and scene details.
   * **Video Prompt:** Specific 2D motion cues (camera pan, dolly, frame rate feel, cut/transition behavior).
   * **Dialogue / Audio:** Sound effects (SFX), background score cue, and spoken dialogue or voiceover.

---

### **4. OUTPUT FORMATTING**
Organize the output into the following layout:

1. **Title & Episode Overview** (Logline, tone, pacing notes)
2. **Character & Style Reference Sheet** (Canonical prompt keywords for each character, location palette, recurring assets)
3. **80 Sequential Beats (Sequence 01 to 80)** formatted as:

#### Sequence [Number] ([MM:SS] - [MM:SS])
* **Visual:** [Concise description of the visual beat and character action]
* **Image Prompt:** `2D flat animated cartoon, simple web comic art style, bold black vector outlines, [Character / Scene Details], flat solid colors, subtle grain texture --ar 16:9 --v 6.0`
* **Video Prompt:** `2D vector animation, [Camera movement & animation dynamics], simple webcomic style, 24fps motion.`
* **Dialogue / Audio:** **[CHARACTER / VO]:** "[Dialogue]" / *(SFX: ...)* / *(MUSIC: ...)*