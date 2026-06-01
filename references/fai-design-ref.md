# FAI 设计参考 · 组件速查 & 界面拼装指南

## 前提：必须先读取 figma-use skill

- **组件库文件 key**: `1IzJjE812UGoArwoWH09wo`
- **导入方式**: `figma.importComponentSetByKeyAsync(componentKey)`
- 需在目标文件的 `use_figma` 中指定目标文件的 `fileKey`，组件通过 key 从远程库导入

---

## 标准页面框架（1920×1080）

```
├── 左侧全局侧导航（状态=收起）
├── 右侧主区域（垂直布局）
│     ├──  顶部栏
│     ├──  内容区（按需求类型组织的多样化内容）
```


### 变体选择规则

**menu 侧导航** - 推荐变体: `状态=收起，业务=对内`

**顶部栏** - 无变体

**Button** - 常用变体:
- 主操作: `尺寸=中, 类型=主要按钮, 种类=标准, 形状=长方形, 状态=默认`
- 次操作: `尺寸=中, 类型=线框按钮, 种类=标准, 形状=长方形, 状态=默认`
- 文字链: `尺寸=中, 类型=文本按钮, 种类=标准, 形状=长方形, 状态=默认`

---

## 核心组件 Key 速查

### 导航布局

| 组件 | Key | 常用变体关键词 |
|------|-----|--------------|
| menu 侧导航 | `06881499da6f87c3596981e7a627f9296e3b9e74` | `状态=收起，业务=对内` |
| 顶部栏 | `8ae8ab95e92dbe1a1ac76dfcabab42cdea3e051d` | -- |
| Divider | `967b441a8299a352e3aff98ea5882a40b9141520` | `类型=水平` |
| pagination | `da175dd8769f612d8ac21168eaf5a9dfc02cbbe4` | — |

### 数据录入

| 组件 | Key | 常用变体关键词 |
|------|-----|--------------|
| Button | `da3e8b7e13d2ed14121fa21ed527c6a69f23e0d7` | `类型=主要按钮/线框按钮/文本按钮` |
| input | `57c201d6c4d4cd318578ae1e74de0352cfaaf67d` | `大小=中` |
| search-box | `d9c707f2fa2c37171bd6426029b716a32723cff4` | — |
| select | `36e935761dbf7344c0c3c30645784436e5865d0d` | — |
| datepicker | `5bf5a76459d31551c05b3924e32548806ecd3ad8` | — |
| checkbox | `1bc26d877f61c9e8041602a80e35ab41955c3485` | — |
| radio | `1eab3acb5fbd8f7f6f4b7c2b958ac0fce5881c27` | — |
| form-item | `62d8212f8b5ef9191e7ce10947fffa6cd9b9524c` | — |

### 表格组件

| 组件 | Key | 变体说明 |
|------|-----|---------|
| table（完整表格） | `9e993d29194a95534627c05437624b55be843463` | `边框=false` |
| 表头/header | `b6fe11a579a0a8989c80e8d0b2096161eb2eef74` | `对齐=左对齐, 状态=默认` |
| 单元格/text | `df2653f8db03f92df3a4665479cee2851d49587a` | `状态=默认, 对齐=左对齐` |
| 单元格/text(2行) | `66045da8e37a180876d1c0ebb7ac5f15ce4a9145` | `状态=默认, 对齐=左对齐` |
| 单元格/action | `e9179ff1149fc982bca1a68515c4bc6c50d888a3` | `状态=默认, 数量=1/2/3` **操作列默认右对齐** |
| 单元格/tag | `1d9471c48c06a44297609c2fa74a83855265a3af` | `状态=默认, 对齐=左对齐` |
| 单元格/link | `f7d915878bea550401d3e371814b1f1ed607ee4c` | `状态=默认, 对齐=左对齐` |
| 单元格/checkbox | `e5d223999ea36460e327097083372c0b821427b1` | `状态=默认` |
| 单元格/status | `0419d94fcda40bd7b6b6fd5098ee666bd0a9abbe` | `状态=默认, 对齐=左对齐` |
| sorter | `2f592c848761b0ede725879d7a89641b71afc295` | `排序=默认/升序/降序` |

### 选项卡

| 组件 | Key | 说明 |
|------|-----|------|
| tabs/line（整体） | `e1a284b3a9783a3a1f3cde68ac71e86d0354c284` | 线型选项卡容器 |
| tabs/capsule（整体） | `392b95d27dd70cd16ff6baee2c0bd8cb44d1bd0a` | 胶囊型选项卡 |
| tabs/面性（整体） | `cc9f9db17645c3b5af0b9d3dc9c2b3c3407baded` | 面性选项卡，目前仅用于资讯模块 |
| components/tab（单个） | `1e5a9204bae92fc804767ffe44514d444d873759` | 单独 tab 项 |

### 数据展示 & 反馈

| 组件 | Key | 常用变体 |
|------|-----|---------|
| 标签样式/方形/面性 | `bb25f32e8515c92aa13deaaff2a182b49ee699ef` | `类型=蓝色/红色/绿色/灰色/黄色, 大小=迷你/小, 状态=默认` **优先使用方形/面性标签**|
| 标签样式/方形/线性 | `0c49d4606259d13bde500c8f9cb45b3652f54056` | `类型=蓝色/红色/绿色/灰色/黄色, 大小=迷你/小, 状态=默认` |
| Alert | `24dfdd503a7c2f5c6ad4882991ad66f1a6daf437` | `类型=信息/成功/警告/错误/停止对话/` |
| Empty（空状态） | `b32fd7e2e554f6d5d8c93b327f3f3f076b01df06` | — |
| modal | `f82158d834f957abfc10ea45f430b0c23db105a4` | ComponentSet，**必须用 `importComponentSetByKeyAsync`** |
| modal-confirm | `4e5879b7bd47c13ff65695d0007de78e5e05b341` | ComponentSet，**必须用 `importComponentSetByKeyAsync`** |
| Drawer | `94aff295ff0e236b212cddbed8776d05f6bc9173` | — |

### 页面模板

| 模板 | Key |
|------|-----|
| 列表页模版 | `c93d8f3c71868c668fe517f489e76672f66482bd` |
| 表单页模版 | `3e0f55028171ec3e594e5001677351e8b3a03ee4` |

---

## 搭建页面的工作流

### 0. 页面模版识别（最优先步骤）

在导入任何原子组件之前，**先判断自然语言描述是否命中以下场景**：

| 描述中出现的关键词 | 应使用的模版 | 组件 Key |
|-----------------|------------|---------|
| `page_template/列表页模版` | 列表页模版 | `c93d8f3c71868c668fe517f489e76672f66482bd` |
| `page_template/表单页模版` | 表单页模版 | `3e0f55028171ec3e594e5001677351e8b3a03ee4` |

命中模版时，按以下流程操作：

```javascript
// ① 导入模版组件（单一组件，非 ComponentSet）
const templateComp = await figma.importComponentByKeyAsync(
  'c93d8f3c71868c668fe517f489e76672f66482bd' // 列表页模版
  // 或 '3e0f55028171ec3e594e5001677351e8b3a03ee4' 表单页模版
);

// ② 创建实例并放入页面
const templateInst = templateComp.createInstance();
templateInst.x = 0;
templateInst.y = 0;
figma.currentPage.appendChild(templateInst);

// ③ 解绑（模版类组件允许解绑）
const pageFrame = templateInst.detachInstance();

// ④ 找到内容区
const contentArea = pageFrame.findOne(n => n.name === '内容区');

// ⑤ 清空内容区各容器 frame 内的占位内容，保留内容区原本骨架
// 先 dump 内容区内部树结构，确认主卡片、页面标题行、筛选区、表格区、分页区等 frame 仍在
// 只在各容器 frame 内删除占位组件/文字，再填入实际业务组件
// ⛔ 禁止 [...contentArea.children].forEach(c => c.remove()) 删掉整个内容区子树后按 HTML 原型重新搭建
```

**使用模版后的注意事项**：
- 模版解绑后已包含 `menu 侧导航` 和 `navbar顶部栏` 的完整骨架，**不再单独导入这两个组件**
- 内容区内部已有固定嵌套（主卡片 → 页面标题行 / 筛选区 / 表格区 / 分页区），**保留这些 frame，只替换其中的组件与文案**
- 导航栏 / 侧边栏保持不动
- 若描述中没有明确命中上表关键词，退回到原有逐组件拼装方式

---

### 1. 在目标文件中获取页面信息

```javascript
for (const page of figma.root.children) {
  await figma.setCurrentPageAsync(page);
  const found = await figma.getNodeByIdAsync('PAGE_OR_FRAME_ID');
  if (found) { break; }
}
```

### 2. 导入并使用 F-AI 组件

```javascript
// 导入组件集（从 F-AI 远程库）
const menuCS = await figma.importComponentSetByKeyAsync('06881499da6f87c3596981e7a627f9296e3b9e74');
const variant = menuCS.children.find(c =>
  c.name.includes('状态=收起') && c.name.includes('业务=对内')
) || menuCS.defaultVariant;
const inst = variant.createInstance();
parentFrame.appendChild(inst);
inst.x = 0; inst.y = 0;
```

### 3. 标准列宽参考（1782px 表格总宽）

- 名称列（主列）: 350–480px
- 数据列: 160–220px
- 操作列: 200–350px（按按钮数量调整）

### 4. 优先使用已有组件

若找不到完全匹配的组件，优先选择同类型中最接近的变体，不要手动绘制。

---

## 注意事项

1. **组件字体处理规范** - 该库使用 PingFang SC，插件无法加载
   - **禁止直接修改**：不要修改组件内文本的 `fontName` 属性
   - **禁止解绑修改**：不要通过 `detachInstance()` 解绑后修改字体
   - **正确做法**：参见 `text-style-ref.md` 组件文本流程（流程 1）

2. **表格组件两套命名**:
   - `/table-header 表头/` + `/table-cell 单元格/` — 逐行拼装
   - `table`（完整表格组件）— 整体导入

3. **变体选择**: 使用 `cs.children.find(c => c.name.includes('关键词'))` 匹配变体

4. **Tag 颜色语义规范**（`标签样式3` 和 `单元格/tag` 均适用）：
   - **灰色**：不表示状态或程度的中性分类标签；以及禁用/次要/已结束状态
   - **蓝色**：带有程度/状态含义的中性信息（如：进行中、待审核）
   - **绿色**：正向/低风险/成功状态
   - **红色**：高风险/错误/紧急
   - **黄色**：中等警告/提醒/待确认

   **判断用灰还是蓝的核心原则**：标签本身是否暗示某种程度高低或状态好坏？
   - 暗示程度/状态 → 用对应语义色（蓝/绿/红/黄）
   - 纯粹分类，无程度含义 → 用灰色

   **Tag 颜色变体切换操作规范**（通过 `use_figma`）：
   - `单元格/tag` 外层实例只有 `状态=默认/Hover` 变体，**颜色由内层嵌套的 `tags-wrapper` 实例控制**
   - 切换颜色需对内层 `tags-wrapper` 调用 `swapComponent(targetVariant)`
   - ⚠️ **`swapComponent` 会清空部分覆写**：操作后必须立即重新写入文案
   - **文案写入方式**：参见 `text-style-ref.md` 组件文本流程（流程 1）

5. **涨跌幅颜色规范**（中国金融惯例：涨红跌绿）：
   - 涨幅（正值）文字色：使用颜色变量 `<!-- TODO: 填入红色变量名 -->`
     - Library variable key: `<!-- TODO -->`
   - 跌幅（负值）文字色：使用颜色变量 `<!-- TODO: 填入绿色变量名 -->`
     - Library variable key: `<!-- TODO -->`
   - **绑定方式**：通过 `use_figma` 执行 `importVariableByKeyAsync`

6. **数值文本样式规范**：参见 `text-style-ref.md` 数字字体使用规范。

7. **组件解绑规范**：
   - **允许解绑**：页面模版（`列表页模版`、`表单页模版` 等）、弹窗（`modal`、`modal-confirm`）
   - **禁止随意解绑**：筛选器、按钮、表格单元格、表头、输入框等原子/分子级组件
   - **解绑后重建内部容器帧规范**：**不得自行追加 `paddingTop` / `paddingBottom`**，禁止凭经验估值

8. **本地组件母版必须填充示例数据**：
   - `headerRow`：所有表头文字替换为实际列名
   - `dataRow`：所有单元格填入一条有代表性的真实样例数据
   - **操作规范**：填充完母组件结构后，立即用 `text-style-ref.md` 流程 1 写入所有文本

9. **页面模版使用限制与退回策略**：
   - 页面模版适用于「整页」场景；弹窗、抽屉等局部布局直接用原子组件拼装
   - 内容区 `findOne` 失败时，打印 `pageFrame.children` 重新确认，不要盲目删除 `pageFrame` 本体
   - 同一页面只能套用**一个**模版

10. **重复元素封装为本地组件**：
    当页面中某个组合结构需要重复出现多次，应先构建为**本地组件（Local Component）**，再通过实例化引用。

    **典型适用场景**（以下必须封装为本地组件）：
    - **表格数据行**：`dataRow` 本地组件，实例化 N 次
    - **表头行**：`headerRow` 本地组件，在 tableSlot 中实例化引用

    **本地组件放置规范**：
    - `headerRow` 和 `dataRow` 并列放置在生成页面下方，上下对齐，纵向紧邻（4px 间隔）

11. **组件宽度设置规范**：
    大多数原子/分子组件不需要手动 resize 宽度，保持默认 AUTO/HUG 自适应行为。若被意外 resize 为 FIXED，通过 `use_figma` 恢复：
    ```javascript
    inst.layoutSizingHorizontal = 'HUG';
    ```
    **例外**：`headerRow` 和 `dataRow` 中每个单元格必须手动给定合适的固定宽度。

12. **表格行单元格高度对齐规范**：
    若存在不同高度的单元格混排，必须确保同行内所有单元格高度一致：
    ```javascript
    dataRowComp.counterAxisAlignItems = 'MIN';
    for (const cell of dataRowComp.children) {
      cell.layoutSizingVertical = 'FILL';
    }
    ```

13. **自动布局与绝对定位规范**：
    普通内容元素一律参与自动布局。只有需要浮层覆盖的元素（徽章、悬浮按钮、Tooltip 等）才设置 `layoutPositioning = "ABSOLUTE"`。
