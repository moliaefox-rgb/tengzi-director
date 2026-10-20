# 十九块：逐块写法

> 骨架来自 Hell Grind 的制作规范（`[FIELD]`），块 3、13、17、19 是后加的。
> 范例是那部片子里的真实镜头，可直接当模板。

---

## 一个铁的事实

**提示词不是文学，是一份施工图。** 每一句都要能被摄影机记录：一个位置、一个动作、一个光源、一个数字。
"气氛压抑"不是施工图，"眼窝落在阴影里、门那边暗两档"是。

**长度**：制作里成品 3,000–4,000 词。别怕长，怕的是**一个 beat 里塞了三个动作**。

---

## B01 · SCENE CONTEXT

**首行必须是人数头。**

```
EXACT 3 CHARACTERS — NO DUPLICATES: ROCO, JAX, REIN. Underground base, training
hall, day. ROCO has been drilling alone for hours; JAX and REIN come in late with
food and find the room wrecked. One continuous 12-second shot, no cuts.
```

要点：
- 数头不是形式。模型**天生要加人、要复制道具**，而且只承认提示词里有参考素材的人。
- 场景、时间、这一镜发生什么，一到两句。
- 时长写在这里也行，写进 FORMAT MODE 也行，但只写一次。
- **不写场号、不写前情、不写"承接上一镜"。** 模型没有"上一镜"。

---

## B02 · ACTIVE REFERENCES

每个素材一行，**角色 + 排除**。

```
@roco for character reference — bare-chested, the crystal sheathing his right arm
from wrist to shoulder, blood dried under his nose.
@jax for character reference — carrying two food trays.
@rein for character reference — tablet in her left hand, screen alive.
@loc_training_room for location reference — take only the space and the texture:
raw concrete, black rock walls, the round mat, the hard light above it. Do not use
as a starting frame, do not inherit the composition, the angle or the grade.
```

三条硬规则：
1. **不写角色，模型就自己定**，而且一定定错：抄构图而不是抄脸，或抄脸而不是抄配色。
2. **场景素材必须禁止继承**：构图、角度、调色都不许带走，只取空间与材质。
3. **一行一个素材**，不要把四个角色写成一句 `@Images 1 through 4 define four characters`——那是经典崩法。

**2.5 增补**：每个素材再加一句保真度——`全保留 / 部分保留 / 属性迁移（迁到谁）/ 松散引导`。
角色三视图还要补一句排除：`Do not take the grey backdrop, the panel borders, or the multi-view layout.`

---

## B02.5 · 绑定纪律：一个素材只干一件事

> 来源：`Seedance 分镜师 3.0`（私域，`[REF-61]`，机制自洽但无第三方验证）
> + `造梦师`（`[CRAFT-45]`，`MODEL SYNTAX MAY CHANGE. SCENE LOGIC MAY NOT.`）
> + `剧本创作工作室`（`[REF-R1]`，编号一致性自检）
>
> 这一节不是新块，是 **B02 的写法纪律**。B02 容易写成"贴一串 @tag"，然后模型自己分配——一定分配错。

### 一、先职责，后 @

句式固定，顺序不能反：

```
{{名字}}，这是该{{角色/场景/道具}}的参考 @图N，作为其唯一的{{长相/空间/材质}}参考；
不得继承{{不该带走的东西}}。
```

**为什么"先职责后 @"**：模型读到的第一件事应该是"这个素材负责什么"，不是"这是个 tag"。顺序反了，它会把 tag 当风格提示。

### 二、反向排除必须写，而且写具体

| 素材类型 | 必写的排除 |
|---|---|
| 角色三视图 | 不继承灰底、分格线、多视图版式、正面无头那张的裁切 |
| 场景板 | 只控几何、材质、光线、氛围；**不控构图、角度、调色** |
| 道具板 | 只控造型与材质；不继承白底、标注文字、多角度拼版 |
| 首帧图 | 只控构图与站位；不继承上一镜的调色（除非要连戏） |

**空泛的排除等于没写。** `不要参考构图` ❌ → `不继承机位高度、镜头度数、画面裁切` ✅

### 三、恒定层 / 可变层：一条提示词是孤岛

模型没有记忆，**每条都要把该说的说全**。所以要分两层装配：

| 层 | 装什么 | 纪律 |
|---|---|---|
| **恒定层** | 风格前缀（逐字）+ 场景 GEO（逐字）+ 时代/世界锚 + 人物短串 + 画质固定项 + 声音基调 | **场内逐条逐字注入，一个同义词都不换** |
| **可变层** | 本镜独有的动作、运镜、光效变化、台词 | 只写增量，不重复恒定层 |

**换措辞 = 扩大采样 = 漂移。** 这是「描述词逐字进每条提示词」（§2 铁律 2）在工程上的说法。

两条具体判据：
1. **场域锚句只取本场那一条。** 外景条里出现一个内景柜台，模型就会在院子里长出一个柜台。
2. **装好回读一遍。** 恒定层里点名的物件，本条正文的画面里要能找到；找不到就是灌错了场域。

### 四、编号一致性自检（落盘前必做）

- [ ] 正文里出现的每个 `@图N`，都在 B02 里有对应行
- [ ] B02 的每一行，在正文里真的被用到了（没用到的删掉，不是留着）
- [ ] 角色 / 场景 / 道具 / 首帧 的编号没有混用
- [ ] 道具单实例：同一件关键道具只用一个编号，不许"桌上那个杯子"和"@图7"指同一物
- [ ] 动作句的主语是**人名或"他/她"**，不是 `@tag`（`@tag` 只做素材声明，不当句子主语）

### 五、不许写进提示词的管理语

这些是给你自己看的，模型读了会当真：

`接下一段` · `承接上一镜` · `同上` · `见分镜2` · `本场共 5 镜` · `参考第 3 条` · `未启用` · `无则删除`

**只用可见画面状态转接。** 接不上就写"上一镜结束在：他右手仍握着门把，身体朝门"，不写"承接上一镜"。

---

## B03 · GEO SPATIAL LAYOUT（场景级常量）

**纯空间地图：没有人物，没有动作。** 一个场景写一次，**每一镜原样粘贴，一个字不改**。

```
GEO SPATIAL LAYOUT (locked across every shot — pure spatial map):
— PLATFORM = raised circular ritual stone disc at the edge of a cliff.
— ALTAR-MONOLITH: at the cliff edge, MID-RIGHT position relative to the platform.
— RITUAL CENTER: CENTER-LEFT, ~3 m from the altar.
— 180° AXIS: camera ALWAYS stays on the corpse-field side — it NEVER crosses the line.
— BACK-LIGHTING: crimson horizon glow comes from BEHIND the platform, rim-lighting
  silhouettes from camera's perspective.
```

读图规则：
- **左右只从摄影机成立**：`frame-left` / `frame-right`。模型不懂"在角色的左边"。
- 位置用地标 + 米数：`at the altar`、`three meters away`。
- **写明摄影机站哪一侧、哪条线永不越过**——这样所有切都在一根轴上。
- 每次切完，**重新点名谁站在哪、看哪里**。
- 静态对话**只给一个角落**，不给整间房。

> GEO 是房间，B05 是"这一镜谁站在房间里"。两层都要。

---

## B04 · LOCATION MAP

本镜的地理，含光的方向。

```
The round training mat sits at the center of the hall under one hard overhead
light. The door is in the far wall at frame-LEFT, about eight metres from the mat.
Five smashed mannequins lie scattered at CENTER-RIGHT, one still rocking on its
base. A bench with two trays stands at frame-RIGHT, two metres off the mat. The
camera lives on the door side of the room and never crosses that line.
```

禁用词：`near`、`around`、`beside`、`somewhere`、`in the area`。
替换为：`within 1 meter`、`touching`、`back against the wall`、`at the south kerb edge`。

---

## B05 · FIRST FRAME AND SPATIAL BLOCKING

**首帧就已经全员到位。** 没有空镜，没有延迟露人，第一帧就能读懂空间关系。

```
First frame is already the full room: ROCO planted at the center of the mat, torso
angled to frame-LEFT, gaze down on the broken mannequins; the open door at
frame-LEFT with JAX and REIN just inside it, trays in hand, two metres apart.
No empty establishing beat, no camera move on frame one.
```

每人给五样：屏幕位置、世界位置、离地标多远、身体朝向、视线方向。

**首秒全景（场景第一镜）**：开头一秒不说话不动作，让模型"拍下"这个摆法。
小技巧：让某人在这一秒里说一个短词（"hm"），模型更容易把全景当成独立一镜。

---

## B06 · FORMAT MODE

```
Single continuous take, 12 seconds, real time, no cuts, no speed ramps.
```

多镜就逐切写死：`SHOT A (~1.0s)` 干什么、切法（HARD CUT / MATCH CUT / INSERT / REVERSE）、
`SHOT B` 的机位与首帧。**用了多镜却不写切点，模型一定自己乱切。**

2.5 的四个模式（写在提示词外，UI 里选）：
`t2v` · `omni_reference` · `video_edit` · `video_extension`。
改一个镜头里的某个东西 → Edit；要接前后 → Extend；**只有彻底重做才是重新生成**。

### 长镜（10–30 秒）：三个数不能混

**`[FIELD — nutllwhy/seedance-tvc-director, 321★, MIT]`** 这份把一个最容易搞混的地方说清了：
一次生成能装下多少个镜头，和你要生成几次，是两件事。

| 数 | 是什么 | 30 秒的典型值 |
|---|---|---|
| **成片时长** | 你要多少秒 | 30 |
| **生成段数** | 调模型几次 | **1**（2.5 原生 30 秒，默认单段） |
| **有效镜头** | 成片里有多少个独立摄影观察 | **8–18**（看节奏档） |

**「16 个镜头 + 1 个 30 秒生成段」是合法组合。** 不要因为"镜头多"就以为要生成很多次。

#### 默认单段，不是默认拆段

`[FIELD — nutllwhy]` 单段优先用于人物关系、跨场景叙事、声音弧线和自然运镜——
因为少一次拼接，就少一次换脸、光色跳变、动作断裂、音乐重启。

只有三种情况才拆：平台不开 30 秒入口 / 用户指定了 15 秒上限的模型 / 精确局部控制的收益大于连续性损失。

> 我上一版写"一集最多一条 30 秒"，是按失败成本推的，没有实测依据。**作废。**

#### 密度档位（成片镜头数，不是生成段数）

`[FIELD — nutllwhy]`

| 档位 | 15 秒 | 30 秒 | 适用 |
|---|---|---|---|
| 快 | 7–10 | **14–18**（默认 16） | 高频新信息、强动作 |
| 标准 | 5–7 | 11–14 | 有呼吸不拖沓，多数剧情 |
| 克制 | 3–5 | **8–10** | 长镜但内部持续变化，情绪戏 |

**克制档的长镜，内部必须至少两个清楚的节拍。** 否则就是"等待、慢慢推、静止凝视"——镜头数够了，节奏还是掉的。

#### 四窗口不是上限

`[OFFICIAL — ByteDance 样例，经 lukasersil/seedance-25 转述]`
官方 30 秒样例本身就跑 8–9 个镜头，每个 2–4 秒。四段结构只是因为好记、能装一个完整的弧，
不是模型的上限。动作密的时候可以上 8 个窗口，每个里减一点。

#### 写法：常数行 + 每窗口的结束状态 + 收尾一致性行

`[FIELD — lukasersil/seedance-25]` 这三样是 30 秒连贯性性价比最高的改动：

```
Constants for the whole clip: {谁/在哪/什么光/什么调色/无文字}.
00-06s: {动作}. End state: {这扇窗结束时画面停在哪}.
06-14s: {动作}. End state: {...}.
14-24s: {动作}. End state: {...}.
24-30s: {动作}. End state: {...}.
Keep {角色/道具/光向} unchanged throughout. No on-screen text, no music.
```

- **常数行**在开头立世界，**收尾行**在 30 秒后再提醒一次模型。两个都要，不是一个。
- **每窗口一个 `End state`**：它给模型一个接缝锚点。没有它，模型会在中段自己编。
- **时间轴必须无缝**：2.5 认整秒，`0-6 / 6-14 / 14-24 / 24-30` 首尾相接，中间不许有空档。
- **最后一拍回扣第一拍**（同一构图或同一物件）：观众自己闭合了叙事，不需要旁白解释。

> **2.0 不认时间戳**，只认 `Shot 1 / Shot 2`。`[OFFICIAL — ByteDance]` 把 2.5 的模板搬到 2.0，必须把 `00-06s` 改写成 `Shot 1`，否则模型自己编时序。

#### 台词预算

15 秒 ≈ 1 句；20 秒 ≈ 1–2 句；30 秒 ≈ 2–4 句短句。台词多了口型会糊，模型还会自己加语气词。

#### 边缘要掐

每条首尾各掐 **0.5 秒**（编辑任务误差可达 0.3 秒）`[OFFICIAL — lukasersil/official-spec]`。
所以 30 秒实际用到 29 秒，预算按 29 算。

---

## B07 · OPTICS

**用视角度数，不用毫米。**

| 度数 | 性格 | 用途 |
|---|---|---|
| 8° | 超长焦观察 | 远处窥视、压缩、前景遮挡 |
| 18° | 长焦 | 紧的情绪特写、压缩背景 |
| 29° | 短焦人像 | 中景人像、背景化开 |
| 47° | 标准 | 自然、人眼、纪实动作 |
| 84° | 广角 | 环境动作、前景身体存在感强 |
| 107° | 超广直线 | 极端环境、宏大地理 |

```
≈40° wide, camera low at chest height, six metres from the mat, deep enough focus
to hold the door and the mannequins in one read; the crystal arm stays sharp.
```

**内容必须和镜头匹配**：广角拍环境，长焦拍人，微距单独做一个 insert beat。
一镜里混"人脸特写 + 大环境 + 微距细节"，镜头必然漂移。

---

## B08 · CAMERA

机位高度、机位侧、手持的物理质感，以及**它永远不做什么**。

```
Calm breathing handheld that holds its framing — a slow reframe of a few degrees
when ROCO turns his head, nothing more. No push, no zoom, no whip.
```

手持要写成人：呼吸、微沉、重量转移、肩扛的质量、迟到的修正。
**一镜一个主运动**，最多加一个极轻的次级运动。

---

## B09 · ACTION TIMING

时间块。**每块 ≤2 个动作**（按**动词数**数，不按句子数）。

> **动作怎么数**：一句话里有几个"改变身体状态"的动词，就是几个动作。
> `她三步冲过去，双手推上他的胸口，两人一起倒向地毯` = **冲 + 推 + 倒 = 3 个**，
> 不是 1 个"扑倒动作"。实测（`postmortem.md 案例 001`）这种写法的成片是：
> 她走过去、他自己蹲下——**三个动作只完成零个**。
>
> **超过 2 个就拆段。** 大动作（扑/摔/倒地/跳）单独占一段。

长镜（20–30 秒）另按"阶段"分，每阶段写**结束状态**。

```
0.0–1.0s — the room holds: positions fixed, one mannequin still rocking.
1.0–4.0s — the door swings; JAX and REIN step in and stop at the edge of the mat,
trays held.
4.0–8.0s — ROCO's eyes find them before his head turns; chest pumping in short
pulls, the blood untouched, the jaw setting once.
8.0–12.0s — he speaks; the smile cracks on all three at once; nobody steps toward
anybody.
```

- **摄影机写在动作里**，不要单独一段"镜头缓缓推进"——它不属于动作的时间。
- **复杂动作放在开头**：`he is ALREADY mid-swing, the door ALREADY cracking`。
  把接近动作的过程另拆一镜。模型拍不好"过程"，拍得好"状态"。
- 动作只能写成正面：`falls on his stomach`，不写 `does not fall on his back`。

### ⚠️ 时间戳格式：必须整数秒（`[OFFICIAL]`）

上面那段 `0.0–1.0s` 的写法来自 Hell Grind 英文原文，**在 Seedance 2.5 上不要照抄格式**。

官方原文：
- 「时间戳……以「1 秒」为单位」
- 「**Seedance 2.0 不响应时间戳只响应镜头序号，而 Seedance 2.5 响应整数秒的时间戳**」
- 「注意时间轴的连续性，避免出现「0-3 秒...5-6 秒...」表达」

| 写法 | 判定 |
|---|---|
| `0—3 秒` `3—7 秒` `7—12 秒` | ✅ 整数、首尾相接 |
| `0.0–2.5s` `2.5–6.0s` `11.0–17.5s` | ❌ 小数，2.5 可能整段不认 |
| `0-3 秒……5-6 秒` | ❌ 有缺口 |
| 「每 2 到 3 秒眨一次眼」「每下 0.15 秒」 | ❌ 用时间戳控频率（官方明确不建议） |

**两条配套纪律：**
1. **频率不写时间戳，写次数**：不写"每 2 秒眨一次"，写"眨两次"；不写"每下 0.15 秒"，写"点两下"。
2. **每个时间段结尾写"结束时……"** —— 官方模板每一段都有结束状态，这是长镜不散架的关键。

详细依据见 `seedance-official.md §2`。

---

## B10 · PHYSICS

```
The crystal arm has real weight — it drags the right shoulder low and swings a
beat behind the body. The rocking mannequin loses momentum and settles. Trays
carry liquid: the cups tilt and steady when JAX stops. Breath is audible work, not
decoration.
```

写这五样：质量、接触、惯性、延迟（布料/头发/尾巴）、液体的黏度与方向。
**不要用形容词代替物理。** "沉重地抬手" 不如 "手抬起来时肩膀被往下拽、手掌在到达前先抖了一下"。

---

## B11 · LIGHTING

**一个光源，一个方向。**

```
One hard overhead source above the mat: ROCO lit from above, eye sockets in
shadow, the crystal catching a cold edge; the door area falls two stops darker;
no fill from the camera side.
```

- 两个太阳 = 每个角度都要重新发明光。
- 摄影机在阴影侧，主体在亮背景前 → 剪影与轮廓光承担画面。
- 允许脸掉进全黑。**不要为了看清脸而补光**——那是电视的做法。

---

## B12 · AUDIO

只写同期声。**台词不在这里展开**（见 B13），这里写"谁说、谁不说、环境是什么"。

```
Diegetic only — the hum of the hall, one mannequin creaking to a stop, footsteps
and trays. ROCO voice (verbatim): "…". His line, and nothing else: "You're late."
Nobody else speaks. No music.
```

硬约束（模型天生爱加）：
`everyone speaks ONLY the line in quotes` · `whoever has no line stays completely silent` ·
`a half-laugh is a facial expression, with no sound`。

---

## B13 · SPOKEN LINE

每个说话角色两样：**voice 描述（逐字，永不改写）+ 引号内台词**。

```
JAX voice (verbatim): "A London street voice in his twenties, loose and hungry,
always half-joking, sentences thrown out mid-stride."
His line, and nothing else: "Man, some cereal and a milkshake would hit the spot
right now."
```

**台词结构**：声音与情绪 → 引号台词 → 身体动作 → 面部反应。
台词**只活在音频段**，动作段里一个字都不能有。

**缝接技巧**（省钱的关键）：
- 全景那一秒里，把上一条的**台词尾巴**喂进来，演员会答对语气，两条接得上。
- 每一次新生成，**用上一条的收尾台词开场**——情绪跟着文字一起过缝。

生僻名字要标发音，否则模型会念错。

---

## B14 · CHARACTER ACTING

**给模型看的只有三样：整体神情 + 一个可见身体反应 + 不做什么。**

```
露娜：露出错愕的神情，身体下意识向后仰了一点，但没有退开。
季秋梧：眉心皱起，下颌绷住，始终没有出声。
```

- **神情** —— 一个整体表情（错愕 / 急切 / 忍着 / 怔住）。**必须有**，没有就是面无表情。
- **身体反应** —— 一个具体部位 + 方向 + 幅度。**紧跟神情**，不能单独存在。
- **不做什么** —— 一句防止过度表演的排除（`但不挣扎、不躲开`）。

### 三条不许写进提示词的

| 不许写 | 为什么 | 改写成 |
|---|---|---|
| 状态 / 想要什么 / 在藏什么 | 这是给演员的，模型读不懂，会自己补一个最省力的表演 | 身体反应 |
| "不许演委屈""只演不想被看见" | 同上，抽象指令会过度执行 | "别过脸，下颌收进去" |
| 纯毫米级（"嘴角压 2 毫米"）**单独出现** | 缺整体方向，表演会僵 | 神情 + 毫米级，两者并写 |

> **这是本系统 2026-10-20 实拍后的修正。**
> 原先写成"状态/想要/在藏什么 + 不许出现情绪词"，结果两个方向都翻过车：
> 写心理 → 模型乱演；只写肌肉 → 模型面无表情。官方模板的做法是三者并写。

### 可选：不自主反应

呼吸、眨眼、重心，写一次放在恒定层，**不要按秒分配**（官方不建议用时间戳控频率）。
「呼吸可见，眨眼每两三次一组」比「每 2.5 秒眨一次」有效。

完整方法见 `acting.md`。

---

## B15 · STYLE

`[Style Prefix, pasted word for word]`

前缀在 `SKILL.md §6`（真人）与 `style-library.md`（3D / 2D / 定格各一份）。
**放在提示词结尾**，不是开头。

---

## B16 · QUALITY

```
8K detail, pore-level skin, no jitter, no flicker; the three faces stay exactly
their references at every distance.
```

注意：`8K` 在多数平台上**不改变输出**（分辨率是 UI 设置）。它在这里的作用是让模型倾向高细节。
真正的质量来自资产和光，不来自这个词。

---

## B17 · GEOMETRY ANCHOR

纯数字，给模型一个可算的锚。

```
@ROCO propped against the sled runner, screen-left, torso at about 40 degrees.
@TYNE kneeling screen-right, her face about 30 cm from his. Lamp on the ice
between them, below the bottom frame edge. Camera at ice level, about 1.2 m away,
15 degrees off their axis.
```

---

## B18 · POSITIVE CONSTRAINTS

**每一个数量和禁令，都写成"画面里有什么"。**

```
Exactly three people in the hall, and no one else. Exactly ONE crystal arm, on
ROCO's right arm, wrist to shoulder — never on the left, never spreading past the
shoulder. FIVE smashed mannequins, never re-rendered as intact, never multiplied.
Two trays, never more. The camera stays on the door side of the room for all
twelve seconds.
```

巨物另加**尺度法则**：画面里放一个人做尺 + 身体地标 + 写出什么叫失败。

```
THE SCALE LAW — VISIBLE PROOF IN THE PICTURE: the stone guardian stands THIRTY
METRES tall — his open palm is as wide as a family car, and ROCO at his foot
reaches just above the ankle. A guardian that reads as a large man, or fits
comfortably in frame next to a standing human = failed shot.
```

---

## B19 · 【排除内容】（原 NEGATIVE）

**官方模板里这是一块独立内容，叫【排除内容】。** 它只处理三件事：
**字幕、音频、已知失败项**（`[OFFICIAL]`）。

三条纪律：

1. **只写真实发生过的失败。** 不抄通用负词表——`no cartoon, not anime, not 3D`
   会把这三个概念喂进去。
2. **按类别列，一条一行，集中在这一块里。** 不许散到 B09、B14 各处。
3. **画面与动作优先正向写。** 这一块只做补充，不做主力。

模板（按需删，别全留）：

```
【排除内容】排除卡通感、游戏渲染感、塑料皮肤、过度磨皮；
排除人物换脸、五官变形、发际线位移、身高突变、角色增减、空间位置跳变；
排除手掌穿模、多余手指、手指粘连、第三只手、手指遮住眼睛和鼻孔；
排除多人同时说话、重复台词、漏词、口型错位、声画不同步；
排除慢动作、跳帧、剧烈抖动、画面闪烁、字幕、文字、标志、水印。
```

**B18 和 B19 的分工**（不冲突）：

| 块 | 写什么 | 例子 |
|---|---|---|
| **B18 正向约束** | 画面里**有什么**、数量是几、机位在哪侧 | `画面里恰好两个人，可以数出来` |
| **B19 排除内容** | 已知会重复出现的**失败** | `排除多余手指、多余的第三只手` |

> 这是本系统 2026-10-20 实拍后的合并。
> 原先把负向拆在 B18/B19 两处，又同时写"只写正面"，**规则自相矛盾**——
> 模型会随机挑一个执行。现在统一：正向在 B18，失败项在 B19，各管一段。

---

## 完整范例（真实镜头，可直接改）

```
SCENE CONTEXT
EXACT 3 CHARACTERS — NO DUPLICATES: ROCO, JAX, REIN. Underground base, training
hall, day. ROCO has been drilling alone for hours; JAX and REIN come in late with
food and find the room wrecked. One continuous 12-second shot, no cuts.

ACTIVE REFERENCES
@roco for character reference — bare-chested, the crystal sheathing his right arm
from wrist to shoulder, blood dried under his nose.
@jax for character reference — carrying two food trays.
@rein for character reference — tablet in her left hand, screen alive.
@loc_training_room for location reference — take only the space and the texture:
raw concrete, black rock walls, the round mat, the hard light above it. Do not use
as a starting frame, do not inherit the composition, the angle or the grade.

LOCATION MAP
The round training mat sits at the center of the hall under one hard overhead
light. The door is in the far wall at frame-LEFT, about eight metres from the mat.
Five smashed mannequins lie scattered at CENTER-RIGHT, one still rocking on its
base. A bench with two trays stands at frame-RIGHT, two metres off the mat. The
camera lives on the door side of the room and never crosses that line.

FIRST FRAME AND SPATIAL BLOCKING
First frame is already the full room: ROCO planted at the center of the mat, torso
angled to frame-LEFT, gaze down on the broken mannequins; the open door at
frame-LEFT with JAX and REIN just inside it, trays in hand, two metres apart. No
empty establishing beat, no camera move on frame one.

FORMAT MODE
Single continuous take, 12 seconds, real time, no cuts, no speed ramps.

OPTICS
≈40° wide, camera low at chest height, six metres from the mat, deep enough focus
to hold the door and the mannequins in one read; the crystal arm stays sharp.

CAMERA
Calm breathing handheld that holds its framing — a slow reframe of a few degrees
when ROCO turns his head, nothing more. No push, no zoom, no whip.

ACTION TIMING
0.0–1.0s — the room holds: positions fixed, one mannequin still rocking.
1.0–4.0s — the door swings; JAX and REIN step in and stop at the edge of the mat,
trays held.
4.0–8.0s — ROCO's eyes find them before his head turns; chest pumping in short
pulls, the blood untouched, the jaw setting once.
8.0–12.0s — he speaks; the smile cracks on all three at once; nobody steps toward
anybody.

PHYSICS
The crystal arm has real weight — it drags the right shoulder low and swings a
beat behind the body. The rocking mannequin loses momentum and settles. Trays
carry liquid: the cups tilt and steady when JAX stops. Breath is audible work, not
decoration.

LIGHTING
One hard overhead source above the mat: ROCO lit from above, eye sockets in
shadow, the crystal catching a cold edge; the door area falls two stops darker; no
fill from the camera side.

AUDIO
Diegetic only — the hum of the hall, one mannequin creaking to a stop, footsteps
and trays. ROCO voice (verbatim): "A worn-out voice in his twenties, dry and low,
humour used as armour." His line, and nothing else: "You're late." Nobody else
speaks. No music.

CHARACTER ACTING
ROCO — burnt out and still going; wants one more clean hit before anyone sees him
fail; hides that the arm is winning; heavy planted rhythm, slow recovery; re-arms
his face when the door opens.
JAX — carries the reaction: the grin holds a half-beat too long, then drops as he
reads the room.
REIN — reads the damage before the person: eyes sweep the broken mannequins, then
the arm, then his face; the tablet lowers without her noticing.

STYLE
[Style Prefix, pasted word for word]

QUALITY
8K detail, pore-level skin, no jitter, no flicker; the three faces stay exactly
their references at every distance.

POSITIVE CONSTRAINTS
Exactly three people in the hall, and no one else. Exactly ONE crystal arm, on
ROCO's right arm, wrist to shoulder — never on the left, never spreading past the
shoulder. FIVE smashed mannequins, never re-rendered as intact, never multiplied.
Two trays, never more. The camera stays on the door side of the room for all
twelve seconds. Photoreal. NON-IP. 16:9. 12s. SFX only. NO CGI. Cinematic.
Write in present tense. Short sentences.
```
