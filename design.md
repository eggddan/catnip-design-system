# Catnips Design System（Final Baseline，给 AI Agent 可读）

> 目标：让 AI 在生成 Catnips（GenZ 海外群体 Meme 互动内容）原型界面时，能稳定复用你在 Figma 里维护的变量（token）与组件（component）。
> 版本：`v1.0-final-baseline`（可扩展）

---

## 0) Codex 代码项目落地入口

当 Codex 在代码项目里使用这套设计系统时，必须先读取本文件，再读取 `AGENTS.md`。

- Source tokens: `/tokens/tokens.optimized.json`
- CSS variables: `/styles/tokens.css`
- Icon helper classes: `/styles/icons.css`
- Raw SVG icon library: `/assets/icons/raw`
- Icon library notes: `/assets/icons/README.md`

### 0.1 代码实现强约束

1. 所有 UI 视觉值优先使用已有 token 与 CSS variables。
2. 不要硬编码颜色、字号、行高、字重、圆角、间距、阴影、描边、icon 尺寸或 icon 颜色。
3. 代码里优先使用 `--color-*`、`--font-*`、`--radius-*`、`--shadow-*`、`--size-*` 变量。
4. 图标优先使用 `/assets/icons/raw`，常规尺寸与颜色状态可使用 `/styles/icons.css`。
5. 若本文档中的 Figma token 名称与代码变量名不同，代码实现以 `/styles/tokens.css` 的变量名为准，语义以本文档为准。
6. 生成页面前先确认产品气质：clean、light、playful、social、content-first、polished。避免 dark gaming、generic AI SaaS dashboard、heavy cyberpunk。

---

## 1) 设计系统来源

- Figma 文件（Design system）：`Catnips_Kit`
  - URL：`https://www.figma.com/design/r1ZOhB0SCOCqEyqLZrd801/Catnips_Kit?m=auto&t=b8wtZV5hQeVTNtQT-6`
  - fileKey：`r1ZOhB0SCOCqEyqLZrd801`

### 相关 Library（用于限定搜索/复用组件与变量）

- `Catnips_Kit`
  - libraryKey：`lk-f1b1c0208d56a9850bac5a6954284569e88374c7dd42ecaadb104b8e27c73cdcc618080612e60240544167b1712d4b500f65351d88c420005d229f0eb017f24d`
- `Catnip web`
  - libraryKey：`lk-d589408d77c862a79e79fd726763255b837b5924b118f367dc51207219d7153e67e636a03d162d8e400dbedf087d6a5bc638fc285fa07ef1b5be6a91c8135263`
- `Catnip Design Kit`
  - libraryKey：`lk-3938ba2f07e15caecf018e19c46ffb9b8725e2b2f2a92d060e33b489082668f26f68518d62976eb8590cf1537a60f621164125dfd4f13877a7755173c65838b4`

---

## 2) AI Agent 使用规则（强约束）

1. 颜色优先使用 `Semantic/*`（语义角色），只有在语义缺失时才考虑 `Color/*`（原始调色板）。
2. 按钮与可交互控件优先使用统一状态语义（`State: enabled / pressed / disabled`）与对应 token，而不是在组件里手写颜色。
2a. `Button` 组件默认使用 `Shape=Capsule` 作为基线；若业务或版式明确需要非 `Capsule`，Agent 可自主探索替代样式并在结果中标注“实验样式（待确认）”。
3. 排版优先使用语义化 typography style（`display-*` / `heading-*` / `body-*` / `label-*`），仅在 style 缺失时回退到底层 `Typography` 变量或 `Primitives/Font size *`。
4. 间距优先使用 `Primitives/spacing/*`（例如 `spacing/0..16`）。组件内部的专用 gap/尺寸可用 `button/*` 相关 token（如果需要）。
5. 深浅色切换：遵循组件 `Empty States` 的提示——通过 Design panel 的 `Appearance` 中“apply variable mode”来切换系统颜色（不要硬编码颜色）。

---

## 3) Token 字典（含关键条目）

> 说明：下面展示的是“可直接用于生成原型的关键 token 示例 + token 命名规则”。agent 在后续需要更多条目时，可以继续基于这些命名前缀做补全。

### 3.0 扩展治理（Compatibility & Extensibility）

1. 本文档采用“双层策略”：`Final Baseline（默认执行）` + `Experimental（可探索）`。
2. Agent 默认使用 Final Baseline；当业务明确需要或基线不足时，可产出 Experimental 方案。
3. Experimental 方案必须附带三项说明：`使用场景`、`与基线差异`、`是否建议纳入 DS`。
4. 新增 token/variant/style 时，优先保持命名兼容，不破坏已有语义键。
5. 若发生命名替换，需保留一个版本周期的别名映射说明（deprecation note）。

### 3.1 Colors（Final Baseline，基于人工校对）

#### 3.1.1 Base Colors

- `color-primary-default`: `#C6FF2E`
- `color-primary-pressed`: `#A9E522`
- `color-primary-soft`: `#F4FFE0`
- `color-primary-disabled`: `#DDF5A7`
- `color-white`: `#FFFFFF`
- `color-black`: `#000000`
- `color-neutral-100`: `#F6F7F9`
- `color-neutral-200`: `#F3F4F6`
- `color-neutral-300`: `#EEF1F4`
- `color-neutral-400`: `#DFE2E6`
- `color-neutral-500`: `#919495`
- `color-neutral-600`: `#0F1115`
- `color-sky`: `#38BDF8`
- `color-violet`: `#7C5CFF`
- `color-pink`: `#FF7EDB`
- `color-yellow`: `#FFD84D`
- `color-orange`: `#F59E0B`
- `color-coral`: `#FF6B6B`
- `color-teal`: `#14B8A6`
- `color-red`: `#EF4444`
- `color-green`: `#22C55E`

#### 3.1.2 Opacity Scale

- `opacity-90`: `0.9`
- `opacity-60`: `0.6`
- `opacity-30`: `0.3`
- `opacity-15`: `0.15`
- `opacity-10`: `0.1`
- `opacity-06`: `0.06`

#### 3.1.3 Derived Colors

- White with opacity:
  - `color-white-90`: `rgba(255, 255, 255, 0.9)`
  - `color-white-60`: `rgba(255, 255, 255, 0.6)`
  - `color-white-30`: `rgba(255, 255, 255, 0.3)`
  - `color-white-15`: `rgba(255, 255, 255, 0.15)`
  - `color-white-10`: `rgba(255, 255, 255, 0.1)`
  - `color-white-06`: `rgba(255, 255, 255, 0.06)`
- Black with opacity:
  - `color-black-90`: `rgba(0, 0, 0, 0.9)`
  - `color-black-60`: `rgba(0, 0, 0, 0.6)`
  - `color-black-30`: `rgba(0, 0, 0, 0.3)`
  - `color-black-15`: `rgba(0, 0, 0, 0.15)`
  - `color-black-10`: `rgba(0, 0, 0, 0.1)`
  - `color-black-06`: `rgba(0, 0, 0, 0.06)`

#### 3.1.4 Gradients

- `gradient-overlay-lime-sky`
  - type: `linear-gradient`
  - direction: `135deg`
  - stops:
    - color: `#C6FF2E`, position: `0%`
    - color: `#24E6FF`, position: `100%`
  - reference: `Gradient-LimeSky`
  - resolved: `linear-gradient(135deg, #C6FF2E 0%, #24E6FF 100%)`
- `gradient-overlay-lime-soft`
  - type: `linear-gradient`
  - direction: `135deg`
  - stops:
    - color: `#C6FF2E`, position: `0%`
    - color: `#E8FF9A`, position: `100%`
  - reference: `Gradient-Lime-Soft`
  - resolved: `linear-gradient(135deg, #C6FF2E 0%, #E8FF9A 100%)`
- `gradient-lime-light`
  - type: `composite`
  - layers:
    - type: `linear-gradient`
      - direction: `180deg`
      - stops:
        - color: `rgba(204, 255, 242, 0.10)`, position: `-0.35%`
        - color: `rgba(147, 255, 215, 0.10)`, position: `30.14%`
        - color: `rgba(82, 255, 73, 0.00)`, position: `100%`
    - type: `solid`
      - color:
        - reference: `color-white`
        - fallback: `#FFFFFF`
  - resolved: `linear-gradient(180deg, rgba(204,255,242,0.10) -0.35%, rgba(147,255,215,0.10) 30.14%, rgba(82,255,73,0.00) 100%), #FFFFFF`
  - key: `N/A`（复合渐变，Figma Variable 不支持 composite；请使用 Paint Style）

#### 3.1.5 Semantic Colors

- `color-success`
  - reference: `color-green`
  - resolved: `#22C55E`
- `color-warning`
  - reference: `color-orange`
  - resolved: `#F59E0B`
- `color-error`
  - reference: `color-red`
  - resolved: `#EF4444`
- `color-info`
  - reference: `color-sky`
  - resolved: `#38BDF8`
- `Background-Create`
  - reference: `gradient-lime-light`
  - resolved: `linear-gradient(180deg, rgba(204, 255, 242, 0.10) -0.35%, rgba(147, 255, 215, 0.10) 30.14%, rgba(82, 255, 73, 0.00) 100%), #FFFFFF`
  - intent: `card/chat background overlay`
  - key: `N/A`（语义别名，引用 style-based gradient）

> 说明：`gradient-lime-light` / `Background-Create` 属于复合渐变场景，需同时查看 Variables 与 Styles。Variables 不支持 composite value，故以 Style 为主。

---

### 3.2 Typography（字体排版 token）

#### 3.2.1 Font Families

- `rubik`
  - role: `brand font`
  - usage: `display, heading`
  - fallback: `-apple-system, system-ui, sans-serif`
- `inter`
  - role: `content font`
  - usage: `body, label`
  - fallback: `-apple-system, system-ui, sans-serif`

#### 3.2.2 Typography Styles

> 命名规范：统一使用 kebab-case，便于 AI 与代码系统稳定映射。

- `display-large`
  - category: `display`
  - font-family: `rubik`
  - font-size: `40px`
  - font-weight: `600`
  - line-height: `48px`
  - letter-spacing: `-0.4px`
- `heading-h1`
  - category: `heading`
  - font-family: `rubik`
  - font-size: `32px`
  - font-weight: `600`
  - line-height: `40px`
  - letter-spacing: `-0.32px`
- `heading-h2`
  - category: `heading`
  - font-family: `rubik`
  - font-size: `24px`
  - font-weight: `500`
  - line-height: `30px`
  - letter-spacing: `-0.24px`
- `heading-h3`
  - category: `heading`
  - font-family: `rubik`
  - font-size: `20px`
  - font-weight: `500`
  - line-height: `26px`
  - letter-spacing: `-0.2px`
- `heading-section`
  - category: `heading`
  - font-family: `rubik`
  - font-size: `16px`
  - font-weight: `500`
  - line-height: `22px`
  - letter-spacing: `-0.16px`
- `body-long-term`
  - category: `body`
  - font-family: `inter`
  - font-size: `17px`
  - font-weight: `400`
  - line-height: `26px`
- `body-large-strong`
  - category: `body`
  - font-family: `inter`
  - font-size: `16px`
  - font-weight: `600`
  - line-height: `24px`
- `body-large`
  - category: `body`
  - font-family: `inter`
  - font-size: `16px`
  - font-weight: `400`
  - line-height: `24px`
- `body-medium-strong`
  - category: `body`
  - font-family: `inter`
  - font-size: `14px`
  - font-weight: `600`
  - line-height: `20px`
- `body-medium`
  - category: `body`
  - font-family: `inter`
  - font-size: `14px`
  - font-weight: `400`
  - line-height: `18px`
- `body-small-strong`
  - category: `body`
  - font-family: `inter`
  - font-size: `13px`
  - font-weight: `600`
  - line-height: `18px`
- `body-small`
  - category: `body`
  - font-family: `inter`
  - font-size: `13px`
  - font-weight: `400`
  - line-height: `16px`
- `body-xsmall-strong`
  - category: `body`
  - font-family: `inter`
  - font-size: `12px`
  - font-weight: `600`
  - line-height: `16px`
- `body-xsmall`
  - category: `body`
  - font-family: `inter`
  - font-size: `12px`
  - font-weight: `400`
  - line-height: `16px`
- `label-small-strong`
  - category: `label`
  - font-family: `inter`
  - font-size: `11px`
  - font-weight: `600`
  - line-height: `14px`
- `label-small`
  - category: `label`
  - font-family: `inter`
  - font-size: `11px`
  - font-weight: `400`
  - line-height: `14px`

#### 3.2.3 与 Figma Variables 的映射说明

- 语义 style（本节）优先；底层变量（`Font / Size / Weight / Height`）作为实现层。
- 已通过 MCP 回填 Text Styles key；若后续新增样式，按同流程补齐。
- 当前版本先以规范定义为准，避免仅依赖历史 `label/*` 条目导致层级表达不足。

#### 3.2.4 Typography Key Mapping（MCP 回填）

> 数据来源：Figma `Text Styles` + `Variables`。  
> 说明：以语义命名（kebab-case）为主，`figma-style-name` 为文件内实际样式名。

- `display-large`
  - figma-style-name: `Display/Large`
  - key: `9cb3c4ae58e925661071d389e9e2cad06d6ea210`
- `heading-h1`
  - figma-style-name: `Heading/H1`
  - key: `565f1a4e0558ac6628025ca473b5ef1ec76b2156`
- `heading-h2`
  - figma-style-name: `Heading/H2`
  - key: `a381b89b32e7cc015406d7eeed71d177ceeee2e9`
- `heading-h3`
  - figma-style-name: `Heading/H3`
  - key: `768e7b0444a220ec6ba986c26e6669b04f08d162`
- `heading-section`
  - figma-style-name: `Heading/Section`
  - key: `60ffe95cca9fdfbccb7646898250d9ec53003253`
- `body-long-term`
  - figma-style-name: `Body/Long term`
  - key: `76170081623dfb7dcdc0c16d45b0dd373e46c16c`
- `body-large-strong`
  - figma-style-name: `Body/Large Strong`
  - key: `e9a807b422cf65944cf70dc42c658593c3c462d9`
- `body-large`
  - figma-style-name: `Body/Large`
  - key: `743847273bebdc7e2a4cf327846bf808c465046d`
- `body-medium-strong`
  - figma-style-name: `Body/Medium Strong`
  - key: `af38184d36819b83a2dd9e80e9ca853407198a59`
- `body-medium`
  - figma-style-name: `Body/Medium`
  - key: `ad4004151518974be0dc89d70160da84e4491fe6`
- `body-small-strong`
  - figma-style-name: `Body/Samll Strong`（Figma 原样拼写）
  - key: `690ae19efa3d38bd769630d4384df646e1b7ebe3`
- `body-small`
  - figma-style-name: `Body/Samll`（Figma 原样拼写）
  - key: `a11a2a2c4b37f976b377272259ad1e11138d328f`
- `body-xsmall-strong`
  - figma-style-name: `Body/XSamll Strong`（Figma 原样拼写）
  - key: `6901f71f1bca5672d7ddbebdca03ceb7d2b51396`
- `body-xsmall`
  - figma-style-name: `Body/XSamll`（Figma 原样拼写）
  - key: `cec03e983557590b2c84b8f5bbeec4177ae317ac`
- `label-small-strong`
  - figma-style-name: `Label/Small Strong`
  - key: `4a33957806f69195f638bc561e12d26a6f6903b0`
- `label-small`
  - figma-style-name: `Label/Small`
  - key: `0a61d5b146d51c84927ad92c83efff1c2fac0b32`

补充（Typography 相关 Variables）：
- `Slider Title`（STRING variable）key: `cf6786946523df2285dace22df502835b8fd6cc5`
- `Text`（STRING variable）key: `c5c978378e93a8da05e721d01effff78e7b4a746`

---

### 3.3 Spacing（间距 token）

> variableCollectionName = `Primitives`；variableType = FLOAT

- `spacing/0`
- `spacing/1`
- `spacing/2`
- `spacing/3`
- `spacing/4`
- `spacing/5`
- `spacing/6`
- `spacing/7`
- `spacing/8`
- `spacing/9`
- `spacing/10`
- `spacing/11`
- `spacing/14`
- `spacing/16`

> agent 在布局时：优先把组件间距、内边距映射到 `spacing/*`，避免自定义数值。

---

### 3.4 Radius（圆角 token）

> variableCollectionName = `Size`；variableType = FLOAT

- `Semantic/radius/large`（key: `0280edff41329212cd512e552270656e937d1b59`）
- `Semantic/radius/xlarge`（key: `feaf40546d288e9e21c37f67f824e8fe40081da0`）

---

### 3.5 Stroke（描边 token）

- `Semantic/stroke/stroke`（FLOAT；key: `4b07c275a670d5fb0ff155b6f67a86abc69cd4ad`）

---

## 4) 组件目录（Component Library Assets）

> agent 生成原型时，尽量从组件库直接复用 component/component_set，而不是用普通矩形+手写样式拼 UI。

### 4.1 导航/工具栏

- `Toolbar`（Catnips_Kit / component_set / componentKey: `8143a00dbdb68d51681f129533c18c36d60f4446`）
- `Navi item`（Catnip Design Kit / component_set / componentKey: `86354067e2d19f01dd4dd4f9341e0b39d44ccdbd`）

#### 4.1.1 Navigation Spec（Toolbar / Navi item）

- **组件定位**
  - 优先复用组件实例：`Toolbar`、`Navi item`，禁止重画导航结构。
- **结构规则（Structure）**
  - 顶部导航默认三段：leading / title(or logo) / trailing actions。
  - 底部导航默认使用重复的 `Navi item` 实例，保持相同宽度策略与对齐基线。
- **布局规则（Layout Rules）**
  - 导航区域优先保持组件原生高度与内边距；页面侧禁止手调单个 item 的 y 值。
  - 同一导航组内图标槽位必须对齐，未激活项也保留占位节奏。
- **视觉 token 规则（Visual Tokens）**
  - 导航背景/分隔/文字使用语义 token；禁止硬编码颜色。
  - 激活态与未激活态必须用组件内状态映射，不以透明度“伪状态”替代。
- **交互规则（Interaction Rules）**
  - 当前页对应 item 必须唯一激活；不可出现多激活。
  - 如需实验型导航样式，允许扩展，但必须标注“实验样式（待确认）”。
- **验收清单**
  - 组件是否全部来自 `Toolbar` / `Navi item`
  - 是否存在手写颜色/手写间距
  - 底部 item 是否等节奏对齐、仅一个激活项

### 4.2 交互控件

- `Button`（Catnips_Kit / component_set / componentKey: `7d77c45409899c6fc193ca8674725595d117c2fc`）
  - 使用约束：默认 `Shape=Capsule`；`Shape=Borderless (Transparent Bg)` 及后续新增样式可用于探索方案，但需明确标注为“待纳入规范”。
- `Toast`（Catnips_Kit / component / componentKey: `0e8667923a5c2e24b6eae362476ca6f94f14ec80`）
- `Switch`（Catnips_Kit / component_set / componentKey: `21eec2bf2c152427a1668e226ada10a691d4fc3d`）

#### 4.2.1 Button Component Spec（Agent 执行规范，目标 100% 还原）

> 本节是给 Agent 的“调用协议”，优先级高于通用经验。若与页面临时样式冲突，以本规范为准。

- **组件定位**
  - component set: `Button`
  - componentKey: `7d77c45409899c6fc193ca8674725595d117c2fc`
  - 必须使用组件实例，不允许用基础图形重画按钮。

- **允许的变体轴（白名单）**
  - `Shape`: 默认 `Capsule`（可扩展；非 Capsule 属于实验样式）
  - `Size`: `L | M | S | XS`
  - `Variant`: `Primary | Secondary`
  - `State`: `enabled | pressed | disabled`
  - `Loading`: `False | True`
  - 若请求或版式需要非 `Capsule`，可保留该形态并输出一版实验方案，同时记录差异点与纳管建议。

- **结构规则（Structure）**
  - 通过组件属性控制内容，不手动拆内部层：
    - `Has Label`（BOOLEAN）
    - `Label`（TEXT）
    - `Has Leading Icon`（BOOLEAN）
    - `Has Trailing Icon`（BOOLEAN）
  - 仅在业务明确要求时隐藏 label；默认 `Has Label=True`。
  - `Loading=True` 时，文案保持可读，不额外叠加自绘 loading 样式。

- **视觉 token 规则（Visual Tokens）**
  - `State=enabled`: 背景 -> `brand/primary`
  - `State=pressed`: 背景 -> `brand/pressed`
  - `State=disabled`: 背景 -> `brand/disabled`
  - Secondary: 背景遵循组件内已绑定语义 token（不可手写 HEX）
  - 主按钮前景文本优先使用组件内已绑定对比色 token（不可手写 HEX）
  - 任何状态都禁止直接写 `#xxxxxx` 或裸 `rgba(...)`（除 DS 明确允许的派生色）。

- **排版规则（Typography）**
  - `Size = L | M` -> `body-large-strong`（`Body/Large Strong`）
  - `Size = S | XS` -> `body-medium-strong`（`Body/Medium Strong`）
  - 文本必须绑定 text style，不接受“仅设置 fontSize/fontWeight 不绑定样式”。
  - 行高单位统一使用 px（避免百分比行高引起还原偏差）。

- **布局规则（Layout Rules）**
  - 使用实例默认 Auto Layout，不手动改内部 padding/gap。
  - 同一按钮组内高度与文本样式必须一致；不同尺寸仅通过 `Size` 变体切换。
  - 不允许通过拉伸文本层或手动移动 icon 修正布局。

- **交互与状态规则（Interaction Rules）**
  - `State=disabled` 必须语义禁用，不得仅做视觉变淡但仍保留可交互语义。
  - `Loading=True` 与 `State` 组合时，保持组件原生状态逻辑，不新增自定义点击反馈。

- **实例化调用顺序（Agent 操作顺序）**
  1. 先实例化 `Button` 组件（按 componentKey）。
  2. 设置变体轴（默认先 `Shape=Capsule`，再 `Size/Variant/State/Loading`；如需实验样式，可替换 Shape 并标注）。
  3. 再设置内容属性（`Label`、前后图标开关）。
  4. 最后做校验（见下方验收清单），不通过则回退并重试一次。

- **验收清单（生成后必须检查）**
  - 是否遵循“默认 Capsule，实验样式需标注”的规则
  - 是否存在手写颜色（若有则失败）
  - 是否绑定了正确 text style（L/M 与 S/XS）
  - Disabled 是否误用 Pressed token
  - 同组按钮是否出现 15px 等异常字号

- **失败回退策略**
  - 任何 token/style 缺失时，优先回退到组件内已绑定变量；
  - 若仍冲突，优先保证语义正确（state/token）再保证视觉微调；
  - 若采用非 Capsule，必须在生成日志中标注“实验样式 + 使用场景 + 是否建议纳入 DS”。

#### 4.2.2 Toast Component Spec

- **组件定位**
  - 复用 `Toast` 组件（componentKey: `0e8667923a5c2e24b6eae362476ca6f94f14ec80`）。
- **结构规则（Structure）**
  - 默认结构：反馈图标 + 文案（可选操作）。
  - 不允许拆开后自行拼接阴影/圆角/背景。
- **视觉 token 规则（Visual Tokens）**
  - 成功/警告/错误/信息分别映射 `semantic/feedback/*`。
  - 文本层级遵循 `body-*` / `label-*`，禁止临时字号。
- **交互规则（Interaction Rules）**
  - Toast 用于短时反馈，不承担主要 CTA；若页面长期驻留，改用卡片或 inline message。
- **验收清单**
  - 是否按 feedback 语义选色
  - 是否复用组件实例而非自绘
  - 文案层级是否落在 typography 规范内

#### 4.2.3 Switch Component Spec

- **组件定位**
  - 复用 `Switch` component set（componentKey: `21eec2bf2c152427a1668e226ada10a691d4fc3d`）。
- **结构规则（Structure）**
  - Switch 与 label 允许分离布局，但交互语义必须绑定同一控制目标。
- **状态规则（State Mapping）**
  - 至少区分 `On/Off` 与 `enabled/disabled`；禁止只改颜色不改状态属性。
- **视觉 token 规则（Visual Tokens）**
  - 开关轨道、thumb、禁用态使用语义 token，不手写颜色。
- **验收清单**
  - 状态是否完整（On/Off + enabled/disabled）
  - 点击区域是否可达（不小于组件原生命中区）
  - 是否存在手写状态色

### 4.3 内容载体（卡片）

- `template card`（Catnip Design Kit / component_set / componentKey: `ab99ab6e1a2fe97767cd1979ad7df245e21a451e`）
- `Stacked card`（Catnip Design Kit / component_set / componentKey: `b231cc5a5d7cfc72b11ea6e6cfa7d99aacd99692`；用于展示内容与可执行信息）
- `Horizontal card`（Catnip Design Kit / component_set / componentKey: `4e3b19040fd02ab2d3377d7b3d1c8c3b77d05bec`；用于网格/列表/轮播展示）
- `Icon/Closed_Caption`（Catnips_Kit / component / componentKey: `c3a106dc66a76623306e4726a60f5157249b46b9`）
- `Icon/Video_Fill`（Catnips_Kit / component / componentKey: `3c19871146d03d008ea54b9dd8d0af15ff04f75b`）

#### 4.3.1 Card Family Spec（template / stacked / horizontal）

- **组件选择策略**
  - 信息密度低且强调视觉：优先 `Horizontal card`
  - 多层内容与操作并存：优先 `Stacked card`
  - 通用内容容器：`template card`
- **结构规则（Structure）**
  - 卡片结构优先保持“媒体区 / 信息区 / 行动区”三段式，不跨段放置元素。
  - 视频/字幕能力优先用 `Icon/Video_Fill` 与 `Icon/Closed_Caption`，不自绘图标。
- **布局规则（Layout Rules）**
  - 卡片列表保持统一宽度与对齐轨道；混排时仅允许高度差，不允许左右轨道漂移。
- **视觉 token 规则（Visual Tokens）**
  - 卡片背景、边框、标题/描述文本都走语义 token，不手写色值。
  - 需要特殊背景时优先 `Background-Create` 等已定义语义背景。
- **验收清单**
  - 卡片类型是否匹配内容密度
  - 列表轨道是否对齐
  - 媒体/字幕图标是否来自组件库

### 4.4 图标/品牌

- `Logo_Name`（Catnips_Kit / component / componentKey: `797e3590a89eb8fc81d7ed681c8a74e70390ab3d`）
- `Icon/Profile_Fill`（Catnips_Kit / component / componentKey: `3fa76efb2af0432d580dea97f30eb6f5e9720b5b`）
- `Icon/Camera_Filter`（Catnips_Kit / component / componentKey: `7949838ce909926039f1d91d991789505f8d3f22`）
- `Icon/Camera_Filter_Fill`（Catnips_Kit / component / componentKey: `f1d05b9d76382183b160daab62e51c760abab632`；description: `CameraFilter - Fill`）

#### 4.4.1 Icon & Brand Spec

- **组件定位**
  - Logo 与品牌图标必须使用库组件，不允许重绘或近似替代。
  - 在代码项目中，优先使用 `/assets/icons/raw` 内的 SVG；这些 SVG 已统一为 `currentColor`，可通过 token-backed `color` 控制。
  - 常规代码场景可使用 `/styles/icons.css` 中的 `.catnip-icon`、`.catnip-icon--small`、`.catnip-icon--large`、`.catnip-icon--secondary`、`.catnip-icon--inverse`、`.catnip-icon--brand`。
- **尺寸与对齐规则**
  - 同一行图标使用统一尺寸档位；若有主次层级，仅允许一档差异。
  - 图标与文字基线对齐优先于视觉居中。
  - 在代码里，图标尺寸只能来自 `--size-*` 或组件自身尺寸 token。
- **视觉 token 规则**
  - 图标颜色优先继承语义文本/前景 token；fill 版与线框版不可混用造成语义歧义。
  - 不要在 SVG 或 CSS 中写死 `fill`、`stroke`、HEX、RGB/RGBA 或裸尺寸。
  - 品牌/social logo 只在真实引用对应平台或品牌时使用。
- **验收清单**
  - 是否全部为库图标实例
  - 是否出现混合风格（fill/outline 无规则混搭）
  - 与相邻文字的基线是否一致
  - 代码实现是否通过 token 控制颜色和尺寸

### 4.5 状态/占位

- `Empty States`（Catnips_Kit / component / componentKey: `18278d151765a05dc0bc10c102bc51f725c3d886`）
  - 关键描述：切换明暗模式通过 Design panel 的 `apply variable mode`（Appearance -> System Colors 子菜单）。

#### 4.5.1 Empty State Spec

- **使用场景**
  - 无内容、无搜索结果、权限受限、离线异常等“无数据/阻断”场景优先使用 Empty State。
- **结构规则**
  - 默认结构：插图/图标 + 标题 + 描述 + 可选行动按钮。
  - 避免在 Empty State 内堆叠过多二级操作。
- **主题规则**
  - 明暗模式切换必须走 `apply variable mode`，不允许复制两套手写配色。
- **文案规则**
  - 标题简短、描述可执行，CTA 明确下一步动作。
- **验收清单**
  - 是否正确区分“空态”与“错误态”
  - 主题切换后可读性是否稳定
  - CTA 是否与页面主任务一致

---

## 5) 给 Agent 的“生成原型”流程（落地版）

1. 先拆页面模块：通常包括 `Toolbar`（顶部）、内容区（卡片：`template card/stacked/horizontal`）、关键 CTA（`Button`）、反馈层（`Toast`）、空状态（`Empty States`）。
2. 再做 token 选择：颜色用 `Semantic/*`，按钮状态用 `Semantic/button/*`，文字优先用 `Typography Styles`（display/heading/body/label），间距用 `Primitives/spacing/*`，圆角用 `Semantic/radius/*`。
3. 深浅色：在使用明暗主题时，确保相关组件与颜色都能随变量模式正确切换（遵循 `Empty States` 的变量模式提示）。
4. 完成后回读：如果出现任何“手写颜色/手写字号/手写间距”，就回退到语义 token/排版 token/spacing token 里替换。

### 5.1 Codex 代码生成验收清单

- 是否读取了 `AGENTS.md` 与本文件。
- 是否引用 `/styles/tokens.css`，必要时引用 `/styles/icons.css`。
- 是否使用 `/tokens/tokens.optimized.json` 或 CSS variables 作为视觉来源。
- 是否避免了硬编码颜色、字号、圆角、间距、阴影、描边和 icon 样式。
- 是否优先使用 `/assets/icons/raw` 中的 Catnip icon，而不是文字 glyph 或其他 icon set。
- UI 是否符合 clean、light、playful、social、content-first、polished 的产品气质。
