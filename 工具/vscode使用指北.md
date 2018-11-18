# 安利一波vscode
> 此文档旨在分享本人使用vscode过程中个人感觉的最佳配置以及使用频率最高、最有帮助的插件，欢迎拍砖，若有更好的配置或插件，欢迎补充^_^

## 个人配置
```json
{
    "workbench.colorTheme": "Solarized Light Custom", // 设置编辑器主题
    "window.zoomLevel": -1, // 编辑器文字缩放
    "editor.scrollBeyondLastLine": false, // 编辑器去除底部空白
    "git.enableSmartCommit": true, // git视图 自动提交至暂存区并commit
    "editor.minimap.enabled": false, // 关闭右侧滚动预览视窗
    "beautify.language": { // beautify插件配置
        "js": {
          "type": [
            "javascript",
            "json",
            "jsonc"
          ],
          "filename": [
            ".jshintrc",
            ".jsbeautifyrc"
          ]
        },
        "css": [
          "css",
          "scss"
        ],
        "html": [
          "htm",
          "html",
          "vue"
        ]
    }
}
```

## 插件推荐
- `Vetur` 用于vue文件的语法高亮，可以说是vue开发者的必备插件了
- `Vue 2 Snippets` 可以自动补全vue语法
- `Npm` 可以自动检测你package.json文件下是否有node_modules没有但在package.json文件下有声明的包
- `Eslint` 自动读取你项目目录下的eslint配置，并在不符合要求的地方标识红线。你也可以设置在保存时自动格式化代码，以此符合eslint配置里的要求
- `Beautify` 可以按照你设定的规则自动帮你格式化代码，和Eslint插件的功能很像，只不过它不仅可以格式化js，也可以格式化html和css
- `Path Intellisense` 可以自动补全代码中的文件路径
- `Auto Close Tag` 可以自动闭合html标签
- `Auto Rename Tag` 可以随着开头标签自动修改闭合标签的名字
