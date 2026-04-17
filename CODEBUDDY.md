本仓库108中是缠中说禅当年的博客原文,因为比较零散,organized-v1是我们通过内容整理后的第一个版本

## graphify

This project has two graphify knowledge graphs:

- **graphify-out/** — organized-v1 的体系化图谱（主图谱，日常查询用）
- **graphify-out-108/** — 108 原始博客的碎片化图谱（回溯原文时用）

Rules:
- Before answering architecture or codebase questions, read graphify-out/GRAPH_REPORT.md for god nodes and community structure
- For questions about original blog content or lesson-level references, check graphify-out-108/GRAPH_REPORT.md
- If graphify-out/wiki/index.md exists, navigate it instead of reading raw files
- After modifying files in organized-v1/, run `/graphify organized-v1 --update` to keep the main graph current
