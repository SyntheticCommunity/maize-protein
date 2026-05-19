# Maize Protein Content Analysis

分析两种玉米品种（HY122=汉玉122、ZD958=郑单958）在营养生长期（VE—V5）不同器官的蛋白质含量差异。

## 技术栈

- **语言**: R
- **文档**: Quarto (.qmd) → HTML
- **可视化**: ggplot2（统一 `theme_bw`）
- **统计**: emmeans、aov
- **导出**: ggsave (PNG) + export::graph2ppt (PPTX)
- **解读集成**: jsonlite 读取视觉模型解读，results:asis 插入正文

## 目录结构

```
├── data/
│   ├── maize-protein-content.csv        # 原始数据
│   └── figure_interpretations.json       # 视觉模型图片解读
├── figures/                              # 导出的 PNG + PPTX
├── analysis.qmd                          # 主分析文档
└── .claude/settings.local.json           # 个人权限配置
```

## 约定

<important>
- ggplot 中禁止使用中文坐标轴/标签——创建 `xxx_en` 因子列用于绘图
- 所有 ggplot 统一使用 `theme_bw(base_size = 13)`
- fig-cap 只描述图形元素（坐标轴、颜色、图形含义），不含结果解读
- 结果解读从 `data/figure_interpretations.json` 读取，以 `results: asis` 写入正文
- 每张图同时导出 PNG（ggsave, dpi=300）和 PPTX（graph2ppt, append=TRUE）
</important>

## 分析流程

1. 探索数据 → 2. 编写 Quarto → 3. 首次渲染生成 PNG → 4. 视觉模型解读保存 JSON → 5. 最终渲染

## 常用命令

```bash
quarto render analysis.qmd        # 渲染文档
```
