# Wiki Schema（结构规则）

本文件是知识库的结构契约：页面类型、命名、frontmatter、时效性规则与交叉引用规范。所有 ingest 与页面更新必须遵守。

## 页面类型

| 类型 | 目录 | 用途 | 命名规范 |
|------|------|------|----------|
| entity | wiki/entities/ | 机构、企业、人物、政策文件、平台等命名实体 | 官方名称，如 `银监会.md`、`商业银行保理业务管理暂行办法.md` |
| concept | wiki/concepts/ | 概念、方法、产品模式、风控框架 | 描述性名词短语，如 `保理定义与四类服务.md` |
| source | wiki/sources/ | 一篇原始资料的摘要与分析页（一资料一页） | 见下方"来源页命名" |
| query | wiki/queries/ | 开放问题、待验证判断 | 疑问句或判断句，如 `2014年大豆违约风波后续演变.md` |
| comparison | wiki/comparisons/ | 两个/多个对象的并列对比分析 | `A与B对比.md`、`XX两种解读视角对比.md` |
| synthesis | wiki/synthesis/ | 跨资料主题综合（演进脉络、框架整合） | 主题 + 时间范围，如 `供应链金融中央政策演进2017-2022.md` |
| finding | wiki/findings/ | 经核验的关键事实、监管口径，**必须含"证据强度分层"小节** | 事实陈述句 |
| overview | wiki/overview.md | 全局概要（单页） | 固定文件名 |

## 来源页命名

- 新闻/公众号：`4-news--7-<分类编号>-<分类名>--4-<年份>-<序号>-<题名去标点>--<6位随机id>.md`
  - 例：`4-news--7-01-政策合规--4-2014--14-保理新规引发关注的三要素保理--1lfgr2k.md`
- 书籍：`5-books--8-<书名>--<6位id>.md`
- 题名去掉标点符号；保留 `-政策` / `-观点` / `-趋势` 等体裁后缀

## Frontmatter 契约

所有页面必备：

```yaml
---
type: entity | concept | source | query | comparison | synthesis | finding | overview
title: 页面标题
tags: []
related: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
---
```

source 页另加（指向原始资料）：

```yaml
authors: []
year: YYYY
url: ""
venue: ""            # 公众号名 / 出版方
sources: ["news/01-政策合规/2014/xxx.md"]   # raw/sources/ 下的相对路径数组
```

finding 页必须含 `sources:`（证据来源数组）。更新已有页面时：追加 `sources:`、扩充 `related:`、更新 `updated:` 日期。

## 时效性规则（重复/冲突信息处理）

**总原则：以最新年份的口径为准。**

1. **事实条目标注年份**：来自资料的事实注明年份（来自 source 页的 `year`），政策注明文号与发布年份。
2. **新旧口径并存**：概念/实体页中，最新信息为"当前口径"；旧口径**不删除**，在其条目后标注 `（YYYY 年口径，已被 [[新页面或新来源]] 取代）`。政策演进脉络记录在 synthesis 页。
3. **政策条文**：以最新有效文件为准。已废止或被取代的政策文件，在其实体页顶部标注状态（如"已废止，被 XX 号文取代"），正文保留原条文要点供历史对照。
4. **统计数值**：标注统计年份。更新数值时旧值移入"历史数据"条目，不覆盖删除。
5. **冲突未决**：无法确定哪个更新或两个口径并存有依据时，建/更新 query 页跟踪，正文两说并存并各自注明年份与证据强度，待证据充分后在 synthesis 页裁决。

## 可信度分层

`书籍 > 监管原文/官方答记者问 > 专业公众号分析 > 一般新闻报道`

- 引用监管文件时区分**原文口径**与**媒体解读**（观点性内容须注明）
- finding 页必须含"证据强度分层"小节，按上述层级标注每条证据

## index.md 格式

顶部保留类型分组头：`## Entities / ## Concepts / ## Sources / ## Queries / ## Comparisons / ## Synthesis / ## Findings`。**实际条目统一追加在 `## Recently Updated` 分节下**（每行 `- [[目录/slug]] — 一句话说明`，来源页用完整 stem `[[sources/4-news--…--1lfgr2k]]`）。每篇 ingest 的新页面/更新页面各占一行。

## log.md 格式

**正序追加**（新条目写在文件末尾，按时间自然排序）：

```
## YYYY-MM-DD ingest | <批次或标题>

- 动作与发现，含 [[wikilinks]]
```

## 交叉引用规则

- 页面间用 `[[slug]]`；指向来源页用完整 stem：`[[sources/4-news--7-…--1lfgr2k]]`
- 新建实体/概念页后，必须回填更新相关已有页面的 `related:`（必要时 `sources:`）
- query 页链接其依据的 sources 与 concepts
- synthesis 页在 `related:` 中列出全部贡献来源
- 每个新实体/概念都应出现在 index.md 对应分组中

## 矛盾处理

1. 在相关概念/实体页记录矛盾，并按**时效性规则**标注最新口径
2. 创建或更新 query 页跟踪开放问题
3. 证据充分后，在 synthesis 页给出裁决并链接双方来源
