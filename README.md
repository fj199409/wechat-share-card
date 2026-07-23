# 微信分享卡片生成器

基于 Open Graph 协议和微信 JS-SDK 的分享卡片自定义工具，无需代码即可生成可在微信中分享的美丽卡片。

## 在线体验

直接打开 `wechat-share-generator.html` 即可使用可视化生成器。

## 功能特性

- 可视化配置：填写标题、简介、LOGO、目标链接
- **自动跳转模式**：点击卡片后直接跳转到目标页面，无需中间点击
- 实时预览：即时查看微信卡片效果
- 双方案支持：
  - **OG标签方案**：简单快速，无需公众号
  - **JS-SDK方案**：功能完整，支持朋友圈/好友自定义
- 一键下载：自动生成HTML文件，直接上传到服务器即可使用

## 使用说明

### 方案一：OG标签（推荐新手）

1. 打开 `wechat-share-generator.html`
2. 选择"方案一：OG标签"
3. 填写分享标题、简介、卡片链接
4. 上传LOGO图片（建议 300x300px，不超过 300KB）
5. **填写"跳转目标"（可选）**：
   - 如果填写了跳转目标，生成的页面会**自动跳转**，用户点击卡片后直接到达目标页面
   - 如果留空，生成的页面会显示"立即查看"按钮（传统落地页模式）
6. 点击"生成分享页面代码"
7. 下载HTML文件并上传到你的服务器
8. 在微信中分享该链接即可显示卡片

### 自动跳转模式示例

```
微信卡片链接：https://your-domain.com/share.html  （含OG标签，供微信抓取）
跳转目标：https://123.com/                     （用户最终到达的页面）
```

用户点击卡片后：
- 微信先打开 share.html（显示"正在跳转..."）
- 页面立即自动跳转到 123.com/
- 用户几乎无感知，体验如同直接跳转

### 方案二：JS-SDK（企业级）

需要：
- 已认证的微信公众号
- 已备案域名（配置JS安全域名）
- 后端签名服务

## 项目结构

```
.
├── wechat-share-generator.html   # 微信分享卡片生成器（主工具）
├── share-demo.html               # 示例分享落地页（自动跳转模式）
└── README.md                     # 项目说明
```

## 注意事项

- 分享图片必须是公网可访问的URL
- 微信会缓存卡片信息，修改后可能需要 24-48 小时生效
- 强制刷新缓存：在链接后添加随机参数，如 `?t=123`
- 自动跳转使用 `window.location.replace()` + `<meta http-equiv="refresh">` 双重保险

## 技术原理

### Open Graph 标签

微信通过抓取网页中的 OG 标签来生成分享卡片：

```html
<meta property="og:title" content="标题">
<meta property="og:description" content="简介">
<meta property="og:image" content="图片URL">
<meta property="og:url" content="链接">
```

### 自动跳转

在中间页添加自动跳转，实现无感知跳转：

```html
<!-- 方式1：Meta标签自动跳转 -->
<meta http-equiv="refresh" content="0;url=https://目标页面">

<!-- 方式2：JS立即跳转（更快） -->
<script>
    window.location.replace('https://目标页面');
</script>
```

### 微信 JS-SDK

通过调用微信官方 SDK 动态设置分享内容：

```javascript
wx.updateAppMessageShareData({
    title: '标题',
    desc: '简介',
    link: '链接',
    imgUrl: '图片URL'
});
```

## 域名示例

本项目示例域名：`https://123.com/`

请将其替换为你自己的域名。

## 开源协议

MIT License

