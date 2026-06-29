# v5：组合图层填充保留修复

本版重点修复 MasterGo 组合图层导入 Figma 后缺失填充的问题。

## 修复点

1. `GROUP / 组合` 继续以 `FRAME` 方式导入，避免 Figma 原生 Group 无法承载填充。
2. 给导入节点写入 `mg2figmaSourceType` / `mg2figmaHasOwnPaint` 插件元数据。
3. 优化导入完成后的容器清理逻辑：
   - 如果父节点是 MasterGo `GROUP` 转成的 Frame，不再删除同名 Rectangle / Fill 子图层。
   - 只有当父节点自己已经有可见 fills/strokes 时，才删除疑似重复的容器壳背景。
4. 避免把组合内部真正承载视觉颜色的 `Fill xx` / `Rectangle` 误删。

## 使用建议

- 使用新版 `ReceiveFromMasterGo Optimized v5` 导入。
- MasterGo 导出端建议也重新导入 `SendToFigma Optimized v5`，但本次修复主要在 Figma 导入端。
- 如果此前导入过缺失填充的页面，需要重新导入 zip；已导入的 Figma 图层不会自动修复。
