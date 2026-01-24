# 用 React 写视频，这是什么操作？

如果你会写前端，大概率做过这种事：用 CSS 做动画、用 React 组织组件、用 npm 包解决问题。那如果告诉你，这些东西能用来做视频呢？

这就是 Remotion 干的事。

目前这个项目在 GitHub上有 2.9 万星，接近 4000 个项目依赖它。它让你用代码写视频——不用拖时间轴，不用点鼠标，就和写网页一样。



![项目概念图](https://s.coze.cn/image/jTSRDJvxBnI/)




## 它能干什么

### 组件化 + 帧级控制

把视频拆成组件，每个组件是一段画面、一个动画或一个场景。props、state、生命周期，React 有的它都有。`useCurrentFrame()` 这个 hook 会告诉你当前在第几帧，你可以在任意帧触发动画、改变样式、切换场景。

不用拖时间轴，代码写清楚，帧数就精确了。组件也能复用，比如做一个片头，所有视频都能用。

### 前端技术全都能用

CSS 动画、Canvas 绘图、SVG、WebGL 3D——浏览器里能做的，视频里都能做。这就把整个前端生态都接进来了。修改代码，预览窗口立马更新，不用渲染等待，和开发网页一个体验。

### 数据驱动，批量输出

从 API 拉数据，自动生成视频。比如 GitHub 年度贡献数据，可以用代码自动生成个性化视频，一人一份不用手动改。输出支持 MP4、GIF、WebM，分辨率可以配到 8K，帧率 1-120fps 随便选。

## 技术架构

原理其实不复杂：用无头浏览器一帧帧渲染 React 组件，然后合成视频。

配置层在 `remotion.config.ts` 里设置帧率、分辨率这些参数。组件层就是 React 组件树，每个组件对应一段视频。渲染层用 Puppeteer 跑无头 Chrome，把每帧的 DOM 树截图。输出层用 FFmpeg 把图片序列编码成视频。

Studio 是开发工具，基于 Vite，用来实时预览。

![技术架构图](https://s.coze.cn/image/aYGnbS8psx8/)

## 什么时候用得上

### 技术内容和数据可视化

Fireship 那个快节奏的 YouTube 频道就是用 Remotion 做的，代码实现转场、动画、数据可视化，比手动调效率高。把统计数据做成视频，比静态图表有冲击力。

### 批量生成个性化内容

年度账单、个人成就报告、定制营销视频——一人一份，代码自动生成。TikTok、YouTube Shorts、Instagram Reels，用模板加数据，可以批量出内容。GitHub Unwrapped 就是这么干的。

### 品牌和产品视频

产品介绍、广告片、宣传片，代码化之后改内容方便，品牌风格也能保持一致。



## 快速开始

```bash
npx create-video@latest
cd my-video
npm install
npm start
```

写个简单组件：

```tsx
// src/Root.tsx
import { Composition } from "remotion";
import { MyVideo } from "./MyVideo";

export const RemotionRoot: React.FC = () => {
  return (
    <>
      <Composition
        id="MyVideo"
        component={MyVideo}
        durationInFrames={300}
        fps={30}
        width={1920}
        height={1080}
      />
    </>
  );
};

// src/MyVideo.tsx
import { useCurrentFrame } from "remotion";

export const MyVideo: React.FC = () => {
  const frame = useCurrentFrame();
  const opacity = Math.min(1, frame / 30);

  return (
    <div style={{
      flex: 1,
      backgroundColor: "white",
      justifyContent: "center",
      alignItems: "center",
      display: "flex",
      opacity,
    }}>
      <h1 style={{ fontSize: 80 }}>Hello Remotion!</h1>
    </div>
  );
};
```

渲染：

```bash
npm run build
```

跑一下，视频会展示"Hello Remotion!"，前 30 帧淡入。整个过程不用碰视频编辑软件。

## 总结

Remotion 把前端开发的工程化能力带进了视频制作。相比 After Effects、Premiere 这些工具，它的优势是可维护、可复用、可自动化。

什么时候用它？批量生成视频、频繁改内容、想用代码玩创意。短视频和个性化内容需求还在增长，这类工具会越来越常见。

如果你是前端开发者，想试试视频创作，Remotion 是个不错的切入点。上手快，生态熟，有问题社区也活跃。

非前端开发者的话，建议先学点 React 基础。复杂动画可以配合 Framer Motion，渲染长视频记得用并行参数。商业用途注意授权条款。

官方 Showcase (https://remotion.dev/showcase) 有不少案例，可以看看别人怎么玩。
