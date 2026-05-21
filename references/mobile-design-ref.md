# 移动端设计参考 · 组件速查 & 界面拼装指南

## 前提：必须先读取 figma-use skill

- **组件库文件 key**: `UvkJyLQtSdLqE87NOLISth`
- **导入方式**: `figma.importComponentSetByKeyAsync(componentKey)`
- 需在目标文件的 `use_figma` 中指定目标文件的 `fileKey`,组件通过 key 从远程库导入

---

## 页面创建规范（必读）

### 1. 页面类型定性与模版使用

**页面类型分类**：
- **表单页**：包含表单输入的页面（如开户申请、信息填写）
- **列表页**：展示多条数据的页面（如基金列表、订单列表）
- **详情页**：展示单条数据详情的页面（如基金详情、订单详情）
- **混合页**：包含多种内容类型的页面

**可用页面模版**（组件库 Templates 页）：

| 模版名称 | Component Key | 适用场景 |
|---------|--------------|---------|
| 表单页 | 9453a9c2cce6f335a0fb1a9c913f9b487d387d9d | 含表单输入项 + 操作按钮的标准表单页 |
| 列表页 | 2aec5ce98819674cf797e4242dbe4218dae25a54 | 含列表展示 + 筛选/搜索的标准列表页 |
| 详情页 | 410e66537de6f19e4fcb8952a477f0a4d7d3235d | 含详情信息展示的标准详情页 |

**模版使用策略**（参考 FinEAM 模版使用流程）：

1. **判断是否命中模版**：
   - 表单页：包含多个表单输入项（Input/Select/Upload/Checkbox 等）+ 提交按钮
   - 列表页：包含列表数据展示（list + list-items）
   - 详情页：包含信息卡片 + 详情字段展示
   
2. **导入模版组件**：
   ```javascript
   // 导入模版组件（单一组件，非 ComponentSet）
   const templateComp = await figma.importComponentByKeyAsync('TEMPLATE_KEY');
   
   // 创建实例并放入页面
   const templateInst = templateComp.createInstance();
   templateInst.x = 0;
   templateInst.y = 0;
   figma.currentPage.appendChild(templateInst);
   ```

3. **解绑模版实例**：
   ```javascript
   // 模版类组件允许解绑
   const pageFrame = templateInst.detachInstance();
   ```

4. **修改模版内容**：
   - 找到对应的内容区域（通过节点名称查找）
   - 清空占位内容
   - 填入实际业务组件和数据

**模版结构说明**：

**表单页模版结构**：
```
├── Status bar - iPhone (顶部状态栏)
├── NavBar (返回按钮 + 标题)
├── step 步骤指示器 (可选)
├── 表单标题 (Form Name)
├── 内容滚动区
│   ├── 多个 form-item (表单项)
│   ├── 身份证上传 (可选)
│   └── 多选项/按钮式选项 (可选)
├── bottom 操作按钮区 (上一步 + 下一步)
└── Home Indicator
```

**使用模版后的注意事项**：
- 模版解绑后已包含 NavBar、Status bar、Home Indicator、bottom 按钮区的完整骨架，**不再单独导入这些组件**
- 只需操作内容滚动区，导航栏/底部按钮保持不动
- 若描述中没有明确命中模版关键词，退回到逐组件拼装方式

### 2. 页面框架变量绑定（必须）

**页面 Frame 必须绑定以下变量**：
- **背景色**：绑定 `bg/primary` 变量 (VariableID:44:106)


**变量绑定方式**：

⚠️ **重要**：组件库已作为 Library 发布并启用，可以直接引用库中的变量。

```javascript
// 步骤 1: 从组件库获取变量
// 使用 VariableID 直接获取库变量
const bgPrimary = await figma.variables.getVariableByIdAsync('44:106'); // bg/primary
const textPrimary = await figma.variables.getVariableByIdAsync('44:101'); // text/primary
const textSecondary = await figma.variables.getVariableByIdAsync('44:102'); // text/secondary

// 步骤 2: 绑定变量到节点
// 绑定页面背景色
pageFrame.fills = [{
  type: 'SOLID',
  color: { r: 1, g: 1, b: 1 },
  boundVariables: { color: { type: 'VARIABLE_ALIAS', id: bgPrimary.id } }
}];

// 绑定文本颜色（非组件文本节点）
textNode.fills = [{
  type: 'SOLID',
  color: { r: 0, g: 0, b: 0 },
  boundVariables: { color: { type: 'VARIABLE_ALIAS', id: textPrimary.id } }
}];
```

**可用变量列表**（从组件库 UvkJyLQtSdLqE87NOLISth）：

**颜色变量**：
- `text/primary` (VariableID:44:101) - 主文本颜色
- `text/secondary` (VariableID:44:102) - 次要文本颜色
- `text/tertiary` (VariableID:44:103) - 第三级文本颜色
- `text/link` (VariableID:44:104) - 链接文本颜色
- `text/inverse` (VariableID:44:105) - 反色文本
- `bg/primary` (VariableID:44:106) - 页面背景
- `bg/secondary` (VariableID:44:107) - 次级背景
- `bg/tertiary` (VariableID:44:108) - 第三级背景
- `border/primary` (VariableID:44:109) - 主边框颜色
- `border/secondary` (VariableID:44:110) - 次级边框颜色

**间距变量**：
- `component/page-padding` (VariableID:959:756) - 页面左右内边距
- `component/form-padding` (VariableID:1006:3577) - 表单内边距

### 3. 非组件文本样式（必须）

**所有非组件的文本节点必须应用组件库预设的文本样式**，不能直接设置 `fontSize` 和 `fontName`。文字样式 Key、操作流程及数字字体规范统一参见 `text-style-ref.md`。

### 4. 非组件元素颜色变量（必须）

**所有非组件元素（如手动创建的 Text、Frame）必须绑定颜色变量**，不能使用硬编码的颜色值。

**文本颜色绑定方式**：
```javascript
// 从组件库获取颜色变量（使用 VariableID）
const textPrimary = await figma.variables.getVariableByIdAsync('44:101'); // text/primary

// 绑定文本颜色到变量
textNode.fills = [{
  type: 'SOLID',
  color: { r: 0, g: 0, b: 0 }, // 默认颜色
  boundVariables: { color: { type: 'VARIABLE_ALIAS', id: textPrimary.id } }
}];
```

**常用文本颜色变量**：
| 变量名称 | VariableID | 用途 |
|---------|-----------|------|
| text/primary | 44:101 | 主文本颜色（标题、正文） |
| text/secondary | 44:102 | 次要文本颜色（辅助说明） |
| text/tertiary | 44:103 | 第三级文本颜色（占位符、禁用文本） |
| text/link | 44:104 | 链接文本颜色 |
| text/inverse | 44:105 | 反色文本（深色背景上的文字） |

**背景色/填充色变量**：
| 变量名称 | VariableID | 用途 |
|---------|-----------|------|
| bg/primary | 44:106 | 主背景色（页面背景） |
| bg/secondary | 44:107 | 次级背景色（卡片背景） |
| bg/tertiary | 44:108 | 第三级背景色（区块背景） |
| border/primary | 44:109 | 主边框颜色 |
| border/secondary | 44:110 | 次级边框颜色 |

**颜色变量选择原则**：
- **页面标题/正文**：使用 `text/primary`
- **辅助说明/次要信息**：使用 `text/secondary`
- **占位符/禁用状态**：使用 `text/tertiary`
- **链接/可点击文本**：使用 `text/link`
- **Frame 背景**：使用 `bg/primary`、`bg/secondary`、`bg/tertiary`
- **边框**：使用 `border/primary`、`border/secondary`

⚠️ **重要提醒**：
- 创建任何非组件元素时，**必须先绑定颜色变量**，再设置文本内容
- 不要使用硬编码的 RGB 值，如 `{ r: 0, g: 0, b: 0 }`
- 直接使用组件库的 VariableID 通过 `getVariableByIdAsync()` 获取变量
- 组件库已作为 Library 发布并启用，所有变量可直接引用

### 5. 组件变体属性检查（必须）

**导入组件实例后，必须检查变体属性，隐藏或调整不必要的元素**：

**常见需要调整的组件**：
- **form-item**：根据 `type` 变体，某些子元素可能不需要显示
  - 检查是否有多余的 Label、提示文字等
  - 检查是否有"拍照提示"区域需要显示/隐藏
- **bottom**：根据 `类型` 变体，调整按钮数量
  - `类型=单按钮`：隐藏第二个按钮
  - `类型=组合按钮`：确保两个按钮都可见
- **list**：根据实际列表项数量，隐藏多余的 list-items 实例
- **step**：根据步骤数量，调整 step-Atoms 的显示

**检查方式**（use_figma）：
```javascript
// 遍历实例的子节点
const instance = await figma.getNodeByIdAsync('INSTANCE_ID');
instance.findAll(n => {
  // 检查不需要的元素并隐藏
  if (n.name.includes('不需要的元素名')) {
    n.visible = false;
  }
  return false;
});
```

**或使用 Vibma 修改**（推荐）：
```javascript
// 通过 Vibma 批量隐藏元素
vibma.frames.update({
  items: [{ id: 'NODE_ID', visible: false }]
});
```

---

## 标准页面框架(375×812)

### 页面尺寸规范

- **宽度**：固定 375px（iPhone 标准宽度）
- **高度**：适应内容，最小 812px
  - 使用 Auto Layout，`layoutMode: 'VERTICAL'`
  - `primaryAxisSizingMode: 'AUTO'`（垂直方向自适应内容）
  - `counterAxisSizingMode: 'FIXED'`（水平方向固定 375px）
  - `minHeight: 812`（最小高度约束）

### 页面结构

```
├── Status bar - iPhone (375×62)         顶部状态栏
├── NavBar 导航栏 (375×54)                顶部导航
├── 内容区 (可滚动)                       左右间距使用 page-padding 变量
│   ├── 列表项(ListItem)
│   ├── 卡片(Card)
│   └── 表单(Form)
├── Tabbar 底部标签栏 (375×60)            底部导航（可选）
└── Home Indicator (375×34)              底部指示条
```

**创建页面 Frame 的标准代码**：
```javascript
const pageFrame = figma.createFrame();
pageFrame.name = '页面名称 (路由路径)';
pageFrame.resize(375, 812); // 初始尺寸

// 设置为垂直自适应 Auto Layout
pageFrame.layoutMode = 'VERTICAL';
pageFrame.primaryAxisSizingMode = 'AUTO'; // 垂直自适应
pageFrame.counterAxisSizingMode = 'FIXED'; // 水平固定
pageFrame.minHeight = 812; // 最小高度
pageFrame.itemSpacing = 0;
pageFrame.paddingLeft = 0;
pageFrame.paddingRight = 0;
pageFrame.paddingTop = 0;
pageFrame.paddingBottom = 0;
```

### 变体选择规则

**NavBar 导航栏** - 常用变体:
- 默认样式: `Type=default, HasBack=true, HasAction=1`
- 透明背景: `Type=transparent, HasBack=true, HasAction=1`
- 无返回按钮: `Type=default, HasBack=false, HasAction=0`

**Button** - 常用变体:
- 主操作: `Type=primary, Size=48px, State=default`
- 次要操作: `Type=secondary, Size=48px, State=default`
- 文本按钮: `Type=text, Size=48px, State=default`
- 危险操作: `Type=danger, Size=48px, State=default`
- 幽灵按钮: `Type=ghost, Size=48px, State=default`

**Input 输入框** - 常用变体:
- 文本输入: `Type=text, State=default, size=md-48`
- 搜索框: `Type=search, State=default, size=md-48`
- 密码输入: `Type=password, State=default, size=md-48`

---

## 核心组件 Key 速查

### 原子组件 (Atoms)

| 组件 | 说明 | 常用变体关键词 |
|------|------|--------------|
| Tag | 标签 | `Type=filled/outlined, Size=md/sm, Color=neutral/blue/green/red/yellow/orange` |
| Avatar | 头像 | `Type=initials/image/icon, Size=md/sm/lg/xl/xs` |
| Button | 按钮 | `Type=primary/secondary/tertiary/ghost/danger/text, Size=48px/44px/40px/36px/32px/28px/24px, State=default/pressed/disabled` |
| Skeleton | 骨架屏 | `Type=line/circle/rect, Size=sm/md/lg` |

### 表单组件 (Forms)

| 组件 | 说明 | 常用变体关键词 |
|------|------|--------------|
| Checkbox | 复选框 | `Size=md/sm/xs, State=default/checked/indeterminate/disabled-off/disabled-on` |
| Switch | 开关 | `Size=md/sm, State=off/on/disabled-off/disabled-on` |
| Input | 输入框 | `Type=text/password/search, State=default/focus/filled/error/disabled, size=md-48/sm-40` |
| MoneyInput | 金额输入 | `Size=lg, State=default/filled/error` |
| Select | 选择器 | `Size=48px/40px, State=default/active/filled/error/disabled/disabled-filled` |
| Upload | 上传 | 单一组件 |
| 身份证上传 | 证件上传 | `地区=香港/内地, 状态=未上传/已上传` |
| 选项 | 选项组件 | `类型=checkbox式/按钮式, 状态=未选/已选` |
| form-item | 表单项容器 | `type=Input/select/upload-default/upload-identify/多选项-默认/按钮式选项` |

### 导航组件 (Navigation)

| 组件 | 说明 | 常用变体关键词 |
|------|------|--------------|
| NavBar | 顶部导航栏 | `Type=default/transparent, HasBack=true/false, HasAction=0/1` |
| Tabbar | 底部标签栏 | `actived=账号/我的` |
| tabbar-atom | 底部标签项 | `actived=true/false` |
| Status bar - iPhone | iOS 状态栏 | 单一组件 |
| Home Indicator | 底部指示条 | 单一组件 |
| top | 顶部区域 | 单一组件 |
| bottom | 底部区域 | `类型=单按钮/组合按钮` |
| actions | 操作区 | `类型=操作, 数量=1/2` |
| Segmented control | 分段控制器 | 单一组件 |
| step | 步骤条 | 单一组件 |
| step-Atoms | 步骤项 | `State=Active/completed/Default` |

### 展示组件 (Display)

| 组件 | 说明 | 常用变体关键词 |
|------|------|--------------|
| ListItem | 列表项 | `Type=default, HasLeft=true/false, HasRight=true/false` |
| EmptyState | 空状态 | `Type=default/error, HasAction=true/false` |
| table-header | 表格表头 | `对齐=左对齐/右对齐` |
| table-cell | 表格单元格 | `类型=两行文本/单行文本/单行数值/两行数值, 对齐=左对齐/右对齐` |
| logo&flag | 标识与旗帜 | `类型=bank/flag, flag=招商/工商/渣打/汇丰/恒生/勇亨/CNA/US/HK/AU/EU/GB/CA/JP/SG` |
| list-items | 列表项 | `type=bank/Normal/CountryCode/message/左数据+右状态/左右布局, status=selected/default` |
| list | 列表容器 | `type=BankList/Default, has-logo=true/false/has-logo3/has-logo4, text=1-text/2-text` |

### 反馈组件 (Feedback)

| 组件 | 说明 | 常用变体关键词 |
|------|------|--------------|
| NoticeBar | 通知栏 | `Type=info/success/warning/error, HasIcon=true/false` |
| Modal | 对话框 | `Type=alert/confirm, HasCancel=true/false, title=true/false, description=true/false` |
| Toast | 轻提示 | `Type=text/icon/loading` |
| 日期选择器 | 日期选择 | `范围选择=true/false/范围选择3, 快捷选项=true/false` |
| BottomSheet | 底部弹出层 | `logo=true/false, type=list/blank/text` |
| 安全密钥 | 密码输入 | `状态=default/filled/filled-visable` |

### 金融组件 (Finance)

| 组件 | 说明 | 常用变体关键词 |
|------|------|--------------|
| PriceChange | 价格变动 | `Direction=up/down/flat, Format=percent, Size=sm/md` |
| RiskBadge | 风险等级 | `Level=R1/R2/R3/R4/R5, Size=sm/md` |
| FundCard | 基金卡片 | `Type=standard/compact, State=default/held` |
| AssetSummaryCard | 资产汇总卡片 | `Type=total/allocation, Privacy=visible/hidden` |
| StockQuoteRow | 股票报价行 | `Market=A/HK, Direction=up/down` |
| OrderStatusBadge | 订单状态 | `Status=pending/filled/cancelled/partial/failed, Size=sm` |

---

## 搭建页面的工作流

### 1. 在目标文件中获取页面信息
```javascript
// 找到目标页面
for (const page of figma.root.children) {
  await figma.setCurrentPageAsync(page);
  const found = await figma.getNodeByIdAsync('PAGE_OR_FRAME_ID');
  if (found) { /* 找到正确页面 */ break; }
}
```

### 2. 导入并使用移动端组件
```javascript
// 导入组件集(从移动端远程库)
const buttonCS = await figma.importComponentSetByKeyAsync('BUTTON_COMPONENT_KEY');
const variant = buttonCS.children.find(c => 
  c.name.includes('Type=primary') && c.name.includes('Size=48px')
) || buttonCS.defaultVariant;
const inst = variant.createInstance();
parentFrame.appendChild(inst);
inst.x = 0; inst.y = 0;
```

### 3. 标准页面尺寸
- 设备宽度: 375px (iPhone 标准宽度)
- 设备高度: 812px (iPhone X 系列)
- 状态栏高度: 62px
- NavBar 高度: 54px
- Tabbar 高度: 60px
- Home Indicator 高度: 34px

### 4. 优先使用已有组件
若找不到完全匹配的组件,优先选择同类型中最接近的变体,不要手动绘制。

---

## 注意事项

1. **组件字体处理规范** - 该库使用系统字体，插件无法加载
   - **禁止直接修改**：不要修改组件内文本的 `fontName` 属性
   - **禁止解绑修改**：不要通过 `detachInstance()` 解绑后修改字体
   - **正确做法**：参见 `text-style-ref.md` 组件文本流程（流程 1）

2. **非组件元素样式规范**：
   - **文本样式**：非组件的独立文本节点，必须使用组件库中预设的文本样式（Key 及操作流程参见 `text-style-ref.md`，数字内容使用 Number 系列样式）
   - **颜色变量**：所有非组件元素（Text、Frame 等）必须绑定颜色变量，不能使用硬编码的 RGB 值
   - **变量优先级**：创建元素时，先绑定变量（背景色、文本色），再设置内容

3. **移动端适配规范**:
   - 所有组件宽度以 375px 为基准设计
   - 触摸区域最小 44px×44px
   - 文字大小建议不小于 24px(移动端 12pt)

4. **变体选择**: 使用 `cs.children.find(c => c.name.includes('关键词'))` 匹配变体

5. **Tag 颜色语义规范**:
   - **neutral(灰色)**: 中性分类标签,无状态含义
   - **blue(蓝色)**: 中性信息,带程度/状态含义
   - **green(绿色)**: 正向/成功/低风险
   - **red(红色)**: 高风险/错误/紧急
   - **yellow(黄色)**: 警告/提醒/待确认
   - **orange(橙色)**: 中等提醒
   - **cyan/teal/navy/pink/purple**: 特殊场景的分类标识

6. **涨跌幅颜色规范**(中国金融惯例:涨红跌绿):
   - 涨幅(正值): 使用 `Direction=up` 的 PriceChange 组件(红色)
   - 跌幅(负值): 使用 `Direction=down` 的 PriceChange 组件(绿色)
   - 持平: 使用 `Direction=flat` 的 PriceChange 组件(灰色)

7. **风险等级颜色规范**:
   - R1(低风险): 蓝色
   - R2(中低风险): 浅蓝/绿色
   - R3(中等风险): 黄色
   - R4(中高风险): 橙色
   - R5(高风险): 红色

8. **表单项组合规范**:
   - 使用 `form-item` 组件包裹表单控件
   - `form-item` 已包含 label 和控件容器
   - 根据表单类型选择对应的 `type` 变体

9. **列表项组合规范**:
   - 使用 `list` 容器包裹多个 `list-items`
   - 根据业务场景选择合适的 `type` 和 `has-logo` 组合
   - 列表项支持左侧图标、中间内容、右侧状态/箭头等布局

10. **底部弹出层规范**:
   - 使用 `BottomSheet` 组件
   - 根据内容类型选择 `type=list/blank/text`
   - 有品牌标识时设置 `logo=true`
   - 底部弹出层默认从屏幕底部向上展开

11. **页面布局层次**:
    ```
    Frame (375×812) - 页面容器
    ├── Status bar - iPhone (顶部固定)
    ├── NavBar (顶部固定)
    ├── ScrollView (内容滚动区)
    │   └── 内容组件
    ├── Tabbar (底部固定,可选)
    └── Home Indicator (底部固定)
    ```

12. **安全区域**:
    - 顶部安全区: 状态栏 + 导航栏
    - 底部安全区: Tabbar + Home Indicator
    - 内容区需避开安全区域,确保可见性

13. **组件解绑规范**:
    不要随意解绑(detach)组件实例,解绑后将失去与主组件的关联。
    - **允许解绑**: 页面级模板、弹窗(Modal/BottomSheet)
    - **禁止解绑**: 原子组件(Button、Input、Tag 等)、表单组件、列表项等
    - **修改组件文字**：始终通过文本操作（参见 `text-style-ref.md`），不要解绑后修改

14. **重复元素封装为本地组件**:
    当页面中某个组合结构需要重复出现多次,应先用原子组件将其构建为**本地组件(Local Component)**,再通过实例化引用。
    
    **典型适用场景**:
    - 列表项(多个 list-items 横向排列)
    - 自定义卡片(图片+标题+描述组合)
    - 表单行(label + input 组合)

15. **移动端特有组件**:
    - **Home Indicator**: iOS 设备底部的横条指示器
    - **Status bar**: 显示时间、电量、信号等系统信息
    - **Tabbar**: 底部标签栏导航,移动端常用的主导航方式
    - **BottomSheet**: 移动端常用的交互模式,从底部向上滑出

16. **触摸反馈**:
    - 所有可交互元素需要明确的 `State=pressed` 变体
    - 按钮需提供 `default/pressed/disabled` 三态
    - 列表项需提供 `default/selected` 状态

---

## 移动端页面类型

### 列表页
适用于展示多条数据,如基金列表、订单列表等。

**标准结构**:
- NavBar(返回按钮 + 标题)
- 搜索框/筛选器(可选)
- list 容器 + 多个 list-items
- Tabbar(可选)

### 表单页
适用于数据录入,如开户申请、信息填写等。

**标准结构**:
- NavBar(返回按钮 + 标题)
- 多个 form-item
- bottom 区域(提交按钮)

### 详情页
适用于展示单条数据详情,如基金详情、订单详情等。

**标准结构**:
- NavBar(返回按钮 + 标题 + 操作按钮)
- 头部信息卡片(FundCard/AssetSummaryCard)
- 详情信息区(ListItem 组合)
- bottom 区域(操作按钮,可选)

### 首页/Tab 页
多 Tab 切换,每个 Tab 对应不同内容。

**标准结构**:
- Status bar
- top 区域(品牌/搜索)
- Segmented control(Tab 切换器,可选)
- 内容区(根据 Tab 切换)
- Tabbar(底部导航)
- Home Indicator

---

## 与 PC 端(FinEAM)的差异

| 特性 | 移动端 | PC 端(FinEAM) |
|------|--------|--------------|
| 屏幕尺寸 | 375px 宽 | 1920px 宽 |
| 主导航 | 底部 Tabbar | 左侧 menu 侧导航 |
| 顶部 | NavBar(54px) | navbar 顶部栏(48px) + 页签 |
| 交互方式 | 触摸(最小 44px) | 鼠标(最小 32px) |
| 弹窗 | BottomSheet(底部弹出) | Modal(居中弹窗) |
| 表格 | table-cell(单元格) | 完整 table 组件 |
| 字号 | 最小 24px(12pt) | 最小 12px |
| 组件密度 | 较疏松,间距大 | 紧凑,信息密度高 |

