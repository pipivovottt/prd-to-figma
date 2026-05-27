# FinEAM 设计参考 · 组件速查 & 界面拼装指南

## 前提：必须先读取 figma-use skill

- **组件库文件 key**: `QxrzU4jigzG5OO4SsxPwJT`
- **导入方式**: `figma.importComponentSetByKeyAsync(componentKey)`
- 需在目标文件的 `use_figma` 中指定目标文件的 `fileKey`，组件通过 key 从远程库导入

---

## 标准页面框架（1920×1080）

```
├── menu 侧导航 (220×1080)           key: 1abf8ebcf49cd91f8e74461a253628e616cd6a56
├── 右侧主区域 (1700×1080)
│   ├── navbar顶部栏 (1700×48)       key: c1cffc6bb543d17d9bc49a6649b49430b334ae99
│   └── 内容区 (1700×1032)
│       ├── 筛选区（filter/select/search-box/datepicker）
│       ├── 表格（table-header + table-cell 行）
│       └── pagination 分页
```

### 变体选择规则

**menu 侧导航** - 推荐变体: `theme=light, 收起=false, 端=机构端`

**navbar顶部栏** - 变体: `类型=带可关闭页签` 或 `类型=客户端`

**Button** - 常用变体:
- 主操作: `尺寸=中, 类型=主要按钮, 种类=标准, 形状=长方形, 状态=默认`
- 次操作: `尺寸=中, 类型=线框按钮, 种类=标准, 形状=长方形, 状态=默认`
- 文字链: `尺寸=中, 类型=文本按钮, 种类=标准, 形状=长方形, 状态=默认`

---

## 核心组件 Key 速查

### 导航布局
| 组件 | Key | 常用变体关键词 |
|------|-----|--------------|
| menu 侧导航 | `1abf8ebcf49cd91f8e74461a253628e616cd6a56` | `收起=false, 端=机构端` |
| navbar顶部栏 | `c1cffc6bb543d17d9bc49a6649b49430b334ae99` | `类型=带可关闭页签` |
| Divider | `eed0e99a3ba6d7f85eb9ce516df33c6b35880fd2` | `类型=水平` |
| pagination | `09f7ba0670903ca49ad1ed4b62cbe5a67ac1f20a` | — |

### 数据录入
| 组件 | Key | 常用变体关键词 |
|------|-----|--------------|
| Button | `24f1fca39d63a16ba2b29c06df1fbd972cbe048e` | `类型=主要按钮/线框按钮/文本按钮` |
| input | `35c8d59aac43079db9c996c7ecb6ec1098f82e9f` | `大小=中` |
| search-box | `f7c74d79c13cfbf9555a5d8fa4b2b6e19a3e1dd3` | — |
| select | `39548a13367e6b8cb157b27828c1bf5964aad923` | — |
| filter | `8c5f30c5b638c769d89f8748e9f4dcfd0653e9b6` | `Type=Select` |
| datepicker | `21cc87a22ac5609e66737bfddad801c11747ce5c` | — |
| checkbox | `3c82df835f4cad2c7da741d65112a02731d24108` | — |
| radio | `9b767a208fc9a5fcd8c9eb8f5ffb872993c57187` | — |
| form-item | `d737d51062365d5dfc9b2ce01d0961c7d585e196` | — |

### 表格组件（核心）
| 组件 | Key | 变体说明 |
|------|-----|---------|
| table（完整表格） | `6a7a3d2480309a03055470927ccd27cc535ecb18` | `边框=false/true` |
| 表头/header | `6ae2445ce3bef3c2a72c914fd610f5f3ba1a9f6d` | `类型=文本, 对齐=左对齐, 状态=默认/简约` |
| 单元格/text | `09dc603f3e4f43b6383464fd362b1dbdbcb3ec83` | `状态=默认, 对齐=左对齐` |
| 单元格/text(双行) | `43e56bb666666f620939d2a79b4a708940b04471` | `状态=默认, 对齐=左对齐` |
| 单元格/action | `2bbd9d0aaef196cc9f41c4e78d7df01f18500934` | `状态=默认, 数量=1/2/3`。**操作列默认右对齐**，对应表头也须选 `对齐=右对齐` 变体 |
| 单元格/tag | `b23b93f34464f40519af60b5fba3e0b3ce8e9b1e` | `状态=默认` |
| 单元格/link | `9afe9bbf82663d7ec790402309d703596b6c1a2a` | `状态=默认` |
| 单元格/checkbox | `cbae108e49a29513354f9ba91ad0058220e39b10` | `状态=默认, 选中=false` |
| 单元格/percent | `4de0794f7452b25581fa643b2bc74453725a4a16` | `状态=默认`。**用途：可视化进度条（如完成率、占比）。⚠️ 不适用于涨跌幅，涨跌幅请用 单元格/text** |
| 单元格/status | `9c798459215d9ddbcd78b4c6826addd17afbbf54` (列) | `对齐=左, 固定=false` |
| sorter | `34a9900f46f2d84451a016b2a09d925df66631e5` | `排序=默认/升序/降序` |

### 选项卡
| 组件 | Key | 说明 |
|------|-----|------|
| tabs/line（整体） | `af171e7a34bff7513db9b4bce9463920b858319e` | 线型选项卡容器 |
| tabs/capsule（整体） | `c5ddc18b862e11ccca6b454c18c20260a80c7160` | 胶囊型选项卡 |
| components/tab（单个） | `852fa19200f2921c97edcbe5db711b993abcaac6` | 单独 tab 项 |

### 数据展示 & 反馈
| 组件 | Key | 常用变体 |
|------|-----|---------|
| 标签样式3 (Tag) | `79b43a158cf93f4a96f54ce9aa66757d907fdfb8` | `类型=蓝色/红色/绿色/灰色/金色, 大小=迷你/小` |
| badge/count | `b20e605252856854e275930f1cb0c9019d910b9d` | — |
| Avatar | `666a7d6e2aab8ade9d48ef61dabc259fe195d4ff` | `尺寸=中` |
| Alert | `951c170ef31eda9abfce762a262e390a420fab81` | `类型=info/success/warning/error` |
| Empty（空状态） | `98ce9fb8f683e3f831cae39dbb78a8b1d690e46d` | — |
| modal | `145da8f90da323737220837c77bcd7354fe126f8` | — |
| progress-line | `910a404b5d0bdb7fbb4e09f8665f35fa459e26f1` | — |

### 页面模板
| 模板 | Key |
|------|-----|
| 列表页模版 | `30a28f84362550a08b321b0fa76db155cad34e29` |
| 表单页模版 | `21038a2ced299f87d43177ce6ed9e88ecf6ca70c` |

---

## 搭建页面的工作流

### 0. 页面模版识别（最优先步骤）

在导入任何原子组件之前，**先判断自然语言描述是否命中以下场景**：

| 描述中出现的关键词 | 应使用的模版 | 组件 Key |
|-----------------|------------|---------|
| page_template/列表页模版 | 列表页模版 | `30a28f84362550a08b321b0fa76db155cad34e29` |
| page_template/表单页模版 | 表单页模版 | `21038a2ced299f87d43177ce6ed9e88ecf6ca70c` |

命中模版时，按以下流程操作：

```javascript
// ① 导入模版组件（单一组件，非 ComponentSet）
const templateComp = await figma.importComponentByKeyAsync(
  '30a28f84362550a08b321b0fa76db155cad34e29' // 列表页模版
  // 或 '21038a2ced299f87d43177ce6ed9e88ecf6ca70c' 表单页模版
);

// ② 创建实例并放入页面
const templateInst = templateComp.createInstance();
templateInst.x = 0;
templateInst.y = 0;
figma.currentPage.appendChild(templateInst);

// ③ 解绑（模版类组件允许解绑，见注意事项 7）
const pageFrame = templateInst.detachInstance();

// ④ 找到内容区（两个模版中该 Frame 均命名为「内容区」）
const contentArea = pageFrame.findOne(n => n.name === '内容区');

// ⑤ 清空内容区，准备填入实际业务组件
[...contentArea.children].forEach(c => c.remove());
// 后续步骤：向 contentArea 添加 PageHeader、筛选区、表格/表单、分页等
```

**使用模版后的注意事项**：
- 模版解绑后已包含 `menu 侧导航` 和 `navbar顶部栏` 的完整骨架，**不再单独导入这两个组件**
- 只需操作内容区，导航栏 / 侧边栏保持不动
- 若描述中没有明确命中上表关键词，退回到原有逐组件拼装方式

---

### 1. 在目标文件中获取页面信息
```javascript
// 找到目标页面
for (const page of figma.root.children) {
  await figma.setCurrentPageAsync(page);
  const found = await figma.getNodeByIdAsync('PAGE_OR_FRAME_ID');
  if (found) { /* 找到正确页面 */ break; }
}
```

### 2. 导入并使用 FinEAM 组件
```javascript
// 导入组件集（从 FinEAM 远程库）
const menuCS = await figma.importComponentSetByKeyAsync('1abf8ebcf49cd91f8e74461a253628e616cd6a56');
const variant = menuCS.children.find(c => 
  c.name.includes('收起=false') && c.name.includes('机构端')
) || menuCS.defaultVariant;
const inst = variant.createInstance();
parentFrame.appendChild(inst);
inst.x = 0; inst.y = 0;
inst.resize(220, 1080);
```

### 3. 标准列宽参考（1652px 表格总宽）
- 名称列（主列）: 350–480px
- 数据列: 160–220px
- 操作列: 200–350px（按按钮数量调整）

### 4. 优先使用已有组件
若找不到完全匹配的组件，优先选择同类型中最接近的变体，不要手动绘制。

---

### 5. 数字文本 Number 字体强制替换（不可省略）

> 此规则来自 `text-style-ref.md` 全局强制规则，适用于 FinEAM 内**所有页面、所有场景**中显示数字的文字节点，不限于表格。

**时机**：向任意数字类文字节点写入内容（`text.set_content`）后，必须立即按 `text-style-ref.md` 流程 1b 执行 `text.update`。样式 Key 见 `text-style-ref.md` Web 端组件库表格。

**FinEAM 中常见的数字节点场景（示例，非穷举）**：

| 页面 / 区域 | 数字内容示例 | 典型节点位置 |
|------------|------------|------------|
| 列表页 - 表格 | `+21.73%`、`144.62`、`2024/03/15` | 涨跌幅列、净值列（主/副行）、日期列 |
| 列表页 - 表格 | `¥1,234.56`、`1/6` | 金额列、计数列 |
| 详情页 - 概览卡片 | `1.5823`、`+3.25%` | 净值、涨幅数字节点 |
| 详情页 - 收益图 / 数据行 | `¥12,000.00`、`+¥580.00` | 收益金额节点 |
| 任意页面 - 统计指标 | `88%`、`NO.001` | 百分比、编号文字节点 |

**标准执行序列**：

```
① Vibma text.set_content: 写入文字内容
② 按 text-style-ref.md 流程 1b：importStyleByKeyAsync → 获取 styleId
③ Vibma text.update: 对所有数字文字节点批量应用 textStyleId
```

步骤 ①②③ 必须在同一轮工作流中连续完成，不允许只做 ① 而跳过 ②③。

---

## 注意事项

1. **组件字体处理规范** - 该库使用 PingFang SC，插件无法加载
   - **禁止直接修改**：不要修改组件内文本的 `fontName` 属性
   - **禁止解绑修改**：不要通过 `detachInstance()` 解绑后修改字体
   - **正确做法**：参见 `text-style-ref.md` 组件文本流程（流程 1）
2. **表格组件两套命名**: 
   - `/table-header 表头/` + `/table-cell 单元格/` — 逐行拼装
   - `/table-column 表格列/` — 按列拼装
   - `table`（key: `6a7a3d2480309a03055470927ccd27cc535ecb18`）— 完整表格组件
3. **变体选择**: 使用 `cs.children.find(c => c.name.includes('关键词'))` 匹配变体
4. **Tag 颜色语义规范**（`标签样式3` 和 `单元格/tag` 均适用）：
   根据标签所表达的语义选择合适颜色变体，不可随意使用：
   - **灰色**（`颜色=灰色`）：**不表示状态或程度的中性分类标签**（如：基金类型、资产类别、一般属性标签）；以及禁用/次要/已结束状态（如：已到期、暂停、不可操作）
   - **蓝色**（`颜色=蓝色`）：带有程度/状态含义的中性信息（如：中风险、进行中、待审核）
   - **绿色**（`颜色=绿色`）：正向/低风险/成功状态（如：低风险、可申购、已完成）
   - **红色**（`颜色=红色`）：高风险/错误/紧急（如：高风险、暂停赎回、异常状态）
   - **黄色**（`颜色=黄色`）：中等警告/提醒/待确认（如：中高风险、待处理、受限）

   **判断用灰还是蓝的核心原则**：标签本身是否暗示某种程度高低或状态好坏？
   - 暗示程度/状态 → 用对应语义色（蓝/绿/红/黄）
   - 纯粹分类，无程度含义 → 用灰色

   **Tag 颜色变体切换操作规范**（通过 `use_figma`）：
   - `单元格/tag` 外层实例只有 `状态=默认/Hover` 变体，**颜色由内层嵌套的 `tags-wrapper` 实例控制**
   - 切换颜色需对内层 `tags-wrapper` 调用 `swapComponent(targetVariant)`，其中 `targetVariant` 需满足 `颜色=目标色, 大小=迷你, 状态=默认`
   - ⚠️ **`swapComponent` 会清空部分覆写**：若新旧变体的文本节点名称不同，文案覆写无法自动保留。操作后必须立即重新写入文案，避免回退为组件默认值
   - **文案写入方式**：参见 `text-style-ref.md` 组件文本流程（流程 1）
   - ⚠️ **不同颜色变体的文本节点 ID 尾部不同**（如 `372:4075`、`372:3883`、`372:4395` 等），不能直接套用固定规律。需先用 Vibma `node.get_children` 或 `use_figma` 查找文本节点，获取正确的 nodeId
   - **颜色变体（swapComponent）和文案写入必须同步操作**，顺序：先 swapComponent 设色，再用 Vibma 写文案

5. **涨跌幅颜色规范**（中国金融惯例：涨红跌绿）：
   - 涨幅（正值）文字色：使用颜色变量 `red/red-6`
     - Library variable key: `fbfaca0d287efb5875766068c990dcc8d7ce5371`
   - 跌幅（负值）文字色：使用颜色变量 `green/green-6`
     - Library variable key: `bb933f053644a9b3bfc483c00edd10bfa17ee149`
   - **绑定方式**：先确认目标文件已开启 FinEAM 变量库，然后通过 `use_figma` 执行：
     ```javascript
     const redVar = await figma.variables.importVariableByKeyAsync('fbfaca0d287efb5875766068c990dcc8d7ce5371');
     const greenVar = await figma.variables.importVariableByKeyAsync('bb933f053644a9b3bfc483c00edd10bfa17ee149');
     // 绑定到文字节点 fills
     node.fills = [{type:'SOLID', color:{r:0.96,g:0.133,b:0.176}, boundVariables:{color:{type:'VARIABLE_ALIAS',id:redVar.id}}}];
     ```
   - Vibma 的 `fontColorVariableName` / `bindings[].variableId` **不支持远程库变量**，必须用 `use_figma` + `importVariableByKeyAsync`
   - **不要使用 `单元格/percent` 展示涨跌幅**，使用 `单元格/text` 并手动绑定对应颜色变量

6. **数值文本样式规范（Number 样式）**：参见 `text-style-ref.md` 数字字体使用规范。

7. **组件解绑规范**：
   不要随意解绑（detach）组件实例，解绑后将失去与主组件的关联，无法跟随组件库更新同步。
   - **允许解绑**：页面模版（`列表页模版`、`表单页模版` 等）、弹窗（`modal`）——这类组件本身就是搭建骨架用的，解绑后再定制是预期用法
   - **禁止随意解绑**：筛选器（`filter`）、按钮（`Button`）、表格单元格（`单元格/*`）、表头（`表头/*`）、输入框（`input`/`search-box`）等原子/分子级组件，应保持实例状态，通过切换变体或覆写属性（Override）来满足需求
   - **修改组件文字**：始终通过文本操作（参见 `text-style-ref.md`），不要解绑后修改
   - **解绑后重建内部容器帧规范**：清空 `body` / `内容区` 等容器帧并切换其 `layoutMode` 时，**不得自行追加 `paddingTop` / `paddingBottom`**。原组件的内容容器帧纵向 padding 设计为 0，上下间距由外层 frame 的 `itemSpacing` 控制。若不确定原始值，先读取再决定：`console.log(body.paddingTop, body.paddingBottom)`；如需保留，显式写出；如需归零，显式 `body.paddingTop = 0; body.paddingBottom = 0`。**禁止凭经验估值。**

8. **本地组件母版必须填充示例数据**：
   创建 `headerRow` 和 `dataRow` 本地组件后，**必须立即向母组件本体填充真实可读的示例数据**，而不是保留占位符（如「单元格」「说明」「状态」「Title」「操作」等默认文案）。
   - **headerRow**：所有表头文字必须替换为实际列名（如「产品名称/ISIN」「近一月」「操作」等）
   - **dataRow**：所有单元格必须填入一条有代表性的真实样例数据（名称、数值、日期、货币、按钮文案等），tag 类单元格需同时完成颜色 swap 和文案写入
   - **原因**：母组件是设计师调整列宽和布局的直接对象。若保留占位符，设计师无法判断实际内容宽度，易造成列宽设置不合理；且母组件的数据会作为默认值影响后续创建的所有实例的显示效果

   **操作规范**：填充完母组件结构后，立即用 `text-style-ref.md` 流程 1（`text.set_content`）写入所有文本。tag 单元格须先通过 `use_figma` 执行 `swapComponent` 设色（参见注意事项 4），再写文案。

9. **页面模版使用限制与退回策略**：
   - 页面模版适用于「整页」场景；若自然语言描述的是**弹窗内的局部布局**（如抽屉、Modal 内的表单），不应套用模版，直接使用原子组件拼装
   - 内容区 `findOne` 失败时（返回 `null`），说明节点名称与预期不符——此时打印 `pageFrame.children` 重新确认，不要盲目删除 `pageFrame` 本体
   - 同一页面只能套用**一个**模版；若描述同时含有列表和表单（如「列表页 + 侧边新增面板」），以主体内容决定模版类型，次要内容用 `modal` 或独立 Frame 处理

10. **重复元素封装为本地组件**：
   当页面中某个组合结构需要重复出现多次，应先用原子组件或基础元素将其构建为**本地组件（Local Component）**，再通过实例化引用。
   - 使用 `use_figma` 中 `figma.createComponent()` 创建本地组件
   - 后续复用时调用 `localComponent.createInstance()` 实例化
   - 优点：修改主组件后所有实例同步更新，维护成本低

   **典型适用场景**（以下必须封装为本地组件）：
   - **表格数据行**：由多个 `单元格/*` 实例横向排列组成，一个页面有多行，结构一致 → 先构建一个 `dataRow` 本地组件，再实例化 N 次
   - **表头行**：由多个 `表头/header` 实例横向排列组成，应封装为 `headerRow` 本地组件后，在 tableSlot 中实例化引用（即使只出现一次，也方便后续调整列宽）
   - **卡片列表项**：由图片、标题、描述、操作等组合而成，列表中每项结构相同
   - **自定义状态标记、特殊信息卡片、组合图标文本**等在页面中重复出现的自定义组合

   **工作流**：
   ```javascript
   // 1. 先构建单行结构，挂到页面根节点临时放置
   const rowComp = figma.createComponent();
   rowComp.name = 'dataRow';
   rowComp.layoutMode = 'HORIZONTAL';
   rowComp.primaryAxisSizingMode = 'AUTO'; // 宽度跟随内容，不要 resize 为固定值
   figma.currentPage.appendChild(rowComp);
   // ... 向 rowComp 内添加各列单元格实例 ...
   // 2. 实例化 N 次放入表格容器
   for (let i = 0; i < 8; i++) {
     const inst = rowComp.createInstance();
     tableSlot.appendChild(inst);
   }
   ```

   **本地组件放置规范**：
   - `headerRow` 和 `dataRow` 两个本地组件应**并列放置在生成页面下方**，上下对齐（相同 x 坐标），纵向紧邻（4px 间隔）
   - 这样设计师可以在同一视图内同时看到两行，方便对齐调整每列的宽度
   - 定位参考：`comp.x = pageFrame.x; comp.y = pageFrame.y + pageFrame.height + 80;`
   - headerRow 在上，dataRow 在下，两者 x 对齐，内部各列宽度对应保持一致（使用 `primaryAxisSizingMode = 'AUTO'` 避免手动 resize 引起宽度不匹配）

11. **组件宽度设置规范**：
   大多数 FinEAM 原子/分子组件（`filter`、`search-box`、`Button`、`input`、`datepicker` 等）**不需要手动 resize 宽度**，直接保持组件默认的 AUTO/HUG 自适应行为即可。若实例化后被意外 resize 为 FIXED，应通过 `use_figma` 恢复：
   ```javascript
   inst.layoutSizingHorizontal = 'HUG'; // 恢复自适应
   ```

   **例外情况——表头行与表格数据行**：
   列表页表格需要铺满容器宽度，因此 `headerRow` 和 `dataRow` 中每个单元格必须手动给定合适的固定宽度：
   - 宽度依据各列展示内容决定（长文本给宽、短数据给窄）
   - 所有列宽之和应等于可用宽度（页面宽度减去左右内边距）
   - 若表格字段较少、列数不多，可将某些列设为 **Fill 容器**（`layoutSizingHorizontal = 'FILL'`）并设置最小宽度（`minWidth`），避免出现大量空白：
     ```javascript
     cell.layoutSizingHorizontal = 'FILL';
     cell.minWidth = 160;
     ```
   - `表头/header` 和 `单元格/*` 对应列的宽度必须保持一致，headerRow 和 dataRow 组件中同列宽度要匹配

12. **表格行单元格高度对齐规范**：
   表格中若存在不同高度的单元格（如双行单元格 `单元格/text(双行)` 与单行单元格混排），必须确保同一行内所有单元格高度一致，否则会出现错位。
   - **正确做法**：将 `dataRow`（和 `headerRow`）组件的 `counterAxisAlignItems` 设为 `'MIN'`，并将每个单元格实例的 `layoutSizingVertical` 设为 `'FILL'`：
     ```javascript
     dataRowComp.counterAxisAlignItems = 'MIN';
     for (const cell of dataRowComp.children) {
       cell.layoutSizingVertical = 'FILL';
     }
     ```
   - ⚠️ `counterAxisAlignItems` 不支持 `'STRETCH'`，应使用 `'MIN'` + 子节点 `'FILL'` 的组合实现等高效果
   - ⚠️ `layoutSizingVertical = 'FILL'` 必须在节点**已加入父容器后**才能设置，否则报错
   - 行高由最高的子单元格决定（`counterAxisSizingMode = 'AUTO'`）；单行单元格内容默认顶部对齐，若需垂直居中需另行调整组件内部设置

13. **自动布局与忽略自动布局规范**：
   页面中的大多数元素应置于自动布局容器内，利用 Auto Layout 管理间距和对齐。
   只有**需要浮层覆盖**在其他内容上方或下方的元素，才需将其设为「忽略自动布局」（`isAbsolute = true` / `layoutPositioning = "ABSOLUTE"`），例如：
   - 图表或卡片上角的数量徽章（Badge/Count）
   - 头像右下角的在线状态指示点
   - 固定定位的悬浮按钮、工具提示
   - 表格行 hover 时浮出的操作按钮组
   普通内容元素一律参与自动布局，不要随意设置绝对定位。

