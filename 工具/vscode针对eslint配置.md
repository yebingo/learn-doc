# vscode针对eslint配置
## 1. 安装依赖
```bash
npm i eslint-plugin-vue
```
## 2. 创建eslint文件
创建项目跟路径下的文件：`.eslintrc` | `.eslint.js`

添加插件
```json
"plugins": [
    "vue"
]
```

## 3. 安装插件并修改vscode配置文件
1.  在vscode添加 eslint 插件
2. 在vscode添加 vetur 插件
3. 修改你的setting.json
```json
"eslint.autoFixOnSave": true,
"eslint.validate": [
    "javascript",{
        "language": "vue",
        "autoFix": true
    },"html",
    "vue"
]
```