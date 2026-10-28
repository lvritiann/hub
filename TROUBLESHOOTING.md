# 统一入口导航站 · 排错手册（TROUBLESHOOTING）

适用对象：`portal/index.html`（高速延长综合管理平台统一入口）。
部署方式：GitHub Pages（仓库 `lvritiann.github.io/hub`，公开地址 `https://lvritiann.github.io/hub/`）。

---

## 1. 页面打不开 / 白屏
- 确认地址正确：`https://lvritiann.github.io/hub/`（末尾斜杠可加可不加）。
- 白屏多为网络/浏览器缓存：强刷 `Ctrl+F5`；手机端杀掉浏览器重进。
- GitHub Pages 刚推送后有几分钟 propagation 延迟，等 1–2 分钟再试。
- 仍白屏：本地用浏览器直接打开 `index.html`，能开说明是 CDN/网络问题，不是文件问题。

## 2. 某张卡片点了跳 404 / 打不开
- 卡片目标站是各业务系统自己的地址，跳不过去通常是**目标站本身挂了或改了路径**，不是入口站的问题。
- 检查 `index.html` 里该条的 `url` 是否和现网一致（对照各系统最新地址）。
- 目标站若是 `*.app.workbuddy.host`，可能需登录或已过期，属正常现象。

## 3. 想新增一个系统入口
打开 `portal/index.html`，在 `<script>` 里的 `SITES` 数组加一项：
```js
{
  name:"系统名称",
  desc:"一句话说明",
  cat:"驾驶舱",          // 或 "业务系统"
  catType:"dash",        // dash=金色标签 / biz=蓝色标签
  url:"https://完整地址",
  icon:'<svg path 内容>'  // 可复制已有项的 icon
}
```
保存后按第 7 条重新推送即可，无需改其他代码。

## 4. 想改标题 / 配色 / 文案
- 标题：改 `<title>` 和 `<h1>高速延长 · 综合管理平台</h1>`。
- 副标题/页脚：改 `.sub`、`<footer>` 文字。
- 配色：改 `:root` 里的 `--gold` / `--blue` / `--bg` 等变量（全局生效）。
- 背景动效太花：把 `.blob` 的 `animation` 删掉即可变静态。

## 5. 样式自定义（不想碰代码时的安全区）
- 卡片数量随 `SITES` 自动换行，加多少都排版自适应，无需调 CSS。
- 想换图标：找一个 24×24 的 line SVG `<path>` 替换对应 `icon` 即可。

## 6. 部署后不生效 / 缓存
- GitHub Pages 有 CDN 缓存，推送后等 1–2 分钟；浏览器再强刷一次。
- 确认推送的是 `main` 分支根目录的 `index.html`（Pages 源设为 `main` / root）。

## 7. 回滚到上一版
- 在 GitHub 仓库 `hub` 的 **History / Commits** 里找到上一个提交，`Revert` 或把旧文件覆盖回来再提交。
- 本地若有旧文件直接覆盖 `index.html` 重新推送即可。

## 8. 本地预览跑法（不部署也能看）
- 最简单：双击 `index.html` 用浏览器打开。
- 或起本地服务：`cd portal && python -m http.server 8080`，浏览器开 `http://localhost:8080`。
- 纯静态、零依赖、零后端，离线也能跑。

---

## 安全提示
- `dinghuo-taizhang` 的旧链接曾在 URL 里带过 GitHub PAT（个人访问令牌），**已在新入口中剔除明文令牌**，跳转用干净地址。如该 PAT 仍有效，请去 GitHub 后台吊销重发。
- 本入口站自身不含任何密钥/令牌，可安全公开托管。
