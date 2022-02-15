---
id: NO0UZdPO2yU8m2BU9lm0j
title: 积累
desc: ''
updated: 1644920756775
created: 1644920583717
---

## 如何使用canvas制作页面水印

```typescript
    const generateWatermark = () => {
  // <p>由数势云创提供技术支持，</p>
  // <p>仅供{{ companyInfo.tenantName }}商家回测使用</p>
    const watchCanvas = document.createElement("canvas");
    watchCanvas.id = "myCanvas";
    watchCanvas.width = 300;
    watchCanvas.height = 200;
    watchCanvas.style.display = "none";
    document.documentElement.appendChild(watchCanvas);

    const ctx = watchCanvas.getContext("2d"); // 获取canvas上下文
    ctx.font = "12px Arial"; // 设置字体
    ctx.fillStyle = "rgba(0,0,0,0.2)";  // 设置canvas填充样式
    ctx.rotate((-15 * Math.PI) / 180);  // 设置水印旋转
    ctx.fillText("由数势云创提供技术支持，", 20, 80);  // 设置水印内容
    ctx.fillText(`仅供${companyInfo.value.tenantName}商家回测使用`, -20, 100);

    const curl = watchCanvas.toDataURL("image/png");  // 把canvas转换为url

    document.getElementById("content").style.background =
        "#0000 url(" + curl + ")";
};
```
