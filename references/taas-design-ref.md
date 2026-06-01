# TaaS 设计参考 · 组件速查 & 界面拼装指南

## 前提：必须先读取 figma-use skill

- **组件库文件 key**: `JknFO7OVAVAnWrkCjAFZg1`
- **导入方式**: `figma.importComponentSetByKeyAsync(componentKey)`
- 需在目标文件的 `use_figma` 中指定目标文件的 `fileKey`，组件通过 key 从远程库导入


---

## 标准页面框架（1920×1080）

```
├── 背景模版 (1920×1089)                    key: c59be673cf4ff3d0f9cac06871eea743ee9f7020，绝对定位，居于最底部的装饰性图层
├── menu 侧导航 (240×1080)                  key: 341b06ec38f2f5f3232223b32be1491cb6a2fba8，位于 left:0 top:0，支持一级/二级导航，激活项高亮
└── 右侧主区域 (1664c1064)                    left:244px, top:12px
    │                                        rounded-24px, backdrop-blur-50px
    │                                        bg: --bgContentColor (#0c121a)
    ├── 内嵌页头 / 页面标题栏                    key: 5341a1ae64ff64bca45fab89ef38f4808be1575c
    └── 内容区 (1664×1004)
        ├── 筛选区（filter/select/search-box/datepicker）
        ├── 表格（table-header + table-cell 行）
        └── pagination 分页

```

### 变体选择规则

**menu 侧导航** - 推荐变体: `theme=dark, 收起=false, 机构类型=代币管理人`

**页头** - 变体: `数量=1`

**Button** - 常用变体:
- 主操作: `尺寸=中, 类型=主要按钮, 种类=标准, 形状=长方形, 状态=默认`
- 次操作: `尺寸=中, 类型=次要按钮, 种类=标准, 形状=长方形, 状态=默认`
- 文字链: `尺寸=中, 类型=文本按钮, 种类=标准, 形状=长方形, 状态=默认`

---

## 核心组件 Key 速查

### 导航布局

| 组件 | Key | 常用变体关键词 |
|------|-----|--------------|
| menu 侧导航 | `341b06ec38f2f5f3232223b32be1491cb6a2fba8` | `theme=dark, 收起=false, 机构类型=代币管理人` |
| 页头 | `5341a1ae64ff64bca45fab89ef38f4808be1575c` |`数量=1` |
| Pagination 分页 | `de57beea65e79b76cb0ab92dd1c088ffeb39766a` | — |


### 数据录入

| 组件 | Key | 常用变体关键词 |
|------|-----|--------------|
| Button | `f91285c461399a795539966a35546fc98cbd92e0` | `类型=主要按钮/次要按钮/文本按钮` |
| input | `27a2f8fade057069f2eb2463659846a67549e4b2` | `大小=中` |
| search-box | `8eacd59a47f69d82b0b6dabc361c7defc0134bf1` | — |
| select | `f281417b32af0ada8d57f4512a879b9684664730` | — |
| datepicker | `7dc4ca686dfc4f4918684e31e021e79d09dce67e` | — |
| checkbox | `295f5d09c54dcb195945909f68a2b291b31f5030` | — |
| radio | `2a3067a53a133963e707c4dc080570795a9d66ea` | — |
| Switch | `2a3067a53a133963e707c4dc080570795a9d66ea` | — |
| form-item | `8459cecc3d4a0214af01637810cb817af0674ec7` | — |

### 表格组件（核心）

| 组件 | Key | 变体说明 |
|------|-----|---------|
| Table（完整表格） | `c8f8dbcc9a97c796fbc687f34593fe6f67c3bf27` | `边框=false` |
| 表头 / Header | `2ff798adea7de722bddf44fb4812091c8287ead4` | `类型=文本, 对齐=左对齐, 状态=默认/简约`  |
| 单元格 / text | `aa0975e2df1dd6d93eefecfdbbe140cfc05f707e` | `状态=默认, 对齐=左对齐` |
| 单元格 / text（双行） | `65867d3be5e30484c66e82faccbe31c9fedc29a6` | `状态=默认，对齐=左对齐` |
| 单元格 / action | `b4cd24206bea41c59b75fe73b95624b8c5740419` | `状态=默认, 数量=1/2/3`。**操作列默认右对齐**，对应表头也须选 `对齐=右对齐` 变体 |
| 单元格 / tag | `156d2ae0043badb8f719bb90c4f58408f9965777` | `状态=默认` |
| 单元格 / link | `6b22026a611de4b5b07a679d74d156f5f5bc4e56` | `状态=默认` |
| 单元格 / checkbox | `974b5c373bcd9382eb59a35b770ce94ef1210abf` | `状态=默认` |
| 单元格 / percent | `44d9c1e2e90ddb264444e9a59760c8ff35a6bce3` | `状态=默认`。**用途：可视化进度条（如完成率、占比）。⚠️ 不适用于涨跌幅，涨跌幅请用 单元格/text** |
| 单元格 / status | `b0600df9023a9cb536e188763069eb35b3b88044` (列) | `对齐=左, 固定=false` |
| Sorter | `1b11a91f1eeb7b11a175eee5365baba1aa1e1827` | `排序=默认/升序/降序` |

### 选项卡

| 组件 | Key | 说明 |
|------|-----|------|
| .components/tabs-line（整体） | `0cd61bfe242aadba89d5560e86906342a9a6b0f6` | 线型选项卡容器 |
| tabs/capsule（整体） | `cd0576b93d5766110e9b3e02b6a4d39c7559e13c` | 胶囊型选项卡 |
| Tab（整体） | `263c8e3c30fc7681ff2cad3633efd9968a4e9d84` | 面性选项卡容器，比较少用 |

### 数据展示 & 反馈

| 组件 | Key | 常用变体 |
|------|-----|---------|
| 标签样式1 | `1d65965bedee7a60a58b37064ed803797c604554` | `颜色=绿色/蓝色/黄色/橙色/红色/灰色` |
| 标签样式3 | `5d025d5171736f53c637cf765a383acf34b2a051` | `类型=绿色/蓝色/黄色/橙色/红色/灰色，大小=迷你/小` |
| badge/count | `0cffb42f4c4e01363746b3b01bdf0e627aaceba3` | — |
| Alert 提示 | ` f2f0d82daf471937af886ee9f6714bd745a3ee3d` | `类型=信息/成功/警告/错误` |
| Empty 空状态 | `02375fe5a682699c97639586753c612c4881d670` | `标题=true/false，按钮=true/false`。缺省图按照不同场景进行选用，默认选择`类型=初始空状态` |
| modal-confirm | `46e1353cc1c23ca00432752393416899a0a8b367` | ComponentSet（6 变体），**必须用 `importComponentSetByKeyAsync`** |
| modal | `9db5845c8cf31e9bdab1851c0efa7b353132c415` | ComponentSet（2 变体），**必须用 `importComponentSetByKeyAsync`** |
| Drawer | `397dd6c53c9bb13be2006b91939affee9e042ba3` | — |

### 页面模板

| 模板 | Key |
|------|-----|
| 列表页模板 | `771baa4dc5b1d1ebbbef9fa8007799e494c615a0` |
| 表单页模板 | `c7cb063639a87041434cb7fbe1a1e2e18755028b` |

---

## 搭建页面的工作流

### 0. 页面模板识别（最优先步骤）

在导入任何原子组件之前，**先判断页面描述是否命中以下模板场景**：

| 描述中出现的关键词 | 应使用的模板 | 组件 Key |
|-----------------|------------|---------|
| `page_template/列表页模板` | 列表页模板 | `771baa4dc5b1d1ebbbef9fa8007799e494c615a0` |
| `page_template/表单页模板` | 表单页模板 | `c7cb063639a87041434cb7fbe1a1e2e18755028b` |

命中模板时，执行流程：

```javascript
// ① 导入模板组件（单一组件，非 ComponentSet）
const templateComp = await figma.importComponentByKeyAsync(
  '771baa4dc5b1d1ebbbef9fa8007799e494c615a0' // 列表页模版
  // 或 'c7cb063639a87041434cb7fbe1a1e2e18755028b' 表单页模版
);

// ② 创建实例并放入页面
const templateInst = templateComp.createInstance();
templateInst.x = 0;
templateInst.y = 0;
figma.currentPage.appendChild(templateInst);

// ③ 解绑（页面模板类组件允许解绑）
const pageFrame = templateInst.detachInstance();

// ④ 找到内容区（根据实际模板内的节点名称调整）
const contentArea = pageFrame.findOne(n => n.name === '内容区');

// ⑤ 清空内容区各容器 frame 内的占位内容，保留内容区原本骨架
// 先 dump 内容区内部树结构，确认主卡片、页面标题行、筛选区、表格区、分页区等 frame 仍在
// 只在各容器 frame 内删除占位组件/文字，再填入实际业务组件
// ⛔ 禁止 [...contentArea.children].forEach(c => c.remove()) 删掉整个内容区子树后按 HTML 原型重新搭建
```

**注意事项**：
- 模板解绑后已包含导航框架，**不再单独导入这些框架组件**
- 内容区内部已有固定嵌套（主卡片 → 页面标题行 / 筛选区 / 表格区 / 分页区），**保留这些 frame，只替换其中的组件与文案**
- 若描述中未命中模板关键词，退回逐组件拼装方式
- 模板仅适用于整页场景；弹窗、抽屉等局部布局直接用原子组件拼装

---

### 1. 在目标文件中获取页面信息

```javascript
for (const page of figma.root.children) {
  await figma.setCurrentPageAsync(page);
  const found = await figma.getNodeByIdAsync('PAGE_OR_FRAME_ID');
  if (found) { break; }
}
```

### 2. 导入并使用 TaaS 组件

```javascript
// 导入组件集（从 TaaS 远程库）
const menuCS = await figma.importComponentSetByKeyAsync('341b06ec38f2f5f3232223b32be1491cb6a2fba8');
const variant = menuCS.children.find(c =>
  c.name.includes('收起=false') && c.name.includes('theme=dark') && c.name.includes('机构类型=代币管理人')
) || menuCS.defaultVariant;
const inst = variant.createInstance();
parentFrame.appendChild(inst);
inst.x = 0;
inst.y = 0;
```

### 3. 标准列宽参考

- 名称列（主列）: 350–480px
- 数据列: 160–220px
- 操作列: 200–350px（按按钮数量调整）

### 4. 优先使用已有组件

若找不到完全匹配的组件，优先选择同类型中最接近的组件变体，**不要手动绘制**。

---

## 注意事项

1. **组件字体处理规范** - 该库使用 PingFang SC，插件无法加载
   - **禁止直接修改**：不要修改组件内文本的 `fontName` 属性
   - **禁止解绑修改**：不要通过 `detachInstance()` 解绑后修改字体
   - **正确做法**：参见 `text-style-ref.md` 组件文本流程（流程 1）
2. **表格组件两套命名**: 
   - `/table-header 表头/` + `/table-cell 单元格/` — 逐行拼装
   - `/table-column 表格列/` — 按列拼装
   - `table`（key: `c8f8dbcc9a97c796fbc687f34593fe6f67c3bf27`）— 完整表格组件
3. **变体选择**: 使用 `cs.children.find(c => c.name.includes('关键词'))` 匹配变体
4. **Tag 颜色语义规范**（`标签样式1``标签样式3` 和 `单元格/tag` 均适用）：
   根据标签所表达的语义选择合适颜色变体，不可随意使用：

   | 颜色 | 变体关键词 | 语义 |
   |------|-----------|------|
   | 灰色 | `颜色=灰色` | **不表示状态或程度的中性分类标签**（如：基金类型、资产类别、一般属性标签）；以及禁用/次要/已结束状态（如：已到期、暂停、不可操作） |
   | 蓝色 | `颜色=蓝色` | 进行中、待处理等中性状态信息 |
   | 绿色 | `颜色=绿色` | 成功、正向、低风险 |
   | 红色 | `颜色=红色` | 错误、高风险、紧急 |
   | 黄色 | `颜色=黄色` | 警告、待确认、受限 |

   **判断用灰还是蓝的核心原则**：标签本身是否暗示某种程度高低或状态好坏？
   - 暗示程度/状态 → 用对应语义色（蓝/绿/红/黄）
   - 纯粹分类，无程度含义 → 用灰色

   **Tag 颜色变体切换操作规范**（通过 `use_figma`）：
   - `单元格/tag` 外层实例只有 `状态=默认/Hover` 变体，**颜色由内层嵌套的 `tags-wrapper` 实例控制**
   - 切换颜色需对内层 `tags-wrapper` 调用 `swapComponent(targetVariant)`，其中 `targetVariant` 需满足 `颜色=目标色, 大小=迷你, 状态=默认`
   - ⚠️ **`swapComponent` 会清空部分覆写**：若新旧变体的文本节点名称不同，文案覆写无法自动保留。操作后必须立即重新写入文案，避免回退为组件默认值
   - **文案写入方式（已验证有效）— 字体替换法**：`tags-wrapper` 使用 PingFang SC（plugin 无法加载），且 `setProperties` 对 TEXT 类型组件属性**静默失败**（无报错但值不变）。**唯一可靠方案是先加载 Noto Sans SC，再直接修改文本节点的 fontName 和 characters**：
     ```javascript
     await figma.loadFontAsync({ family: 'Noto Sans SC', style: 'Medium' });
     const rowInst = await figma.getNodeByIdAsync(rowId);
     const tagCells = rowInst.findAll(n => n.name === '/table-cell 单元格/tag');
     for (const cell of tagCells) {
       const textNode = cell.findOne(n => n.name === 'tags-wrapper')?.findOne(n => n.type === 'TEXT');
       if (textNode) {
         textNode.fontName = { family: 'Noto Sans SC', style: 'Medium' };
         textNode.characters = '目标文案';
       }
     }
     ```
   - ⚠️ **`setProperties({ '替换文本#148903:630': '...' })` 对 TEXT 类型属性静默失败**：VARIANT 和 BOOLEAN 类型属性 setProperties 有效，但 TEXT 类型不生效（测试确认：调用后 `componentProperties` 仍返回原默认值）
   - ⚠️ Vibma `text.set_content` 对深度嵌套实例的文本节点可能**视觉上无效**（返回 ok 但画布不更新），不推荐用于 tag 文案写入
   - ⚠️ **不同颜色变体的文本节点 ID 尾部不同**（如 `372:4075`、`372:3883`、`372:4395` 等），不能直接套用固定规律。推荐通过 traversal（`rowInst.findAll(n => n.name === '/table-cell 单元格/tag')`）查找，而非构造 ID
   - **颜色变体（swapComponent）和文案（字体替换法）必须同步操作**，顺序建议：先 swapComponent 设色，再用字体替换法写文案

5. **涨跌幅颜色规范**（中国金融惯例：涨红跌绿）：
   - 涨幅（正值）文字色：使用颜色变量 `危险色/危险色`
     - Library variable key: `4563d046e10088948862cac27722d79c5156af89`
   - 跌幅（负值）文字色：使用颜色变量 `成功色/成功`
     - Library variable key: `8fdc8e694a3dbae0ff995f000596bee740366ad7`
   - **绑定方式**：先确认目标文件已开启 TaaS 变量库，然后通过 `use_figma` 执行：
     ```javascript
     const redVar = await figma.variables.importVariableByKeyAsync('4563d046e10088948862cac27722d79c5156af89');
     const greenVar = await figma.variables.importVariableByKeyAsync('8fdc8e694a3dbae0ff995f000596bee740366ad7');
     // 绑定到文字节点 fills
     node.fills = [{type:'SOLID', color:{r:0.96,g:0.133,b:0.176}, boundVariables:{color:{type:'VARIABLE_ALIAS',id:redVar.id}}}];
     ```
   - Vibma 的 `fontColorVariableName` / `bindings[].variableId` **不支持远程库变量**，必须用 `use_figma` + `importVariableByKeyAsync`
   - **不要使用 `单元格/percent` 展示涨跌幅**，使用 `单元格/text` 并手动绑定对应颜色变量

6. **数值文本样式规范**：
   页面中展示的数字类数据（如净值、涨跌幅、金额、比率等），需应用 TaaS 的 **Number** 系列文本样式，而非普通 CN 正文样式。Number 样式使用等宽数字字形，保证列对齐和数据可读性。
   - 样式命名格式：`正文/{字号}/Number-Regular`，如 `正文/14/Number-Regular`、`正文/12/Number-Regular`
   - **字号选择原则**：
     - 若数值位于**组件内部**（如 `单元格/text` 等表格组件），字号跟随组件本身已有的字号，不另行修改
     - 若数值位于**非组件的独立文本节点**，则根据上下文选择合适字号（如卡片大数字用 20px，正文数据用 14px，辅助说明用 12px）
   - 通过 Vibma `text.update` 用 `textStyleName` 绑定，例如：`textStyleName: "正文/14/Number-Regular"`
   - 或通过 `use_figma` 用 `figma.importStyleByKeyAsync` 导入后应用

7. **组件解绑规范**：
   不要随意解绑（detach）组件实例，解绑后将失去与主组件的关联，无法跟随组件库更新同步。
   - **允许解绑**：页面模版（`列表页模版`、`表单页模版` 等）、弹窗（`modal`、`modal-confirm`）——这类组件本身就是搭建骨架用的，解绑后再定制是预期用法。⚠️ 注意：`modal` / `modal-confirm` 是 **ComponentSet**，导入时必须用 `importComponentSetByKeyAsync`（与页面模板用 `importComponentByKeyAsync` 不同），再对 `defaultVariant` 创建实例后解绑
   - **禁止随意解绑**：筛选器（`filter`）、按钮（`Button`）、表格单元格（`单元格/*`）、表头（`表头/*`）、输入框（`input`/`search-box`）等原子/分子级组件，应保持实例状态，通过切换变体或覆写属性（Override）来满足需求
   - 若需修改组件内部文字，应优先尝试通过实例属性覆写；仅当 API 确实无法写入（如字体加载失败）时，才考虑解绑后修改，并在注释中说明原因
   - **解绑后重建内部容器帧规范**：清空 `body` / `内容区` 等容器帧并切换其 `layoutMode` 时，**不得自行追加 `paddingTop` / `paddingBottom`**。原组件的内容容器帧纵向 padding 设计为 0，上下间距由外层 frame 的 `itemSpacing` 控制。若不确定原始值，先读取再决定：`console.log(body.paddingTop, body.paddingBottom)`；如需保留，显式写出；如需归零，显式 `body.paddingTop = 0; body.paddingBottom = 0`。**禁止凭经验估值。**


8. **重复元素封装为本地组件**
   当页面中某个组合结构需要重复出现多次，应先用原子组件或基础元素将其构建为**本地组件（Local Component）**，再通过实例化引用。
   - 使用 `use_figma` 中 `figma.createComponent()` 创建本地组件
   - 后续复用时调用 `localComponent.createInstance()` 实例化

   **典型适用场景**（以下必须封装为本地组件）：
   - **表格数据行**：由多个 `单元格/*` 实例横向排列组成，一个页面有多行，结构一致 → 先构建一个 `dataRow` 本地组件，再实例化 N 次
   - **表头行**：由多个 `表头/header` 实例横向排列组成，应封装为 `headerRow` 本地组件后，在 tableSlot 中实例化引用（即使只出现一次，也方便后续调整列宽）
   - **卡片列表项**：由图片、标题、描述、操作等组合而成，列表中每项结构相同
   - **自定义状态标记、特殊信息卡片、组合图标文本**等在页面中重复出现的自定义组合

   **工作流**：
   ```javascript
   // 0. 准备表格容器（tableSlot）
   //    ⚠️ tableSlot 不是新建 frame，而是在 contentArea 内创建的透明包装层
   //    必须在 contentArea 已清空的前提下执行
   const tableSlot = figma.createAutoLayout('VERTICAL', { name: 'tableSlot', itemSpacing: 0 });
   tableSlot.fills = [];  // ← 必须清空默认白色填充！否则会在深色背景上盖一层大白块
   contentArea.insertChild(0, tableSlot);   // 插到 pagination 之前
   tableSlot.layoutSizingHorizontal = 'FILL';
   tableSlot.layoutSizingVertical = 'HUG';

   // 1. 先构建单行结构，挂到页面根节点临时放置
   const rowComp = figma.createComponent();
   rowComp.name = 'dataRow';
   rowComp.layoutMode = 'HORIZONTAL';
   rowComp.primaryAxisSizingMode = 'AUTO'; // 宽度跟随内容，不要 resize 为固定值
   figma.currentPage.appendChild(rowComp);
   // ... 向 rowComp 内添加各列单元格实例 ...

   // 2. 实例化 N 次放入 tableSlot
   for (let i = 0; i < 8; i++) {
     const inst = rowComp.createInstance();
     tableSlot.appendChild(inst);
   }
   ```

   **本地组件放置规范**：
   - `headerRow` 和 `dataRow` 两个本地组件应**并列放置在生成页面下方**，上下对齐（相同 x 坐标），纵向紧邻（4px 间隔）
   - 定位参考：`comp.x = pageFrame.x; comp.y = pageFrame.y + pageFrame.height + 80;`
   - headerRow 在上，dataRow 在下，两者 x 对齐，内部各列宽度对应保持一致（使用 `primaryAxisSizingMode = 'AUTO'` 避免手动 resize 引起宽度不匹配）

9. **本地组件母版必须填充示例数据**
   创建 `headerRow` 和 `dataRow` 本地组件后，**必须立即向母组件本体填充真实可读的示例数据**，而不是保留占位符（如「单元格」「说明」「状态」「Title」「操作」等默认文案）。
   - **headerRow**：所有表头文字必须替换为实际列名（如「产品名称/ISIN」「近一月」「操作」等）
   - **dataRow**：所有单元格必须填入一条有代表性的真实样例数据（名称、数值、日期、货币、按钮文案等），tag 类单元格需同时完成颜色 swap 和文案写入

   **操作规范**：
   ```javascript
   // 填充完母组件结构后，立即用 Vibma set_content 写入所有文本
   // 示例：headerRow 基金
   await vibma.text.set_content([
     { nodeId: 'I{headerCellId};1145:55969', text: '产品名称/ISIN' },
     // ... 其余列名
   ]);
   // dataRow 填充一条代表性数据
   await vibma.text.set_content([
     { nodeId: 'I{cell0Id};4559:10194', text: '南方基金未来视野科技基金A' },
     { nodeId: 'I{cell0Id};4559:10201', text: 'HK0000252101' },
     // ... 其余字段
   ]);
   // tag 单元格：先 swapComponent 设色，再字体替换法写文案
   tw.swapComponent(grayTag);
   const t = tw.findOne(n => n.type === 'TEXT');
   t.fontName = { family: 'Noto Sans SC', style: 'Medium' };
   t.characters = '股票型';
   ```

10. **组件宽度设置规范**
   大多数 TaaS 原子/分子组件（`filter`、`search-box`、`Button`、`input`、`datepicker` 等）**不需要手动 resize 宽度**，直接保持组件默认的 AUTO/HUG 自适应行为即可。若实例化后被意外 resize 为 FIXED，应通过 `use_figma` 恢复：
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

11. **自动布局与绝对定位规范**
   页面中的大多数元素应置于自动布局容器内，利用 Auto Layout 管理间距和对齐。
   只有**需要浮层覆盖**在其他内容上方或下方的元素，才需将其设为「忽略自动布局」（`isAbsolute = true` / `layoutPositioning = "ABSOLUTE"`），例如：徽章（Badge/Count）、悬浮按钮、Tooltip

   普通内容元素一律参与自动布局，不要随意设置绝对定位。

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

13. **页面模版使用限制与退回策略**：
   - 页面模版适用于「整页」场景；若自然语言描述的是**弹窗内的局部布局**（如抽屉、Modal 内的表单），不应套用模版，直接使用原子组件拼装
   - 内容区 `findOne` 失败时（返回 `null`），说明节点名称与预期不符——此时打印 `pageFrame.children` 重新确认，不要盲目删除 `pageFrame` 本体
   - 同一页面只能套用**一个**模版；若描述同时含有列表和表单（如「列表页 + 侧边新增面板」），以主体内容决定模版类型，次要内容用 `modal` 或独立 Frame 处理

---

