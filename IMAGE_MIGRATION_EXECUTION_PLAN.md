# 图片迁移执行方案

## 核心问题

项目当前有两套图片系统：
1. **`images/`** - 原始图片存储（部分有组织）
2. **`translated_images/`** - 自动生成的 48+ 语言版本（1000+ 文件）

问题：文档中的图片引用混合使用两个来源，且 `translated_images` 是由自动翻译系统（co-op-translator）生成，不应手动删除。

## 推荐方案：保守迁移（RECOMMENDED）

### 第 1 步：建立清晰的目录结构

在 `images/` 下创建按模块组织的目录：

```
images/
├── mcp-beginners.png                          # 根目录 Logo
├── video-thumbnails/                          # 现有视频缩略图
├── 02-Security/                               # 安全模块
│   ├── README.md (新增) - 图片清单
│   └── [图片文件]
├── 03-GettingStarted/                         # 入门模块
│   ├── README.md (新增) - 图片清单
│   └── [图片文件]
├── 10-StreamliningAIWorkflowsBuildingAnMCPServerWithAIToolkit/  # 工作坊
│   ├── lab1/
│   │   ├── README.md (新增) - 图片清单
│   │   └── [图片文件]
│   ├── lab2/
│   ├── lab3/
│   └── lab4/
└── README.md (新增) - 总体图片管理指南
```

### 第 2 步：图片清单与映射

创建 `images/README.md` 列出所有图片及其用途：

```markdown
# 图片资源管理

## 基础图片清单（来自 translated_images）

| 图片名 | 用途 | 模块 | 状态 |
|--------|------|------|------|
| mcp-list-servers | MCP 架构展示 | 核心 | 需迁移 |
| playground | AI 工具包演示 | 10-Workshops | 需迁移 |
| prompt-injection | 安全威胁 | 02-Security | 需迁移 |
| ... | ... | ... | ... |

## 迁移指南

### 对于文档作者：
1. 优先引用 `./images/` 下的本地文件
2. 仅在必要时引用 `translated_images`
3. 新增图片请直接放在相应模块的 `images/` 子目录

### 对于贡献者：
- 上传新图片时，同时更新清单
- 保持文件名简洁且描述性强
```

### 第 3 步：更新引用路径

**关键原则**：
- 为了保持多语言支持，**暂时保留** `translated_images` 的引用
- 建立映射关系，便于后续统一迁移
- 更新路径时添加注释说明来源

**示例**（模块 02-Security/README.md）：

```markdown
<!--
<!-- Image sourced from: translated_images/03.175aed...zh.png
<!-- TODO: Migrate to ./images/02-Security/mcp-security-overview.png
-->
![MCP Security Overview](./images/02-Security/mcp-security-overview.png)
```

### 第 4 步：建立贡献者指南

创建 `CONTRIBUTING.md` 更新部分：

```markdown
## 图片管理

### 上传新图片

1. **保存位置**：`images/{module}/`
2. **文件名约定**：`{module}-{description}.png` (如 `02-security-architecture.png`)
3. **格式**：PNG 或 SVG（优先）
4. **大小**：< 500KB
5. **更新清单**：编辑 `images/README.md`
6. **多语言**：自动翻译系统会在 co-op-translator 运行时生成版本

### 引用图片

```markdown
![描述](./images/module/file.png)
```

**注意**：不要直接引用 `translated_images`；由系统自动处理多语言版本。
```

### 第 5 步：逐步迁移（可选，后期执行）

如果需要完全清理 `translated_images`：

1. **检查依赖**：确认没有文档仍在引用
2. **备份**：将 translated_images 归档到 `archives/` 或分支
3. **更新工作流**：修改 GitHub Actions 配置，避免生成 translated_images
4. **清理**：删除目录

## 执行步骤顺序

### 立即执行（本次）
- [x] 分析当前情况 
- [x] 制定方案
- [ ] **第 1 步**：在 `images/` 创建目录结构
- [ ] **第 2 步**：创建 `images/README.md` 清单

### 后续周期
- [ ] **第 3 步**：逐个模块更新引用（模块 02 → 03 → 10）
- [ ] **第 4 步**：贡献者文档更新
- [ ] **第 5 步**：(可选) 后期彻底清理

## 为什么这个方案最优

✅ **保持兼容**：不破坏自动翻译工作流  
✅ **逐步优化**：分阶段实施，易于验证  
✅ **清晰结构**：模块化图片组织，便于维护  
✅ **易于回滚**：每步都可以验证，出问题容易修复  
✅ **扩展性**：为未来的新图片建立规范

## 备选方案比较

| 方案 | 优点 | 缺点 | 复杂度 |
|------|------|------|--------|
| **保守迁移** ⭐ | 低风险，保持工作流 | 需要多步 | 中 |
| 激进清理 | 快速完成，仓库整洁 | 可能破坏工作流 | 高 |
| 完全不动 | 零风险 | 组织不清，难维护 | 低 |

---

**建议**：采用"保守迁移"方案，从第 1-2 步开始。
