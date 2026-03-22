# 版本更新记录

## v2.2.0 (2026-03-22)

### 全面Agent化改造
- 新增 app/agents/ 多Agent分析子系统（LangGraph编排）
- 9角色4层架构：技术/基本面/资金/情绪分析师 → 多空辩论 → 风控 → 决策
- 投资者人格Agent：巴菲特/芒格/彼得林奇/达摩达兰 四大投资风格
- LangGraph StateGraph动态深度路由（1-5级）
- 特性开关 USE_AGENT_SYSTEM 控制新旧系统切换

### 搜索引擎集成
- 新增统一搜索层 app/core/search.py（DuckDuckGo→Tavily→SERP多源降级）
- DuckDuckGo搜索免费无限制，无需API key

### 基础设施增强
- 新增 Redis统一缓存层 app/core/cache.py（Redis优先/内存降级）
- 新增 Agent记忆系统 app/core/agent_memory.py（分析历史+经验学习）
- 新增 事件总线 app/core/event_bus.py（Agent间事件通信）
- 新增 Human-in-the-Loop app/agents/hitl.py（高风险决策人工审批）
- 新增 MCP工具服务器 app/mcp/（标准化工具接口）

### 安全与稳定性修复
- CORS限制为环境变量白名单
- 移除硬编码API密钥
- 8个API端点添加股票代码验证
- 统一AI客户端（超时180s/重试2次/友好错误消息）
- akshare自适应列名映射 + 14处异常日志
- baostock线程安全 + 动态季度
- 新闻去重窗口扩大(7天) + 双字段去重
- 前端XSS防护 + 全局AJAX超时60s

---

## v2.1.2 (2025-12-16)

### 数据接口双层冗余架构
- **新增adapters层**：实现数据源适配器模式
  - `akshare_adapter.py` - akshare适配器，含东财→腾讯内部冗余
  - `baostock_adapter.py` - baostock备用适配器
  - `base_adapter.py` - 适配器基类
- **新增DataProvider统一数据层**：封装多数据源故障转移
- **新增FallbackManager**：自动故障转移管理器
- **改造6个分析模块**接入DataProvider：
  - stock_analyzer.py
  - fundamental_analyzer.py
  - index_industry_analyzer.py
  - capital_flow_analyzer.py
  - industry_analyzer.py
  - etf_analyzer.py

### Bug修复
- 修复情景预测AI分析JSON解析失败问题（支持```json代码块格式）
- 修复概念板块成分股显示问题
- 移除mock数据降级，API无数据时返回空数组

---

## v2.1.1

- **Issue #34 修复**: TradingAgentsGraph.propagate()参数兼容性问题，使用inspect动态检查方法签名
- **Issue #29 新增**: 市场扫描按板块扫描功能（科创50/100、北证50），使用指数成分股接口增强稳定性
- **Issue #31 新增**: 智能问答历史记录功能，LocalStorage保存查询记录和对话内容
- 新增板块股票API：`/api/board_stocks`

---

## v2.1.0

- 重构项目为模块化架构（app/analysis、app/web、app/core）
- 新增ETF分析功能，支持ETF基金评估和持仓分析
- 新增Agent智能分析功能，基于AI Agent的深度分析
- 新增认证中间件，增强系统安全性
- 优化缓存机制，增加市场收盘时自动清理缓存
- 增强错误处理和系统稳定性
- 新增智能问答功能，支持联网搜索实时信息和多轮对话
- 优化情景预测模块，提高预测精度和可视化效果
- 新增行业分析功能
- 改进首页为财经门户风格，实时显示财经要闻与舆情热点
- 增加全球主要市场状态实时监控
- 优化服务器超时处理
- 改进UI交互体验

---

## v2.0.0

- 增加多维度分析能力
- 整合AI API实现AI增强分析
- 新增投资组合管理功能
- 重构用户界面，添加交互式图表
- 优化技术分析和评分系统

---

## v1.0.0 (初始版本)

- 基础股票分析功能
- 技术指标计算
- 简单评分系统
- 基础Web界面
