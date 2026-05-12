# prd2figma·需求文档转 Figma 设计稿

一个支持将产品需求文档（PRD）自动分析为结构化页面描述，并调用项目设计系统在 Figma 中逐页生成设计稿的 Skill。提供 PRD 后自动运行完整流水线，支持多项目路由。

## 安装

在终端中运行以下指令。默认会安装到 Cursor 和 Codex 的本地 skill 文件夹，也可以通过参数自定义安装路径，适配更多应用：

```bash
npx skills add https://github.com/pipivovottt/prd-to-figma --skill prd-to-figma
```

安装完成后，在对话中调用 Skill 并提供 PRD 内容，Agent 会自动识别项目、拆解页面并在指定文件中生成 Figma 设计稿。
