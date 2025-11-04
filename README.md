# 🔬 Open Deep Research

Open Deep Research 是一个可配置的深度研究代理，支持多家模型、搜索服务与 MCP（Model Context Protocol）工具。项目内包含从需求澄清、资料检索到报告撰写的完整多代理工作流，可通过本地可视化界面进行调试与扩展。

## 🚀 快速开始

1. **准备环境**
   ```bash
   cd open_deep_research
   uv venv
   source .venv/bin/activate  # Windows: .venv\Scripts\activate
   ```
2. **安装依赖**
   ```bash
   uv sync
   ```
3. **配置密钥**
   ```bash
   cp .env.example .env
   # 填写所需的 API Key，例如 OPENAI_API_KEY、ANTHROPIC_API_KEY、GOOGLE_API_KEY、DEEPSEEK_API_KEY 等
   ```
4. **启动本地服务**
   ```bash
   uvx --refresh --from "langgraph-cli[inmem]" --with-editable . --python 3.11 langgraph dev --allow-blocking
   ```
   启动后可在浏览器内访问 Studio UI，向代理发送问题并观察流程图运行情况。

## ⚙️ 关键配置

### 模型设置

`src/open_deep_research/configuration.py` 中提供以下核心字段，可在 Studio UI 或环境变量中覆盖：

- `summarization_model`：对搜索结果进行摘要的模型。
- `research_model`：驱动研究流程的主模型。
- `compression_model`：整合子代理输出的模型。
- `final_report_model`：撰写最终报告的模型。

每个字段都可配合 `*_max_tokens` 限制生成长度。

### 搜索与 MCP

- `search_api`：选择 Tavily、OpenAI/Anthropic 原生搜索或关闭搜索功能。
- `mcp_config` / `mcp_prompt`：配置 MCP 服务器地址、可用工具及额外指令。

### 其他参数

- `max_concurrent_research_units`：并发研究代理数量。
- `max_structured_output_retries`：结构化输出失败时的重试次数。
- `max_content_length`：网页摘要前允许的内容长度。

所有字段均可通过环境变量（大写字段名）或 Studio UI 的 “Manage Assistants” 面板调整。

## 📂 目录结构

- `src/open_deep_research/`：主工作流、工具与配置。
- `tests/`：评估脚本与回归数据。
- `examples/`：示例研究脚本与说明。
- `src/security/`：本地部署所需的认证逻辑。
- `langgraph.json`：可视化调试与部署使用的图配置。

## 🧪 测试与质量

- 单元与集成测试：`uv run pytest`
- 静态检查：`uv run ruff check .`
- 类型检查：`uv run mypy src`

如修改了检索或摘要逻辑，建议更新 `tests/expt_results/` 中的基准数据以防回归。

## 🏛️ Legacy 版本

`src/legacy/` 保留了早期的两套实现，提供不同的多代理拓扑与实验性的工具使用方式。若需调研旧版本的思路，可参考其中的文档与示例代码。

