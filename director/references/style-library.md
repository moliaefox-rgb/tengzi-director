---
title: "导演风格库 — Seedance 2.5 可执行版"
date: 2026-10-20
version: v1
tags: [视频生成, 提示词, 摄影, 风格库]
---

# 导演风格库

> **用法**：这里不是影评，是**参数表**。每条都能直接变成 prompt 里的一个短句。
> **一条铁律**：一条 prompt 只挂**一个主锚点**，最多加 1–2 个辅助词。挂五个风格词，等于没有风格。

---

## 0 · 先把三个空词删掉

这些词在提示词里不产生任何像素：

| 别写 | 因为 | 换成 |
|---|---|---|
| `cinematic` | 每个生成结果默认都"电影感" | `anamorphic 2.39, warm highlights, cool shadows` |
| `dramatic lighting` | 没有方向、没有质地 | `single hard key from frame-left, 6:1 ratio, no fill` |
| `8K / masterpiece / stunning` | 模型的采样器不吃这套 | `pore-level skin, three-day stubble, sweat on the upper lip` |
| `moody` | 情绪形容词 | `crushed blacks, one desk lamp, faces half in shadow` |
| `teal and orange` | 用滥了，模型会直接套 LUT | 写具体光源：`sodium street light against cold blue shade` |

**为什么**：模型对"看得见的东西"采样，对"评价性的词"不采样。这是所有失败提示词的共同病根。

---

## 1 · 三个 register（选风格前先选这个）

真人片、3D 动画、2D 动画**不是同一套语法**，摄影机的行为都不一样。开项目第一件事是定 register，然后整片不许串。

| Register | 摄影机语法 | 质感栈 | 锚点槽写什么 |
|---|---|---|---|
| **真人电影** | 手持呼吸感、允许几条地平线不平、自然运动 | 35mm 颗粒、低对比微乳白、门织晃动、光晕、四角与中心一样亮 | 摄影师的**光与镜** |
| **3D 动画** | 稳定、可编排、可穿墙；镜头是"设计过的"不是"拍到的" | 次表面散射、毛发布料解算、接触阴影真实、无胶片颗粒 | 渲染器的**材质与光比** |
| **2D 动画** | 每镜一个具名机位；物理描述大幅减少 | 赛璐璐平涂、2–3 阶色阶、线条有粗细变化、背景是画的水彩 | 美术**年代/画风**（如"2000 年代初赛璐璐动画"） |
| **定格** | 逐帧运动：`animated on twos`，每个姿势停两帧再跳 | 手作痕迹、布料毛边、微缩景深 | 介质的**物理**（12fps、黏土/毛毡质感） |

> **最容易踩的坑**：把真人片的光影词搬到动画上（"ARRI Alexa" 出现在动画 prompt 里），模型会给你一个"像动画的实拍"。反之亦然。

---

## 2 · 摄影师库（真人片主力）

每条给的是**技术包**——光、镜、色、材质四件事，可以直接拼进 prompt，不依赖模型认不认识这个人名。

| 条目 | 一句话识别 | 技术包（可直接粘） |
|---|---|---|
| **Roger Deakins** | 克制的自然主义，一个光源说清一切 | `single motivated source from a practical window, deep negative fill, faces falling toward silhouette against a bright exterior, cool neutral grade, locked-off camera, no movement` |
| **Emmanuel Lubezki** | 自然光 + 广角 + 不剪 | `natural magic-hour backlight, 24mm wide, handheld breathing, zero fill, warm rim on skin, dust suspended in the air, one unbroken take` |
| **Hoyte van Hoytema** | 大画幅贴近皮肤与机器 | `65mm large-format, cold practical light, extreme close-up on skin texture and worn machinery, muted desaturated palette, fine grain` |
| **Greig Fraser** | 沙与热浪里的剪影 | `sun-bleached desaturated sand palette, hard overhead sun, heavy atmospheric haze, figures read as silhouettes against a bright sky, still large-format framing` |
| **Robert Richardson** | 硬顶光、爆高光、饱和 | `hard hot top light, blown specular highlights, saturated colour, smoke visible in the beam, wide lens, no fill` |
| **Darius Khondji** | 银盐残留的浑浊琥珀 | `bleach-bypass silver retention, murky amber-green, heavy grain, faces half lost in shadow, cramped framing` |
| **Janusz Kamiński** | 逆光、爆窗、手持 | `backlit haze, blown-out windows, handheld, desaturated with hot highlights, long-lens close-ups` |
| **Gordon Willis** | 故意欠曝的脸 | `deliberately underlit faces, top light, eyes lost in shadow, deep crushed blacks, static wide-angle` |
| **Conrad Hall** | 窗光、雨玻璃、剪影 | `window backlight through rain-streaked glass, silhouette, soft bounce only, no fill` |
| **Sven Nykvist** | 北欧窗光贴脸 | `soft north-window light, close faces, plain wall background, no fill, warm skin against a cool wall` |
| **Néstor Almendros** | 魔幻时刻的麦田 | `magic-hour natural light, silhouettes against a low sun, wheat and dust, no fill, warm haze` |
| **Vilmos Zsigmond** | 闪曝底片的朦胧 | `flashed negative, hazy muted pastel, soft contrast, long zoom lens, period grain` |
| **Bradford Young** | 欠曝的深肤色 | `underexposed faces, deep rich shadow on dark skin, available light only, no fill, cool ambient` |
| **Sean Bobbitt** | 不眨眼的自然主义 | `naturalistic available light, 40mm, medium close-up, static unblinking frame` |
| **Rodrigo Prieto** | 冷暖同框 | `mixed colour temperature from practicals, warm interior against cold exterior, naturalistic, subtle handheld` |
| **Łukasz Żal** | 固定机位 + 大留白 | `fixed frame, off-centre composition, natural window light, muted near-monochrome palette, large negative space, no camera movement` |
| **Sayombhu Mukdeeprom** | 树叶间的日光 | `dappled sunlight through leaves, warm skin, tactile texture, intimate close-up, gentle handheld` |
| **Robbie Ryan** | 广角/鱼眼的怪趣 | `wide or fisheye distortion, natural light, painterly saturated period colour, off-kilter framing` |
| **Christopher Doyle** | 饱和红绿 + 拖影 | `saturated red and green gels, step-printed motion blur, cramped framing through doorways, handheld, neon spill` |
| **Mark Lee Ping-bin** | 柔光里的绸缎 | `diffused soft window light, painterly muted colour, fabric texture, slow lateral drift, frame within frame` |
| **Philippe Le Sourd** | 雨里的逆光慢镜 | `rain-soaked backlight, slow motion, reflective wet surfaces, deep blacks, warm highlights` |
| **Linus Sandgren** | 三原色的老好莱坞 | `saturated primary colours, 35mm, smooth crane and dolly, old-Hollywood glow` |
| **Yves Bélanger** | 无补光的太阳 | `available natural light, handheld, no fill, sun flare allowed, unretouched skin` |
| **Benoît Debie** | 频闪霓虹 | `strobing neon, wide-angle, saturated magenta and cyan, aggressive camera energy` |
| **Newton Thomas Sigel** | 变形宽银幕霓虹黑 | `anamorphic neon-noir, magenta and cyan, wet streets, heavy low-key` |
| **Matthew Libatique** | 颗粒与手持的焦虑 | `handheld, coarse grain, high contrast, cold shadows` |

---

## 3 · 导演／视觉作者库

| 条目 | 一句话识别 | 技术包（可直接粘） |
|---|---|---|
| **David Fincher** | 冷、准、空 | `locked symmetrical frames, cold cyan-green grade, deep blacks, negative space in frame, precise slow push-in, no handheld` |
| **Denis Villeneuve** | 人在巨大空间里很小 | `monumental scale, human figure tiny against vast negative space, fog and brutalist mass, silhouette, minimal camera motion` |
| **Christopher Nolan** | 实拍尺度的冷 | `IMAX-scale practical realism, cool neutral grade, wide establishing geometry, cross-cut rhythm, no stylisation` |
| **王家卫** | 拖影、饱和、挡住 | `step-printed motion, saturated reds and greens, foreground obstruction, longing glances across gaps, decayed texture, handheld` |
| **Nicolas Winding Refn** | 对称霓虹与静止 | `perfect symmetry, neon pools in darkness, long static holds, silence, ritualised violence` |
| **Stanley Kubrick** | 单点透视的冷 | `one-point perspective symmetry, wide-angle, cold even light, ceiling in frame, detached observation` |
| **Andrei Tarkovsky** | 长镜、湿土、火 | `long unbroken take, frame within frame through a doorway, wet earth, fire, desaturated sepia` |
| **黑泽明** | 风雨与长焦压缩 | `telephoto compression, driving wind and rain, deep-focus group geometry, weather as drama` |
| **Terrence Malick** | 魔幻时刻的低机位 | `magic-hour wide-angle low camera, handheld, no fill, inserts of the natural world, whispered voice-over` |
| **Wes Anderson** | 平面化对称 | `planimetric centred composition, pastel palette, whip pans, dollhouse cross-section` |
| **Robert Eggers** | 只有烛光 | `candlelight only, natural darkness, grey desaturated palette, 1.66 frame, textured fabric and mud` |
| **Jonathan Glazer** | 极简的恐惧 | `austere static frames, black plus one blood-red accent, clinical framing, dread carried by sound` |
| **Paul Thomas Anderson** | 70mm 的长焦温情 | `70mm large-format, long-lens close-ups, warm amber, restless drifting camera` |
| **奉俊昊** | 垂直的社会 | `vertical social geography, abrupt tonal shifts, rain-soaked set pieces, ensemble staging` |
| **朴赞郁** | 对称的残酷美 | `ornate symmetry, saturated colour, violence staged as beauty, precise camera` |
| **张艺谋** | 红与队列 | `saturated red, symmetrical crowd choreography, flowing cloth, dust caught in backlight` |
| **毕赣** | 长镜与雨夜霓虹 | `long take, neon rain, layered memory, mirrors and clocks` |
| **侯孝贤** | 远处的静观 | `distant static long shot, natural light, action placed off-centre and partly off-screen` |
| **是枝裕和** | 温的自然家庭光 | `warm natural domestic light, static medium shots, seasonal detail, no score` |
| **Michael Mann** | 数字夜城的冷蓝 | `digital night, cold blue city, wide 1.85, available street light` |
| **Steven Soderbergh** | 现有光的黄绿 | `available light, wide lens, naturalistic, cool yellow-green` |
| **Martin Scorsese** | 动能跟拍 | `kinetic tracking, freeze frames, saturated period detail, voice-over` |
| **Steven Spielberg** | 单光的惊奇 | `single warm key, backlit haze, wonder readable in the eyes, oner blocking` |
| **Krzysztof Kieślowski** | 绿色滤镜 | `green filter, soft contrast, intimate close-ups, melancholy` |
| **David Lynch** | 梦的逻辑 | `dream logic, red curtain, industrial haze, low light` |

---

## 4 · 时代与胶片库

| 条目 | 技术包（可直接粘） |
|---|---|
| **70 年代新好莱坞** | `long zoom lens, naturalistic available light, warm faded palette, coarse grain, soft contrast, wide 2.39` |
| **90 年代香港** | `step-printed blur, saturated red and green, neon spill, cramped handheld, heavy grain` |
| **VHS 录像带** | `4:3 frame, chroma bleed, scanlines, tracking noise, timestamp overlay, washed warm low contrast` |
| **Super 8** | `4:3, warm grain, soft vignette, slight gate weave, muted colour, home-movie imperfection` |
| **Hi8 / 2000 年代初电视** | `heavy soft diffusion, blooming highlights, telecine grain, flat neutral daytime, locked-off framing` |
| **Kodachrome** | `saturated reds, deep contrast, warm midtones, fine grain, 1970s colour response` |
| **Kodak Portra** | `soft pastel skin, gentle highlight rolloff, low saturation, fine grain` |
| **Vision3 500T** | `tungsten-balanced, halation around highlights, organic moving grain, magenta shadows` |
| **Tri-X 黑白** | `black and white, coarse grain, high contrast, blown highlights, deep blacks` |
| **Technicolor 三色** | `three-strip saturated colour, dense blacks, painted-backdrop vividness, 1950s` |
| **早期数字（F900）** | `early digital capture, clipped highlights, thin shadows, slightly plastic skin, 2000s` |
| **2000 年代漂白动作片** | `bleach-bypass, silver highlights, desaturated skin, handheld, hard contrast` |
| **冷蓝的未来都市** | `ice blue and silver, stark white practical light, wet reflective surfaces, cold grade` |

---

## 5 · 光线方案库（技术层，最该背下来的部分）

| 方案 | 效果 | 写法 |
|---|---|---|
| **伦勃朗** | 暗侧脸颊一个三角光，一只眼亮 | `Rembrandt key from frame-left at 45 degrees, small triangle of light on the shadow cheek, one eye lit` |
| **分割光** | 半脸亮半脸全黑 | `split lighting, hard line down the nose, half the face in complete shadow` |
| **蝴蝶光** | 鼻下阴影，美人光 | `butterfly light from above the lens, small shadow under the nose, glamour` |
| **环形光** | 自然的小鼻影 | `loop lighting, soft shadow beside the nose, flattering and unobtrusive` |
| **轮廓/边缘光** | 勾边，从背景里剥出来 | `hard rim light along the shoulder and jaw, subject separated from a dark background` |
| **顶光** | 眼窝进阴影，压迫 | `hard top light, eye sockets in shadow, cheekbones lit, ceiling visible` |
| **底光** | 反常识、不安 | `single underlight from a fire below frame, upward shadows on the face` |
| **剪影** | 只给形状 | `pure silhouette against a blown-out background, no detail in the figure` |
| **实用光源唯一** | 画面内可见的光源 | `every light in frame is a practical: one desk lamp, one doorway, no off-screen key` |
| **动机光** | 光有出处 | `motivated by the window at frame-right, falloff visible across the wall` |
| **硬太阳** | 中午的曝露感 | `harsh midday sun from overhead, hard-edged shadows under the brow and nose` |
| **黄金时刻** | 暖、长影 | `low sun from camera-right, long shadows across the ground, warm rim on skin` |
| **蓝调时刻** | 冷、安静 | `blue hour ambient, no direct sun, cool steel-blue fill, practicals just coming on` |
| **阴天柔光** | 无影、可信 | `overcast diffused light, no directional shadow, soft wraparound` |
| **火光** | 唯一暖源 | `firelight only from below frame, flicker rate 8-12 Hz, warm falloff within two metres` |
| **钠灯** | 城市夜的老黄 | `sodium vapour street light, amber pools on wet asphalt, green-black shadows` |
| **霓虹溢光** | 彩色污染 | `neon sign spill, magenta on one cheek and cyan on the other, no fill` |
| **屏幕光** | 现代夜戏 | `screen glow on the face, cold blue, flicker as the image changes` |
| **负补光** | 让暗部真的暗 | `deep negative fill on the shadow side, no bounce, blacks stay black` |
| **单一光源** | 最贵的高级感 | `one source, one direction, everything else falls off` |

---

## 6 · 材质与质感词

| 类别 | 可用词 |
|---|---|
| **皮肤** | `pore-level texture, broken capillaries, sun damage, three-day stubble, sweat sheen, dry cracked lips` |
| **布料** | `coarse weave, pilling, faded dye, dirt in the seams, wet and clinging` |
| **金属** | `brushed finish, oxidation, fingerprints, edges worn bright, rust bloom` |
| **木材** | `split grain, oil-darkened handles, splinters, soot in the joints` |
| **玻璃/水** | `smudged, rain-beaded, condensation on the inside, refraction at the edge` |
| **大气** | `haze in the beam, dust motes, breath vapour, smoke layer between camera and subject` |
| **颗粒** | `organic moving grain, halation on highlights, gate weave, slight chroma fringing` |
| **镜头** | `anamorphic oval bokeh, breathing on focus pull, shallow cinemascope focus, softened corners` |

---

## 7 · 八种类型配方（结构级）

不只是一句风格词，是"这类片子怎么排镜头"。

| 配方 | 结构 | 关键签名 |
|---|---|---|
| **真人史诗** | 一镜到底或多镜；一个钩子事件触发一次定住的慢镜，然后弹回 | 尺度对比：极小的人 vs 极大的物 |
| **3D 动画长片** | 15 秒 6 个镜头，明确写"不要一个机位拍到底" | 每镜一句台词并描述表演方式；必须落一个视觉笑点 |
| **2D 赛璐璐** | 每镜一个具名机位，物理块大幅删减 | 平涂、2–3 阶色阶、线条粗细变化、背景手绘水彩 |
| **定格** | 逐帧：`on twos`，姿势停两帧再跳 | 大气（雪、烟、呼气）**平滑**流动，人物**逐帧**跳——这个"分裂运动"是和模型默认平滑对抗的关键 |
| **游戏过场** | 15 秒 3 个硬切 | 钉在屏幕上的 HUD，每个元素写清文案，绝不随镜头视差移动 |
| **产品广告** | 8–10 个小段，动作匹配切 | 收在一个英雄产品镜：产品占三分之一，暗部留白，慢推，粒子飘移 |
| **VFX 合成** | 原片是主，只加一层 | 输入锁：构图、机位、调色全部继承；新增元素只带自己的光和接触阴影 |
| **怪兽/巨物** | 6 个切，每切单独定光学 | 用"容器法则"固定物理（"只在海面，始终不腾空"）+ 画面里放人做尺度尺 |

---

## 8 · 用法示例

**同一个场景，三种 register 的写法差异**

同一句"她推开门，屋里的灯亮着"：

```
真人：She pushes the door open. Warm practical light from a single bare bulb
spills across her face from frame-right; the corridor behind her stays cold blue.
Handheld, the frame settling a beat late. Half her face falls into shadow.

3D 动画：She pushes the door open. Warm key light from the bare bulb inside
wraps her face with soft subsurface scattering on the skin; fur-lined hood
catches a rim. Camera glides through the doorway at chest height, smooth and
designed, no handheld.

2D 动画：She pushes the door open. Flat warm yellow fill from the doorway;
two-value cel shading, clean line weight on the shoulder; hand-painted
watercolour interior. Camera held in a fixed medium shot, no movement.
```

差异不在形容词，在**摄影机怎么动、光怎么落、材质怎么读**。

---

## 9 · 来源与授权

- 光线/色彩/镜头词表与"register 极点"部分改写自 **smixs/visual-skills**（CC BY 4.0，作者 Serge Shima），已按许可证要求署名。
- 类型配方与"一个风格锚点"原则改写自 **OSideMedia/higgsfield-ai-prompt-skill**（MIT）。
- 摄影师与导演条目为本库自行整理，技术参数以"可被摄影机记录的事实"为准，不含任何真人姓名进入 prompt 的用法建议——**prompt 里写参数，不写人名**。

---

## 10 · Register 前缀模板（整片逐字粘贴，只改这一个）

### 真人电影（Hell Grind 正式版）

见 `../SKILL.md §6`。放置在提示词结尾。

### 3D 动画

```
Style: 3D animated feature, theatrical quality — NOT photoreal, NOT live action,
NOT a game cutscene.
Render: path-traced with real subsurface scattering on skin, strand-based fur and
hair, cloth solved with visible weight; contact shadows correct on every surface.
Lighting: motivated, single dominant source; soft bounce from environment; rim
separation on characters.
Color: 60:30:10 — dominant / secondary / accent, saturated but controlled.
Camera: virtual cine lens, designed moves, no handheld shake, no film grain.
Acting: readable squash-and-stretch on beats, held poses, eyes with live catch-lights.
Composition: rule of thirds; every character moving from frame one.
Technical: 24fps, crisp edges, no jitter, no flicker, no texture boiling.
Audio: environmental SFX only. No music. No subtitles.
```

### 2D 动画（赛璐璐）

```
Style: 2D cel animation, hand-drawn look — NOT 3D, NOT CG, NOT painterly.
Render: clean flat fills, two-to-three value cel shading, line weight that varies
with pressure, hand-painted watercolor backgrounds.
Lighting: flat key with one hard shadow shape; no volumetric gradients on characters.
Color: limited palette, 60:30:10; one saturated accent reserved for the story prop.
Camera: one named camera move per shot, held flat; no lens distortion, no grain.
Acting: pose-to-pose with held extremes, smear frames on fast actions.
Technical: 24fps on ones for action, on twos for dialogue; no motion blur.
Audio: environmental SFX only. No music. No subtitles.
```

### 定格

```
Style: stop-motion, hand-animated on twos — true 12fps stepped motion, each pose
held two frames then snapping, never gliding.
Render: physical miniature set, visible craft — fingerprints, fabric fuzz, dust,
scratches on the paint; shallow miniature depth of field.
Lighting: practical table-top sources, one direction, hard shadows from the set.
Split-motion rule: atmosphere (snow, smoke, breath) moves SMOOTHLY while figures
step on twos.
Technical: no digital smoothing, no motion blur, no interpolation.
Audio: environmental SFX only. No music. No subtitles.
```

> **最容易踩的坑**：把真人片的光影词搬到动画上（提示词里出现 `ARRI Alexa`、`35mm grain`），
> 模型会给你一个"像动画的实拍"。反之亦然。**风格前缀只能整块替换，不能混搭。**
