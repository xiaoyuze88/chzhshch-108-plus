本仓库108中是缠中说禅当年的博客原文,因为比较零散,organized-v1是我们通过内容整理后的第一个版本,graphify-out是我们针对 108 目录做的知识图谱扫描

## graphify

This project has a graphify knowledge graph at graphify-out/.

Rules:
- Before answering architecture or codebase questions, read graphify-out/GRAPH_REPORT.md for god nodes and community structure
- If graphify-out/wiki/index.md exists, navigate it instead of reading raw files
- After modifying code files in this session, run `python3 -c "from graphify.watch import _rebuild_code; from pathlib import Path; _rebuild_code(Path('.'))"` to keep the graph current
