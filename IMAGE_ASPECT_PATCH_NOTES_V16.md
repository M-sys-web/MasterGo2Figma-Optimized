# v16 图片比例修复

新增“保持图片比例”选项，默认开启。

- 导出 IMAGE 填充时尝试保留 MasterGo 的 imageTransform / cropTransform / paintTransform。
- 如果没有可用裁剪矩阵，则把容易在 Figma 中被压扁的 CROP / TILE / FILL / STRETCH 图片降级为 FIT，优先保持图片原始比例。
- 与“图片保真 SVG”不同，本选项尽量保留图层，不把图片整体合并成 SVG。

建议：普通图片先开“保持图片比例”；仍然变形的营销图/复杂蒙版图片，再开“图片保真 SVG”。
