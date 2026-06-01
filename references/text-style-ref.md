# 文字样式参考 (Text Style Reference)

## 前置：Vibma 连接检查

**每次执行文字相关操作前，必须先验证 Vibma 连接状态。**

```typescript
// 检查连接
CallMcpTool(server: "user-Vibma", toolName: "connection", arguments: { method: "get" })
```

- 若返回 `{ status: "pong" }` → 已连接，继续执行
- 若返回错误 `No channel joined` → **停止操作**，提示用户：
  > 请在 Figma 中打开 Vibma 插件，点击 Connect 后告知我，再继续操作。

---

## 文字操作三类流程

### 流程 1：组件文本 — 内容替换（最常用）

适用：已存在的组件实例内部文字节点，只需更新文案，不改变样式。

```typescript
// Vibma: 批量替换文字内容
text.set_content([
  { nodeId: "节点ID", text: "新文案" },
  { nodeId: "节点ID2", text: "新文案2" }
])
```

> ⚠️ 默认情况下不要对组件内部文字节点使用 `text.update` 改样式，保持组件实例的样式绑定不变。
> **例外规则（数字字体）**：若组件内部文字节点显示的是数字内容（如金额、日期、编号、计数、百分比等），**必须**额外执行流程 1b，将其字体改为对应的 Number 系列样式（MiNum 等宽字形）。此规则优先于「不改样式」约定。

---

### 流程 1b：组件数字文本 — 强制换用 Number 字体（数字内容专用）

适用：组件实例内部显示数字的文字节点（即使不更换文案也要执行）。

**判断标准**：文本内容为以下类型时，必须更换为 Number 系列样式：
- 纯数字：`123`、`4211251995024929`
- 日期：`1988-02-18`、`2024/12/31`
- 金额：`¥1,234.56`
- 百分比：`+5.2%`
- 计数：`1/6`、`0/4`
- 混合含数字：`SHAN`（纯英文字母不算）

**Step 1**：用 Key 导入 Number 系列样式，拿到 style.id：
```typescript
// 根据字号选择合适的 Number 样式 Key（见下方快速选样式）
use_figma: const style = await figma.importStyleByKeyAsync("Number样式Key");
// → 返回 style.id
```

**Step 2**：用 Vibma 对目标节点更新字体样式（保留文案内容）：
```typescript
text.update([
  { id: "数字文字节点ID", textStyleId: "style.id" }
])
```

> ✅ 此操作只修改字体样式，不影响文案内容，可与 `set_content` 配合使用。
> ✅ 对于同一字号，选用与当前节点字号相同的 Number 系列样式。不确定字号时，先用 `text.get` 检查当前字号再选样式。

---

### 流程 2：非组件文本 — 创建并绑定样式

适用：新建独立文字节点，需要绑定库样式。

> **关于 style.id 与 Key 的区别**：
> - **Key**（本文件存储的值）：全局唯一、跨文件永久稳定，可放心存入本文件复用。
> - **style.id**（`S:KEY,nodeId` 格式）：**每个目标设计文件不同**，不能跨文件复用，**不要存入本文件**。每次切换工作文件都需要重新 `importStyleByKeyAsync` 获取。

**Step 1**（每次在新目标文件中首次使用该样式时执行）：
```typescript
// plugin-figma-figma: 用 Key 导入远程库样式，拿到当前文件可用的 style.id
use_figma: const style = await figma.importStyleByKeyAsync("此处填本文件中存储的 Key");
// → 返回 style.id，格式为 "S:KEY,当前文件特有的nodeId"，仅在本次会话/当前文件使用
```

**Step 2**（拿到 style.id 后立即使用）：
```typescript
// Vibma: 创建文字节点并绑定样式
text.create([{
  characters: "文字内容",
  textStyleId: style.id,  // Step 1 刚获取的 id，不要缓存到文件
  parentId: "父节点ID",
  x: 0,
  y: 0
}])
```

> ✅ 不要手动设置 `fontName`，让 Vibma 通过 `textStyleId` 自动应用正确字体（含 PingFang SC）。

---

### 流程 3：样式绑定 — 对已有节点绑定样式

适用：已存在的独立文字节点需要更换或绑定库样式。

```typescript
// Vibma: 更新节点的样式绑定
text.update([{
  id: "节点ID",
  textStyleId: "S:KEY,fileNodeId"
}])
```

---

## Key 与 style.id 的区别

| | Style Key | style.id |
|---|---|---|
| **存储位置** | ✅ 本文件 | ❌ 不存储 |
| **稳定性** | 永久稳定，跨文件通用 | 每个目标文件不同，会话结束即废弃 |
| **获取方式** | Figma 库发布时固定 | 运行时 `importStyleByKeyAsync(key)` 获取 |
| **用途** | 作为 `importStyleByKeyAsync` 的入参 | 作为 Vibma `text.create/update` 的 `textStyleId` 入参 |

---

## Web 端组件库

### FinEAM 组件库

- **Figma 文件**：https://www.figma.com/design/QxrzU4jigzG5OO4SsxPwJT/FinEAM-组件
- **Library Key**：`lk-a0a28399889d96c53a9513d5ee042ef4083387fe1bac69b3f23da3e1f9ed5e66a96cc257d0841853b7b0b4fd1bc544f95ce5f511e1438c66b5ef64f09670c487`
- **字体**：中文 PingFang SC / 英文 Arial / 数字 MiNum

#### 辅助文字（12px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `辅助/12/CN-Regular` | PingFang SC Regular | `7ede3bc055657b4675cd87bd00cc9a3adeadd8c8` |
| `辅助/12/CN-Medium` | PingFang SC Medium | `f5a86f4334527e63db24d9f1c6a42f42b8561904` |
| `辅助/12/EN-Regular` | Arial Regular | `37159baad84d7fa6e167cf8bf1bc5f5538b902b1` |
| `辅助/12/Number-Regular` | MiNum Regular | `dffa90e4589cc23e143783631397a833294bcb51` |
| `辅助/12/Number-Medium` | MiNum Medium | `6249ca1f115479330b2b1acb44d1812d9378ff8c` |

#### 正文（14px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `正文/14/CN-Regular` | PingFang SC Regular | `2ba3463ee945f53bb91d7e70f5a435fb7642f3b1` |
| `正文/14/CN-Medium` | PingFang SC Medium | `834abb90885c1a3a691da5a78e53c7b64ef85419` |
| `正文/14/EN-Regular` | Arial Regular | `6eaf614a15de4812844e5199e5d070514bb8631d` |
| `正文/14/Number-Regular` | MiNum Regular | `6146b3764aacd5ba79e7f5c42f2d32034bd3787e` |
| `正文/14/Number-Medium` | MiNum Medium | `8b49fd3a878c6f84f5289fb7fee2b2b6a3ddf7e0` |

#### 标题/小（16px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `标题/小-16/CN-Regular` | PingFang SC Regular | `176848aeda0f10f86c87b7bfe09e09e83c9b60f2` |
| `标题/小-16/CN-Medium` | PingFang SC Medium | `7dabac9ca4ccce6cd3f121e661d1c715a72c80d4` |
| `标题/小-16/EN-Regular` | Arial Regular | `66487ee5b4d0e78bcd04d1d0cd8941eea117ae34` |
| `标题/小-16/Number-Regular` | MiNum Regular | `0ecd7735d2be02847e8c8b3cbe0bae45388040ff` |
| `标题/小-16/Number-Medium` | MiNum Medium | `e3e44b85acb82c247bf681a14d0d9cf7956901f8` |

#### 标题/中（18px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `标题/中-18/CN-Regular` | PingFang SC Regular | `e4a2a88a925c8985289d7c69adfb5ba543acb4db` |
| `标题/中-18/CN-Medium` | PingFang SC Medium | `12bb25cf00b3085ca635472db73605a611237f04` |
| `标题/中-18/EN-Regular` | Arial Regular | `955320ee68fe2347d8cf8676a640cc4b3a57d689` |
| `标题/中-18/Number-Regular` | MiNum Regular | `70a978372769b309a43d16bc2925fa00e226dfc0` |
| `标题/中-18/Number-Medium` | MiNum Medium | `d986da73259719a89f52ad6b2de4ba15dbd4fd14` |

#### 标题/大（20px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `标题/大-20/CN-Regular` | PingFang SC Regular | `a199fe008af774644fc76de03c5f2e1c0001b840` |
| `标题/大-20/CN-Medium` | PingFang SC Semibold | `0ad0ff597d87bbb604df4ffe8c5eda938dca1e5e` |
| `标题/大-20/EN-Regular` | Arial Regular | `3b6fad02e9b693b1ddba7368c777bba5aa68e35f` |
| `标题/大-20/Number-Regular` | MiNum Regular | `4e156e7622ab26bb56e3b0665c64c058eb0993f0` |
| `标题/大-20/Number-Medium` | MiNum Medium | `bf03f97101273fc0a77726c49d35aaef9c1410b6` |

#### 标题/大（24px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `标题/大-24/CN-Regular` | PingFang SC Regular | `12e8b6e17210517f6237677bf3850b23ca473279` |
| `标题/大-24/CN-Medium` | PingFang SC Semibold | `b9b3f5bc72c269b43fb26850d9acf820abc9c059` |
| `标题/大-24/EN-Regular` | Arial Regular | `3fd88411c6b7272197a273a1494f9511cc1c7512` |
| `标题/大-24/Number-Regular` | MiNum Regular | `025826ac913ec310a596a1053952f994310ee9dd` |
| `标题/大-24/Number-Medium` | MiNum Medium | `85db116bd74dbc89f83fd503b4e308882ae8fccc` |

#### 运营标题/小（32px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `运营标题/小-32/CN-Regular` | PingFang SC Regular | `71ce07ca85751929829b4753591c48d17d3d62ec` |
| `运营标题/小-32/CN-Medium` | PingFang SC Medium | `1d434475d30cedab4e73930d6b96f9cd60accb7f` |
| `运营标题/小-32/EN-Regular` | Arial Regular | `22ed1de6aedf8f29abdcc864371fd9fbdfac2bbe` |
| `运营标题/小-32/Number-Regular` | MiNum Regular | `4b4d3202b0f3e83e7c40c15ecb3b514b25a76f70` |
| `运营标题/小-32/Number-Medium` | MiNum Medium | `ed84c8bae0e9b7eafd4081bc18b6a764eb35be94` |

#### 运营标题/中（36px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `运营标题/中-36/CN-Regular` | PingFang SC Regular | `d21a79a619c6e23b3f73f11da5378039b9719100` |
| `运营标题/中-36/CN-Medium` | PingFang SC Medium | `a00212ea5c7e735187b645c49271480ece4dfea5` |
| `运营标题/中-36/EN-Regular` | Arial Regular | `2d5276da481b3b1d301b1c535f834633bbdcefe1` |
| `运营标题/中-36/Number-Regular` | MiNum Regular | `d1f96fad969ee6ed1832e43b86e6d3d940c7dfe8` |
| `运营标题/中-36/Number-Medium` | MiNum Medium | `6b699d3b366bfe8296d97d669aa98ada493754ac` |

#### 运营标题/大（48px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `运营标题/大-48/CN-Regular` | PingFang SC Regular | `b9185dd52a13de861b57e12f4560e430835561df` |
| `运营标题/大-48/CN-Medium` | PingFang SC Medium | `b3b9199c76a4b7598c95dbe5ed3e21282b804693` |
| `运营标题/大-48/EN-Regular` | Arial Regular | `0d6bc72716cfe82fa2221b395351b28344fdae8d` |
| `运营标题/大-48/Number-Regular` | MiNum Regular | `e91e14123b8c1cd66c1460156443e67dab1b1ac4` |
| `运营标题/大-48/Number-Medium` | MiNum Medium | `9a28ca40f29a2c0eaa1ab19601b1036eb78cad19` |

### FAI 组件库

- **Figma 文件**：https://www.figma.com/design/1IzJjE812UGoArwoWH09wo/F-AI-%E7%BB%84%E4%BB%B6%E5%BA%93?node-id=103-331&p=f&t=ER44RbjkAnHxnAR5-0
- **Library Key**：`lk-ddbfedc1416a33d371c04333ac8f745d7cb624efcce11d3a6572ffd4da22eacd5387abf92b3ada51aaf40d91a42eac04910778884be5ba1362b3c0c36ffdffeb`
- **字体**：中文 PingFang SC / 英文 Arial / 数字 MiNum

#### 辅助文字（12px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `辅助/12/CN-Regular` | PingFang SC Regular | `6eacad865a12cbe228e81a537402b02c93758a2d` |
| `辅助/12/CN-Medium` | PingFang SC Medium | `418662e6d6e8634c1be2c2b677ff0b5e1f8edee0` |
| `辅助/12/EN-Regular` | Arial Regular | `3161365478ce167f35d75aed6ca900c66ddd68b3` |
| `辅助/12/Number-Regular` | MiNum Regular | `2ce444e26d57720c03fe981c2db906503bde0da0` |
| `辅助/12/Number-Medium` | MiNum Medium | `1283375a2379cd367b9ff1f6791fa8e59decd58c` |

#### 正文（14px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `正文/14/CN-Regular` | PingFang SC Regular | `6183aacbcdf5517094645692d9bdd1c691f14eea` |
| `正文/14/CN-Medium` | PingFang SC Medium | `c1c4c49c234ccf2f407cbe6a1e2bf404ed52d4c9` |
| `正文/14/EN-Regular` | Arial Regular | `a240613f96ad208ac98a89b5a3fea63fb9c1750e` |
| `正文/14/Number-Regular` | MiNum Regular | `653bdca8974db08dc4e020525b27f3501b714fe3` |
| `正文/14/Number-Medium` | MiNum Medium | `9de81bd75749fe65cf2d0314879e93fe815bfd5c` |

#### 标题/小（16px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `标题/小-16/CN-Regular` | PingFang SC Regular | `7817c7c0c7f857ec66b1bb605ddf4c71c5e76182` |
| `标题/小-16/CN-Medium` | PingFang SC Medium | `8b28e392584ecd1139ae5f7eb626ab59a283461c` |
| `标题/小-16/EN-Regular` | Arial Regular | `1362205fa69448e6c61bba620204dec2c52cc923` |
| `标题/小-16/Number-Regular` | MiNum Regular | `c5a93187a4328e9f1e807b54acfae403954ae806` |
| `标题/小-16/Number-Medium` | MiNum Medium | `86de187573abd0a94026f88286e5004c0181d376` |

#### 标题/中（18px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `标题/中-18/CN-Regular` | PingFang SC Regular | `151fbe1a68f6335c2f05a5bec648cd24a5f3babd` |
| `标题/中-18/CN-Medium` | PingFang SC Medium | `e6d692be8a2ef91507ff714e556efe7da6e7f3de` |
| `标题/中-18/EN-Regular` | Arial Regular | `9423ce1f8f908fe48a374b25ba6ab5acc7bae9e7` |
| `标题/中-18/Number-Regular` | MiNum Regular | `35b6d55374e6bf7f1e5600fde8bb77b4edbe8d1e` |
| `标题/中-18/Number-Medium` | MiNum Medium | `2951d06864d2f664f8941f3bca0db66c8ab1aa2b` |

#### 标题/大（20px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `标题/大-20/CN-Regular` | PingFang SC Regular | `2a7dacbded1346e85ad8e516d60405bb292dc48c` |
| `标题/大-20/CN-Medium` | PingFang SC Semibold | `3d2e56220a966aa5e32ebb1fec27462e4cfb0986` |
| `标题/大-20/EN-Regular` | Arial Regular | `c301107d08f6f4ae1e77ad2dc51a00f9eb2ec71b` |
| `标题/大-20/Number-Regular` | MiNum Regular | `80d0179d4be9ec7d43d2db3b6bef6949c7512d21` |
| `标题/大-20/Number-Medium` | MiNum Medium | `cc7fa3237ee99cf1c17599c4e827469264cbbd39` |

#### 标题/大（24px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `标题/大-24/CN-Regular` | PingFang SC Regular | `ceda7298d70b97f1e3e0be709b609aedb45ad70f` |
| `标题/大-24/CN-Medium` | PingFang SC Semibold | `0ca393e79ca6efce5e0baede8b275180706a7afd` |
| `标题/大-24/EN-Regular` | Arial Regular | `0be463a4f5bb3269ba292f92bbbd08b1012c91dc` |
| `标题/大-24/Number-Regular` | MiNum Regular | `988f7c66087f6297a9d61884cbe49972c3600388` |
| `标题/大-24/Number-Medium` | MiNum Medium | `d6060b6f3f873e00207583e7438798090a7434e7` |

#### 运营标题/小（32px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `运营标题/小-32/CN-Regular` | PingFang SC Regular | `b691ac536da2a661578727a363eb447cedbe42fd` |
| `运营标题/小-32/CN-Medium` | PingFang SC Medium | `840fddbf219db8a8d604424cba05ff96361989b6` |
| `运营标题/小-32/EN-Regular` | Arial Regular | `dfdb1a879e22763c07707c5f8b798a92fd6ffc6f` |
| `运营标题/小-32/Number-Regular` | MiNum Regular | `caee8a9cde1a0648d90236db4a6c95b1cc71e10d` |
| `运营标题/小-32/Number-Medium` | MiNum Medium | `e9513bcfc4d77e4ed3baa868c583c9dd72ded51a` |

#### 运营标题/中（36px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `运营标题/中-36/CN-Regular` | PingFang SC Regular | `6673aec35f01094ba7f223e4e1c0b21554431b08` |
| `运营标题/中-36/CN-Medium` | PingFang SC Medium | `bd17734295ce8d21ea67f8a96d24d5dc56ade0b8` |
| `运营标题/中-36/EN-Regular` | Arial Regular | `3d94fde3ff8a697591da77f3e2b2e79540e9afc6` |
| `运营标题/中-36/Number-Regular` | MiNum Regular | `2d9a96bc12be7264886f312f13980b9b089a5654` |
| `运营标题/中-36/Number-Medium` | MiNum Medium | `619c0c1ef4bf395b3f1919577c1c34b9e9516146` |

#### 运营标题/大（48px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `运营标题/大-48/CN-Regular` | PingFang SC Regular | `2b4bd89bbb23a134780f619756c8e8a556fd73e8` |
| `运营标题/大-48/CN-Medium` | PingFang SC Medium | `064cef0e6577ebeb430aa45f75d2d6512b20ddfb` |
| `运营标题/大-48/EN-Regular` | Arial Regular | `42a17bb5bdf91e1c38683cf40ff26e74303a35ab` |
| `运营标题/大-48/Number-Regular` | MiNum Regular | `28a2e731d863e74e6b6c872ea4a0e6797792c221` |
| `运营标题/大-48/Number-Medium` | MiNum Medium | `6410f86181f09afc63561493018833fe58345707` |

---

### AI 运营-组件库（Finloop）

- **Figma 文件**：https://www.figma.com/design/scodnBKwhh8jBoPorOkf3X/AI-%E8%BF%90%E8%90%A5-%E7%BB%84%E4%BB%B6%E5%BA%93
- **Library Key**：`lk-42303f5ad3b4a675c8b42dffb4f79ddcbd771302803d07b97f1d99443a204cc74c8a034daf533a45e7ddf612dc98309eb18f18a98a886086ac1eef1ed109fa96`
- **字体**：中文 PingFang SC / 英文 Arial / 数字 MiNum

#### 辅助文字（12px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `辅助/12/CN-Regular` | PingFang SC Regular | `ff291e37069c9036a1ea55737fa3b9657a0517c5` |
| `辅助/12/CN-Medium` | PingFang SC Medium | `97404d1b361aadffafbcde667fc2a7b329334edd` |
| `辅助/12/EN-Regular` | Arial Regular | `11b82efbd0cdf3a8091833fd1a34679ff7820399` |
| `辅助/12/Number-Regular` | MiNum Regular | `a6399c2ac23f966e7c1efd01cffca754a145855c` |
| `辅助/12/Number-Medium` | MiNum Medium | `a99423500be3e5c4bc1f6256ae0eec0898546eca` |

#### 正文（14px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `正文/14/CN-Regular` | PingFang SC Regular | `19a4393675a95ac22931315adfaf923bd1ec2e91` |
| `正文/14/CN-Medium` | PingFang SC Medium | `cbde781870a9fc26b208f684a792c6e6838e8ff7` |
| `正文/14/EN-Regular` | Arial Regular | `15898196dc9bac981882c062b03420e56b4914d0` |
| `正文/14/Number-Regular` | MiNum Regular | `c15cab2653a1b6d579e52003872a489e300e3393` |
| `正文/14/Number-Medium` | MiNum Medium | `518938d747a4b453552abfc2441cdb2399bf2e8b` |

#### 标题/小（16px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `标题/小-16/CN-Regular` | PingFang SC Regular | `fe03b34c4443bfa316a6101b59a87981ed49c183` |
| `标题/小-16/CN-Medium` | PingFang SC Medium | `855e2624d777ca2ffdacdf8a2df15657d280a974` |
| `标题/小-16/EN-Regular` | Arial Regular | `3a0bf713d5b71b37aeb960ce4261d886c11a6270` |
| `标题/小-16/Number-Regular` | MiNum Regular | `eaaee5255f232503fa1fbd726a7686ce0ec8a790` |
| `标题/小-16/Number-Medium` | MiNum Medium | `f59f14a916860a5b2e50d9233fe7d76774350f91` |

#### 标题/中（18px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `标题/中-18/CN-Regular` | PingFang SC Regular | `d3c501385a69051942adcdbccf0dfcac2ab33624` |
| `标题/中-18/CN-Medium` | PingFang SC Medium | `5c4e5c02e379153cd52a00b55465d5304f179652` |
| `标题/中-18/EN-Regular` | Arial Regular | `e74cd18624ae1f3a5b767e91294311f8cb7cc40c` |
| `标题/中-18/Number-Regular` | MiNum Regular | `5aa4caf4dbbb374d92c29360825388f8ec9fa34b` |
| `标题/中-18/Number-Medium` | MiNum Medium | `a66b516e58d370547a5d901a36346101bc95253a` |

#### 标题/大（20px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `标题/大-20/CN-Regular` | PingFang SC Regular | `5844453c5e14cdfeafe57cbdf400d007d895d8d8` |
| `标题/大-20/CN-Medium` | PingFang SC Medium | `f04e2dd20b6045da73ee57ac2446aaf3b7113317` |
| `标题/大-20/EN-Regular` | Arial Regular | `50fa64ede7157de0c4f3883def0c4aa78def58ba` |
| `标题/大-20/Number-Regular` | MiNum Regular | `88cb7ea31cfdf02f198bd05ff5f383ca5265ac5d` |
| `标题/大-20/Number-Medium` | MiNum Medium | `c491d627b4eb9f978e449e5ea572fdb1aa6a25ad` |

#### 标题/大（24px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `标题/大-24/CN-Regular` | PingFang SC Regular | `2a37f2088361f7875fffa8886ea6054e92f4d844` |
| `标题/大-24/CN-Medium` | PingFang SC Medium | `055de55d64ae8823d607823bbb588b7e8fe03838` |
| `标题/大-24/EN-Regular` | Arial Regular | `f8e13cd40cac4715a41bf4ad64523f8910b1078b` |
| `标题/大-24/Number-Regular` | MiNum Regular | `575743b932b5e9788686139603fa82134bdae4d8` |
| `标题/大-24/Number-Medium` | MiNum Medium | `3a0925520085b8ff6cac9dd82bc4323d864ac8bc` |

#### 运营标题/小（32px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `运营标题/小-32/CN-Regular` | PingFang SC Regular | `23cb3d478bb4c02bbc2446d2c4c9eba6ac271044` |
| `运营标题/小-32/CN-Medium` | PingFang SC Medium | `279abee71379971f614f7b33cc448d9f496f44ef` |
| `运营标题/小-32/EN-Regular` | Arial Regular | `84a1c1a99d99322b400d00bf4d52c3c3bdc3873f` |
| `运营标题/小-32/Number-Regular` | MiNum Regular | `4e6a05d51cb6862d6f75c14c79086b66152bb486` |
| `运营标题/小-32/Number-Medium` | MiNum Medium | `2af990a599708d33dea657338c9dbb60af563d4c` |

#### 运营标题/中（36px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `运营标题/中-36/CN-Regular` | PingFang SC Regular | `62ef22de3e1c5c47a4c2e79ed018c1da81f4140a` |
| `运营标题/中-36/CN-Medium` | PingFang SC Medium | `9b1f700b0e3bd3208ac18269d176a1165ac7f3f5` |
| `运营标题/中-36/EN-Regular` | Arial Regular | `a4d493b9c329fb8b1daaa2609a18e08f0080f58c` |
| `运营标题/中-36/Number-Regular` | MiNum Regular | `c6f0d28136229b35090b245cb6aabd90be05b486` |
| `运营标题/中-36/Number-Medium` | MiNum Medium | `3ea7c4919928d5bb231294cf4d0a0c6d5b17bae3` |

#### 运营标题/大（48px）

| 样式名 | 字体 | Key |
|--------|------|-----|
| `运营标题/大-48/CN-Regular` | PingFang SC Regular | `03cdf5684269a46f8c213fd9f726da6669d0f2f5` |
| `运营标题/大-48/CN-Medium` | PingFang SC Medium | `f9eb46aeaaa2d4bf0e9bc29e96e31f673cb4828c` |
| `运营标题/大-48/EN-Regular` | Arial Regular | `d3b3c636724d9f1a7c4668ed6aaed3e5ccb7de4d` |
| `运营标题/大-48/Number-Regular` | MiNum Regular | `bad0ccae727dfe6a02954b431a69d1c2dda6e932` |
| `运营标题/大-48/Number-Medium` | MiNum Medium | `a8e03473716cb96b40c15cae33d0d2bafaab907f` |

---

## 移动端组件库

- **Figma 文件**：https://www.figma.com/design/UvkJyLQtSdLqE87NOLISth/移动端组件
- **Library Key**：`lk-28cf6286524e4c5cd741ec2d723f43940750a7dac6ec5f5c7f7182fd9e0130db35c0e4e64ea6e5085855254622f59947639a059a7892684145f8785f224135e5`
- **字体**：中文 PingFang SC / 数字 MiNum

#### Display（展示大数字）

| 样式名 | 字号 | 字体 | 用途 | Key |
|--------|------|------|------|-----|
| `text/display/xl-Semibold` | 32 | PingFang SC Semibold | 页面最大标题，资产总量特大数字 | `01548eecc5155ab5628a5791778124807c756e8c` |
| `text/display/lg-Semibold` | 28 | PingFang SC Semibold | 大标题，收益总量、净值大数字 | `7f8e12e4c3e47ad281357650505a0106db251683` |

#### Heading（标题）

| 样式名 | 字号 | 字体 | 用途 | Key |
|--------|------|------|------|-----|
| `text/heading/xl-Semibold` | 24 | PingFang SC Semibold | 页面主标题 | `b3b0491fb89347cb8105817abe01c9ed6f22a594` |
| `text/heading/lg-Semibold` | 20 | PingFang SC Semibold | 卡片标题、弹层标题 | `d5103efbfe47c3d89a705b7d9e4bf1147e02182b` |
| `text/heading/md-Semibold` | 18 | PingFang SC Semibold | 模块标题 | `f3e9db212d8ea9fb7f5a8379a60440fd9ae3c170` |
| `text/heading/sm-Semibold` | 16 | PingFang SC Semibold | 小节标题、列表项主文强调 | `782748a34f4c612a8dd7523a6cce828a07f0b87d` |

#### Body（正文）

| 样式名 | 字号 | 字体 | 用途 | Key |
|--------|------|------|------|-----|
| `text/body/xl-Regular` | 16 | PingFang SC Regular | 主要正文，产品说明、弹层内容 | `92083ab0507e94693a52d9b8dc14a4dc91727ae8` |
| `text/body/xl-Medium` | 16 | PingFang SC Medium | 强调正文，列表项名称、Tab 选中文字 | `2dbe1be33967411b81d545a120cfba40950abfef` |
| `text/body/lg-Regular` | 15 | PingFang SC Regular | 主要正文，产品说明、弹层内容 | `5637da1fb3e5b8101c32d87f844bca0f68fce6cc` |
| `text/body/lg-Medium` | 15 | PingFang SC Medium | 强调正文，列表项名称、Tab 选中文字 | `bf4a47cb0271e5fa73eaabd2120d9aa48f26161c` |
| `text/body/md-Regular` | 14 | PingFang SC Regular | 常规正文，最常用尺寸 | `f276144d7c669ea6fe0abda657e39aca78f9bc7c` |
| `text/body/md-Medium` | 14 | PingFang SC Medium | 强调常规正文，表单标签、按钮文字 | `a5d3f66c2cbbc5840c875ab38fa43bbda952265a` |
| `text/body/sm-Regular` | 13 | PingFang SC Regular | 辅助文字，小标注、辅助说明 | `e4b7d16e5dc120eadebedd9ba00c35e3ca5927bf` |
| `text/body/sm-Medium` | 13 | PingFang SC Medium | 辅助文字，小标注、辅助说明 | `991745ba3f96013e4f17b1681b2cdccd7a3d1b39` |

#### Caption（说明文字）

| 样式名 | 字号 | 字体 | 用途 | Key |
|--------|------|------|------|-----|
| `text/caption/lg-Regular` | 12 | PingFang SC Regular | 标注、提示文字，时间戳、辅助说明 | `319cd90b7a32a21988477d40113bbf725eb6ac6c` |
| `text/caption/lg-Medium` | 12 | PingFang SC Medium | 标签文字，如 Tag、状态小标签 | `d289999852be7ec0c44b4d4c23042f279b31b65c` |
| `text/caption/md-Regular` | 11 | PingFang SC Regular | 法律条款、极小说明文字 | `ca6af0dc42df3c7f77894afad4e094e815f7260f` |
| `text/caption/md-Medium` | 11 | PingFang SC Medium | — | `a80843f976d216f4597495f3d25d3192900c071a` |
| `text/caption/sm-Regular` | 10 | PingFang SC Regular | — | `5857a54f7d4f53d27f67cf990667a18b41c9c813` |
| `text/caption/sm-Medium` | 10 | PingFang SC Medium | — | `e4fdd778e5ee4f3893f7caf159b5f3fe4456bf6f` |

#### Number / Display（数字展示）

| 样式名 | 字号 | 字体 | 用途 | Key |
|--------|------|------|------|-----|
| `text/number/diplay/xl-Demibold` | 32 | MiNum Demibold | 资产总量数字，等宽字形保证列对齐 | `33d4578e8d65402ea2658517e6e4c561dd612c4b` |
| `text/number/diplay/xl-Demibold` | 28 | MiNum Demibold | 资产总量数字，等宽字形保证列对齐 | `3967cce9b59a8ab02ded2a61797242c01f4013b9` |
| `text/number/heading/xl-Demibold` | 18 | MiNum Demibold | 单产品净值、收益金额 | `97c0ce4ad3497e31eb26099ff41d1f8101af5111` |
| `text/number/heading/lg-Demibold` | 20 | MiNum Demibold | 单产品净值、收益金额 | `493e399501264d8501d0e4df132fad71e0730f26` |

#### Number / Body（数字正文）

| 样式名 | 字号 | 字体 | 用途 | Key |
|--------|------|------|------|-----|
| `text/number/body/xl-Regular` | 16 | MiNum Regular | 列表数字、涨跌幅 | `85d5181747e731d5c37f2cef3b4c21ea0c1c5fee` |
| `text/number/body/xl-Medium` | 16 | MiNum Medium | 列表数字、涨跌幅 | `701ef484d3eadfc1edd50e0d777fde002b79f64c` |
| `text/number/body/lg-Regular` | 15 | MiNum Regular | 列表数字、涨跌幅 | `955b59712d78adbb7bb81422de34809af7182bad` |
| `text/number/body/lg-Medium` | 15 | MiNum Medium | 列表数字、涨跌幅 | `143571dccea6c6e3698ab5ef21ed7e7a1d94a20a` |
| `text/number/body/md-Regular` | 14 | MiNum Regular | 表格数字、辅助数字 | `df7267c770a3f83880f6d56f9a2e6b30cbc6b10c` |
| `text/number/body/md-Medium` | 14 | MiNum Medium | 表格数字、辅助数字 | `2b39fb22e80b41c48fa34452256c4b55b129f7a3` |
| `text/number/body/sm-Regular` | 13 | MiNum Regular | 列表数字、涨跌幅 | `c66ad4d82407e0f20a008e3bece8b7728fb5a3ba` |
| `text/number/body/sm-Medium` | 13 | MiNum Medium | 列表数字、涨跌幅 | `e5cbb9e88fc3667edd9c4a2852314e07e4f9f150` |

#### Number / Caption（数字说明）

| 样式名 | 字号 | 字体 | 用途 | Key |
|--------|------|------|------|-----|
| `text/number/caption/lg-Regular` | 12 | MiNum Regular | 最小数字，指数、百分比注释 | `a508f18f3b87462006c49110996811ccafe0100d` |
| `text/number/caption/lg-Medium` | 12 | MiNum Medium | 最小数字，指数、百分比注释 | `3ac353ba77bbb38044b6a845f9bf38fb7a5c0849` |
| `text/number/caption/md-Regular` | 11 | MiNum Regular | — | `ed4455d5b4b2413f3673c6802f6bea22d58409e8` |
| `text/number/caption/md-Medium` | 11 | MiNum Medium | 最小数字，指数、百分比注释 | `c9dd900d911431b206d576d2f43d10f8041320b0` |
| `text/number/caption/sm-Regular` | 10 | MiNum Regular | — | `5fac79a99ed02631af7696ffa5e22e46ae1ed697` |
| `text/number/caption/sm-Medium` | 10 | MiNum Medium | — | `1307674440c7930768296257c3a2b49a32eeeedf` |

---

## 数字字体使用规范（全局强制规则）

**核心原则**：页面中**任意场景**下所有显示数字内容的文字节点，无论是独立文本节点还是组件实例内部文字节点，都必须使用组件库预设的 **Number** 系列文本样式（MiNum 等宽字形），不能使用普通中文（CN）或英文（EN）样式。

**适用场景（不限于表格，覆盖所有页面区域）**：
- 纯数字：`123`、`1,234.56`、`45%`、`¥100.00`
- 金融数据：净值、涨跌幅、金额、比率、数量、百分比
- 日期：`2024/03/15`、`2019-06-20`
- 混合文本含数字：`涨幅 +5.2%`、`价格 ¥1,234`
- 编号 / 计数：`1/6`、`NO.001`

**为什么使用 Number 样式**：Number 样式使用等宽数字字形（Tabular Figures），保证列表 / 表格中数字列对齐，提升金融数据可读性。

**操作方式**：
- 独立文本节点 → 流程 2 或流程 3 直接绑定 Number 样式
- 组件实例内部数字文本 → 流程 1b（`text.set_content` 写内容后立即执行 `text.update` 替换样式）

**对应样式查找**：

| 端 | 样式前缀 | 字号示例 |
|----|---------|---------|
| Web（FinEAM） | `辅助/12/Number-*`、`正文/14/Number-*`、`标题/小-16/Number-*` 等 | 见上方 Web 端组件库表格 |
| 移动端 | `text/number/body/*`、`text/number/caption/*`、`text/number/heading/*` 等 | 见上方移动端组件库表格 |

---

## 快速选样式指南

### Web 端（FinEAM）

| 场景 | 推荐样式 |
|------|---------|
| 页面标题 | `标题/大-20/CN-Medium` 或 `标题/大-24/CN-Medium` |
| 正文内容 | `正文/14/CN-Regular` |
| 强调正文 | `正文/14/CN-Medium` |
| 辅助/说明文字 | `辅助/12/CN-Regular` |
| 数字数据（净值/涨跌） | `正文/14/Number-Regular` 或 `正文/14/Number-Medium` |
| 英文/混排 | 对应尺寸的 `EN-Regular` |

### 移动端

| 场景 | 推荐样式 |
|------|---------|
| 页面主标题 | `text/heading/xl-Semibold`（24px） |
| 卡片/弹层标题 | `text/heading/lg-Semibold`（20px） |
| 主要正文 | `text/body/lg-Regular`（15px） |
| 常规正文 | `text/body/md-Regular`（14px） |
| 辅助说明 | `text/caption/lg-Regular`（12px） |
| 资产大数字 | `text/number/diplay/xl-Demibold`（32px） |
| 列表数字/涨跌幅 | `text/number/body/lg-Regular`（15px） |
