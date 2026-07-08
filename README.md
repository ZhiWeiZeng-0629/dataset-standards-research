# dataset-standards-research

一个用于 Codex 的高质量数据集文件调研 skill。它面向国内政策、标准和行业文件场景，帮助用户按行业调研高质量数据集建设相关的顶层设计、政策文件、标准规范、技术指南、白皮书和典型案例，并按固定中文表头输出可汇报、可归档的表格。

## 适用场景

- 调研农业、医疗、工业制造、交通、金融、能源、教育、科研数据等行业的高质量数据集建设文件。
- 整理高质量数据集相关政策、标准、指南、案例和支撑性治理文件。
- 输出固定表头表格，并区分“标准明确指标”和“可参考质量指标”。
- 下载官方 PDF 或附件，并记录来源网页、附件链接和下载状态。

## 安装方法

将仓库中的 `dataset-standards-research` 文件夹复制到本机 Codex skills 目录。

如果是从 GitHub 获取：

```bash
git clone https://github.com/ZhiWeiZeng-0629/dataset-standards-research.git
cd dataset-standards-research
```

Windows 示例：

```powershell
Copy-Item -Path .\dataset-standards-research -Destination $env:USERPROFILE\.codex\skills\dataset-standards-research -Recurse
```

macOS/Linux 示例：

```bash
cp -R ./dataset-standards-research ~/.codex/skills/dataset-standards-research
```

安装后重启 Codex 或新开一个对话。

## 验证安装

新开对话后，可以输入：

```text
使用 数据集标准调研 调研【目标领域】高质量数据集相关文件。快速测试：只找 5 个官方文件，不下载 PDF。严格使用固定表头，并在最后写一段 100 字左右总结。
```

如果输出中使用了固定表头，并优先给出官方网页链接，说明 skill 已正常触发。可参考 `examples/results/` 中的真实运行结果。

## 使用示例

快速测试：

```text
使用 数据集标准调研 调研农业高质量数据集相关文件。快速测试：只找 10 个官方文件，不下载 PDF。必须包含顶层设计与政策框架、高质量数据集专项文件、农业专项文件三类。严格使用固定表头，优先中文检索，官方链接必须是具体网页，不使用门户首页或搜索首页。最后从完整清单中推荐 5-8 个重点阅读文件。
```

```text
使用 数据集标准调研 调研医疗领域高质量数据集相关政策、标准、指南和典型案例。输出固定表头表格，并说明医疗领域与农业领域在数据采集、标注、质量控制和合规方面的差异。
```


更完整的通用正式调研 prompt 见 `examples/domain-formal-research-template.md`。该文件开头有“怎么替换”步骤，说明应替换哪些位置。农业只是一个具体领域样例，见 `examples/agriculture-formal-research.md`。

## 输出表头

默认使用以下表头：

| 文档名称 | 发布机构和时间 | 文档类型 | 适用行业或场景 | 与高质量数据集构建的关系 | 核心内容摘要 | 可参考的质量指标 | 官方链接 |
| --- | --- | --- | --- | --- | --- | --- | --- |

## 核心规则

- 国内文件必须中文优先检索，优先使用中文文件名、中文机构名、标准号、文号和 `site:` 限定检索。
- 正式调研必须包含“顶层设计与政策框架”类别，不能只收集技术标准和行业案例。
- 官方链接优先使用具体 HTML 详情页、通知页或标准详情页，不使用门户首页、搜索首页替代。
- 标准类文件应优先使用标准主管平台的具体标准页；标准销售、交易、购买、付费在线阅读等商业服务网站一律排除，不纳入检索范围，也不作为补充来源。
- 判断 PDF 或正文是否可获取时，以官方详情页为准，不把第三方收费页面的限制写成官方限制。
- 完整调研应先形成完整文件清单，再从中推荐 5-8 个重点阅读文件；简版汇报才压缩为 3-5 个。
- 不得把推导出的质量指标写成文件原文指标。

## 个性化使用

安装后可以通过三种方式个性化使用。

### 1. 在提问中个性化

适合临时任务，不需要改文件。可以指定：

- 目标领域：农业、医疗、工业制造、交通、金融、能源、教育等。
- 调研深度：快速测试、正式调研、只找顶层政策、只找行业标准、只找典型案例。
- 来源范围：只要国内官方文件，或同时补充 ISO、OECD、FAO、WHO 等国际来源。
- 输出形式：只输出 Markdown 表格，或同时生成 Excel、下载 PDF、生成总结。
- 推荐数量：完整调研推荐 5-8 个重点阅读文件，简版汇报推荐 3-5 个。

示例：

```text
使用 数据集标准调研 调研能源行业高质量数据集相关文件。要求覆盖顶层政策、行业标准、数据安全和典型案例；只使用官方网页链接，不直接给 PDF 链接；最后总结能源行业与农业行业在采集、标注和合规方面的差异。
```

### 2. 修改参考文件

适合长期使用某个行业。可以 fork 仓库后修改：

- `dataset-standards-research/references/source-priorities.md`：增加优先检索的网站、主管部门、标准平台和行业机构。
- `dataset-standards-research/references/output-template.md`：调整固定表头或增加单位内部需要的字段。
- `examples/`：增加本单位常用的示例问题和期望输出。

### 3. 修改 skill 规则

适合做成单位内部版本。可以修改：

- `dataset-standards-research/SKILL.md`：调整默认调研范围、推荐文件数量、下载规则和输出口径。
- `dataset-standards-research/agents/openai.yaml`：调整显示名称和默认提示。

建议保留“官方来源优先”“固定表头”“区分原文指标和可参考指标”这三条规则，否则输出可信度会下降。

## 文件结构

```text
dataset-standards-research/
├─ SKILL.md
├─ agents/
│  └─ openai.yaml
└─ references/
   ├─ output-template.md
   └─ source-priorities.md
```

## 示例与测试

- `examples/domain-formal-research-template.md`：任意领域正式调研模板，文件开头说明了具体替换步骤。
- `examples/agriculture-quick-test.md`
- `examples/agriculture-formal-research.md`
- `examples/medical-quick-test.md`
- `examples/results/agriculture-quick-test-result.md`：一次真实运行后的农业快速测试结果样例。
- `examples/results/medical-quick-test-result.md`：一次真实运行后的医疗快速测试结果样例。
- `test-checklist.md`

## 注意事项

本 skill 主要面向中国国内政策、标准和行业文件调研。国际标准和国外政策可以作为补充，但不是默认重点。

使用时仍需人工复核关键链接、标准号、文号、文件状态和发布时间，尤其是征求意见稿、标准计划和即将实施标准。

本仓库提供的是 Codex skill。使用者需要支持本地 skills 目录的 Codex 环境；如果使用的是其他 AI 工具，可以把 `SKILL.md` 和 `references/` 中的规则作为系统提示或项目说明手动迁移。
