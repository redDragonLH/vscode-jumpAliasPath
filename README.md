# vscode 识别webpack 别名 跳转

**完成度不高，暂不建议使用**


>识别webpack 别名跳转，但是需要点击`from`引用部分，`import`名称部分由于暂时无法拦截vscode 自身的事件(点击名称会提示两个位置)所以暂时关闭

----
暂时只支持 `/@.*\*/` 模式

支持webpack的配置文件的`alias` 字段，其他相关项暂不支持

----

## Configuration
在 `settings.json`内的配置项

**请谨慎设置`default`项**

### 映射关系
`fileAliasSetting.aliasMap` 设置映射关系,使用~~相对路径~~（暂时使用 绝对路径，后期适配分组与相对路径），也会查找webpack config 文件，不过会以此配置为主，同名项会覆盖 webpack config 文件（暂时）

*没有太好的办法确定根目录，暂时使用绝对路径*

**aliasMap分组识别已经完成**

        // 以命名空间顶层文件夹名为键
        "fileAliasSetting.aliasMap": {
            "webpack": {
                "@":"D:\\work\\webpack\\src"
            },
            "default":{ // 默认项
                "@":"D:\\work\\webpack\\src"
            },
        },

### 文件后缀
`fileAliasSetting.fileSuffixs` 识别文件后缀（默认以下四种，如有其他可在 `settings.json` 中另行配置，这四种不需要在setting.json 配置）

    "fileAliasSetting.fileSuffixs":[
        "js",
        "ts",
        "vue",
        "jsx",
    ],


### 指示 webpack config 文件名称
`fileAliasSetting.configPos`指示 webpack config 文件名称，键名为项目文件夹名，值为 `webpack config` 文件名

*暂不支持返回函数的配置文件*

        "fileAliasSetting.configPos": {
            "项目根目录":"webpack 配置项文件名",
        },

**配置文件未在根目录下方的键值不要带 ./ 或/**

        "fileAliasSetting.configPos": {
            "webpack-project-name":"webpack.config.js",
            "vue-project-name": "build\\webpack.config.dev.js" // 不要带相对或绝对符号
            "default":"webpack.config.js",  // 默认webpack 配置文件名，可填可不填
        },


## 未来计划
|计划名称|优先级|完成度|备注|
|--|--|--|---|
|支持 webpack config| 高| 完成|支持webpack的配置文件的`alias` 字段 |
|支持 完整[webpack 别名](https://webpack.docschina.org/configuration/resolve/#resolve-alias)|高|未完成| |
| typeScript 化| 低|未完成||
|支持分项目解析|低|99%| ~~需要先识别根目录~~，以工作空间的顶层文件夹名为根目录|
|数据持久化|低|未完成||