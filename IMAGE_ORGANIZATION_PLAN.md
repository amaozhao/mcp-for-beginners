# 图片组织与管理计划

## 当前状态分析

### 图片目录结构
- **`images/`** - 主要图片目录
  - `mcp-beginners.png` - 主要 Logo
  - `video-thumbnails/` - 视频缩略图
  - `02-Security/` - 安全模块专用图片
  - `03-GettingStarted/` - 入门模块专用图片
  - `10-StreamliningAIWorkflowsBuildingAnMCPServerWithAIToolkit/` - 工作坊专用图片

- **`translated_images/`** - 自动生成的多语言翻译版本
  - 包含 1000+ 个图片文件（基础图片 × 48+ 种语言）
  - 通过 co-op-translator GitHub Action 自动生成
  - 格式: `{basename}.{hash}.{language}.png`

### 图片引用现状

#### 模块 02 (Security)
```
![MCP安全最佳实践](../../../translated_images/03.175aed6dedae133f9d41e49cefd0f0a9a39c3317e1eaa7ef7182696af7534308.zh.png)
```
- 引用 translated_images 中的图片
- 路径为相对路径 (../../../translated_images)

#### 模块 10 (AI Toolkit Workshops)
```
![Model Catalog](../../../../translated_images/aimodel.263ed2be013d8fb0e2265c4f742cfe490f6f00eca5e132ec50438c8e826e34ed.zh.png)
![Playground Setup](../../../../translated_images/playground.dd6f5141344878ca4d4f3de819775da7b113518941accf37c291117c602f85db.zh.png)
```
- 大量图片引用翻译后的版本
- 每个图片对应多语言版本

#### 根目录 (README.md)
```
![MCP-for-beginners](./images/mcp-beginners.png)
```
- 使用本地 images 目录

## 识别的基础图片名称（来自 translated_images）

从 translated_images 中提取的唯一基础图片（去除语言代码）:

1. **mcp-list-servers** - MCP 列表服务器
2. **plant** - 架构相关
3. **playground** - AI 工具包 Playground
4. **prompt-injection** - 安全威胁示例
5. **prompt-shield** - 提示防护
6. **pythonagent** - Python 代理
7. **ran-tool** - 工具运行
8. **result** - 结果演示
9. **scenario2** - 场景示例
10. **set** - 设置/配置
11. **sse-inspector** - SSE 检查器
12. **step1-mcp-json** - 步骤 1
13. **step2-copilot-panel** - 步骤 2
14. **step3-agent-mode** - 步骤 3
15. **step3-verify-mcp-tool** - 步骤 3 验证
16. **step4-prompt-chat** - 步骤 4
17. **step5-live-queries** - 步骤 5
18. **tool-injection** - 工具注入
19. **tool** (多个变体) - 工具相关
20. **vscode-agent** - VS Code 代理
21. **vscode-start-server** - VS Code 启动服务器
22. **vscode-tool** - VS Code 工具

## 建议的优化方案

### 方案 A: 逐步迁移（推荐）

**优点:**
- 不破坏当前自动翻译工作流
- 可以逐步验证每个模块
- 保留备份以防需要回滚

**步骤:**
1. 为每个模块创建子目录: `images/module-XX-name/`
2. 从源位置（可能是原始英文仓库或设计资源）复制原始图片
3. 更新 Markdown 文件中的引用路径
4. 保留 translated_images，但标记为"已弃用"
5. 后续 co-op-translator 可以按需要生成新版本

### 方案 B: 完全清理（激进）

**优点:**
- 项目结构更清晰
- 仓库体积减小
- 引用路径简化

**缺点:**
- 可能破坏自动翻译工作流
- 需要修改 GitHub Actions 配置
- 多语言用户无法看到图片说明的翻译

## 建议行动

根据项目的自动翻译策略（co-op-translator），建议采用**方案 A: 逐步迁移**：

### 短期（本周）
1. ✅ 整理 README 和核心文档（已完成）
2. ⏳ 创建 `images/` 的标准目录结构
3. ⏳ 记录当前引用的所有图片文件
4. ⏳ 从原始来源获取或重新生成高质量图片

### 中期（后续 Sprint）
5. ⏳ 逐模块更新图片引用
6. ⏳ 测试所有链接有效性
7. ⏳ 验证多语言渲染（如有需要）

### 长期
8. ⏳ 建立图片管理指南（贡献者指南）
9. ⏳ 评估是否完全弃用 translated_images
10. ⏳ 考虑图片版本控制和 CDN 部署

## 当前建议

鉴于：
1. 项目有自动翻译工作流（co-op-translator）
2. translated_images 由系统自动生成和维护
3. 图片引用主要集中在特定模块（02, 10 等）

**建议先执行以下步骤而不立即删除 translated_images：**

1. **建立图片清单** - 精确找出所有被引用的图片
2. **创建组织结构** - 在 images/ 中创建每模块子目录
3. **补充缺失图片** - 确保每个引用的图片都在 images/ 中有副本
4. **更新文档链接** - 改为指向新位置（可以共存两个位置）
5. **后续清理** - 在自动翻译系统适配后再删除 translated_images

## 下一步

需要执行的任务列表：
- [ ] 精确扫描所有 Markdown 文件的图片引用
- [ ] 区分"原始图片"vs"翻译版本"
- [ ] 创建图片映射表（源→新位置）
- [ ] 建立标准的图片目录结构
- [ ] 执行逐个模块的迁移

---

**状态**: 分析完成  
**下一步**: 等待用户确认最终方案  
**估计工作量**: 2-3 小时（取决于图片数量和源获取难度）
