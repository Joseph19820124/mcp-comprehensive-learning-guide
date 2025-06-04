# 🚀 基础 MCP 服务器示例

这是一个简单的MCP服务器实现，帮助你理解MCP的核心概念和基本用法。

## 📁 项目结构

```
basic-server/
├── basic_mcp_server.py      # 主服务器文件
├── requirements.txt         # Python依赖
├── config.json             # 配置文件模板
├── README.md               # 说明文档
└── tests/                  # 测试文件
    └── test_server.py
```

## 🛠️ 安装和运行

### 1. 环境准备
```bash
# 确保Python 3.8+
python --version

# 创建虚拟环境（推荐）
python -m venv mcp-env
source mcp-env/bin/activate  # Linux/Mac
# 或
mcp-env\Scripts\activate     # Windows
```

### 2. 安装依赖
```bash
pip install -r requirements.txt
```

### 3. 运行服务器
```bash
python basic_mcp_server.py
```

## 🔧 功能特性

### 包含的工具
1. **get_weather**: 获取天气信息
2. **calculate**: 执行数学计算
3. **get_time**: 获取当前时间

### 包含的资源
1. **user_preferences**: 用户偏好设置
2. **system_info**: 系统信息

### 包含的提示模板
1. **summarize_text**: 文本摘要提示
2. **code_review**: 代码审查提示

## 📝 代码示例

### 基础服务器结构
```python
from mcp.server.fastmcp import FastMCP
import asyncio

# 创建MCP服务器
mcp = FastMCP("BasicServer")

@mcp.tool()
def get_weather(city: str) -> dict:
    """获取指定城市的天气信息"""
    # 简单模拟天气数据
    return {
        "city": city,
        "temperature": "22°C",
        "condition": "Sunny",
        "humidity": "65%"
    }

@mcp.resource("user_preferences")
def get_user_preferences() -> str:
    """获取用户偏好设置"""
    return "Theme: Dark, Language: Chinese, Notifications: Enabled"

if __name__ == "__main__":
    mcp.run()
```

## 🔗 与Claude Desktop集成

### 配置文件 (claude_desktop_config.json)
```json
{
  "mcpServers": {
    "basic-server": {
      "command": "python",
      "args": ["path/to/basic_mcp_server.py"],
      "env": {}
    }
  }
}
```

### 使用步骤
1. 启动Claude Desktop
2. 在设置中添加MCP服务器配置
3. 重启Claude Desktop
4. 在对话中测试工具功能

## 🧪 测试

### 运行测试
```bash
python -m pytest tests/
```

### 手动测试
```bash
# 测试天气工具
curl -X POST http://localhost:3000/tools/get_weather \
  -H "Content-Type: application/json" \
  -d '{"arguments": {"city": "Beijing"}}'
```

## 📚 学习要点

### 1. MCP服务器基础
- 理解工具(Tools)、资源(Resources)、提示(Prompts)的区别
- 掌握MCP服务器的生命周期
- 学会处理客户端请求

### 2. API设计
- 工具函数的参数类型定义
- 错误处理和异常管理
- 资源的访问控制

### 3. 集成模式
- STDIO传输协议
- JSON-RPC通信格式
- 客户端-服务器握手过程

## 🚀 扩展建议

### 初学者任务
1. 添加新的工具函数
2. 实现文件读写功能
3. 集成外部API调用

### 进阶任务
1. 添加数据库支持
2. 实现用户认证
3. 支持异步操作
4. 添加日志和监控

## 🐛 常见问题

### Q1: 服务器启动失败
**A**: 检查Python版本和依赖安装
```bash
pip list | grep mcp
```

### Q2: Claude Desktop无法连接
**A**: 验证配置文件路径和格式
```bash
# 检查配置文件
cat ~/.config/Claude\ Desktop/claude_desktop_config.json
```

### Q3: 工具调用失败
**A**: 查看服务器日志和错误信息
```bash
# 启用详细日志
DEBUG=1 python basic_mcp_server.py
```

## 📖 相关文档

- [MCP官方文档](https://modelcontextprotocol.io/)
- [FastMCP文档](https://github.com/modelcontextprotocol/python-sdk)
- [Claude Desktop集成指南](https://docs.anthropic.com/claude/docs/mcp)

---

**下一步**: 查看 [GitHub集成示例](../github-integration/) 了解更复杂的MCP服务器实现。