# TRAE 个人规则 - 智能体协作规范

## 1. 语言与交互规范

### 响应语言
- 使用中文（简体）进行沟通和技术解释
- 代码注释使用中文
- 专业术语首次出现时给出英文原词

### 沟通风格
- 直接给出解决方案，避免过度铺垫
- 技术决策提供简要理由（1-2句话）
- 复杂问题先给结论再展开说明

---

## 2. 智能体及时调用规范

### 调用原则
**遇到以下情况，必须立即调用对应智能体，不得自行处理：**

#### 产品阶段
| 触发场景 | 调用智能体 |
|---------|-----------|
| 用户说"新产品"、"需求分析"、"产品设计" | `product-manager` |
| 用户提到"竞品分析"、"市场调研" | `product-manager` |
| 用户需要"PRD"、"产品路线图" | `product-manager` |

#### 设计阶段
| 触发场景 | 调用智能体 |
|---------|-----------|
| 用户说"界面设计"、"UI设计" | `ui-designer` |
| 用户提到"组件库"、"设计系统" | `ui-designer` |
| 用户需要"响应式设计"、"适配移动端" | `ui-designer` |

#### 开发阶段
| 触发场景 | 调用智能体 |
|---------|-----------|
| 用户说"前端架构"、"技术选型" | `frontend-architect` |
| 用户提到"组件设计"、"性能优化" | `frontend-architect` |
| 用户需要"状态管理"、"SSR" | `frontend-architect` |
| 用户说"后端架构"、"API设计" | `backend-architect` |
| 用户提到"数据库设计"、"微服务" | `backend-architect` |
| 用户需要"认证授权"、"安全加固" | `backend-architect` |
| 用户说"接入GPT"、"AI功能" | `ai-integration-engineer` |
| 用户提到"RAG知识库"、"问答系统" | `ai-integration-engineer` |
| 用户需要"推荐系统"、"AI Agent" | `ai-integration-engineer` |

#### 测试阶段
| 触发场景 | 调用智能体 |
|---------|-----------|
| 用户说"测试API"、"接口测试" | `api-test-pro` |
| 用户提到"性能测试"、"负载测试" | `api-test-pro` |
| 用户需要"安全测试"、"漏洞扫描" | `api-test-pro` |
| 用户说"E2E测试"、"用户流程" | `e2e-test-engineer` |
| 用户提到"跨浏览器"、"兼容性" | `e2e-test-engineer` |
| 用户需要"验收测试"、"发布测试" | `e2e-test-engineer` |

#### 部署阶段
| 触发场景 | 调用智能体 |
|---------|-----------|
| 用户说"部署上线"、"CI/CD" | `devops-architect` |
| 用户提到"Kubernetes"、"容器化" | `devops-architect` |
| 用户需要"监控搭建"、"日志聚合" | `devops-architect` |
| 用户说"性能慢"、"加载慢" | `performance-expert` |
| 用户提到"优化性能"、"压力测试" | `performance-expert` |
| 用户需要"容量规划"、"建立基准" | `performance-expert` |

#### 运营阶段
| 触发场景 | 调用智能体 |
|---------|-----------|
| 用户说"数据分析"、"业务洞察" | `data-analyst` |
| 用户提到"图表"、"仪表板" | `data-analyst` |
| 用户需要"复杂SQL"、"数据提取" | `data-analyst` |
| 用户说"合规审查"、"法律审查" | `compliance-checker` |
| 用户提到"隐私政策"、"GDPR" | `compliance-checker` |
| 用户需要"风险评估" | `compliance-checker` |

---

## 3. 智能体调用方式

```bash
# 使用 Task 工具调用智能体
Task(description="任务描述", query="详细需求", subagent_type="智能体ID", response_language="zh")

# 使用 Skill 工具调用技能
Skill(name="技能名称")
```

### 优先级规则
- **高优先级场景**：必须调用智能体（如新项目启动、关键功能开发）
- **中优先级场景**：建议调用智能体（如性能优化、重构）
- **低优先级场景**：可自行处理（如小bug修复、代码审查）

---

## 4. 开发工作流

```
需求分析 (Product Manager)
    ↓
界面设计 (UI Designer)
    ↓
架构设计 (Frontend/Backend Architect)
    ↓
代码实现
    ↓
测试验证 (API Test Pro + E2E Test Engineer)
    ↓
部署上线 (DevOps Architect)
    ↓
性能优化 (Performance Expert)
    ↓
运营分析 (Data Analyst + Compliance Checker)
```

---

## 5. 技能使用规范

| 技能 | 使用场景 |
|------|---------|
| `python-patterns` | Python后端开发 |
| `python-testing` | Python测试编写 |
| `frontend-patterns` | 前端开发（React/Vue） |
| `postgres-patterns` | PostgreSQL数据库操作 |
| `security-review` | 安全审计、漏洞修复 |
| `docker-patterns` | 容器化部署 |
| `api-design` | RESTful API设计 |
| `tdd-workflow` | 测试驱动开发 |

---

## 6. 代码规范

### 通用规范
- 使用UTF-8编码
- 文件末尾保留一个换行符
- 代码缩进：Python 4空格，JavaScript/TypeScript 2空格
- 一行代码不超过120个字符

### Python规范
- 遵循PEP 8
- 使用类型注解
- 函数和类包含docstring
- 导入顺序：标准库 → 第三方库 → 本地模块

### JavaScript/TypeScript规范
- 优先使用TypeScript
- 组件文件PascalCase
- 工具函数camelCase
- 使用ESLint检查

### 禁止事项
- 禁止使用eval()或exec()
- 禁止直接拼接SQL（必须参数化查询）
- 禁止在前端存储敏感信息
- 禁止使用不安全的加密算法

---

## 7. 验证要求

所有代码修改完成后：
1. 实际运行程序进行测试验证
2. 记录验证结果
3. 确保功能正常后再提交

---

## 8. 权限使用

- 在需要时使用sudo权限完成必要操作
- 包括：安装依赖、修改配置、启动服务、端口绑定等
- 确保操作安全性，合理使用权限
