# 设计团队分享资产管理规范（试行）_2026.06.08

## 一、目标

我们希望将设计分享从“一次性内容”升级为“长期可复用资产”，实现以下能力：

* 设计资产 → 可 diff（版本可追踪）
* 可检索（结构化搜索）
* 可复用（方法论沉淀）
* 可训练 AI（未来可接入 Copilot / 语义检索）

---

## 二、基本原则

一次完整的设计分享，应包含两类能力，并统一上传至 GitHub 设计团队仓库：

### 1️⃣ 展示层（Presentation Layer）

用于现场表达、阅读和托管：

* 首选：`index.html`
* 兜底：`slides.pdf`

👉 作用：保证视觉表达与阅读体验
👉 目标：对人友好

---

### 2️⃣ 结构层（Structured Layer）

用于保留分享的知识结构：

* 分享背景
* 核心观点
* 方法模型
* 框架结构
* 可复用结论
* 行动建议

结构层可以由 `index.html` 内的结构化正文承担；如果只有 PPT/PDF，则需要额外生成 `README.md`。

👉 作用：保证结构化沉淀
👉 目标：对系统 / AI 友好

---

## 三、关于 HTML、PDF 与 Markdown 的关系

如果 `index.html` 已经包含完整正文，并且内容可阅读、可检索、可维护，它就可以同时承担展示层和结构层。

这种情况下，不必再导出 `slides.pdf`，也不必再转写一份 `README.md`。

如果暂时没有 HTML，先用 `slides.pdf` 作为展示兜底；只有需要结构化沉淀时，再补充 `README.md`。

原则是：

* `index.html` = 可展示、可阅读、可托管的首选交付
* `slides.pdf` = 传统展示兜底
* `README.md` = 当 HTML 不具备结构化内容时的知识结构层
* `asset.md` = 外部资源链接占位，只在有源文件、七牛链接或补充资源时需要

结构要求不等于文件数量要求。只要产物能被阅读、检索、版本追踪和复用，就不必人为拆成多份文件。

---

## 四、仓库结构建议

每次分享建立独立文件夹。优先使用 HTML 交付：

```
design-sharing/
└── product-design-workflow/
    ├── index.html       （首选：可展示、可阅读、可托管）
    ├── README.md        （可选：摘要、入口、维护说明）
    └── asset.md         （可选：源文件、七牛链接或补充资源）

```

如果暂时只能产出 PPT/PDF，则使用兜底结构：

```
design-sharing/
└── material-design-3/
    ├── slides.pdf       （展示版）
    ├── README.md        （可选：由 slides.pdf 转写的结构化 Markdown）
    └── asset.md         （可选：源文件、七牛链接或补充资源）

```
补充：
- 文件夹命名格式默认使用 `分享主题`，中文或英文均可，但同一文件夹内保持一致。
- 如需区分同名主题、系列内容或多人同题分享，可使用 `分享主题_日期` 或 `分享主题_作者_日期`。
- HTML 分享入口统一命名为 `index.html`，便于本地打开和静态托管。
- `README.md` 和 `asset.md` 不是强制文件，只在确实承担摘要、结构化转写或外部资源链接时创建。

---

## 五、长期价值

这样做的意义是：让分享能被检索、复用、版本对比，并逐步沉淀为设计知识系统。

---

## 六：你需要如何做

### 首选流程：已经有 HTML

- 第一：在 `design-sharing/` 下创建独立文件夹，默认命名为 `分享主题`。
- 第二：将 HTML 保存为 `index.html`。
  - 预览地址拼接规则：`Pages 根地址 + 文件在仓库里的相对路径`。
  - 例如，`design-sharing/产品设计工程化工作流/index.html` 对应：
    ```text
    https://qiniu-ued.github.io/UED_Assets/design-sharing/产品设计工程化工作流/index.html
    ```
  - 浏览器地址栏可以直接粘贴中文路径；如需对外分享，优先使用转码后的地址：
    ```text
    https://qiniu-ued.github.io/UED_Assets/design-sharing/%E4%BA%A7%E5%93%81%E8%AE%BE%E8%AE%A1%E5%B7%A5%E7%A8%8B%E5%8C%96%E5%B7%A5%E4%BD%9C%E6%B5%81/index.html
    ```
- 第三：检查 HTML 是否可以直接打开，正文是否可阅读，核心观点是否可检索。
- 第四：如有源文件、七牛链接或补充资源，再创建 `asset.md` 保存链接。
- 第五：如需要在 GitHub 文件列表中补充说明，再创建薄版 `README.md`，只写摘要和入口。

### 兜底说明：暂时没有 HTML

- 先上传 `slides.pdf`，保证内容可展示、可下载。
- 如有 PPT/Keynote 源文件或外部链接，按内部 Kodo 上传规范保存到 `asset.md`。
- 只有需要结构化沉淀时，再把 `slides.pdf` 转写为 `README.md`。

注意：不要为了满足旧流程重复制造文件。产物已经具备展示、阅读和结构化能力时，保留 `index.html` 即可。
