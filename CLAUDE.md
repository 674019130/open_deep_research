# Open Deep Research Repository Overview

## Project Description
Open Deep Research 是一套可配置的自动化研究代理，支持多种模型提供方、搜索接口与 MCP（Model Context Protocol）服务器，可用于快速搭建端到端的深度研究流程。

## Repository Structure

### Root Directory
- `README.md` - 项目说明与快速开始
- `pyproject.toml` - Python 项目配置
- `langgraph.json` - 图工作流入口定义
- `uv.lock` - UV 包依赖锁定文件
- `LICENSE` - 许可证
- `.env.example` - 环境变量示例（未跟踪）

### Core Implementation (`src/open_deep_research/`)
- `deep_researcher.py` - 主图工作流（入口：`deep_researcher`）
- `configuration.py` - 统一的配置管理
- `state.py` - 工作流状态与数据结构
- `prompts.py` - 系统提示词与模版
- `utils.py` - 辅助函数集合
- `files/` - 样例输出与附加文件

### Legacy Implementations (`src/legacy/`)
包含两套历史实现：
- `graph.py` - 计划—执行式工作流
- `multi_agent.py` - 监督者-研究员多代理架构
- `legacy.md`、`CLAUDE.md` - 旧版文档
- `tests/` - 旧版评估脚本

### Security (`src/security/`)
- `auth.py` - 本地部署用的认证逻辑

### Testing (`tests/`)
- `run_evaluate.py` - 评估脚本
- `evaluators.py`、`prompts.py` 等 - 测试与比对工具

### Examples (`examples/`)
- `arxiv.md`、`pubmed.md` 等示例研究场景

## Key Technologies
- **图工作流引擎**：用于编排多节点研究流程
- **多家模型 API**：OpenAI、Anthropic、Google、DeepSeek 等
- **搜索服务**：Tavily 以及原生搜索接口
- **MCP 服务器**：扩展外部工具访问能力

## Development Commands
- `uvx langgraph dev` - 启动本地可视化调试环境
- `python tests/run_evaluate.py` - 执行完整评估
- `uv run ruff check .` - 代码静态检查
- `uv run mypy src` - 类型检查

## Configuration
配置方式包括：
- 环境变量（`.env`）
- Studio UI 中的可视化配置面板
- 直接修改 `configuration.py`

常见可调项覆盖模型选择、搜索设置、并发数量和 MCP 相关参数。
