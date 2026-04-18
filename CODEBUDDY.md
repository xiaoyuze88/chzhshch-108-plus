本仓库108中是缠中说禅当年的博客原文,因为比较零散,organized-v1是我们通过内容整理后的第一个版本

## graphify

This project has two graphify knowledge graphs:

- **graphify-out/** — `organized-v2/` 的体系化图谱（主图谱，日常查询用）
- **archived/graphify-out-108/** — `archived/108/` 原始博客的碎片化图谱（回溯原文、课文级问题、图例出处时用）

Rules:
- For `organized-v2/` 的体系、概念关系、跨章节问题，先读 `graphify-out/GRAPH_REPORT.md` 了解 god nodes 与 community structure
- For 原始博客措辞、课文级引用、图例出处、原文上下文问题，先读 `archived/graphify-out-108/GRAPH_REPORT.md`
- If the target graph directory contains a wiki-style index, navigate that index instead of reading raw graph data files
- After modifying files in `organized-v2/`, run `/graphify organized-v2 --update` to keep the main graph current

## 缠论知识库查询规则

知识库位置：`organized-v2/`（36个章节文件，约2.8万字）
主图谱数据：`graphify-out/graph.json`（供 graphify query 命令使用，不要直接 Read）
原文图谱报告：`archived/graphify-out-108/GRAPH_REPORT.md`（108 原文回溯用）
附录速查：
- `organized-v2/附录/A-定义速查.md` — 全部 `📖定义` 条目，精确充要条件表述
- `organized-v2/附录/B-定理索引.md` — 全部 `📐定理` 条目，前提→结论完整逻辑链
- `organized-v2/附录/C-操作规则总表.md` — 全部 `💡操作规则`，含前提/触发/操作/冲突优先级
- `organized-v2/附录/D-状态条件速查.md` — 15种市场状态组合→映射附录C规则ID
- `organized-v2/附录/E-原文索引.md` — 课文编号→v2章节反向索引

**总原则：附录负责“准”，图谱负责“广”，正文负责“深”；这里的“附录优先”指先做低成本命中检测，而不是先完整阅读附录。**
- **低成本命中检测** = 只做词条名 / 标题 / 规则ID / 状态组合 / 课文编号级别的检索与定位；检测阶段**不要先完整读取附录正文**，也**不要横向扫完全部附录**。应先按题型锁定**单个候选附录**，未命中则立即转图谱或正文路径。
- **命中分两层**：`存在性命中` = 确认附录里有相关条目；`答案级命中` = 附录内容本身已足以直接回答用户。只有达到答案级命中时，才可以不补正文；若只是存在性命中，则继续到正文或图谱核对适用边界、上下文和推导。
- 对于**定义类 / 定理类 / 操作类 / 溯源类**问题，先根据题型锁定候选附录，并做**低成本命中检测**（如词条、规则ID、状态组合、课文映射）；只有检测到相关条目时，才读取附录正文。若附录不足以覆盖，再补图谱或正文。
- 对于**关系类 / 综合类 / 模糊提问**，先用图谱定位范围，再回附录抽取标准表述，最后用正文补足推导与上下文。
- **不要把图谱节点标签、社区名称或边关系直接当答案输出**；图谱只用于导航、定位、关系发现，标准定义/定理/规则以附录和正文为准。

**当用户提问任何缠论相关问题时，执行以下流程：**

0. **问题分类与路由（优先级最高）**：先判断问题类型，再决定默认入口；**不要跳过分类，直接机械执行“附录优先”**。
   - 【定义类】“什么是X” / “X的定义” → **先对附录A做低成本命中检测**；命中后读取对应定义条目，必要时再读对应章节正文
   - 【定理类】“X定理的前提/结论” → **先对附录B做低成本命中检测**；命中后读取对应定理条目，必要时再读对应章节正文
   - 【操作类】“当前应该怎么做” / “X之后怎么办” / “如何操作” → 若问题已经能清楚映射为**状态组合/规则表查询**，则**先探测附录D**；命中后再查**附录C** 获取操作规则；回答时**必须引用规则ID与冲突优先级**。若状态描述本身模糊、附录无法唯一定位或规则边界不明确，则**直接先用主图谱缩小范围**，再回附录/正文确认
   - 【溯源类】“原文怎么说” / “108课怎么讲” / “这句话出自哪课” → **先对附录E做低成本命中检测**，定位 `organized-v2` 章节；若用户要看原始博客措辞、图例出处或课文上下文，再转查 `archived/108/`，并优先参考 `archived/graphify-out-108/GRAPH_REPORT.md`
   - 【关系类】“X和Y的关系” / “X怎么影响Y” / “X在体系里的位置” → **先用主图谱定位**，再回附录与正文确认
   - 【综合类】不确定类型、跨多个概念、同时涉及定义+关系+操作 → **先用主图谱定位范围**，再对照附录抽取结构化信息，最后读正文组织答案

1. **按路由结果执行：先探测，再决定是否正式读取**（仅定义类 / 定理类 / 可清晰映射的操作类 / 溯源类默认做附录探测）：
   - 优先在 `organized-v2/附录/` 中做**低成本命中检测**，确认是否存在相关定义、定理、规则、状态映射或课文索引
   - 若附录达到**答案级命中**，则只补充必要正文，不必强行走图谱
   - 若附录只有**存在性命中**，只能给出索引、规则ID或候选范围，则继续到对应章节正文核对上下文与适用边界
   - 若附录未命中，或问题一开始就属于关系类 / 综合类 / 模糊提问，则转入主图谱缩小正文范围，再读相关章节

2. **用 graphify query 定位相关文件**（关系类 / 综合类必做；其他类型仅在附录不足或问题模糊时补做）：从问题中提取 2-4 个核心中文关键词，替换下方 `terms`，运行命令，获得 BFS 遍历后的相关文件列表：

```bash
cd /Users/xyz/Sites/private/chzhshch-108-plus && python3 -c "
import sys, json
from networkx.readwrite import json_graph
from pathlib import Path

data = json.loads(Path('graphify-out/graph.json').read_text())
G = json_graph.node_link_graph(data, edges='links')

# 从问题提取关键词（中文不能用 split()，由模型手动列出）
terms = ['关键词1', '关键词2']  # ← 替换为实际关键词

# 找匹配的起始节点（子串匹配，无长度限制）
scored = []
for nid, ndata in G.nodes(data=True):
    label = ndata.get('label', '').lower()
    score = sum(1 for t in terms if t in label)
    if score > 0:
        scored.append((score, nid))
scored.sort(reverse=True)
start_nodes = [nid for _, nid in scored[:3]]

if not start_nodes:
    print('No matching nodes found for terms:', terms)
    sys.exit(0)

# BFS depth=3 扩展邻居节点
frontier = set(start_nodes)
subgraph_nodes = set(start_nodes)
for _ in range(3):
    next_frontier = set()
    for n in frontier:
        for neighbor in G.neighbors(n):
            if neighbor not in subgraph_nodes:
                next_frontier.add(neighbor)
    subgraph_nodes.update(next_frontier)
    frontier = next_frontier

# 输出去重的 source_file 列表（按相关度排序）
def relevance(nid):
    return sum(1 for t in terms if t in G.nodes[nid].get('label', '').lower())

ranked = sorted(subgraph_nodes, key=relevance, reverse=True)
files = list(dict.fromkeys(
    G.nodes[n].get('source_file') for n in ranked
    if G.nodes[n].get('source_file')
))
for f in files[:8]:
    print(f)
"
```

3. **阅读正文**：用 Read 工具读取上一步定位到的 `organized-v2/` 文件（通常 1-3 个即可）
   - 读每个文件时，先检查文件头的 `<!-- 前置知识：... -->` 注释
   - 若有前置知识，先读前置知识对应的文件，再读当前文件
   - 前置知识文件路径规则：同目录下同章节编号（如 `P3-09` 的前置 → 找 `P3-08`）
   - 若问题是原文回溯类，再按需读取 `archived/108/` 对应课文或图例文件

4. **理解后回答**：用自己的话回答，要求：
   - 先给结论，再给推导
   - 用日常语言，避免直接引用术语堆砌
   - 可以举例类比
   - 如果问题跨多个章节，先读再综合
   - 回复结尾附上“📎 引用来源”，列出本次阅读的文件路径及用到的具体段落标题（如 `P3-08 § 定义一`），方便用户深入查阅

**禁止**：不要把图谱节点标签或边关系直接当答案输出。`graph.json` 不要用 Read 直接读，那是机器格式，只能通过上述 `python3` 命令查询。

## organized-v2 项目

正在将 organized-v1 的简单聚合内容提炼为教科书式知识体系。

**关键文件：**
- 设计规格: `docs/superpowers/specs/2026-04-17-organized-v2-textbook-design.md`
- 实施计划: `docs/superpowers/plans/2026-04-17-organized-v2-textbook.md`
- 进度表: `v2-systematic/PROGRESS.md`
- 工作目录: `v2-systematic/`（prompt、draft）
- 输出目录: `organized-v2/`

**当用户说"继续 organized-v2"或"恢复 v2 任务"时：**
1. 读取 memory 中的进度记录
2. 读取 `v2-systematic/PROGRESS.md` 获取细粒度状态
3. 僵尸清理：将"进行中"全改为"失败"
4. 从断点继续执行

## 目录结构

```
archived/108/              # 缠中说禅原始博客原文（零散）
archived/organized-v1/     # 第一版整理：通过 systematic/ 流程从 archived/108 整理而来
archived/graphify-out-108/ # archived/108 的知识图谱
archived/graphify-out-v1/  # archived/organized-v1 的知识图谱
organized-v2/              # 第二版整理：通过 v2-systematic/ 流程从 archived/organized-v1 提炼而来（当前主版本）
```

## 溯源路径

```
archived/108  →(archived/systematic/)→  archived/organized-v1  →(archived/v2-systematic)→  organized-v2
     ↓                                         ↓
archived/graphify-out-108            archived/graphify-out-v1
```

如需溯源某个知识点，可按此路径逐层回溯至原始博客。