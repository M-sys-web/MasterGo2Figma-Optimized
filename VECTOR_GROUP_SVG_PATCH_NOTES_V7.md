# v7 Vector-only Group SVG Fallback

修复方向：MasterGo 中由多个路径/Fill 组成的 Logo/Icon 组合，在导入 Figma 后可能只剩轮廓或局部填充。

原因：这些组合的子路径经常没有 Figma 可用的 vectorNetwork.regions，单独转 Vector 会丢失填充区域。

本版处理：
- 对 GROUP 类型且子树几乎全是 PEN/VECTOR/Fill 的小型组合，自动导出为 SVG。
- 导入端用 Figma createNodeFromSvg 还原，优先保证视觉正确。
- 此类 Logo/Icon 的局部可编辑性会下降，但整体视觉会更稳定。
