# 设计稿自检项（Design Self-Check）

执行时机：绘制完毕后，对本次生成的全部页面及弹窗逐条运行以下自检项。发现不符项，立即通过 `use_figma` 修正后再继续下一条。

---

## CHECK-01 · 弹窗  body 帧无额外纵向 padding

**适用场景**：页面中存在通过 `detachInstance()` 重建了 body 内容区的 modal / modal-confirm / Drawer。

**检查方式**：
```javascript
// 对每一个 detach 后的弹窗 frame 执行
const body = modalFrame.findOne(n => n.name === 'body');
console.log('paddingTop:', body?.paddingTop, 'paddingBottom:', body?.paddingBottom);
// 期望值：均为 0
```

**修正方式**：若 `paddingTop` 或 `paddingBottom` 非零且无主动设计意图（即是重建时随手填写的经验值），立即归零：
```javascript
body.paddingTop = 0;
body.paddingBottom = 0;
```

**根因说明**：modal 的 `body` 容器帧在原组件中纵向 padding 为 0，上下留白由外层 modal frame 的 `itemSpacing` 控制。若在重建时额外添加了 `paddingTop/Bottom`，会与 `itemSpacing` 叠加，产生过大的空白间距。

---

<!-- 按以上格式继续追加新的自检项，编号递增：CHECK-02、CHECK-03… -->
