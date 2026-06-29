# MasterGo2Figma Optimized Patch

本版本在原仓库基础上做了稳定性补丁：

1. 导出稳定性
   - 将页面分包阈值从 8000 图层降为 1200 图层，减少单包体积。
   - 将传输 chunk 从 64KB 降为 32KB，并更频繁 yield，降低插件 UI 卡死概率。
   - 文件/整体传输 ACK 超时时间加长，避免大文件本地流传输误判失败。
   - 图片资源读取增加 30 秒超时；单张异常图片会标记为 missing，不再拖死整个导出任务。
   - 导出图片资源阶段增加逐张进度提示。

2. 导入稳定性
   - 导入还原进度从每 100 节点改为每 20 节点，时间间隔从 500ms 改为 200ms，减少“看起来卡住”的情况。

3. 组合图层填充修复
   - MasterGo 的 GROUP 可能有填充/描边，但 Figma 原生 Group 不支持 fills。
   - 因此将 MasterGo GROUP 保留为 Figma Frame 容器，并保留 geometry paint，避免导入后组合图层无填充。

使用方式：
- MasterGo 导入 `SendToFigma/manifest.json`
- Figma 导入 `ReceiveFromMasterGo/manifest.json`

建议仍然分页面导出，尤其不要一次性导出草稿页、外部控件、组件库页。
