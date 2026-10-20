# 藤子导演系统 · 剧本到提示词

一套把**剧本**变成**可生成视频提示词**的导演工作法。不依赖任何平台，纯 Markdown。

> A director's working method that turns a screenplay into production-ready AI video prompts.
> Plain Markdown — no code, no API, no vendor lock-in.

---

## 这是什么

一个开源库，两部分，**互不合并**：

| 目录 | 内容 | 给谁 |
|---|---|---|
| `director/` | **导演系统**：读剧本 → 划镜头 → 写提示词 → 交前自检 | 装进任意智能体使用 |
| `handoff/` | **交付包**：串联说明、场景交接卡、通用版、网页极简版 | 给人看，用来上手和交接 |

```
剧本 ──[编剧环节]── 剧本 + 交接卡 ──[导演系统]── Unit 表 + 提示词
                          ↑
                    唯一的接口，只有六个字段
```

**两个环节之间靠人递一张卡，不做自动调用。** 这是可维护性的前提，不是省事的妥协。

---

## 三条核心理念

### 1. 镜头按「谁的目标变了」切，不按时间切

一场戏有几次权力或信息的位置变化，就该有几个镜头。

> 真实案例：一场 30 秒的戏按时间切成 6 段、塞进 15 个动作，
> 成片只完成 4 个——**丢掉的恰好是"扑倒、松手、起身、搂住"，全是转折。**

方法来源：Alexander Mackendrick《On Film-making》的 step outline，
与 Judith Weston《Directing Actors》的 Scene Action → Scene Objective → Unit Action。
两位独立、结论一致：*objective 一变，就换一个 unit*。

### 2. 一段最多两个动作

动作按**动词**数，不按句子数。

> `她三步冲过去，双手推上他的胸口，两人一起倒向地毯`
> = 冲 + 推 + 倒 = **3 个动作**，不是"1 个扑倒动作"。
> 模型只会选成本最低的实现：她走过去，他自己蹲下。

### 3. 抽象动词必须拆成三件套

**哪块身体 / 往哪个方向 / 停在哪。**

| 抽象 | 写成 |
|---|---|
| 搂住 | 右手从身后绕过 → 掌压后腰侧面 → 往回带 |
| 捏脸 | 两手掌贴住脸颊 → 拇指在前四指在后 → 往中间挤 |
| 嗅 | 鼻尖凑到颈侧 → 蹭两下 → 鼻翼张两次 → **嘴唇闭着** |

---

## 怎么用

### 只想马上试
打开任意网页版 AI，把 `handoff/03-网页极简版.md` 里分割线内的内容粘成第一条消息，
然后贴剧本。**30 秒出第一条提示词。**

### 装进自己的智能体
把 `handoff/02-导演系统-通用版.md` 整份作为指令 / 知识库 / skills 文件加载即可。
纯文本，不联网，任何能读长文的 agent 都能用。

### 要做一部剧
1. 读 `handoff/00-串联说明.md`
2. 每场戏填一张 `handoff/01-场景交接卡.md`
3. 用 `director/` 出提示词
4. 交前过 `director/references/preflight.md` 的 24 项检查

---

## 目录

```
director/
├── SKILL.md                  主控（§0–§12）
├── CHANGELOG.md              版本日志
├── references/               16 份方法文件
│   ├── scene-study.md        读剧本：Scene Action → Objective → Unit
│   ├── preflight.md          出稿前 24 项检查 + 5 条一票否决
│   ├── postmortem.md         实拍复盘（带秒数、帧号、根因）
│   ├── seedance-official.md  平台官方规则摘录
│   ├── blocks.md             19 块骨架 → 8 块交付
│   ├── acting.md             表演：行为不是情绪
│   ├── blocking.md           走位、轴线、画幅语法
│   ├── composition.md        构图与色彩判断
│   ├── failure-modes.md      失败模式库（14 类）
│   ├── production-notes.md   成本、门禁、节奏档位
│   ├── assets.md             资产：三视图、压力测试
│   ├── style-library.md      摄影师 / 导演 / 光线方案
│   ├── transitions.md        交接帧
│   ├── chinese-prompts.md    中文提示词规范
│   ├── review.md             审稿流程与报告格式
│   └── evidence-log.md       证据台账
├── templates/
│   ├── prompt-8blocks.md     8 块填空模板（交付用这个）
│   └── project-skill.md      项目层常量
└── 剧本/                     归档模板（项目事实表 / 场次表 / 镜头清单 / 镜头日志）

handoff/
├── README.md                 导航：三条路怎么选、各平台怎么装
├── 00-串联说明.md            两个系统怎么交接、出错怎么定位
├── 01-场景交接卡.md          双形态：贴剧本填 3 格 / 没剧本填 6 格
├── 02-导演系统-通用版.md     单文件自包含
└── 03-网页极简版.md          粘贴即用
```

---

## 来源与边界

**本仓库的方法来自三类来源，每一类都能指回具体的片子或文档：**

| 来源 | 用途 |
|---|---|
| Higgsfield Studio《Hell Grind》（95 分钟 AI 长片，制作系统官方开源） | 19 块骨架、资产法、表演法、迭代纪律 |
| `OSideMedia/higgsfield-ai-prompt-skill`（MIT）、`nutllwhy/seedance-tvc-director`、`lukasersil/seedance-25` | 参数面、GEO、失败库、证据标签制度 |
| Alexander Mackendrick《On Film-making》、Judith Weston《Directing Actors》 | scene study / unit action / action verbs |
| 平台官方文档（火山引擎 Seedance 2.5 提示词指南） | 整数秒时间戳、素材上限、台词与字幕规则 |
| 作者自己的实拍复盘（`postmortem.md`） | 动作预算、动词退化、竖屏杀手 |

**本仓库不包含：**
- 任何付费课程的原始文件
- 第三方技能的完整复制（只保留方法与来源标注）
- 作者的私有项目资产、客户资料、模板库

**许可**：本仓库文字部分采用 MIT。文中提及的第三方内容各自遵循原许可，
引用处已标注来源；如需商用，请自行核对其原始条款。

---

## 它不保证什么

- 不保证出片。它是一套纪律，用来减少**已知的**失败。
- 不知道你的平台额度、账号、套餐。花钱前自己算。
- 不替你做审美判断。它只保证：**你写的东西，模型跟得住。**

---

## 相关

- `handoff/README.md` — 30 秒上手
- `director/CHANGELOG.md` — 每条规则是哪次失败逼出来的
- `director/references/postmortem.md` — 真实崩盘记录（含视频参数与逐秒现象）
