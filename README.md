<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./docs/images/logo-white.png" />
  <img src="./docs/images/logo.png" alt="Rainy Mart" width="124" />
</picture>

# Rainy Mart

**雨夜里的一座便利店微缩景：单文件 Three.js 场景，无构建、零依赖、无外部资源**

一家 24 小时便利店立在雨夜的街角，停车场积着水洼，灯箱和招牌映在湿漉漉的沥青上。
对面是斑马线、信号灯、电线和一排小楼 —— 打开 `rainy-mart.html` 就跑，不需要构建，也不需要服务器。

[![Build](https://img.shields.io/badge/build-none_required-3fb950?style=flat-square&logo=html5&logoColor=white)](#运行)
[![Dependencies](https://img.shields.io/badge/dependencies-0-3fb950?style=flat-square&logo=npm&logoColor=white)](#结构)
[![three.js](https://img.shields.io/badge/three.js-inlined-2f80ed?style=flat-square&logo=threedotjs&logoColor=white)](#结构)

</div>

---

## 运行

需要支持 WebGL 2 的浏览器（Chrome / Edge / Safari / Firefox 的近年版本），硬件加速开启。

```sh
open rainy-mart.html
```

`file://` 直接打开即可，不需要起服务器。

## 操作

- 拖动旋转视角，滚轮 / 双指缩放；拖动右键或双指平移
- 视角有角度和远近限制，相机始终围着便利店转，不会翻到地面以下
- 场景是循环播放的雨夜：雨一直下，灯光和水洼的反光持续变化

## 场景

- 便利店：整面玻璃门面透出室内的暖光，屋顶有空调外机，招牌、立柱灯箱和 24H 牌都在发光
- 停车场：车位线、水洼、便利店门口的分类回收箱
- 街道：斑马线、停止线、信号灯、路灯、电线杆和架空线，路边停着自行车、立着邮筒
- 配楼：两层小楼、窗灯、外挂空调、雨棚和阳台
- 整个街区悬在一块方形地台上，昼夜固定在雨夜

## 渲染

- three.js r170 全量内联在一个 `<script>` 里，没有任何网络请求或外部图片
- 后处理：EffectComposer + UnrealBloomPass 做灯光泛光，再叠一层自定义 final pass（暗角 + 颗粒 + 色调）
- 雨是每一帧重画的线，亮度按镜头距离补偿：拉远时更亮，雨丝不会消失在远处
- 便利店、路灯、信号灯和招牌灯箱是自发光材质，bloom 只吃这些高亮区域
- 所有招牌文字（YORU MART、OPEN、24H、YORU COFFEE 等）都是运行时用 canvas 画出来的贴图，不是图片文件
- 雨夜固定：没有昼夜切换，光照和配色都按夜晚调好

## 结构

```
rainy-mart.html          主文件，HTML + CSS + JS + three.js 全在里面
docs/images/             README 标志（浅色 / 深色两版）
```

## 致谢

**图标**：[杂货店图标](https://igoutu.cn/icon/xZyuCF92KCHC/%E6%9D%82%E8%B4%A7%E5%BA%97)，来自 [Icons8](https://icons8.com)（中文站 [igoutu.cn](https://igoutu.cn)），风格为 Pulsar Color / 脉冲彩色，作者 Icons8 团队。按 Icons8 免费许可使用，需保留指向 Icons8 的链接。

图标做了三处调整：

1. 以 1600×1600 PNG 导出，作为仓库标志存为 `docs/images/logo.png`；
2. 另生成深色模式版本 `docs/images/logo-white.png` —— 只把深蓝笔画转成白色，浅绿的店面保留原色，暗色底上仍能看出前后两层；
3. 同一张图缩到 128×128，以 data URI 内嵌进 HTML 作为 favicon，不额外产生文件请求。