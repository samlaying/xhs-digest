# xhs-digest · 搜索帖子汇总

小红书搜索爬取的档案站(GitHub Pages,编辑杂志风 Editorial):
**按日期-主题归档,每爬一次出一期**。数据由 [ego-lite](https://github.com/samlaying/ego-lite) 的
`ego-browser + xhs-crawler` 自动爬取,全部笔记通过完整性校验(详情指纹 / URL 与卡片 ID 一致性 / 跨话题去重)。

线上:<https://samlaying.github.io/xhs-digest/>

## 结构

```
index.html                        # 封面画廊:刊头 + 排序(最新/最热)+ 专题卡片
20261025-mac-timemachine.html     # №01 专题一:Mac 时间机器使用指南
20261025-external-hdd.html        # №01 专题二:外置硬盘推荐
covers/*.jpg                      # 封面插画(ChatGPT 生成,ego-browser 驱动,720px JPEG)
styles.css                        # 设计系统(纸白/墨黑/社论红,衬线,双细线)
```

## 如何新增一期

1. 爬取:`sh skills/xhs-crawler/scripts/xhs_run.sh "<关键词>" "<slug>" <篇数>`
2. 封面:让 ChatGPT 生成 3:4 无文字编辑风插画(纸底/墨线/正红点缀,顶部留白),
   存为 `covers/<slug>.jpg`(720px 宽即可,~70KB)
3. 新建 `YYYYMMDD-<slug>.html`(复制任一专题页改内容;章节用 壹/贰/叁 kicker + `.section-kicker`)
4. `index.html` 画廊加一张卡片:`.card`(data-date/data-heat 供排序)+ `.cover-photo`
   (img + `.cover-overlay` 排版文字:№、标题、红规线);统计行同步更新
5. commit + push,Pages 自动发布

## 设计令牌

| 令牌 | 值 | 用途 |
|---|---|---|
| `--paper` | `#faf8f3` | 纸白背景 |
| `--ink` | `#1c1a17` | 正文墨色 |
| `--accent` | `#9e2b25` | 社论红(期号 / 引语 / 链接 / 首字下沉) |
| `--rule` | `#ddd5c5` | 分隔线 |
| `--serif` | Georgia + Songti SC 栈 | 标题与正文(无外部字体依赖) |

版式约定:正文栏宽 42em;杂志元素 = 双细线刊头、letterspaced kicker、首字下沉、
居中 pullquote、点线索引行、上下粗线夹表格。
