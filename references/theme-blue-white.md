# 公众号排版组件库 —— 蓝白色系

> **使用说明**：本组件库为「蓝白色系」主题（英文标识 `blue-white`），是「红白色系」的一比一品牌蓝版本。除下述长期正文阅读规范与公众号使用边界外，版式结构、标题、卡片、章节编号、引用、列表、重点标记和组件组合逻辑均与母版一致；所有组件使用**内联样式**，可直接复制粘贴到微信公众号编辑器。
>
> **设计风格**：蓝白干净 + 克制点睛。浅蓝下划线为主标记、左竖条块引用、品牌蓝仅在锚点处出现。编号章节 + 条件式引言/导读/签名的经典编辑骨架，适合企业服务、跨境财税、政策解读、专业观点、业务判断、流程说明和案例复盘。
>
> **公众号平台限制须知**：
> - ❌ 不支持 `<style>`/`<script>`、CSS class/id、`position:fixed/absolute`、`float`、`@media`/`@keyframes`、`display:grid`
> - ✅ 支持内联 `style`、`display:flex`（有限）、`linear-gradient`（可渲染但有暗色模式检测风险，文字背景默认用纯色）、`border-radius`、`box-shadow`、`<section>/<p>/<span>/<strong>/<img>` 等基础标签
>
> **WeChat 兼容铁律**（本主题组件全部已按此写好，改动时必须遵守）：
> - 所有"装饰性空元素"（蓝色渐变分割线、END 短线、光晕竖条、数据卡分隔）**必须在内部放 `<span leaf=""><br></span>` 占位**，否则微信会剥掉样式
> - **不要把 `font-size`/`border-bottom` 打在 `<strong>` 上**，也不要在同一个 `<p>` 里混多个不同 `font-size`——微信编辑器会自动"纠正"导致样式被重写。正确做法：拆成多个 `<p>`，每个 `<p>` 只有一个字号；高亮样式统一挂在外层 `<span>` 上
> - 不用 `position:absolute` 做划线/高亮，删除线用 `text-decoration:line-through`
> - 结构化区域（如引言卡右下署名、图片说明）没有内容时**整块删掉**，不留空 section

---

## 设计变量速查表

```
主色调：       #1E5876（品牌蓝）
主色调深：     #153F55（深蓝）
主色调浅：     #94BDCE（浅蓝）
主色调极浅：   #E6F0F4（浅蓝白）
主色调背景：   #F3F8FA（极浅蓝灰底）
浅蓝标记色：   #B8D3DE（下划线/左竖条专用）
标题色：       #1C1917（近黑）
正文色：       #374151（深灰）
辅助文字色：   #9CA3AF（中灰）
分割线色：     #E5E7EB
灰竖条：       #D6D3D1（灰底引用左竖条）
正文字号：     15px（长期基线）
行高：         1.75
字间距：       1px
段前：         0
段后：         8px
普通重点：     正文原字号加粗为主
强结论：       必要时 16–17px
最大宽度：     677px
内容区边距：   0 10px（左右各 10px）
```

字体栈：`-apple-system,BlinkMacSystemFont,'PingFang SC','Hiragino Sans GB','Microsoft YaHei',sans-serif`

---

## 公众号正文使用边界

1. **文章标题不进入正文 HTML**：`# 标题` 只用于微信公众号后台“标题”栏。
2. **公众号摘要不进入正文 HTML**：frontmatter 摘要或单独提供的公众号摘要只用于后台“摘要”栏，不得复制或改写成正文引言。
3. **引言不是固定组件**：政策解读、热点分析、专业判断、对比分析类文章，仅在原文已有引言、导语或开头引用时使用组件 2；流程、步骤、FAQ、基础实操类文章不得自动新增引言。
4. **导读不是固定组件**：组件 3 完整保留，但仅在原文已有目录/导读或用户明确要求时使用，不得为了套主题新增原文不存在的信息层级。
5. **人工配图定位标记只保留位置**：原文中的 `【配图X】` 只作为用户在微信公众号后台手动插入真实图片的定位标记。预览 HTML 使用组件 14b 显示简洁、居中的浅灰文字；不使用大面积占位框，不设置固定高度或 `min-height`，不使用明显背景、边框、虚线框或大 `padding`，也不额外生成空段落。上下间距保持克制，配图后的正文或小标题继续沿用原有组件和样式自然衔接。`【图片X】`、`【插图X】` 等同类人工定位标记沿用同一原则。
6. **可选图片来源只对应具体图片**：仅当原文在 `【配图X】` 后提供同编号的 `【图片来源X】来源文字` 时，才按组件 14c 紧跟对应图片位置输出 `图片来源：来源文字`；控制标记 `【图片来源X】` 本身不得进入最终 HTML。不得自行补充、猜测或生成来源；没有对应来源时不得生成图注或预留空白。
7. **图片来源与文末信息来源严格分开**：`【图片来源X】` 只对应编号相同的单张图片，显示在该图片下方；`【信息来源】` 是整篇文章的信息依据，仍按文章末尾的信息来源规则处理。两者不得合并或互相替代。
8. **固定公司介绍模板不进入正文主题排版**：由用户在微信公众号后台另行插入。组件 16 仅用于原文已有的作者签名，或用户明确要求的作者签名；不得用它代替固定公司介绍模板。
9. **内容保真优先**：不得为了套组件新增目录、总结、英文标签、互动 CTA 或其他原文不存在的信息层级；组件按原文结构和用户明确要求条件使用。

---

## 组件 1 全局容器

```html
<section style="max-width:677px;margin:0 auto;background:#ffffff;font-family:-apple-system,BlinkMacSystemFont,'PingFang SC','Hiragino Sans GB','Microsoft YaHei',sans-serif;color:#374151;font-size:15px;line-height:1.75;letter-spacing:1px;overflow-x:hidden;">

  <!-- 所有组件放在这里 -->

</section>
```

---

## 组件 2 开头引言卡片（白底 + 蓝色阴影光晕）

> **文案策略（先读，比代码重要）**：
> - 本组件仅排版原文已有的引言、导语或开头引用，不得从标题、摘要或正文另行提炼、改写或补充金句
> - 政策解读、热点分析、专业判断、对比分析可按原文使用；流程、步骤、FAQ、基础实操类文章不得自动新增
> - 原文没有引言时，组件 2 整块不生成，左上方装饰性双引号也不得单独输出
> - 引言中的重点词只从原文已有重点关系中映射，不得为了视觉效果改写原句
> - **引言组件左上方的装饰性双引号属于主题固定视觉元素，必须保留。该双引号不是正文内容，不属于“新增正文字符”，排版时不得因为“不能修改或增加正文文字”而删除。**固定沿用当前组件参数：颜色 `#1E5876`，位置、字号、字重、行高和间距不得改动
> - 右下署名按文章实际作者填，未知则整行删掉，**不要固定写"甲木"**
> - 蓝底白字标签仅在本卡片内使用（视觉焦点），正文中的关键词标签一律用浅蓝底深蓝字（组件 7b）

```html
<section style="margin:10px 10px 32px;background:#ffffff;border-radius:12px;box-shadow:0 4px 24px -4px rgba(30,88,118,0.15);padding:28px 24px 22px;overflow:hidden;">
  <p style="font-size:42px;color:#1E5876;font-weight:900;margin:0;line-height:0.6;">
    <span leaf="">"</span>
  </p>
  <p style="font-size:16px;font-weight:800;color:#1C1917;margin:12px 0 8px;line-height:1.75;padding-left:4px;">
    <span style="background:#1E5876;color:#FFFFFF;padding:2px 8px;border-radius:4px;"><span leaf="">{{高亮关键词}}</span></span>
    <span leaf="">{{金句中段}}</span>
    <span style="background:#1E5876;color:#FFFFFF;padding:2px 8px;border-radius:4px;"><span leaf="">{{高亮关键词}}</span></span>
    <span leaf="">{{金句收尾}}</span>
  </p>
  <p style="text-align:right;font-size:12px;color:#9CA3AF;margin:8px 0 0;letter-spacing:1px;">
    <span leaf="">—— {{作者名，未知则删整行}}</span>
  </p>
</section>
```

---

## 组件 3 前言导读区域（本文看点，三列目录卡片）

> 蓝底白字编号 + 深色标题；仅在原文已有目录/导读或用户明确要求时使用，展示原文已有的 3 个核心看点，不自动提炼或新增目录。

```html
<section style="padding:0 10px 32px;">
  <p style="font-size:14px;color:#9CA3AF;margin:0 0 14px;letter-spacing:1px;">
    <span leaf="">📌 本文看点</span>
  </p>
  <section style="display:flex;justify-content:space-between;">
    <section style="flex:1;background:#F3F8FA;border-radius:10px;padding:16px 12px;margin-right:8px;text-align:center;border:1px solid #E6F0F4;">
      <p style="display:inline-block;background:#1E5876;color:#FFFFFF;font-size:12px;font-weight:800;padding:2px 10px;border-radius:4px;margin:0 0 8px;"><span leaf="">01</span></p>
      <p style="font-size:13px;font-weight:700;color:#1C1917;margin:0;"><span leaf="">{{看点一}}</span></p>
    </section>
    <section style="flex:1;background:#F3F8FA;border-radius:10px;padding:16px 12px;margin-right:8px;text-align:center;border:1px solid #E6F0F4;">
      <p style="display:inline-block;background:#1E5876;color:#FFFFFF;font-size:12px;font-weight:800;padding:2px 10px;border-radius:4px;margin:0 0 8px;"><span leaf="">02</span></p>
      <p style="font-size:13px;font-weight:700;color:#1C1917;margin:0;"><span leaf="">{{看点二}}</span></p>
    </section>
    <section style="flex:1;background:#F3F8FA;border-radius:10px;padding:16px 12px;text-align:center;border:1px solid #E6F0F4;">
      <p style="display:inline-block;background:#1E5876;color:#FFFFFF;font-size:12px;font-weight:800;padding:2px 10px;border-radius:4px;margin:0 0 8px;"><span leaf="">03</span></p>
      <p style="font-size:13px;font-weight:700;color:#1C1917;margin:0;"><span leaf="">{{看点三}}</span></p>
    </section>
  </section>
</section>
```

---

## 组件 4 章节分割线（蓝色渐变）

```html
<section style="padding:0 10px;">
  <section style="height:1px;background:linear-gradient(to right,transparent,#94BDCE,#1E5876,#94BDCE,transparent);margin:0;">
    <span leaf=""><br></span>
  </section>
</section>
```

---

## 组件 5 章节标题（蓝底编号标签 + 标题）

> 蓝色实底编号标签 + 英文小标签 + 中文大标题，底部蓝色实线。第一章 `margin-top:16px`，后续章节 `margin-top:48px`。
>
> **内容保真规则**：原文标题未编号时，可按主题默认使用 `01/02/03…`；原文已含“一、／二、”等编号时必须复用原编号，不能叠加第二套编号。英文标签仅在原文已有或用户明确要求时保留；严格保真场景删除英文标签整行，不新增 `SECTION` 等文字。结语只有在原文确为结语且允许主题编号时才使用 `∞`，否则保留原文标题。

```html
<section style="margin-top:48px;margin-bottom:28px;padding:0 10px;">
  <section style="display:flex;align-items:center;justify-content:space-between;margin-bottom:20px;padding-bottom:14px;border-bottom:3px solid #1E5876;">
    <section style="display:flex;align-items:center;">
      <span style="display:inline-block;background:#1E5876;color:#FFFFFF;font-size:18px;font-weight:900;padding:4px 14px;border-radius:6px;margin-right:14px;line-height:1.3;"><span leaf="">01</span></span>
      <section>
        <p style="font-size:10px;color:#1E5876;font-weight:700;letter-spacing:3px;margin:0 0 2px;text-transform:uppercase;">
          <span leaf="">{{ENGLISH TAG}}</span>
        </p>
        <h3 style="font-size:18px;font-weight:800;color:#1C1917;margin:0;letter-spacing:0.5px;">
          <span leaf="">{{中文章节标题}}</span>
        </h3>
      </section>
    </section>
  </section>

  <!-- 本章节正文内容放在这里 -->

</section>
```

**结语章节变体**（编号用 `∞` 替代数字，英文标签用 `THE END` / `EPILOGUE`）：

```html
<span style="display:inline-block;background:#1E5876;color:#FFFFFF;font-size:18px;font-weight:900;padding:4px 14px;border-radius:6px;margin-right:14px;line-height:1.3;"><span leaf="">∞</span></span>
```

---

## 组件 6 正文段落

> **关键规则**：每段主动识别 1~3 个关键短语，用**浅蓝下划线（7d）**标记——这是本风格的核心视觉特征，让读者快速扫到每段重点。

**基础段落**：

```html
<p style="margin:0 0 8px;font-size:15px;line-height:1.75;letter-spacing:1px;text-align:justify;">
  <span leaf="">{{正文内容}}</span>
</p>
```

**带关键词下划线标记的段落**（推荐默认）：

```html
<p style="margin:0 0 8px;font-size:15px;line-height:1.75;letter-spacing:1px;text-align:justify;">
  <span leaf="">{{前半句}}</span>
  <span style="border-bottom:2px solid #B8D3DE;font-weight:600;"><span leaf="">{{需要强调的关键短语}}</span></span>
  <span leaf="">{{后半句}}</span>
</p>
```

**标记原则**：每段选 1~3 个关键短语（4~15 字）加下划线，不要整段都标；优先标核心观点、结论判断、关键数据、专有名词；无重点的段落可不标。

---

## 组件 6b 子标题（`###` 小节标题）

> `###` 子标题用蓝色左竖条 + 深色标题，**不套用组件 5 的编号章节样式**（编号章节只给 `##`）。

```html
<p style="font-size:15px;font-weight:800;color:#1C1917;margin:28px 0 14px;padding-left:10px;border-left:3px solid #1E5876;line-height:1.4;">
  <span leaf="">{{子标题}}</span>
</p>
```

---

## 组件 7 正文高亮样式（5 种变体 + 使用策略）

> **核心理念**：克制用色，蓝色只在真正需要的锚点出现。
>
> **优先级**：① 7d 浅蓝下划线（正文默认标记）→ ② 7a 普通加粗为主、蓝色加粗仅锚点 → ③ 7b 浅蓝底深蓝字标签（每篇 2~4 个）→ ④ 7c 浅蓝背景（次要）→ ⑤ 7e 荧光笔（偶尔长句强调）

### 7a. 加粗强调

普通加粗（默认，绝大部分加粗用这个）：

```html
<strong><span leaf="">普通加粗强调</span></strong>
```

普通重点继承正文 `15px`，只增加字重。整段强结论仍沿用组件 6 的结构，仅在必要时把外层正文段落设为 `16px`；全文最终强结论可极少量使用 `17px`，不得同时改变原文内容或新增结论。

蓝色加粗（仅限产品名/步骤/CTA 等锚点，全文 ≤5 处）：

```html
<strong style="color:#1E5876;"><span leaf="">蓝色加粗锚点</span></strong>
```

### 7b. 浅蓝底深蓝字标签（核心概念，每篇 2~4 个）

```html
<span style="background:#E6F0F4;color:#153F55;padding:2px 6px;border-radius:3px;font-weight:700;"><span leaf="">关键词标签</span></span>
```

### 7c. 浅蓝背景高亮（次要关键词）

```html
<span style="background:#E6F0F4;padding:1px 6px;border-radius:3px;font-weight:600;color:#153F55;"><span leaf="">浅蓝背景关键词</span></span>
```

### 7d. 浅蓝下划线（最常用，本风格标志性标记）

```html
<span style="border-bottom:2px solid #B8D3DE;font-weight:600;"><span leaf="">浅蓝下划线关键词</span></span>
```

### 7e. 荧光笔效果（偶尔用于长句强调）

```html
<span style="background:#B8D3DE;font-weight:700;color:#1C1917;"><span leaf="">荧光笔效果的重要长句</span></span>
```

### 7f. 行内代码

```html
<span style="background:#F3F4F6;color:#1F2937;padding:2px 6px;border-radius:4px;font-size:14px;font-weight:600;"><span leaf="">code</span></span>
```

---

## 组件 8 引用高亮块（3 种变体）

### 8a. 浅蓝底左竖条金句引用（视觉焦点最强，核心金句）

```html
<section style="background:#F3F8FA;border-radius:0 10px 10px 0;border-left:4px solid #1E5876;padding:18px 22px;margin-bottom:24px;">
  <p style="font-size:16px;font-weight:800;color:#153F55;margin:0;line-height:1.8;">
    <span leaf="">「{{核心观点或关键金句}}」</span>
  </p>
</section>
```

### 8b. 浅蓝背景引用块（Prompt / 引用内容）

```html
<section style="background:#F3F8FA;border-radius:10px;padding:18px 20px;margin-bottom:24px;border:1px solid #B8D3DE;">
  <p style="font-size:15px;color:#374151;margin:0;line-height:1.8;text-align:justify;">
    <span leaf="">{{引用内容，可含 7d 下划线等内联样式}}</span>
  </p>
</section>
```

### 8c. 灰色左竖条引用（轻量旁注、个人吐槽）

```html
<section style="border-left:4px solid #D6D3D1;padding:14px 20px;margin-bottom:24px;background:#FAFAFA;border-radius:0 8px 8px 0;">
  <p style="font-size:14px;color:#374151;margin:0;line-height:1.8;text-align:justify;">
    <span leaf="">{{轻量旁注内容}}</span>
  </p>
</section>
```

### 8d. 居中金句分隔（章节间的过渡金句）

```html
<p style="font-size:15px;margin:0 0 24px;text-align:center;color:#1E5876;font-weight:700;letter-spacing:1px;border-top:1px solid #E6F0F4;border-bottom:1px solid #E6F0F4;padding:14px 10px;">
  <span leaf="">{{居中金句}}</span>
</p>
```

---

## 组件 9 提示 / 警示条

### 9a. 蓝色提示条（重要提醒、核心结论）

```html
<section style="background:#F3F8FA;border-left:4px solid #1E5876;border-radius:0 8px 8px 0;padding:14px 20px;margin-bottom:24px;">
  <p style="font-size:14px;font-weight:700;color:#153F55;margin:0;line-height:1.8;">
    <span leaf="">💡 {{重要提示或核心结论}}</span>
  </p>
</section>
```

### 9b. 踩坑提示（灰底，风险/注意事项）

```html
<section style="padding:6px 0 4px;margin-bottom:16px;">
  <p style="margin-bottom:6px;font-size:12px;font-weight:700;color:#9CA3AF;letter-spacing:1px;">
    <span style="color:#1E5876;"><span leaf="">！踩坑提示 🕳</span></span>
  </p>
  <p style="font-size:14px;color:#374151;margin:0;line-height:1.7;">
    <span leaf="">{{提示内容}}</span>
  </p>
</section>
```

---

## 组件 10 内容标签组（STEP / SKILL / TOOL / CASE）

> 教程用 STEP、盘点用 SKILL/TOOL、案例用 CASE。蓝底白字编号标签 + 标题。

### 10a. step-label（教程步骤）

```html
<section style="margin-bottom:22px;">
  <section style="display:flex;align-items:center;gap:8px;margin-bottom:10px;">
    <span style="display:inline-block;background:#1E5876;color:#fff;font-size:11px;font-weight:700;padding:2px 8px;border-radius:4px;"><span leaf="">STEP 01</span></span>
    <span style="font-size:15px;font-weight:800;color:#1C1917;"><span leaf="">{{步骤标题}}</span></span>
  </section>
  <p style="font-size:15px;margin:0 0 16px;color:#374151;line-height:1.8;text-align:justify;">
    <span leaf="">{{步骤内容}}</span>
  </p>
</section>
```

`STEP 01` 可替换为 `SKILL 1`、`TOOL 摄像机`、`CASE 01`（盘点/案例场景）；盘点场景标签底色可改灰 `#E5E7EB`+字 `#153F55` 做次级层次。

### 10b. tool-card（工具/条目说明卡）

```html
<section style="background:#fff;border-radius:12px;padding:16px 20px;box-shadow:0 4px 16px rgba(30,88,118,0.10);margin-bottom:24px;">
  <p style="font-size:14px;color:#374151;margin:0;line-height:1.8;">
    <span leaf="">{{条目说明内容}}</span>
  </p>
</section>
```

---

## 组件 11 列表组件

### 11a. ordered-list（蓝色圆标数字编号列表）

```html
<section style="margin-bottom:24px;">
  <section style="display:flex;align-items:flex-start;gap:10px;margin-bottom:12px;">
    <span style="display:inline-flex;align-items:center;justify-content:center;width:22px;height:22px;background:#1E5876;color:#fff;font-size:12px;font-weight:700;border-radius:50%;flex-shrink:0;margin-top:2px;"><span leaf="">1</span></span>
    <p style="font-size:15px;color:#374151;margin:0;line-height:1.8;flex:1;"><span leaf="">{{列表项内容}}</span></p>
  </section>
  <section style="display:flex;align-items:flex-start;gap:10px;margin-bottom:12px;">
    <span style="display:inline-flex;align-items:center;justify-content:center;width:22px;height:22px;background:#1E5876;color:#fff;font-size:12px;font-weight:700;border-radius:50%;flex-shrink:0;margin-top:2px;"><span leaf="">2</span></span>
    <p style="font-size:15px;color:#374151;margin:0;line-height:1.8;flex:1;"><span leaf="">{{列表项内容}}</span></p>
  </section>
  <section style="display:flex;align-items:flex-start;gap:10px;margin-bottom:12px;">
    <span style="display:inline-flex;align-items:center;justify-content:center;width:22px;height:22px;background:#1E5876;color:#fff;font-size:12px;font-weight:700;border-radius:50%;flex-shrink:0;margin-top:2px;"><span leaf="">3</span></span>
    <p style="font-size:15px;color:#374151;margin:0;line-height:1.8;flex:1;"><span leaf="">{{列表项内容}}</span></p>
  </section>
</section>
```

### 11b. pill-list（无序要点，蓝点前缀 + 说明）

```html
<section style="margin-bottom:14px;">
  <p style="margin:0 0 6px;">
    <span style="display:inline-block;font-size:14px;font-weight:700;color:#153F55;background:#E6F0F4;padding:3px 10px;border-radius:999px;"><span style="display:inline-block;width:6px;height:6px;background:#1E5876;border-radius:50%;margin-right:5px;vertical-align:middle;"><span leaf=""><br></span></span><span leaf="">{{要点标题}}</span></span>
  </p>
  <p style="font-size:14px;color:#4B5563;margin:0;line-height:1.7;text-align:justify;">
    <span leaf="">{{要点说明}}</span>
  </p>
</section>
```

### 11c. timeline（时间线 / 递进脉络，访谈经历、案例演进）

```html
<section style="display:flex;margin-bottom:24px;">
  <section style="display:flex;flex-direction:column;align-items:center;margin-right:16px;flex-shrink:0;">
    <section style="width:14px;height:14px;border-radius:50%;border:3px solid #1E5876;background:#fff;margin-top:4px;"><span leaf=""><br></span></section>
    <section style="width:2px;background:#E6F0F4;flex:1;margin-top:4px;min-height:44px;"><span leaf=""><br></span></section>
  </section>
  <section style="flex:1;padding-bottom:12px;">
    <p style="margin:0 0 6px;font-size:15px;font-weight:800;color:#1C1917;"><span leaf="">{{节点标题}}</span></p>
    <p style="font-size:15px;margin:0;color:#374151;line-height:1.8;text-align:justify;"><span leaf="">{{节点内容}}</span></p>
  </section>
</section>
```

最后一个节点去掉竖线段。

---

## 组件 12 数据 / 要点卡片组

### 两列版

```html
<section style="display:flex;margin-bottom:24px;padding:0;">
  <section style="flex:1;background:#F3F8FA;border-radius:10px;padding:18px 16px;margin-right:8px;text-align:center;border:1px solid #E6F0F4;">
    <p style="font-size:28px;font-weight:900;color:#1E5876;margin:0 0 4px;line-height:1;"><span leaf="">{{数字}}</span></p>
    <p style="font-size:12px;color:#9CA3AF;margin:0;"><span leaf="">{{说明}}</span></p>
  </section>
  <section style="flex:1;background:#F3F8FA;border-radius:10px;padding:18px 16px;text-align:center;border:1px solid #E6F0F4;">
    <p style="font-size:28px;font-weight:900;color:#1E5876;margin:0 0 4px;line-height:1;"><span leaf="">{{数字}}</span></p>
    <p style="font-size:12px;color:#9CA3AF;margin:0;"><span leaf="">{{说明}}</span></p>
  </section>
</section>
```

### 三列版

```html
<section style="display:flex;margin-bottom:24px;padding:0;">
  <section style="flex:1;background:#F3F8FA;border-radius:10px;padding:16px 10px;margin-right:8px;text-align:center;border:1px solid #E6F0F4;">
    <p style="font-size:24px;font-weight:900;color:#1E5876;margin:0 0 4px;line-height:1;"><span leaf="">{{数字}}</span></p>
    <p style="font-size:11px;color:#9CA3AF;margin:0;"><span leaf="">{{说明}}</span></p>
  </section>
  <section style="flex:1;background:#F3F8FA;border-radius:10px;padding:16px 10px;margin-right:8px;text-align:center;border:1px solid #E6F0F4;">
    <p style="font-size:24px;font-weight:900;color:#1E5876;margin:0 0 4px;line-height:1;"><span leaf="">{{数字}}</span></p>
    <p style="font-size:11px;color:#9CA3AF;margin:0;"><span leaf="">{{说明}}</span></p>
  </section>
  <section style="flex:1;background:#F3F8FA;border-radius:10px;padding:16px 10px;text-align:center;border:1px solid #E6F0F4;">
    <p style="font-size:24px;font-weight:900;color:#1E5876;margin:0 0 4px;line-height:1;"><span leaf="">{{数字}}</span></p>
    <p style="font-size:11px;color:#9CA3AF;margin:0;"><span leaf="">{{说明}}</span></p>
  </section>
</section>
```

### 表格（真实数据表用）

```html
<section style="margin-bottom:24px;overflow-x:auto;">
  <table style="width:100%;border-collapse:collapse;font-size:14px;">
    <thead>
      <tr>
        <th style="background:#1E5876;color:#fff;font-weight:700;padding:8px 12px;text-align:left;"><span leaf="">{{列标题}}</span></th>
        <th style="background:#1E5876;color:#fff;font-weight:700;padding:8px 12px;text-align:left;"><span leaf="">{{列标题}}</span></th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td style="padding:8px 12px;border-bottom:1px solid #E6F0F4;color:#374151;"><span leaf="">{{内容}}</span></td>
        <td style="padding:8px 12px;border-bottom:1px solid #E6F0F4;color:#374151;"><span leaf="">{{内容}}</span></td>
      </tr>
      <tr>
        <td style="padding:8px 12px;border-bottom:1px solid #E6F0F4;color:#374151;background:#F3F8FA;"><span leaf="">{{内容}}</span></td>
        <td style="padding:8px 12px;border-bottom:1px solid #E6F0F4;color:#374151;background:#F3F8FA;"><span leaf="">{{内容}}</span></td>
      </tr>
    </tbody>
  </table>
</section>
```

---

## 组件 13 标签胶囊

浅蓝底深蓝字（默认）：

```html
<span style="display:inline-block;background:#E6F0F4;color:#153F55;font-size:12px;font-weight:700;padding:2px 10px;border-radius:4px;margin-right:6px;"><span leaf="">标签名</span></span>
```

蓝色描边（轻量）：

```html
<span style="display:inline-block;border:1px solid #1E5876;color:#1E5876;font-size:12px;font-weight:600;padding:1px 10px;border-radius:4px;margin-right:6px;"><span leaf="">标签名</span></span>
```

---

## 组件 14 图片容器

```html
<section style="background:#FFF;border-radius:12px;padding:6px;border:1px solid #E5E7EB;box-shadow:0 4px 12px -2px rgba(0,0,0,0.08);margin-bottom:10px;">
  <section style="margin:0;border-radius:8px;overflow:hidden;">
    <span leaf=""><img src="{{图片URL}}" style="max-width:100%;height:auto;display:block;margin:0 auto;"></span>
  </section>
</section>
```

带说明文字时，图片 `margin-bottom` 改 `8px`，其后加：

```html
<p style="font-size:12px;color:#9CA3AF;text-align:center;margin:0 0 24px;">
  <span leaf="">— {{图片说明}}</span>
</p>
```

多行代码块用通用增量库 `common-components.md` 的 1a 深色 / 1b 浅色（左竖条换 `#1E5876`），禁 `white-space:pre`。

### 14b. 人工插图定位标记（`【配图X】`）

> 本组件只在预览 HTML 中标示用户后续手动插图的位置，不代表图片容器。采用已经确认有效的简单段落方案：定位文字简洁、居中、浅灰，不设置固定高度或 `min-height`，不使用大面积背景、边框、虚线框或大 `padding`，也不额外生成空段落。上下间距保持克制，后续正文或小标题继续使用原有 blue-white 组件自然衔接；不得改用零高度特殊容器或 `font-size:0 / line-height:0` 等空段塌缩实验方案。

```html
<p style="margin:12px 0 8px;font-size:13px;color:#9298A1;line-height:1.5;text-align:center;letter-spacing:0.5px;">
  <span leaf="">【配图1】</span>
</p>
```

### 14c. 可选图片来源（`【图片来源X】来源文字`）

> 仅当原文提供与 `【配图X】` 编号相同的 `【图片来源X】` 时使用。`【图片来源X】` 后面的文字就是该张图片本次实际来源，必须原样使用，不得修改、补充、替换或猜测。输出时删除控制标记，只保留 `图片来源：来源文字`。图注是独立块，必须紧跟组件 14b；使用本组件时，组件 14b 的 `margin-bottom` 从 `8px` 改为 `2px`，让图注与配图位置保持较小距离。没有对应来源时整行不生成，不预留空白。

```html
<p style="margin:0 0 16px;font-size:12px;color:#9298A1;font-weight:400;line-height:1.5;text-align:center;letter-spacing:0.5px;">
  <span leaf="">图片来源：{{来源文字}}</span>
</p>
```

**与文末信息来源的边界**：组件 14c 只对应单张具体图片；文章末尾的 `【信息来源】` 是整篇文章的信息依据，继续按文末信息来源规则处理。二者不得合并或互相替代。

---

## 组件 15 END 结尾分割线

```html
<section style="padding:0 10px;">
  <section style="text-align:center;margin:0 0 32px;">
    <section style="display:flex;align-items:center;justify-content:center;">
      <span style="height:2px;width:60px;background:linear-gradient(to right,transparent,#1E5876);margin-right:12px;"><span leaf=""><br></span></span>
      <span style="font-size:11px;color:#1E5876;letter-spacing:3px;font-weight:700;"><span leaf="">END</span></span>
      <span style="height:2px;width:60px;background:linear-gradient(to left,transparent,#1E5876);margin-left:12px;"><span leaf=""><br></span></span>
    </section>
  </section>
</section>
```

---

## 组件 16 尾部作者签名区

> 固定签名文案以正文段落形式呈现；有个人名片/引导图素材才放图，无素材整块删。

```html
<section style="padding:0 10px;">
  <section style="text-align:center;margin-bottom:10px;border-radius:12px;overflow:hidden;">
    <span leaf=""><img src="{{个人名片或引导图URL，无则删本 section}}" style="max-width:100%;height:auto;display:block;margin:0 auto;"></span>
  </section>
  <p style="margin-bottom:20px;font-size:15px;line-height:1.8;text-align:justify;">
    <span leaf="">我是 {{作者名}}，{{一句话简介，如：热衷于分享 AI 观察与干货}}。</span>
  </p>
  <p style="margin-bottom:20px;font-size:15px;line-height:1.8;text-align:justify;">
    <span leaf="">如果你觉得今天这篇有收获，欢迎</span>
    <strong style="color:#1E5876;"><span leaf="">点赞、在看、转发</span></strong>
    <span leaf="">三连，我们下篇见。</span>
  </p>
</section>
```

---

## 完整文章模板骨架

```html
<section style="max-width:677px;margin:0 auto;background:#ffffff;font-family:-apple-system,BlinkMacSystemFont,'PingFang SC','Hiragino Sans GB','Microsoft YaHei',sans-serif;color:#374151;font-size:15px;line-height:1.75;letter-spacing:1px;overflow-x:hidden;">

  <!-- 1. 可选开头引言卡片（组件2）：仅原文已有引言/导语/开头引用，或用户明确要求时使用 -->

  <!-- 2. 原文前言正文（组件6 段落 × N，放 0 10px 边距 section） -->

  <!-- 3. 可选前言导读（组件3）：仅原文已有目录/导读或用户明确要求时使用 -->

  <!-- 4. 第一章（组件5 章节标题，margin-top:16px） -->
  <!--    章内：组件6 正文 + 6b 子标题 + 7 行内高亮 + 8 引用 + 9 提示 + 10 标签组 + 11 列表 + 12 数据 + 14 图片 -->

  <!-- 5. 第二章…第N章（组件5，margin-top:48px）；组件4 分割线按原文结构和兼容性要求选用 -->

  <!-- 6. 原文存在结语时：结语章（组件5；允许主题编号时可用 ∞ 变体） -->

  <!-- 7. 可选 END 分割线（组件15）：仅原文存在或用户明确要求时使用 -->

  <!-- 8. 可选作者签名（组件16）：仅原文存在或用户明确要求时使用 -->

  <!-- 公众号标题、公众号摘要、后台来源说明、固定公司介绍模板均不放入本正文容器 -->

</section>
```

**装配边界**：引言、导读、END、作者签名均为条件组件，不能为了主题完整性自动新增；使用时保持上述相对顺序。文章标题、公众号摘要、后台来源说明、固定公司介绍模板始终位于正文主题之外。

---

## 视觉层级（3 层递进）

| 层级 | 样式 | 用途 | 频率 |
|------|------|------|------|
| **锚点层** | 蓝色加粗 7a / 蓝底白字（仅引言卡）/ 金句引用 8a | 产品名、关键结论、核心金句 | 全文 ≤5 处 |
| **标记层** | 浅蓝下划线 7d（默认）/ 浅蓝底标签 7b | 正文关键词强调 | 每段 1~3 处 |
| **容器层** | 左竖条引用 8x / 提示 9x / 标签组 10 / 卡片 11-12 | 引用、旁注、提示、结构化信息 | 按需 |

**克制原则**：
- 蓝底白字标签（`bg:#1E5876`）**仅在引言卡内**，正文关键词标签用浅蓝底深蓝字 7b
- 蓝色加粗全文 ≤5 处
- 引用/提示统一用左竖条 + 浅底 + 类型小标签，**不用四周虚线框**（dashed）
- 渐变蓝仅出现在章节分割线 4 和 END 线 15

---

## 文章类型 → 组件组合配方

按 SKILL.md 第 3 步判定的文章类型选配方；核心组件构成本篇排版主旋律，点缀组件按内容出现处使用，一篇文章点缀组件种类 ≤3，避免花哨。

| 文章类型 | 核心组件组合 | 点缀组件 |
|---|---|---|
| 观点/深度分析/政策解读/业务判断 | 正文6 + 金句引用8a + 居中金句8d | 浅蓝引用8b、踩坑提示9b |
| 教程/操作指南/流程说明/FAQ | step-label 10a + 代码块（通用库1a）+ ordered-list 11a | 蓝色提示9a、tool-card 10b |
| 盘点/工具清单 | skill/tool-label 10a + tool-card 10b + pill-list 11b | 数据卡12、标签胶囊13 |
| 访谈/人物特稿 | 正文6 + 金句引用8a（引语）+ timeline 11c（经历脉络） | 居中金句8d、灰底旁注8c |
| 数据复盘/报告 | 数据卡12（两列/三列）+ 表格12 + ordered-list 11a | 蓝色提示9a、荧光笔7e |
| 生活/情感随笔 | 正文6 + 居中金句8d + 灰底旁注8c | 金句引用8a（少量） |
| 案例实战/案例复盘 | case-label 10a / timeline 11c + step-label 10a | 浅蓝引用8b、踩坑提示9b |

企业服务、跨境财税类文章通常以“正文 6 + 章节标题 5”为基础，提示、引用、列表、数据组件仅按原文语义选用。所有类型中的引言 2、导读 3、END 15、作者签名 16 均为条件组件；不得为了套配方增加原文不存在的信息层级。

---

## Markdown → 蓝白排版 映射规则

| Markdown 元素 | 对应组件 | 说明 |
|---|---|---|
| `# 标题` | 不输出到正文 | 填写到微信公众号后台“标题”栏 |
| frontmatter 摘要 / 公众号摘要 | 不输出到正文 | 填写到微信公众号后台“摘要”栏，不得复制成正文引言 |
| 文章开头 `> 引言金句` | 组件 2 白底蓝色光晕引言卡 | 仅原文已有时使用，不从标题或摘要自动生成；左上方装饰性双引号是主题固定视觉元素，必须保留，不属于新增正文字符 |
| `## 章节标题` | 组件 5 章节标题 | 原文无编号时可用 01/02…；已有编号时复用，不能重复编号；英文标签按原文/用户要求决定 |
| `### 子标题` | 组件 6b 蓝色左竖条小标题 | 不套编号章节样式 |
| 普通段落 | 组件 6 正文段落 | 15px / 1px 字距 / 1.75 行高 / 段前 0 / 段后 8px；下划线仅按原文重点关系或用户要求使用 |
| `**加粗文字**` | 组件 7a 普通加粗（默认）/ 蓝色加粗（锚点 ≤5） | 普通加粗为主 |
| `==高亮文字==` | 组件 7b 浅蓝底深蓝字标签 | 核心概念 |
| `<u>下划线</u>` / `++文字++` | 组件 7d 浅蓝下划线 | 次要强调 |
| `~~删除线~~` | `text-decoration:line-through` + 灰字 | 被淘汰概念 |
| 行内 `` `code` `` | 组件 7f 行内代码 | |
| `> 引用段落`（金句） | 组件 8a 浅蓝底左竖条 | 核心金句 |
| `> 引用段落`（旁注） | 组件 8c 灰底左竖条 | 轻量旁注 |
| 核心金句 | 组件 8a / 8d 居中金句 | 视觉焦点 |
| 操作步骤 | 组件 10a step-label | STEP 01/02… |
| 技能/工具清单 | 组件 10a skill/tool-label + 10b tool-card | |
| 案例/经历脉络 | 组件 10a case-label / 11c timeline | |
| Prompt 提示词 | 组件 8b 浅蓝引用块 / 通用库 1a（长多行） | |
| ` ``` 多行代码块 ``` ` | 通用库 1a 深色 / 1b 浅色（左竖条换 #1E5876） | 每行一个 `<p style="margin:0">` |
| 并列要点 | 组件 11b pill-list | |
| `1. 2. 3.` 编号列表 | 组件 11a ordered-list | 蓝色圆标 |
| 数据展示 | 组件 12 数据卡片组 / 表格 | 蓝色大号数据 |
| Markdown 表格 | 组件 12 表格 | 偶数行浅蓝底 |
| 注意/警告 | 组件 9a 蓝色提示 / 9b 踩坑提示 | |
| 行内标签 | 组件 13 标签胶囊 | 浅蓝底默认 |
| `---` | 组件 4 章节分割线 | 蓝色渐变 |
| `![](图片)` | 组件 14 图片容器 | 圆角卡片 + 说明 |
| `【配图X】` | 组件 14b 简洁人工插图定位标记 | 原位显示简洁、居中的浅灰文字；无固定高度、`min-height`、大面积背景、边框、虚线框、大 `padding` 或额外空段落；上下间距克制，不使用零高度特殊容器或 `font-size:0 / line-height:0` 等实验方案；不生成图片 |
| `【图片来源X】来源文字` | 组件 14c 可选图片来源 | 仅与同编号 `【配图X】` 配对并紧随其后；严格原样使用控制标记后的本次来源文字，最终只显示 `图片来源：来源文字`，不显示控制标记；无对应来源时不输出、不留白 |
| `【图片X】` / `【插图X】` | 组件 14b 人工插图定位标记 | 按同类人工定位标记处理，不生成图片，不补说明 |
| `【信息来源】` | 文章末尾信息来源区域 | 属于整篇文章的信息依据；不得与 `【图片来源X】` 合并或互相替代 |
| 文末 END / 作者签名 | 组件 15 / 16 | 仅原文存在或用户明确要求时使用；不代替固定公司介绍模板 |
| 固定公司介绍模板 | 不输出到正文 | 由用户在微信公众号后台另行添加 |
