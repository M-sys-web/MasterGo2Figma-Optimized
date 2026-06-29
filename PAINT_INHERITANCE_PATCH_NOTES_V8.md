# v8 painted vector container fallback

修复场景：MasterGo 中外层 `Fill xx` 有颜色，但内部 `组/路径` 没有独立填充；导入 Figma 后只导入了内部路径，导致图标/Logo 变成空白或灰色。

策略：
- 识别有可见填充/描边的外层容器，且其子树基本由矢量路径构成；
- 将该外层容器整体导出为 SVG 兜底；
- 在 Figma 导入端用 `createNodeFromSvg` 还原，避免丢失父层填充关系；
- 对业务页面的普通 Frame、文本、图片不会触发此兜底。

代价：命中的 Logo / 图标会更偏“视觉还原”，局部可编辑性弱于逐路径重建。
