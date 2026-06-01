# Finloop 设计参考 · 组件速查 & 界面拼装指南

## 前提：必须先读取 figma-use skill

- **组件库文件 key**: `scodnBKwhh8jBoPorOkf3X`
- **组件库名称**: `AI 运营-组件库`
- **组件库 libraryKey**: `lk-42303f5ad3b4a675c8b42dffb4f79ddcbd771302803d07b97f1d99443a204cc74c8a034daf533a45e7ddf612dc98309eb18f18a98a886086ac1eef1ed109fa96`
- **导入方式**: `figma.importComponentSetByKeyAsync(componentKey)`；若组件 `assetType=component`，使用 `figma.importComponentByKeyAsync(componentKey)`
- 需在目标文件的 `use_figma` 中指定目标文件的 `fileKey`，组件通过 key 从远程库导入

---

## 标准页面框架（1920×1080）

```
├── menu 侧导航 (220×1080)           key: ee9ca3a0bc5218931b3ba9e62ff93bf7510416bf
├── 右侧主区域 (1700×1080)
│   ├── navbar顶部栏 (1700×48)       key: 1f59053b94fdeab4fdee1eb111564c948dd59e0e
│   └── 内容区 (1700×1032)
│       ├── 筛选区（筛选/select/search-box/datepicker）
│       ├── 表格（/table-cell 单元格/header + /table-cell 单元格/* 行）
│       └── pagination 分页
```

### 变体选择规则

**menu 侧导航** - 推荐优先使用较新的 `menu` key: `ee9ca3a0bc5218931b3ba9e62ff93bf7510416bf`。若导入后变体结构不完整，可回退到同名导航组件 key: `554e133a2e2f21174886c10d6976e78229dc4f81`。

**navbar顶部栏** - 变体: 优先选择包含多页签 / 用户信息 / 工具入口的变体；若需要固定顶部导航，可评估 `FixedNavbar`。

**Button** - Finloop / AI 运营平台优先使用渐变按钮:
- 主操作: `Button渐变`，`尺寸=中, 类型=主要按钮, 种类=标准, 形状=长方形, 状态=默认`
- 次操作: `Button`，`尺寸=中, 类型=线框按钮/次要按钮, 种类=标准, 形状=长方形, 状态=默认`
- 文字链: `Button`，`尺寸=中, 类型=文本按钮, 种类=标准, 形状=长方形, 状态=默认`

---

## 核心组件 Key 速查

### 导航布局

| 组件 | Key | 常用变体关键词 |
|------|-----|--------------|
| menu 侧导航（推荐） | `ee9ca3a0bc5218931b3ba9e62ff93bf7510416bf` | 侧边导航 / 展开态 |
| menu 侧导航（备用） | `554e133a2e2f21174886c10d6976e78229dc4f81` | `菜单分类：导航` |
| vertical-menu-item/1st-level | `0119bc07fd010c6b416b15abfb5390ffd801eaca` | 一级菜单项 |
| navbar顶部栏 | `1f59053b94fdeab4fdee1eb111564c948dd59e0e` | 顶部栏 |
| FixedNavbar | `ab325165be0e954bb41303161591bd932bb9614d` | 固定导航 |
| FixedNavbar/subnavigation | `ee81da96555916aba9386a2fcebc82d5a929458f` | 子导航 |
| Divider | `96bcb5357a79fe1f7c7a08ce9c7ade40ff4e8fc1` | 分割线 |
| pagination | `86947ca2a5706e6a67ed95ef91bc1d1d8d9a729b` | 标准分页 |
| pagination-simple | `c1400c6ad9ca8efc1ede36fe461ac425bd4d9f31` | 简版分页 |

### 数据录入

| 组件 | Key | 常用变体关键词 |
|------|-----|--------------|
| Button渐变（AI 运营主按钮） | `f6121bfac231f6da5bb6e84f6957d9786cbfcbea` | `类型=主要按钮` |
| Button | `d16bb4855a5b89525c3b08809c3dec236af62a22` | `类型=主要按钮/线框按钮/文本按钮` |
| Button-group渐变 | `a7a0a9990ffff29db2146e586eae8ec53ec44a3b` | AI 运营按钮组 |
| Button-group | `7f2ea08739089e583b3dbd2ec06139ed79929a4f` | 标准按钮组 |
| input | `e733b5721742097664455241c493457a83986ab7` | 输入框 |
| input- Prefix suffix | `442815207872b28ac9d745e33e45421c37a2d77d` | 前后缀输入框 |
| input-number | `bac5dda3d0402687363286d0f0e4ca2ee2947ad5` | 数字输入框 |
| textarea | `c2fded96837badccef62ce9d6ff1e75dd072a683` | 文本域 |
| password | `fc53948d59e9d1c81760ed99d5cabe7378e81528` | 密码框 |
| search-box | `973ea85a05f1205326faca6ab2a8a2b4a29a3e9a` | 搜索框 |
| select | `a7ce3740671f97b15edcd15fd011363339d69f69` | 选择器 |
| select menu | `ee3a97f57ad4622a74982928fe9b74ce0e73e3dc` | 下拉选项面板 |
| Dropdown menu | `d340d3ac953d6b8a9d071ce65fa086c374e45e6e` | 下拉菜单 |
| filter | `3cd7b4e18ad3812e0d3b3d8026979f9f9110ccdd` | 列表或表格上方的筛选区控件 `Type=select/datepicker`  |
| datepicker-dropdown | `de93a2912144aa7367e7dbb07583cc26cdaa3803` | 日期选择器 |
| datapicker/quick-select | `53caed1bb9b50bf0e3993878c5fca0d2046c036c` | 日期快捷选择 |
| checkbox | `311d6af212fb7b834d8e48e620a8d7145a1c0c71` | 复选框 |
| checkbox-input | `0684b0d3203034f6069c209bc25d2a28890a239d` | 复选输入项 |
| checkbox-group | `afa93b67c155912c8afc2d78981b2b919dfb1787` | 复选框组 |
| radio | `2cd1d3af4d20d5d5ac063dc722a19193670aa1bc` | 单选框 |
| radio-group | `0dc0d23945d52b8e40c09d6dc8ebb9b80a0176d6` | 单选框组 |
| form-item | `7c6d62a3a27cd4aeaa1ecc7f14af054c507652eb` | 表单项 |
| treeselect | `f3023b6947607f2239bcfb19ea6775a138d2af9b` | 树选择 |
| Cascader menu | `04c81d86a1a63122f297500c99db0c4f4b499735` | 级联菜单 |

### 表格组件（核心）

| 组件 | Key | 变体说明 |
|------|-----|---------|
| table（完整表格） | `95963f0616881d8c4f703bad1b036d0b8b63152e` | 标准表格 |
| 表头/header | `89c0b61b29abbe337c21d16730e0c59bcdb626ed` | `/table-cell 单元格/header` |
| 单元格/text | `b01bb1742588e893e0afaa495003dc6eb30733e1` | 文本单元格 |
| 单元格/text(2行) | `27090d57f88f353a5a8e0873057ce8c5da0fdabb` | 双行文本 |
| 单元格/action | `8a90918d553bd890b8e49f20d724751f829b71ad` | 操作列 |
| 单元格/tag | `162418665bb03695f2f63aabbaa61d17b7ba25a2` | 标签列单元格 |
| 单元格/link | `322e1d56c41be9b690dd9ed887f9d00c8b55bb8e` | 链接单元格 |
| 单元格/checkbox | `129ef8866360f484ee85dbd8ab1fca5f87bbeb8a` | 复选单元格 |
| 单元格/header-checkbox | `2d791bd3fe42a28bbea7570594c18068e7d19ea8` | 表头复选 |
| 单元格/radio | `0f1ee0e49c62b2d7a128198b522373c759222c86` | 单选单元格 |
| 单元格/status | `bdbd4a29e283549a8d18964ab143f861dc151631` | 状态单元格 |
| 单元格/from | `3f1709f607e984489538b3d9780baaacc34256ef` | 表单型单元格（名称沿用库内 from） |
| 单元格/switch | `1ce74458f122f19998974207f2cdced0f6c5cf34` | 开关单元格 |
| 单元格/avatar+text | `a17873acec9abeb6bb68423ffade955976610c0e` | 人员/头像文本 |
| 单元格/text+icon | `161d70bee937e1aaf93a7c117e36c42a462597b4` | 文本加图标 |
| 单元格/+icon | `919dd9695495690c98fa4ad05e8e203d6f0c7bdf` | 图标单元格 |
| 单元格/expand icon | `c179ef1733d0dd3805614f96bc080011d8af1863` | 展开图标 |
| 表格列/text | `712162ec7b3096738ddaef976dbc542b0487883e` | 标准列 |
| 表格列/link | `9ce94837773869eea32d3d853fe1c032881c725d` | 链接列 |
| 表格列/tags | `e04439143005df7cae5b4261cd1a38fa67ce68df` | 标签列 |
| 表格列/avatar | `9220bfaa087f5d3f2255dbde020620151f814f97` | 人员信息列 |
| 表格列/checkbox | `44b9df3a261b52eafa34315a87861c0655c0782c` | 多选列 |
| 表格列/radio | `e55135675d805fb81532f4c054708cd77ff07d01` | 单选列 |
| 表格列/from | `0913029325dd0036c92f523849a6e952ea799fc0` | 输入框列 |
| 表格列/text+icon | `cceedfaf3d7f47b0810e1e0e25bf53a75f6927c8` | 文本图标列 |
| sorter | `34d7c5a4dd35a798c6d73ab5f8b2a1cd07a0c59c` | 排序 |

### 选项卡

| 组件 | Key | 说明 |
|------|-----|------|
| tabs/line（整体） | `de6f1264c9f26644ca0e67555007106e23b5cb43` | 线型选项卡容器 |
| tabs/capsule（整体） | `cca8c83c22c9e720fe30efeb1b95c6235d9f4cf6` | 胶囊型选项卡 |
| tabs/card-gutter | `0e60b0ed28771f412e72569cac4c2d2fa89dd6c6` | 卡片型选项卡 |
| Tab组件（单个） | `bc0cb9cd3100d757c331f9798b20ac33a7bb341b` | 单独 tab 项 |

### 数据展示 & 反馈

| 组件 | Key | 常用变体 |
|------|-----|---------|
| 标签样式3 (Tag) | `406931f9545919f8d9d25abe442377d5c1ff4c74` | 常用状态标签 |
| 标签样式1 | `199fd37ea3f4db8bc69aa9370ff7b61752aa73e0` | 标签 |
| 标签样式4 | `089c08ec925a953ac60f0039eb27443efd7168d9` | 标签 |
| 标签样式5 | `88bff0204763926a867908ce817abf66d2e3ba67` | 标签 |
| 标签样式6 | `5ee532b7e5a3126ed293fdfba77f12107f0b729a` | 标签 |
| Label 标签 | `77287b40014918da599dc4d225876d2df18cc107` | 标签 |
| Tag-input | `29e599d89f358c4710d386392f69616472c2d179` | 可输入标签 |
| badge/count | `360a18ffdcc498bb6d6c8e82125d002b94645a0e` | 数字徽标 |
| Avatar | `677cc9a7bd691f1c70d7883d4c7c8fe976de2602` | 头像 |
| Avatar.Group | `e891af97748e34009e727aa102d45bd498d8e691` | 头像组 |
| Alert | `3c558681b8afd8e874b0f1958fb8077bafbc9852` | `类型=info/success/warning/error` |
| Empty（缺省页样式） | `ac80ff7d5ce0dffbeb1e00a9d9842560f0b87fe9` | 空状态页面 |
| 缺省图 | `0b3ae5a696ee109dbc52a68213f761a9ac647e7f` | 空状态插图 |
| modal | `08ca5eccf00d21155b8df5c5fcda703f143f2109` | 弹窗 |
| modal-confirm | `f2569d7efef7e35e94bcd9cafcb02f8d737ddac0` | 确认弹窗 |
| drawer | `81d7e86b263463558adc43c90b86a968aa803efa` | 抽屉 |
| drawer-非模态 | `97eecc212dddcf5f4f009172400993e77955cc01` | 非模态抽屉 |
| progress-line | `68effa25e1935eb9d56ac61210ac89743f367934` | 条状进度条 |
| process | `c7ab58b1492439865a73a2058e6a5252120c5f5f` | 流程/进度 |
| steps-dot | `26beea44e18d13e1fe76f448602850bf3b9ea658` | 点状步骤条 |

### 页面模板

| 模板 | Key | 状态 |
|------|-----|------|
| 列表页模版 | `845cd88185779896021c1a878eb08358d67d0837` | ComponentSet，变体：`项目=星企通` / `项目=支付机构` |
| 表单页模版 | `8f030a3e7c3525e25e485d70abe2211359b79d75` | ComponentSet，变体：`项目=星企通` / `项目=支付机构` |
| 详情页模版 | `e7249613519a63fe02eae5a36ad95badab635448` | ComponentSet，变体：`项目=星企通` / `项目=支付机构` |
| 空白模版 | `93b6d92fb63324baf093d94726da1e3102bac55c` | ComponentSet，变体：`项目=星企通/支付机构, 页面标题=Default/Tab` |

---

## 缺失 / 待人工确认组件

| 组件 | 状态 | 建议处理 |
|------|------|---------|
| 单元格/percent | 未精确命中 | 涨跌幅使用 `单元格/text` 并绑定涨跌颜色；完成率/进度可使用 `progress-line` |
| table-header 命名 | 未发现独立 `table-header` | 使用 `/table-cell 单元格/header` 作为表头 |
| menu 侧导航 | 存在两个同名 `menu` key | 默认使用较新 key `ee9ca...`，若导入变体不完整则切换备用 key `554e...` |

---

## 搭建页面的工作流

### 0. 页面模版识别（最优先步骤）

生成页面时先判断自然语言描述是否命中以下场景：

| 描述中出现的关键词 | 推荐处理方式 |
|-----------------|------------|
| page_template/列表页模版 | 导入 `列表页模版` ComponentSet：`845cd88185779896021c1a878eb08358d67d0837` |
| page_template/表单页模版 | 导入 `表单页模版` ComponentSet：`8f030a3e7c3525e25e485d70abe2211359b79d75` |
| page_template/详情页模版 | 导入 `详情页模版` ComponentSet：`e7249613519a63fe02eae5a36ad95badab635448` |
| page_template/空白模版 | 导入 `空白模版` ComponentSet：`93b6d92fb63324baf093d94726da1e3102bac55c` |

命中模版时，按以下流程操作：

```javascript
// ① 导入模版组件集
const templateCS = await figma.importComponentSetByKeyAsync(
  '845cd88185779896021c1a878eb08358d67d0837' // 列表页模版
  // 或 '8f030a3e7c3525e25e485d70abe2211359b79d75' 表单页模版
  // 或 'e7249613519a63fe02eae5a36ad95badab635448' 详情页模版
  // 或 '93b6d92fb63324baf093d94726da1e3102bac55c' 空白模版
);

// ② 按项目选择变体
const variant = templateCS.children.find(c =>
  c.name.includes('项目=星企通') // 或 项目=支付机构
) || templateCS.defaultVariant;

// ③ 创建实例并放入页面
const templateInst = variant.createInstance();
figma.currentPage.appendChild(templateInst);
templateInst.x = 0;
templateInst.y = 0;

// ④ 模版类组件允许解绑后定制内容区
const pageFrame = templateInst.detachInstance();
```

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

### 2. 导入并使用 Finloop 组件

```javascript
// 导入组件集（从 AI 运营-组件库远程库）
const menuCS = await figma.importComponentSetByKeyAsync('ee9ca3a0bc5218931b3ba9e62ff93bf7510416bf');
const variant = menuCS.children.find(c =>
  c.name.includes('展开') || c.name.includes('默认')
) || menuCS.defaultVariant;
const inst = variant.createInstance();
parentFrame.appendChild(inst);
inst.x = 0; inst.y = 0;
inst.resize(220, 1080);
```

### 3. 标准列宽参考（1652px 表格总宽）

- 名称列（主列）: 350–480px
- 数据列: 160–220px
- 状态列: 120–180px
- 操作列: 200–350px（按按钮数量调整）

### 4. 优先使用已有组件

若找不到完全匹配的组件，优先选择同类型中最接近的变体，不要手动绘制。若组件在本文件标注为「待补充」，允许临时手动拼装并在最终汇报中列出。

---

### 5. 数字文本 Number 字体强制替换（不可省略）

> 此规则来自 `text-style-ref.md` 全局强制规则，适用于 Finloop 内**所有页面、所有场景**中显示数字的文字节点，不限于表格。

**时机**：向任意数字类文字节点写入内容（`text.set_content`）后，必须立即按 `text-style-ref.md` 流程 1b 执行 `text.update`。

**Finloop 中常见的数字节点场景（示例，非穷举）**：

| 页面 / 区域 | 数字内容示例 | 典型节点位置 |
|------------|------------|------------|
| 列表页 - 表格 | `+21.73%`、`144.62`、`2026/06/01` | 指标列、涨跌幅列、日期列 |
| 运营看板 - 指标卡 | `1,234`、`88.23%`、`¥12,000.00` | 指标数字节点 |
| 详情页 - 数据行 | `NO.001`、`1/6`、`10,000` | 编号、计数、金额 |

**标准执行序列**：

```
① Vibma text.set_content: 写入文字内容
② 按 text-style-ref.md 流程 1b：importStyleByKeyAsync → 获取 styleId
③ Vibma text.update: 对所有数字文字节点批量应用 textStyleId
```

步骤 ①②③ 必须在同一轮工作流中连续完成，不允许只做 ① 而跳过 ②③。

---

## 注意事项

1. **AI 运营平台主操作按钮**：优先使用 `Button渐变`，普通次级按钮、文本按钮仍使用标准 `Button`。
2. **表格组件两套命名**：
   - `/table-cell 单元格/*` — 逐行拼装
   - `/table-column 表格列/*` — 按列拼装
   - `table` — 完整表格组件
3. **变体选择**: 使用 `cs.children.find(c => c.name.includes('关键词'))` 匹配变体。
4. **Tag 颜色语义规范**（`标签样式3` 和 `单元格/tag` 均适用）：
   - 灰色：中性分类标签、禁用/次要/已结束状态
   - 蓝色：中性信息、进行中、待审核
   - 绿色：正向/成功/可用状态
   - 红色：错误/高风险/紧急状态
   - 黄色：警告/提醒/待确认
5. **涨跌幅颜色规范**（中国金融惯例：涨红跌绿）：
   - 涨幅（正值）：红色语义变量；若变量 key 未补齐，先使用库内红色文本样式或色值并标注
   - 跌幅（负值）：绿色语义变量；若变量 key 未补齐，先使用库内绿色文本样式或色值并标注
   - 不要使用进度条组件展示涨跌幅，使用 `单元格/text` 并绑定对应颜色
6. **数值文本样式规范（Number 样式）**：参见 `text-style-ref.md` 数字字体使用规范。
7. **组件解绑规范**：
   - 允许解绑：页面骨架、弹窗、抽屉等用于承载业务内容的结构类组件
   - 禁止随意解绑：筛选器、按钮、表格单元格、表头、输入框等原子/分子级组件
   - 修改组件文字：始终通过文本操作，不要解绑后修改
8. **本地组件母版必须填充示例数据**：
   - `headerRow`：所有表头文字必须替换为实际列名
   - `dataRow`：所有单元格必须填入一条有代表性的真实样例数据
   - tag 类单元格需同时完成颜色 swap 和文案写入
9. **页面模版使用限制与退回策略**：
   - 模板 key 未补齐前，不要引用 FinEAM 的模板 key
   - 直接按标准页面框架拼装，或在最终汇报中说明「页面模板待补充」
10. **重复元素封装为本地组件**：
    - 表格数据行、表头行、卡片列表项等重复结构应先构建本地组件，再实例化复用
11. **组件宽度设置规范**：
    - `筛选`、`search-box`、`Button`、`input`、`datepicker` 等默认保持 HUG/AUTO
    - 表头行与表格数据行需要根据列内容设置固定宽度或 Fill
12. **表格行单元格高度对齐规范**：
    - 混排双行文本和单行文本时，确保同一行内所有单元格高度一致
13. **自动布局与忽略自动布局规范**：
    - 普通内容元素一律参与自动布局
    - 只有浮层、角标、悬浮操作等需要覆盖的元素才设置绝对定位
