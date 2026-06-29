# Selection Scope Patch v4

修复「选中画板」仍导出整个页面的问题。

根因：v3 在导出前的 rootCount / scan 预处理阶段会调用 clearTargetNodes，导致已按 selectedNodeIds 解析出来的选中画板节点被清空；后续真正导出时 ensureTargetNodes 会回退到当前页面的全部子节点，因此变成整页导出。

修复：当 scope === selected 时，预处理阶段不清空 target.nodes，只在导出完成后释放。
