# 9Corner 博客写作规范

一套给中文技术博客用的写作规范，打包成 agent skill。解决的不是「排版好看」，是**文章越写越水**这个问题。

## 它治什么病

写博客最难的不是格式，是两件事：

**一是每篇风格都在漂。** 同一个题目隔两个月自己写两遍，标题长度、摘要写法、开篇方式都不一样。换成 AI 写，一次比一次漂得更远。

**二是分类和标签会随文章数量膨胀。** 写作时顺手造一个新标签最省事，一年后标签页变成几十个各有一篇文章的孤岛，点进去和不点没区别。

这份规范的答案是：**分类锁死 5 个永不新增，标签改成有预算的封闭词表**——词表就那么多个坑，想加新词必须先合并或下线一个。加法变成零和，写作时的那点顺手就没了。这条规则不需要谁自觉，它自己会挡住膨胀。

## 装

四个文件，放对位置就能用。

### Claude Code / 兼容 skills 的 agent

```bash
git clone https://github.com/9corner/9corner-blog-skill.git ~/.claude/skills/9corner-blog
```

或者直接放到 `~/.workbuddy/skills/9corner-blog/`。

没有 git 就直接复制整个目录过去，效果一样。

### 不支持 skill 的工具

Cursor、GitHub Copilot、网页版 AI 这些没有技能机制，把 `SKILL.md` 正文整段贴进对话，再接你的草稿。

### 验证装上了

问一句「按 9Corner 规范写一篇关于 XXX 的短文」。它会先问你要不要覆盖已有的分类和标签——会问就是装上了。

## 里面有什么

| 文件 | 什么时候读 | 约 token |
|---|---|---|
| `SKILL.md` | 每次写文章 | 1093 |
| `references/format.md` | 查字段、分类、语法细节 | 1996 |
| `references/cover.md` | 做封面时 | 619 |
| `references/images.md` | 配截图时 | 605 |
| `references/prompt-full.md` | **平时不读**，只在怀疑拆分后丢了东西时对照 | 5416 |

拆开的理由就是省上下文：写一篇普通文章只加载 1093 tokens，需要查细则才加 1996。做封面时不会顺带把语法清单也读进来——这是一次性贴长文做不到的。

`prompt-full.md` 是拆开之前的原始全文，留作对照，也方便不装 skill 的人整段复制。它没有被 `SKILL.md` 引用，不会被自动加载。

内容上，`SKILL.md` 只放「每次都要」的：硬约束、优先级、怎么写。细则全在 references。

## 配套的两个技能

这套规范管「写什么、怎么写」，管不了「写得对不对」。格式过了之后还得审一遍，那两个技能不是这份包里的东西，得自己装：

| 技能 | 管什么 | 出处 |
|---|---|---|
| `technical-writer` | 论据、结构、可溯源 | [riekelt/technical-writer](https://github.com/riekelt/technical-writer) |
| `humanizer-zh` | 空泛铺垫、重复、模板化节奏 | [op7418/Humanizer-zh](https://github.com/op7418/Humanizer-zh) |

**顺序不能反：先查论据，再查句子。** 反过来会把「说了没依据的话」当成「措辞不好」来改——这是我自己踩过的坑，改完读起来顺了，但那句话仍然是没根据的。

两个都只管形式。命令能不能跑、版本对不对、结论成不成立，还是得自己核。

`technical-writer` 是英文的十件套（设计文档、ADR、changelog、runbook……），跟博客有关的只有 `technical-writing` 和 `reviewing-technical-prose` 两个，只用这两个就够。直接读英文，不必等翻译——规则全是短祈使句，机翻反而把 `severity`、`house style` 这类有确定含义的说法译糊。

## 换成你自己的

这份规范里的分类、标签表、front matter 字段都是 9Corner 这个站的，直接抄会水土不服。三处改动让它变成你的：

**1. 分类（`SKILL.md` 硬约束第 2 条 + `references/format.md`）**

现在是「折腾笔记 / 工具实测 / AI 实践 / 建站笔记 / 随想」。换成你自己的五六个，然后**再也不加**。装不进去的选题说明该拆，或者该用 `series` 做系列。

**2. 标签表（`references/format.md` 的 30 个词）**

按你的写作面重列，但保留「预算」这个机制：总数定死，想加先砍。词太少会不够用，太多会重新碎片化——20 到 40 之间挑一个你压得住的数量。

**3. Front matter（`references/format.md`）**

字段名照你用的静态站点改（Hugo、Hexo、Astro 各不相同）。如果地址取自文件名，记得在硬约束里写明「没有 slug 字段」。

封面那套尺寸、安全区、配色是给 Firefly 主题算的，换主题要重算，或者直接删掉 `references/cover.md` 和 `SKILL.md` 里引用它的两行。

## 适用范围

**直接能用**：Firefly 主题 + 支持 skills 的 agent。

**能借鉴**：任何想给自己的博客定写作规范的人——尤其是「分类锁死 + 标签预算」这套机制，跟主题无关。

**不适合**：写营销文案、写小说、写公文。它的立论起点是「读者带着具体问题来，要能照着做」，不是「读起来舒服」。

## 出处

提炼自 <https://9corner.com/posts/writing-prompt/>，那篇里有完整的推导过程和两版可直接粘贴的提示词。

## 版本

- `1.0.0` 2026-11-08 首版：硬约束 7 条、分类与标签预算制、Firefly 语法清单、封面与截图流程。

## License

MIT。拿去改，改成自己的。
