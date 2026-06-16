# api32one

**一个只在小圈子内流转的大模型中转服务**

api32one 源自我身边开发者的真实痛点：想用先进大模型，却被多平台密钥管理、账单追踪和接口不一致这些琐事卡住。做了十几年软件开发，又在上市公司深度参与过 MPoC 这种对稳定性和合规要求极高的支付项目，我觉得自己有能力帮大家把这层麻烦抽象掉，于是就有了这个内部小平台。

## 核心特性

### 多模型统一接入
- 一套 API 调用 GPT-4o、Claude、Gemini、DeepSeek 等主流模型
- 标准 OpenAI 兼容接口，轻松迁移
- 一键切换模型，无需修改业务代码

### 智能路由
- 根据场景自动选择最优模型
- 支持"速度优先"或"成本优先"策略
- 自动 fallback，保障服务稳定性

### 用量管理
- 实时用量看板，清晰展示 token 消耗
- 预算上限设置，告别月底账单惊吓
- 百分比告警，及时掌握异常消耗

### 安全合规
- 敏感词检测
- 个人信息(PII)脱敏
- 完整的日志审计

### 高可用保障
- 自动重试机制
- 熔断保护
- 完善的错误处理

### 团队协作
- 多成员隔离
- 额度按需分配
- 灵活的权限管理

## 工作原理

```
┌─────────────┐     ┌─────────────┐     ┌──────────────┐
│   Your App  │────▶│  api32one   │────▶│   OpenAI     │
│  (OpenAI SDK)│     │   Proxy     │     │   / Claude   │
└─────────────┘     └─────────────┘     └──────────────┘
                           │
                     ┌──────┴──────┐
                     │  Smart Route │
                     │  + Monitor  │
                     └─────────────┘
```

## 快速开始

### 激活方式

所有接入全靠我发放的**兑换码**。拿到兑换码的朋友可以直接激活使用，里面有预置的初始额度。

如果额度不够，随时告诉我，我再给你加。没有什么月费、年费，也没有复杂的套餐层级，就是朋友之间互相方便的工具。

### API 调用示例

```bash
curl https://api.api32.one/v1/chat/completions \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-4o",
    "messages": [{"role": "user", "content": "Hello!"}]
  }'
```

### 切换模型

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_API_KEY",
    base_url="https://api.api32.one/v1"  # 只需改这一个地址
)

# 模型选择: gpt-4o / claude-3-5-sonnet / gemini-pro / deepseek-chat
response = client.chat.completions.create(
    model="claude-3-5-sonnet",  # 一键切换
    messages=[{"role": "user", "content": "Hello!"}]
)
```

## 技术栈

- **后端**: Go
- **数据库**: PostgreSQL + Redis
- **部署**: Docker / K8s
- **协议**: OpenAI Compatible API

## 关于

api32one **不对外公开销售**，所有接入全靠朋友间的兑换码机制。这是我作为十几年老程序员，把自己在工程和合规上积累的经验，变成一个大家拿来就能用的工具。

如果你也想加入这个开发者朋友圈子，欢迎联系我获取兑换码。

## 联系方式

- GitHub Issues: 有问题可以提 Issue

## 许可证

本项目仅供内部技术交流使用。
