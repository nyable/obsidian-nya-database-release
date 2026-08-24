# Obsidian Nya Database

`Obsidian Nya Database` 是一个为 Obsidian 提供数据库体验的插件。它使用自定义 `.nyason` 文件保存结构化 JSON 数据，并由插件接管显示、编辑、查询和保存。

当前支持 Table、Gallery、Timeline、Calendar、Chat、Grouped Board 和 Charts 七类视图。

### Markdown `nyadb` 查询

- `nyadb` 使用 JSON 结构化查询；数据库可通过 `@id:`、`@path:` 或精确名称引用，列引用统一使用 `code`。
- Markdown 查询支持七类布局、本地保存的 view 设置、Refresh、Save、筛选和布局切换，默认只读。
- 显式启用 `editMode` 后可进行受限的单元格、详情字段、选项和源行写回

最小查询示例：

```json
{
  "from": "@path:Tasks.nyason"
}
```

## 安装与兼容性

- 最低 Obsidian 版本为 `1.11.4`，支持桌面端和移动端。
- 手动安装时，将生产构建生成的 `main.js`、`manifest.json` 和 `styles.css` 放入 Vault 的 `.obsidian/plugins/obsidian-nya-database/`，然后在 Obsidian 中启用插件。

## API调用

```js
const api = app.plugins.plugins[`obsidian-nya-database`].api.createAPI({
  token: `Your API Token`,
});
```
