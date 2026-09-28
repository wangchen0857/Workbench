# Workbench

全栈脚手架项目：FastAPI 后端 + Vue 3 + Vite + TypeScript 前端。

## 项目结构

```
Workbench/
├── backend/                          # FastAPI 后端
│   ├── app/
│   │   ├── __init__.py
│   │   ├── main.py                   # 应用入口，提供 / 与 /hello/{name} 路由
│   │   ├── config.py                 # 配置（空，待实现）
│   │   ├── database.py               # 数据库连接（空，待实现）
│   │   ├── dependencies.py           # 依赖注入（空，待实现）
│   │   ├── models/__init__.py        # SQLAlchemy 模型（空，待实现）
│   │   ├── routers/__init__.py       # 路由模块（空，待实现）
│   │   ├── schemas/__init__.py       # Pydantic schema（空，待实现）
│   │   └── services/__init__.py      # 业务服务（空，待实现）
│   ├── tests/
│   │   ├── __init__.py
│   │   └── test_main.http            # HTTP 测试占位文件
│   ├── requirements.txt              # Python 依赖（含 FastAPI/Uvicorn/SQLAlchemy 等）
│   └── .env.example                  # 环境变量示例：GREETING_MESSAGE
└── frontend/                         # Vue 3 + Vite + TypeScript 前端
    ├── public/
    │   └── favicon.ico
    ├── src/
    │   ├── App.vue                   # 根组件（Vue 默认模板）
    │   ├── main.ts                   # 应用入口
    │   ├── assets/
    │   │   ├── base.css
    │   │   ├── main.css
    │   │   └── logo.svg
    │   ├── components/
    │   │   ├── HelloWorld.vue
    │   │   ├── TheWelcome.vue
    │   │   ├── WelcomeItem.vue
    │   │   └── icons/                 # 5 个预置图标组件
    │   ├── api/                      # API 调用层（空，待实现）
    │   ├── composables/              # 组合式函数（空，待实现）
    │   ├── layouts/                  # 布局组件（空，待实现）
    │   ├── router/                   # 路由配置（空，待实现）
    │   ├── stores/                   # 状态管理（空，待实现）
    │   ├── utils/                    # 工具函数（空，待实现）
    │   └── views/                    # 页面视图（空，待实现）
    ├── env.d.ts
    ├── index.html
    ├── vite.config.ts                # Vite 配置，含 `@` → `./src` 别名
    ├── tsconfig.json                 # TS 配置入口（引用 app/node 子配置）
    ├── tsconfig.app.json
    ├── tsconfig.node.json
    ├── package.json
    └── package-lock.json
```

## 技术栈

### 后端
- **框架**：FastAPI 0.115
- **运行时**：Uvicorn（ASGI）
- **数据库**：SQLAlchemy 2.0（已声明依赖，未启用）
- **校验**：Pydantic v2
- **环境变量**：python-dotenv

### 前端
- **框架**：Vue 3.5
- **构建工具**：Vite 8
- **语言**：TypeScript 6
- **类型检查**：vue-tsc
- **别名**：`@` → `./src`

## 环境要求

- **Node.js**：`^22.18.0 || >=24.12.0`
- **Python**：建议 3.10+
- **包管理器**：npm（前端）、pip（后端）

## 快速开始

### 1. 启动后端

```bash
cd backend
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env               # 按需修改
uvicorn app.main:app --reload --port 8000
```

访问 http://127.0.0.1:8000 查看根路由，或访问 http://127.0.0.1:8000/docs 查看 Swagger 文档。

### 2. 启动前端

```bash
cd frontend
npm install
npm run dev
```

默认在 http://localhost:5173 启动开发服务器，支持热更新。

## 常用脚本

### 后端
| 命令 | 说明 |
| --- | --- |
| `uvicorn app.main:app --reload` | 启动开发服务器（热重载） |
| `uvicorn app.main:app` | 启动生产服务器 |
| `python -m pytest tests/` | 运行测试 |

### 前端
| 命令 | 说明 |
| --- | --- |
| `npm run dev` | 启动开发服务器 |
| `npm run build` | 类型检查 + 生产构建 |
| `npm run preview` | 预览生产构建 |
| `npm run type-check` | 仅运行类型检查 |

## API 接口

当前后端仅暴露示例接口：

| Method | Path | 描述 |
| --- | --- | --- |
| `GET` | `/` | 返回 `{"message": "Hello World"}` |
| `GET` | `/hello/{name}` | 返回 `{"message": "Hello {name}"}` |

## 当前状态

- 后端 `app/` 下 `config.py`、`database.py`、`dependencies.py` 及 `models/routers/schemas/services` 子模块为空文件 / 空目录，等待业务实现。
- 前端使用 Vue 默认模板，`api/composables/layouts/router/stores/utils/views` 等目录已建立但内容待填充。
- `tests/test_main.http` 为 HTTP 测试占位文件。

## 开发建议

- IDE：VS Code + Vue (Official) 插件（禁用 Vetur）+ Python 插件
- 前端在 `vite.config.ts` 中配置 `@` 别名指向 `src`，导入时使用 `@/...`
- 后端环境变量参考 `backend/.env.example`
- 跨域：当前前后端独立运行，对接 API 时需在 FastAPI 中配置 CORS 中间件
