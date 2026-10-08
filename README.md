[README.md](https://github.com/user-attachments/files/33197508/README.md)
# 河西走廊 · 内陆河动画

河西走廊夜景底图上的三条内陆河动画：**石羊河、黑河、疏勒河**依次从祁连山流出，蓝色粒子沿河向下游流动，到尾闾处逐渐淡出，最后消失在荒漠里。

这是地图故事《河西走廊生态恢复》中"水的格局"一节的配图，用来引出"内陆河"这个概念：河水出山后养活一片绿洲，不入海，终点在荒漠里。

纯静态网页，无需安装任何东西，用浏览器直接打开即可播放。

## 文件说明

| 文件 | 作用 |
|---|---|
| `index.html` | 网页本体：绘制底图、河流、城市，并播放粒子动画 |
| `hexi_base.png` | 夜景底图（2400 × 1180 px），在 Google Earth Engine 中生成 |
| `rivers.js` | 三条河的坐标（经度、纬度，顺序为上游到下游） |
| `README.md` | 本说明 |

三个文件必须放在**同一个文件夹**里。

## 本地预览

双击 `index.html`，用 Chrome 或 Edge 打开。点击页面可重播，动画每 20 秒自动循环。

## 部署到 GitHub Pages

不需要安装 Git，全程在网页上操作。

**1. 新建仓库**

登录 GitHub，点右上角 **+ → New repository**。

- Repository name：`hexi-rivers`（可改成别的）
- 选 **Public**（免费账号的 Pages 需要公开仓库）
- 点 **Create repository**

**2. 上传文件**

在新仓库页面点 **uploading an existing file**，把 `index.html`、`hexi_base.png`、`rivers.js`、`README.md` 一起拖进去，点 **Commit changes**。

文件名区分大小写，不要写成 `Index.html` 或 `Hexi_base.png`。

**3. 开启 Pages**

进入仓库的 **Settings → Pages**：

- Source 选 **Deploy from a branch**
- Branch 选 **main**，文件夹选 **/ (root)**
- 点 **Save**

**4. 等待并访问**

等 1 到 3 分钟，刷新 Pages 设置页，顶部会出现网址：

```
https://你的用户名.github.io/hexi-rivers/
```

打开能看到动画就说明部署成功。

## 嵌入地图故事

把下面的代码放进地图故事的 HTML 或嵌入块里，把网址换成你自己的：

```html
<iframe
  src="https://你的用户名.github.io/hexi-rivers/"
  style="width:100%; aspect-ratio:2400/1180; border:0; background:#000"
  loading="lazy"
  title="河西走廊三大内陆河动画">
</iframe>
```

如果平台只允许贴链接，直接贴上面的网址即可。

## 参数调整

打开 `index.html`，在 `<script>` 开头可以改这些：

| 参数 | 作用 | 默认值 |
|---|---|---|
| `TL` | 每条河出现的时间区间（秒） | 石羊河 0–4，黑河 4.5–8.5，疏勒河 9–13 |
| `SPEED` | 粒子流速（每秒走完全程的比例） | `0.05` |
| `P` | 每条河的粒子数 | `40` |
| `COL` | 每条河的颜色（RGB） | 三种蓝青色 |
| `REVERSE` | 某条河的粒子方向反了就改成 `true` | 全部 `false` |
| `CITIES` | 城市名和经纬度 | 武威、张掖、酒泉、敦煌 |
| `% 20` | 循环周期（秒），建议等于 `1 / SPEED` | `20` |

改 `SPEED` 时同步改 `% 20`，否则循环衔接处会跳一下。比如 `SPEED = 0.1` 对应 `% 10`。

## 更新内容

在仓库页面点开要修改的文件，点铅笔图标编辑，或点 **Add file → Upload files** 覆盖上传，提交后 1 到 2 分钟内网页自动更新。浏览器如果显示的还是旧版，按 `Ctrl + F5` 强制刷新。

## 常见问题

- **页面一片黑**：按 `F12` 打开控制台看红色报错。多半是文件名大小写不对，或三个文件不在同一目录。
- **画面上提示"找不到 rivers.js / hexi_base.png"**：同上，检查文件名和位置。
- **网址打开是 404**：Pages 刚开启需要几分钟；仍然 404 就检查 Settings → Pages 里 Branch 是否选了 `main` 和 `/ (root)`。
- **大陆网络下打开慢或打不开**：GitHub Pages 在大陆访问不稳定。可以把三个文件同样放到 Gitee Pages、Cloudflare Pages 等托管服务，或录成视频使用。
- **更新后看到的还是旧版**：`Ctrl + F5` 强制刷新。

## 数据与制作说明

- **底图**：用 Google Earth Engine 生成。地形阴影基于 SRTM（USGS/SRTMGL1_003）；植被为 MODIS MOD13Q1 NDVI，2023 年 7 至 8 月中值合成，250 m 分辨率；绿色光晕由 NDVI 模糊得到，仅作视觉效果。
- **河流**：在卫星影像上手工描绘，是示意性的河道走向，不是测绘数据，位置和尾闾终点仅供示意。
- **城市**：武威、张掖、酒泉、敦煌，为市区大致位置。
- 坐标范围：93.0°E–104.8°E，36.8°N–42.6°N，经纬度直接拉伸成矩形，没有做投影变换。
- 疏勒河最西端约 0.12° 超出底图西边界，画面中被截断。

使用数据和影像前，请确认各数据源的使用条款，并在发布时注明来源。
