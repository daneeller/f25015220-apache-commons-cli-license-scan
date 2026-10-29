# 软件许可测试报告 — Apache Commons CLI

《开源创新思维》第 7 周作业（作业 1：第 2 章 开源合规与许可证）

- **学号**：f25015220
- **姓名**：陈思宇
- **班级**：f250117
- **测试对象**：[Apache Commons CLI](https://github.com/apache/commons-cli)（org.apache.commons:commons-cli，1.12.0-SNAPSHOT）
- **测试工具**：[ScanCode Toolkit 32.5.0](https://github.com/nexB/scancode-toolkit)（规则库对齐 SPDX License List 3.27）
- **扫描日期**：2026-10-29

## 一句话结论

对项目全部 **141 个受控文件**完成许可证/版权扫描：代码文件许可证检出率 **100%**，主体许可证为 **Apache-2.0**，与 LICENSE / NOTICE / 文件头三要素一致，运行时零依赖；发现 **9 个未声明文件**（多为 ASF 品牌图像资源）、**2 处表达式误报**（README / CONTRIBUTING 被并入 generic-cla）及**版权检测盲区**（ASF 标准头不含 Copyright 字样），报告均已分析并给出对策。

## 仓库结构

```
├── report/
│   ├── f25015220-陈思宇-ApacheCommonsCLI-软件许可测试报告.docx   # 作业报告（成品）
│   └── preview.pdf                                              # 报告 PDF 预览
├── scan-result/
│   ├── scancode-result.json        # ScanCode 原始 JSON 结果（Output Format 4.1.0）
│   ├── scancode-report.html        # ScanCode HTML 报告（可直接浏览器打开）
│   ├── fig_console.png             # 控制台输出摘要
│   └── fig_html_report.png         # HTML 报告节选
└── README.md
```

## 复现步骤

```bash
# 1. 环境（ScanCode 32.5.0 需 Python ≤3.12；pluggy 需 ≤1.5.0）
uv python install 3.12
uv venv --python 3.12 .venv-scan
uv pip install --python .venv-scan/Scripts/python.exe "scancode-toolkit==32.5.0" "pluggy==1.5.0"

# 2. 获取被测项目
git clone --depth 1 https://github.com/apache/commons-cli.git

# 3. 扫描（许可证 + 版权，2 进程）
.venv-scan/Scripts/scancode.exe -cl \
    --json-pp result/scancode-result.json \
    --html result/scancode-report.html \
    --processes 2 --timeout 120 commons-cli
```

## 关键数据

| 指标 | 结果 |
| --- | --- |
| 扫描文件 | 141（36 个目录） |
| 耗时 | 175.28 s（0.84 files/sec），0 错误 0 警告 |
| 许可证检出 | 132 文件（93.6%），其中 Apache-2.0 130 个 |
| 未检出 | 9 个（6.4%）：7 个图像资源 + 2 个无头文本 |
| 版权声明 | 仅 1 条（NOTICE.txt：Copyright 2002-2026 ASF） |
| 误报 | 2 个 Markdown 文件的复合表达式（人工复核确认） |
