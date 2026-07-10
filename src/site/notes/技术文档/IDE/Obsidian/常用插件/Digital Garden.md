---
{"dg-publish":true,"permalink":"/技术文档/IDE/Obsidian/常用插件/Digital Garden/","dg-note-properties":{}}
---


# 笔记发布
### 核心方法：使用笔记属性 (Frontmatter)

这是最基础、最推荐的方法。你需要在想要发布的笔记最顶部，添加一个名为 `dg-publish` 的属性，并将其值设为 `true`[](https://deepwiki.com/oleeskild/obsidian-digital-garden/1.2-core-concepts)[](https://dg-docs.ole.dev/advanced/tips-and-tricks/)。

具体操作如下：
1. 在 Obsidian 中打开你想发布的笔记。
2. 在笔记的最顶部，输入 `---` 并换行，这代表 Frontmatter 区域的开始。
3. 在新的一行输入 `dg-publish: true`。
4. 再换行，输入 `---` 结束 Frontmatter 区域。

一个完整的例子如下：
```markdown
---
dg-publish: true
---

# 我的笔记标题
这里是笔记的正文内容...
```
设置好之后，使用 Digital Garden 的“发布”功能时，该笔记就会被上传[](https://deepwiki.com/oleeskild/obsidian-digital-garden/1.2-core-concepts)。

> **如何不发布笔记**：如果你想让某篇笔记**不上传**，可以确保它没有 `dg-publish` 属性，或者将该属性值设为 `false`。
### 进阶方案一：批量管理已发布的笔记

如果你的笔记很多，可以借助以下插件来提高效率：

- **使用 MetaEdit 批量添加属性**：`MetaEdit` 插件可以让你为多个文件**批量**添加或修改 Frontmatter 属性[](https://dg-docs.ole.dev/advanced/tips-and-tricks/)。你可以一次性选中某个文件夹内的所有笔记，然后统一添加 `dg-publish: true`。
    

### 进阶方案二：自动化流程（新笔记自动发布）

如果你希望将某类笔记（例如放在特定文件夹的笔记）自动设置为“可发布”，可以组合使用 **Templater** 插件[](https://dg-docs.ole.dev/advanced/tips-and-tricks/)：

1. 为不同的文件夹创建不同的模板。
    
2. 在“发布”文件夹对应的模板中，**预先写好** `dg-publish: true` 属性。
    
3. 之后，只要在该文件夹下使用模板创建新笔记，它就会自动带有“可发布”的标记。