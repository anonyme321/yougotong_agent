# 优购通 V2.0 - AI驱动的电商个性化推荐系统

基于大语言模型、知识图谱和多模态理解的智能电商推荐平台，覆盖生鲜、电子数码、服装穿搭、美妆护肤四大品类。

## 项目简介

优购通是一个融合了 LangChain Agent、知识图谱（Neo4j）、向量数据库（Milvus）和多模态大模型（通义千问 Qwen-VL）的电商个性化推荐系统。用户可以通过自然语言对话或上传商品图片获取智能推荐。

## 核心功能

- **四大推荐模块**：生鲜食品、电子数码、服装穿搭、美妆护肤
- **多模态交互**：支持文本输入和图片上传，AI 自动分析图片内容并生成推荐
- **知识图谱驱动**：基于 Neo4j 构建商品知识图谱，支持结构化关系查询
- **向量语义检索**：基于 CLIP 模型构建商品向量数据库，支持语义相似度匹配
- **LangChain Agent**：集成通义千问大模型，实现意图理解和智能对话
- **用户系统**：完整的注册/登录功能，支持会话管理和历史记录

## 技术栈

| 类别 | 技术选型 |
|------|---------|
| 前端框架 | Streamlit |
| 大语言模型 | 通义千问 Qwen-Plus / Qwen-VL |
| Agent 框架 | LangChain |
| 知识图谱 | Neo4j |
| 向量数据库 | Milvus / ChromaDB |
| 多模态模型 | OpenAI CLIP (ViT-B/32) |
| 图片处理 | Pillow |
| 用户认证 | bcrypt + JSON 存储 |
| 数据处理 | Pandas, NumPy |

## 项目结构

```
new/2.0/
├── src/                          # 主应用代码
│   ├── app.py                    # Streamlit 主入口
│   ├── langchain_agent.py        # LangChain Agent 实现
│   ├── Auth.py                   # 用户认证模块
│   ├── db_operations.py          # 数据库操作
│   ├── fusion_service.py         # 融合推荐服务
│   ├── gradio_app.py             # Gradio 备选前端
│   └── modules/                  # 推荐子模块
│       ├── base_module.py        # 子模块抽象基类
│       ├── fresh_module.py       # 生鲜推荐
│       ├── electronic_module.py  # 电子数码推荐
│       ├── clothing_module.py    # 服装穿搭推荐
│       ├── face_module.py        # 美妆护肤推荐
│       ├── multimodal_llm.py     # 多模态LLM调用
│       ├── multimodal_embedding.py # 多模态向量化
│       ├── semantic_vector_store.py # 语义向量存储
│       └── *_knowledge_graph.py  # 各品类知识图谱
├── scripts/                      # 数据处理脚本
│   ├── import_*_knowledge_graph.py # 知识图谱导入
│   ├── build_*_vector_db.py      # 向量数据库构建
│   └── train_clip_*.py           # CLIP 模型训练
├── data/                         # 数据文件
├── models/                       # 模型文件
└── requirements.txt              # Python 依赖
```

## 快速开始

### 环境要求

- Python 3.10+
- Neo4j 数据库（可使用 Aura 云实例）

### 安装

```bash
# 克隆项目
git clone https://github.com/your-username/yougoutongzuizhong.git
cd yougoutongzuizhong/new/2.0

# 安装依赖
pip install -r requirements.txt
```

### 配置

在 `new/2.0/src/` 目录下创建 `.env` 文件：

```env
DASHSCOPE_API_KEY=your_dashscope_api_key
NEO4J_URI=neo4j+s://your_instance.databases.neo4j.io
NEO4J_USER=neo4j
NEO4J_PASSWORD=your_password
```

### 运行

```bash
# 启动 Streamlit 应用
cd new/2.0/src
streamlit run app.py
```

应用默认运行在 `http://localhost:8501`。

## 推荐流程

```
用户输入（文本/图片）
       │
       ▼
  LangChain Agent ──→ 意图识别 + 实体提取
       │
       ▼
  ┌────┴─────┐
  │          │
  ▼          ▼
Neo4j    CLIP 向量
知识图谱   数据库
  │          │
  └────┬─────┘
       ▼
  结果融合 + LLM 生成推荐
       │
       ▼
  返回用户推荐结果
```

## 许可证

本项目仅供学习和研究使用。
