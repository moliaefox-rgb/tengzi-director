# 中文提示词规范

> 用户指定：**提示词用中文输出**。这份文件定义怎么译、哪些不译、以及三个必须防的坑。

---

## 1 · 为什么不能"随手翻译"

同一个概念换一种说法，模型就当成两条不同指令。
比如 `frame-left` 这次译"画面左侧"、下次译"镜头左边"、再下次译"屏幕左方"——三次就是三个空间关系。

**所以：块名固定、术语固定、一个词只有一个译法，永不换说法。**

---

## 2 · 十九块的固定中文块名

| # | 中文块名 | 英文原块 |
|---|---|---|
| 1 | 场景上下文 | SCENE CONTEXT |
| 2 | 参考素材 | ACTIVE REFERENCES |
| 3 | 空间平面图 | GEO SPATIAL LAYOUT |
| 4 | 场景地理 | LOCATION MAP |
| 5 | 首帧与空间锁 | FIRST FRAME AND SPATIAL BLOCKING |
| 6 | 镜头模式 | FORMAT MODE |
| 7 | 光学 | OPTICS |
| 8 | 摄影机 | CAMERA |
| 9 | 动作时间轴 | ACTION TIMING |
| 10 | 物理 | PHYSICS |
| 11 | 光照 | LIGHTING |
| 12 | 声音 | AUDIO |
| 13 | 台词 | SPOKEN LINE |
| 14 | 角色表演 | CHARACTER ACTING |
| 15 | 风格 | STYLE |
| 16 | 画质 | QUALITY |
| 17 | 几何锚点 | GEOMETRY ANCHOR |
| 18 | 正向约束 | POSITIVE CONSTRAINTS |
| 19 | 负向约束 | NEGATIVE |

---

## 3 · 译名表（固定，不许同义替换）

### 空间与走位
| 英文 | 中文 | 禁止译法 |
|---|---|---|
| frame-left / frame-right | 画左 / 画右 | 画面左侧、镜头左边、屏幕左方 |
| screen position | 屏幕位置 | 画面里的位置 |
| world position | 场景位置 | 实际位置 |
| within 1 meter | 一米以内 | 靠近、附近、旁边 |
| touching | 贴着 | 挨着 |
| body facing | 身体朝向 | 身体方向 |
| gaze line | 视线 | 眼神方向 |
| 180° axis | 180 度轴线 | 轴线、中轴线 |
| foreground / midground / background | 前景 / 中景 / 背景 | 前中后层 |
| off frame | 画面外 | 出画 |
| crosses the line | 越过轴线 | 越轴 |

### 镜头与光学
| 英文 | 中文 |
|---|---|
| diagonal field of view | 对角线视角 |
| lens character | 镜头性格 |
| camera height | 机位高度 |
| handheld | 手持 |
| locked-off | 固定机位 |
| push-in / pull-back | 推近 / 拉远 |
| tilt up / tilt down | 上摇 / 下摇 |
| lateral tracking | 横向跟移 |
| depth of field | 景深 |
| falloff | 衰减 |
| single continuous take | 单镜连续，不切 |
| hard cut | 硬切 |
| real time, no speed ramps | 实时，无变速 |
| rule of thirds | 三分法 |
| golden ratio | 黄金比例 |

### 光
| 英文 | 中文 |
|---|---|
| key light | 主光 |
| fill / negative fill | 补光 / 负补光 |
| rim light | 轮廓光 |
| backlight / contre-jour | 逆光 |
| camera on shadow side | 摄影机在阴影侧 |
| practical | 实用光源（画面内可见的光源） |
| motivated light | 有动机的光 |
| hard light / soft light | 硬光 / 柔光 |
| one stop darker | 暗一档 |
| crushed blacks | 死黑 |
| halation | 光晕 |
| catch-light | 眼神光 |
| falloff within a metre | 一米内衰减完 |

### 质感与物理
| 英文 | 中文 |
|---|---|
| pore-level skin | 毛孔级皮肤 |
| vellus hair | 绒毛 |
| capillary flush | 毛细血管泛红 |
| contact shadow | 接触阴影 |
| identity drift | 身份漂移 |
| follow-through | 随动 |
| cloth delay | 布料延迟 |
| real weight | 真实重量 |
| texture boiling | 纹理沸腾（贴图抖动） |

### 表演
| 英文 | 中文 |
|---|---|
| goal / obstacle / tactic | 目标 / 障碍 / 战术 |
| beat | 节拍 |
| subtext | 潜台词 |
| micro-pause | 微停顿 |
| micro-saccade | 微扫视 |
| double-blink | 连眨两下 |
| reset-blink | 重置眨眼 |
| held tension | 绷住的静止 |
| eye-line | 视线落点 |
| plays the result | 演结果 |
| inner monologue (INNER) | 内心独白（标注"内心"，不出声） |

### 约束与数量
| 英文 | 中文 |
|---|---|
| EXACT 3 CHARACTERS — NO DUPLICATES | 严格三人——不得重复 |
| exactly ONE | 只有一件 |
| never multiplied | 不得复制增多 |
| positive constraints | 正向约束 |
| subtitle safe zone | 字幕安全区 |

### 不译的
- **人名、@tag、品牌**：原样保留（`@luna`、`@loc_luna_living`）
- **镜头度数**：`47°` 保留阿拉伯数字加度数符号
- **文件名、模型名**：`Seedance 2.5`、`Nano Banana Pro`
- **摄影师/导演名**：保留原名（技术血缘，不是长相）

---

## 4 · 三个必须防的坑

**① 中文容易写成文学腔。**
中文的诱惑是"暧昧的光线缓缓流淌"。这句话什么也不采样。
**规矩：短句、动词开头、每句至少含一个数字或一个物理事实。**

| 别写 | 写成 |
|---|---|
| 暧昧的光线洒在两人身上 | 光从画左的一扇窗进来，她逆光，他右脸暗一档 |
| 她被吓了一跳 | 瞳孔放大，眼睛睁到能看见上眼白，肩膀抬了一下 |
| 两人深情对视 | 他的视线从她眼睛落到她肩膀上，头晚了半拍才转过去 |

**② 台词与描述必须物理隔离。**
中文写作习惯把对白混进叙述。**台词只出现在「台词」块，加引号，一个字不多。**
动作块里出现引号，模型就会在该说话的时候说话、不该说的时候也说。

**③ 中文的"不"和"没有"更危险。**
`不要摔倒` 在中文里比英文 `do not fall` 更像一个动作短语——模型更容易直接执行"摔倒"。
**一切否定改成正面动作**：`他趴在地上`，不写 `他没有仰面倒下`。

---

## 5 · 一个最小的对照样例

```
英文：First frame already has both of them, stacked: LUNA in the upper third,
leaning in from frame-LEFT...

中文：首帧两人已经在画面里，上下叠放：露娜在上三分之一，从画左探身压下去，
两只手已经捧住季秋梧的下巴，头发向前甩过他的额头；季秋梧在画面中间偏下，
陷在沙发右角的靠垫里，下巴抬起，嘴里还含着半口蛋糕，一只手举着叉子停在
半空，位置在画右。两人的手落在下三分之一，桌沿之上。
```

注意中文版做了什么：
- `stacked` → **上下叠放**（不是"叠在一起"）
- `upper third` → **上三分之一**
- 保留 `画左 / 画右 / 下三分之一` 三个固定词
- 数字（三分之一定位、桌沿）都在
- **没有形容词**，全是位置和动作

---

## 6 · 如果某条中文不灵

**允许但不是规则**：在中文术语后加括号补英文，例如
`47° 对角线视角（47° diagonal FOV）`。

只在**某一条反复失败**时这么做，并且记进项目日志——下次直接用带括号的版本。
不要全篇中英混写，那是两头不靠。
