# Obsidian Nya Database

[中文](./README.zh-CN.md)  
[English](./README.md)

为 Obsidian 提供数据库体验的插件，使用自定义 `.nyason` 文件保存结构化 JSON 数据，并由插件接管显示、编辑、查询和保存。

## 视图

支持七类保存视图：表格、画廊、时间线、日期、聊天、分组看板、图表。

![Table](./screenshot/Table.png)
![Gallery](./screenshot/Gallery.png)
![Charts](./screenshot/Charts.png)
![Timeline](./screenshot/Timeline.png)
![Markdown](./screenshot/markdown-codeblock.png)

## 支持的列类型

- `text`：文本
- `number`：数值
- `checkbox`：布尔勾选
- `date`：日期
- `datetime`：日期时间
- `select`：单选选项
- `multiselect`：多选选项
- `link`：链接
- `image`：图片
- `formula`：运行时派生列，不持久化自身单元格值
- `action`：按钮行为列，不持久化自身单元格值，可运行脚本
- `reference`：引用列，按条件匹配本库或其他数据库的记录，结果运行时派生、不保存到行值

每列都有必填且 schema 内唯一的 `code`，作为 Markdown `nyadb`、XLSX/TSV/JSON 交换、Plugin API 和 Formula 的稳定引用。

## Markdown `nyadb` 查询

- `nyadb` 使用 JSON 结构化查询；数据库可通过 `@id:`、`@path:` 或精确名称引用，列引用统一使用 `code`。
- 支持七类布局、本地保存的 view 设置、Refresh、Save、筛选和布局切换，默认只读。
- 显式启用 `editMode` 后可进行受限的单元格、详情字段、选项和源行写回。

最小查询示例：

```json
{
  "from": "@path:Tasks.nyason"
}
```

## 安装与兼容性

- 最低 Obsidian 版本为 `1.11.4`，支持桌面端和移动端。
- 手动安装：将 `main.js`、`manifest.json`、`styles.css` 放入 Vault 的 `.obsidian/plugins/obsidian-nya-database/`，然后在 Obsidian 中启用插件。

## API 调用

插件通过 `plugin.api` 暴露 Obsidian 内部 JavaScript API（版本 `0.3`）。默认关闭；行写入、字段配置、视图写入和元数据修改使用独立权限，并支持可选的 Obsidian secret storage token。

```js
const api = app.plugins.plugins['obsidian-nya-database'].api.createAPI({
  token: 'Your API Token',
});
```

未配置 secret storage ID 时可省略 token：

```js
const api = app.plugins.plugins['obsidian-nya-database'].api.createAPI();
```
