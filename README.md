# AI-Router 🚀

<p align="center">
  <strong>企业级 AI 网关平台 | Enterprise-Level AI Gateway</strong>
</p>

<p align="center">
  统一接口调用多个主流 AI 模型，支持智能路由、自动故障转移、实时监控
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.12-blue" alt="Python"/>
  <img src="https://img.shields.io/badge/FastAPI-0.104+-brightgreen" alt="FastAPI"/>
  <img src="https://img.shields.io/badge/Vue-3.5-green" alt="Vue"/>
  <img src="https://img.shields.io/badge/Docker-latest-blue" alt="Docker"/>
  <img src="https://img.shields.io/badge/License-MIT-yellow" alt="License"/>
</p>

---

## 📖 项目简介

AI-Router 是一个参考 [OpenRouter.ai](https://openrouter.ai/) 设计的**企业级 AI 网关平台**，提供统一的 API 接口来访问多个主流 AI 模型（通义千问、智谱AI、DeepSeek、OpenAI 等），实现智能路由、自动故障转移、完善的监控体系和 Python SDK 支持。

### 🎯 核心价值

| 特性 | 说明 | 价值 |
|------|------|------|
| 🔌 **即插即用** | 兼容 OpenAI SDK 格式，一行代码切换模型 | 零学习成本 |
| 🛡️ **高可用设计** | 智能重试 + 健康检查 + 自动 Fallback | 99.9% 可用性 |
| 🎯 **智能路由** | 支持 auto 模式（成本/速度优先） | 成本降低 30%+ |
| 📊 **全链路监控** | Prometheus + Grafana + TraceId 追踪 | 秒级定位问题 |
| 🚀 **开发者友好** | Python SDK + 完整文档 + 示例代码 | 5 分钟上手 |
| 💰 **消耗透明** | 实时统计 Token 消耗与费用 | 成本可控 |

---

## ✨ 功能特性

### 核心功能

- **🤖 多模型接入**：支持通义千问、智谱AI、DeepSeek 等主流大模型
- **💬 在线对话**：支持流式响应、多轮对话、上下文管理
- **🔑 API Key 管理**：创建、查看、撤销 API Key，支持调用统计
- **📊 Token 统计**：实时统计每次请求的 Token 消耗
- **🖼️ AI 绘图**：支持通义万相、智谱 CogView 等文生图模型
- **💳 在线充值**：Stripe 支付集成，支持余额管理

### 高级特性

- **🔀 智能路由**：成本优先 / 速度优先 / 轮询策略
- **♻️ 自动 Fallback**：模型故障自动切换到备用模型
- **⏱️ 智能重试**：指数退避重试策略
- **🔒 安全防护**：IP 黑名单、请求限流、TraceId 追踪
- **🔌 插件系统**：Web 搜索、PDF 解析、图片识别
- **🗝️ BYOK 支持**：用户自带 API Key，直连模型

### 监控告警

- **📈 实时监控**：QPS、成功率、错误率、延迟分布
- **📉 Prometheus 指标**：完整的业务指标导出
- **📊 Grafana 大盘**：预置监控仪表盘

---

## 🛠️ 技术栈

### 后端技术

| 技术 | 版本 | 说明 |
|------|------|------|
| Python | 3.12+ | 编程语言 |
| FastAPI | 0.104+ | 异步 Web 框架 |
| SQLAlchemy | 2.0+ | ORM 框架 |
| Pydantic | 2.0+ | 数据验证 |
| httpx | 0.25+ | 异步 HTTP 客户端 |
| aiomysql | 0.2.0+ | 异步 MySQL 驱动 |
| Redis | 7+ | 缓存 / Session / 分布式锁 |
| LangChain | 0.1+ | AI 模型集成框架 |
| Stripe | 10+ | 在线支付 |
| Prometheus | 2.48+ | 指标收集 |

### 前端技术

| 技术 | 版本 | 说明 |
|------|------|------|
| Vue | 3.5.17 | 前端框架 |
| Vite | 7.0.0 | 构建工具 |
| Ant Design Vue | 4.2.6 | UI 组件库 |
| Pinia | 3.0.3 | 状态管理 |
| ECharts | 5.5.0 | 图表组件 |
| Axios | 1.11.0 | HTTP 客户端 |
| TypeScript | 5.8.0 | 类型安全 |

### 基础设施

| 组件 | 说明 |
|------|------|
| Docker + Docker Compose | 容器化部署 |
| Nginx | 反向代理 / 负载均衡 |
| Prometheus | 指标存储 |
| Grafana | 监控可视化 |

---

## 🏗️ 系统架构

```
┌─────────────────────────────────────────────────────────────────┐
│                        客户端层                                  │
│   ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐        │
│   │ Java SDK │  │ 前端应用  │  │ HTTP API │  │  其他SDK  │        │
│   └────┬─────┘  └────┬─────┘  └────┬─────┘  └────┬─────┘        │
└────────┼─────────────┼─────────────┼─────────────┼──────────────┘
         │             │             │             │
         ▼             ▼             ▼             ▼
┌─────────────────────────────────────────────────────────────────┐
│                     API 网关层                                   │
│  ┌─────────────────────────────────────────────────────────┐    │
│  │                   认证 & 鉴权层                           │    │
│  │     • API Key 验证    • 权限检查    • 配额控制              │   │
│  └──────────────────────────┬──────────────────────────────┘    │
│                              │                                  │
│  ┌──────────────────────────▼──────────────────────────────┐    │
│  │                    智能路由层                             │    │
│  │  • 成本优先路由    • 速度优先路由    • 健康检查              │    │
│  │  • 自动 Fallback   • 负载均衡      • 模型映射              │    │
│  └──────────────────────────┬──────────────────────────────┘    │
│                              │                                  │
│  ┌──────────────────────────▼──────────────────────────────┐    │
│  │                   模型调用层 (Spring AI)                  │    │
│  │  • 统一接口封装    • 流式响应    • 智能重试                 │    │
│  │  • 超时控制        • 响应缓存    • 错误处理                 │    │
│  └───────┬────────────────┬────────────────┬───────────────┘    │
└──────────┼────────────────┼────────────────┼────────────────────┘
           │                │                │
           ▼                ▼                ▼
    ┌──────────┐     ┌──────────┐     ┌──────────┐
    │ 通义千问  │     │  智谱AI   │     │ DeepSeek │  ...更多模型
    └──────────┘     └──────────┘     └──────────┘
```

---

## 📁 项目结构

```
ai-router/
├── frontend/                        # 前端项目 (Vue.js)
│   ├── src/
│   │   ├── api/                     # API 接口定义
│   │   ├── components/              # 公共组件
│   │   ├── layouts/                 # 布局组件
│   │   ├── pages/                   # 页面
│   │   │   ├── admin/               # 管理员页面
│   │   │   └── user/                # 用户页面
│   │   ├── router/                  # 路由配置
│   │   └── stores/                  # Pinia 状态管理
│   ├── Dockerfile                   # 前端 Docker 配置
│   └── package.json
├── python-backend/                  # Python 后端项目
│   ├── app/
│   │   ├── adapter/                 # 模型适配器
│   │   │   ├── dashscope_adapter.py    # 通义千问适配器
│   │   │   ├── deepseek_adapter.py     # DeepSeek 适配器
│   │   │   ├── openai_adapter.py       # OpenAI 适配器
│   │   │   ├── zhipu_adapter.py        # 智谱AI 适配器
│   │   │   └── adapter_factory.py      # 适配器工厂
│   │   ├── api/                     # API 路由 (Controllers)
│   │   │   ├── apikey.py            # API Key 管理
│   │   │   ├── chat.py              # 对话接口 (OpenAI 兼容)
│   │   │   ├── image.py             # AI 绘图接口
│   │   │   └── ...
│   │   ├── models/                  # 数据模型
│   │   │   ├── schemas/             # Pydantic 数据模型
│   │   │   └── db/                  # 数据库实体
│   │   ├── services/                # 业务逻辑
│   │   │   ├── chat_service.py      # 对话服务
│   │   │   ├── routing_service.py   # 路由服务
│   │   │   ├── health_service.py    # 健康检查服务
│   │   │   └── billing_service.py   # 计费服务
│   │   ├── strategy/                # 路由策略
│   │   ├── middleware/              # 中间件 (认证、限流等)
│   │   ├── task/                    # 异步任务 (健康检查等)
│   │   └── utils/                   # 工具类
│   ├── Dockerfile                   # 后端 Docker 配置
│   ├── requirements.txt             # Python 依赖
│   ├── run.py                       # 启动脚本
│   └── main.py                      # FastAPI 主文件
├── yu-ai-router-sdk/                # Python SDK
│   ├── yu_ai_router_sdk/
│   │   ├── client.py                # 客户端
│   │   ├── models.py                # 数据模型
│   │   └── config.py                # 配置
│   ├── examples/                    # 示例代码
│   └── pyproject.toml               # Python 项目配置
├── sql/                             # SQL 脚本
│   └── create_table.sql             # 建表语句
├── grafana/                         # Grafana 配置
│   ├── provisioning/
│   │   ├── dashboards/              # 监控仪表板
│   │   └── datasources/             # 数据源配置
├── docker-compose.yml               # Docker Compose 配置
├── prometheus.yml                   # Prometheus 配置
└── README.md                        # 项目文档
```

---

## 🚀 快速开始

### 环境要求

- Python 3.12+
- Node.js 22+
- MySQL 8.0+
- Redis 7.0+

### 本地开发

#### 1. 克隆项目

```bash
git clone https://github.com/your-repo/ai-router.git
cd ai-router
```

#### 2. 初始化数据库

```bash
# 执行 SQL 脚本创建数据库和表
mysql -u root -p < sql/create_table.sql
```

#### 3. 配置 Python 后端

进入后端目录并创建虚拟环境：

```bash
cd python-backend
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

配置环境变量，创建 `.env` 文件：

```bash
# 数据库配置
DATABASE_URL=mysql+aiomysql://root:123456@localhost:3306/yu_ai_router
REDIS_URL=redis://localhost:6379

# AI 模型配置
DASHSCOPE_API_KEY=your-qwen-api-key
DEEPSEEK_API_KEY=your-deepseek-api-key
ZHIPU_API_KEY=your-zhipu-api-key
OPENAI_API_KEY=your-openai-api-key

# Stripe 配置
STRIPE_API_KEY=your-stripe-api-key
```

#### 4. 启动后端服务

```bash
python run.py
```

访问 API：http://localhost:8123/api

#### 5. 启动前端

```bash
cd frontend
npm install
npm run dev
```

访问前端页面：http://localhost:5173

---

## 🐳 Docker 部署

### 一键部署（推荐）

```bash
docker-compose up -d
```

服务访问地址：

| 服务 | 地址 |
|------|------|
| 前端页面 | http://localhost |
| 后端 API | http://localhost:8123/api |
| Prometheus | http://localhost:9090 |
| Grafana | http://localhost:3000 (admin/admin) |

### 单独构建

```bash
# 构建后端镜像
cd python-backend
docker build -t ai-router-backend .

# 构建前端镜像
cd ../frontend
docker build -t ai-router-frontend .
```

---

## 📡 API 使用

### 对话接口（兼容 OpenAI 格式）

```bash
curl -X POST "http://localhost:8123/api/v1/chat/completions" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer sk-your-api-key" \
  -d '{
    "model": "qwen-plus",
    "messages": [
      {"role": "user", "content": "你好"}
    ],
    "stream": true
  }'
```

### 支持的模型

| 模型标识 | 提供商 | 说明 |
|----------|--------|------|
| `qwen-plus` | 通义千问 | 增强版，性能更强 |
| `qwen-turbo` | 通义千问 | 快速版，响应更快 |
| `qwen-max` | 通义千问 | 旗舰版，支持深度思考 |
| `glm-4.7` | 智谱AI | 高智能旗舰模型 |
| `glm-4.6` | 智谱AI | 超强性能模型 |
| `glm-4.7-flash` | 智谱AI | 免费模型 |
| `deepseek-chat` | DeepSeek | 对话模型 |
| `deepseek-reasoner` | DeepSeek | 支持深度思考 |
| `deepseek-coder` | DeepSeek | 代码模型 |

### 智能路由

```bash
# 使用 auto 模式，自动选择最优模型
curl -X POST "http://localhost:8123/api/v1/chat/completions" \
  -H "Authorization: Bearer sk-your-api-key" \
  -d '{
    "model": "auto",
    "messages": [{"role": "user", "content": "你好"}],
    "routing_strategy": "cost_first"
  }'
```

路由策略：
- `cost_first`：成本优先，选择最便宜的健康模型
- `latency_first`：速度优先，选择响应最快的模型
- `round_robin`：轮询所有健康模型

---

## 📦 Python SDK

### 安装

```bash
pip install yu-ai-router-sdk
```

或本地安装：

```bash
cd yu-ai-router-sdk
pip install -e .
```

### 使用示例

```python
from yu_ai_router_sdk import AIRouter

# 创建客户端
client = AIRouter(
    api_key="sk-your-api-key",
    base_url="http://localhost:8123/api"
)

# 同步调用
response = client.chat("你好")
print(response)

# 指定模型
response = client.chat("你好", model="qwen-plus")
print(response)

# 流式调用
for chunk in client.chat_stream("讲一个故事"):
    print(chunk, end="", flush=True)

# 指定路由策略
response = client.chat(
    "你好",
    model="auto",
    routing_strategy="cost_first"
)
print(response)
```

---

## 📊 监控指标

### Prometheus 指标

| 指标名称 | 类型 | 说明 |
|----------|------|------|
| `ai_gateway_requests_total` | Counter | 请求总数 |
| `ai_gateway_request_duration` | Histogram | 请求延迟分布 |
| `ai_gateway_tokens_total` | Counter | Token 消耗总数 |
| `ai_gateway_model_health` | Gauge | 模型健康状态 |

### Grafana 仪表盘

项目提供预置的 Grafana 仪表盘（`grafana-dashboard.json`），包含：

- 实时 QPS 曲线
- 各模型成功率/错误率
- Token 消耗趋势
- 平均延迟分布
- 模型健康状态

---

## 🔧 配置说明

### 应用配置

在 `python-backend/.env` 文件中配置：

```bash
# 服务器配置
HOST=0.0.0.0
PORT=8123

# 数据库配置
DATABASE_URL=mysql+aiomysql://root:123456@localhost:3306/yu_ai_router

# Redis 配置
REDIS_URL=redis://localhost:6379

# AI 模型 API Key
DASHSCOPE_API_KEY=your-qwen-api-key
DEEPSEEK_API_KEY=your-deepseek-api-key
ZHIPU_API_KEY=your-zhipu-api-key
OPENAI_API_KEY=your-openai-api-key

# 路由策略
DEFAULT_ROUTING_STRATEGY=cost_first
FALLBACK_ENABLED=true
RETRY_TIMES=3

# Stripe 支付
STRIPE_API_KEY=your-stripe-api-key
```

### 环境变量

| 变量名 | 说明 | 默认值 |
|--------|------|--------|
| `DATABASE_URL` | 数据库连接 | - |
| `REDIS_URL` | Redis 地址 | redis://localhost:6379 |
| `DASHSCOPE_API_KEY` | 通义千问 Key | - |
| `DEEPSEEK_API_KEY` | DeepSeek Key | - |
| `ZHIPU_API_KEY` | 智谱 AI Key | - |
| `OPENAI_API_KEY` | OpenAI Key | - |
| `DEFAULT_ROUTING_STRATEGY` | 默认路由策略 | cost_first |
| `FALLBACK_ENABLED` | 启用自动 Fallback | true |
| `RETRY_TIMES` | 重试次数 | 3 |

---

## 🗃️ 数据库设计

### 核心表

| 表名 | 说明 |
|------|------|
| `user` | 用户表 |
| `api_key` | API Key 表 |
| `model_provider` | 模型提供者表 |
| `model` | 模型表 |
| `request_log` | 请求日志表 |
| `plugin_config` | 插件配置表 |
| `user_provider_key` | 用户自带密钥表（BYOK） |

---

## 🔐 安全特性

- **API Key 认证**：所有 API 请求需携带有效的 API Key
- **请求限流**：支持 API Key 级别和 IP 级别的限流
- **IP 黑名单**：可配置 IP 黑名单，防止恶意请求
- **TraceId 追踪**：全链路追踪，便于问题排查
- **HTTPS 支持**：建议生产环境启用 HTTPS

---

## 📝 开发计划

- [x] 基础功能（用户系统、对话、API Key 管理）
- [x] 多模型接入（通义千问、智谱AI、DeepSeek、OpenAI）
- [x] 智能路由与 Fallback
- [x] 请求限流与 IP 黑名单
- [x] Python SDK
- [x] Prometheus + Grafana 监控
- [x] Stripe 在线支付
- [x] AI 绘图功能
- [x] 插件系统（Web 搜索、PDF 解析）
- [x] BYOK（用户自带密钥）
- [ ] Function Calling 支持
- [ ] Go/Node.js SDK

---

## 🤝 贡献指南

欢迎贡献代码！请遵循以下步骤：

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 发起 Pull Request

---

## 📄 开源协议

本项目采用 MIT 协议开源，详见 [LICENSE](LICENSE) 文件。

---

## 🙏 致谢

- [FastAPI](https://fastapi.tiangolo.com/) - 异步 Web 框架
- [LangChain](https://www.langchain.com/) - AI 模型集成框架
- [OpenRouter](https://openrouter.ai/) - 产品设计参考
- [Ant Design Vue](https://antdv.com/) - UI 组件库
- [Prometheus](https://prometheus.io/) - 监控指标收集
- [Grafana](https://grafana.com/) - 可视化仪表板

---

<p align="center">
  Made with ❤️ by AI Router Contributors
</p>
