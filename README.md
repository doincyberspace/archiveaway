# 随备 Archive Away

一个简洁的网页备份搜索工具。支持在多个网页存档服务之间快速查询和保存网页快照。

## 功能

- **搜索网页备份**：输入网址，选择备份站，即可查看历史快照
- **保存网页备份**：一键将当前网页提交到各大备份站进行存档
- **浏览器搜索引擎集成**：支持 [OpenSearch](https://developer.mozilla.org/zh-CN/docs/Web/OpenSearch) 协议，可将"随备"添加为浏览器默认搜索引擎
- **URL 参数直达**：通过 `?q=网址` 等参数直接跳转，方便书签和脚本调用
- **响应式设计**：适配桌面端和移动端屏幕

## 支持的备份站

| 备份站 | 查看备份 | 保存备份 | 备注 |
|--------|----------|----------|------|
| [Wayback Machine](https://web.archive.org) | 支持 | 支持 | 默认备份站 |
| [Archive-It](https://archive-it.org) | 支持 | 支持 | 基于 Wayback Machine |
| [Archive.today](https://archive.ph) | 支持 | 支持 | — |
| [Ghost Archive](https://ghostarchive.org) | 支持 | 跳转首页 | 需在其页面内手动提交 |
| [Megalodon.jp](https://megalodon.jp) | 支持 | 支持 | 自动补全 `https://` 协议 |
| [Arquivo.pt](https://arquivo.pt) | 支持 | 跳转首页 | 需在其页面内手动提交 |

## 部署

本项目为纯静态网站，单 HTML 文件，无需构建步骤。

### Cloudflare Pages

1. Fork 本仓库
2. 登录 [Cloudflare Pages](https://pages.cloudflare.com/)，创建新项目
3. 选择 Git 仓库，直接部署（无需构建命令，输出目录填 `/`）

### GitHub Pages

1. Fork 本仓库
2. 进入仓库 **Settings** → **Pages**
3. Source 选择 **Deploy from a branch**，分支选 `main`，目录选 `/ (root)`
4. 保存后等待部署完成

### Vercel

1. Fork 本仓库
2. 登录 [Vercel](https://vercel.com/)，导入项目
3. Framework Preset 选择 **Other**，无需修改其他配置
4. 直接部署

### 本地运行

直接双击 `index.html` 在浏览器中打开，或使用任意本地服务器：

```bash
python3 -m http.server 8080
```

## 添加为浏览器搜索引擎

本页支持 OpenSearch 协议。部署后，使用 Chrome / Edge / Firefox 打开网站，浏览器会自动识别搜索引擎：

- **Chrome / Edge**：地址栏右侧点击 **+** 图标添加
- **Firefox**：地址栏点击右侧 **...** → **添加搜索引擎**
- 或进入浏览器设置 → 搜索引擎 → 管理搜索引擎 → 添加

添加后，在地址栏输入关键词即可直接搜索网页备份。

## OpenSearch 语法

通过 URL 参数可以直接执行搜索或保存操作。

### 参数

| 参数 | 说明 | 必填 |
|------|------|------|
| `q` | 要查询或保存的网址 | 是 |
| `s` | 目标备份站 ID（见下表） | 否，默认 `wayback` |
| `a` | 执行动作：`latest` / `all` / `save` | 否，默认 `latest` |

### 备份站 ID

| ID | 备份站 |
|----|--------|
| `wayback` | Wayback Machine（默认） |
| `archiveit` | Archive-It |
| `archivetoday` | Archive.today |
| `ghostarchive` | Ghost Archive |
| `megalodon` | Megalodon.jp |
| `arquivo` | Arquivo.pt |

### 示例

```
/?q=example.com                          # Wayback Machine 查看最新备份
/?q=example.com&s=archivetoday           # Archive.today 查看备份
/?q=example.com&a=save                   # Wayback Machine 保存网页
/?q=example.com&s=megalodon&a=save       # Megalodon.jp 保存网页
/?q=example.com&s=ghostarchive&a=all     # Ghost Archive 查看所有备份
```

通过 URL 参数访问时，页面会在当前标签页直接跳转到目标备份站。

## 项目结构

```
.
├── index.html          # 主页面（含内联 CSS 和 JS）
├── opensearch.xml      # OpenSearch 描述文件
├── favicon.ico         # 多尺寸 ICO 图标
├── logo.png            # 网站 Logo
└── icons/
    ├── icon-16x16.png
    ├── icon-32x32.png
    ├── icon-48x48.png
    ├── icon-180x180.png   # Apple Touch Icon
    ├── icon-192x192.png   # PWA 图标
    └── icon-512x512.png   # PWA 大图标
```

## 技术细节

- 纯 HTML + CSS + JavaScript，无外部依赖
- 单页面应用，所有代码内联于 `index.html`
- 零构建步骤，可直接部署到任何静态托管服务
- 使用原生 ES5 JavaScript 语法，兼容旧版浏览器
- URL 参数自动跳转使用 `window.location.href`（避免浏览器弹窗拦截）
- 按钮点击打开备份使用 `window.open('_blank')`

## License

本项目采用 MIT 许可证开源。详见 [LICENSE](LICENSE) 文件。

---

- [Fediverse](https://c7.io/@doin)
- [GitHub](https://github.com/doincyberspace/archiveaway)
