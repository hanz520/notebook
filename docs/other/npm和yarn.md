## npm

### 常用命令    
所有命令，带`-g`代表全局操作    
```bash
npm -v    // 查看版本
npm install <Module Name>[@1.0.0] -g  // 安装模块 install可以简写为i  @1.0.0为指定版本号
// -S 和 --save 或者不带后缀 安装到dependencies
// -D 和 --save-dev 安装到devDependencies

npm uninstall <Module Name> -g  // 卸载模块
npm list [-g]   // 查看安装的模块
npm list [-g] --depth 0   // 查看自己主动安装过的模块，不包括模块的依赖
npm list <Module Name>    // 查看模块的版本号，这两个 list可以简写为ls
npm root [-g]   // 查看模块安装路径

npm init  // 创建模块
npm adduser   // 添加用户
npm publish   // 发布模块
npm unpublish <package>@<version> // 可以撤销发布自己发布过的某个版本代码

npm pack <Module Name>  // 会生成一个 tgz版本文件
npm install 路径/文件-1.0.0.tgz // 安装tgz版本文件

```   

## 其他命令
```bash
npm help <command>  // 可查看某条命令的详细帮助，例如npm help install
npm cache clear   // 清空NPM本地缓存
npm repo <Module Name>  // 打开模块的github仓库
npm docs <Module Name>  // 查看模块的git文档
npm update <Module Name>  // 更新模块
npm search <Module Name> // 搜索模块
npm view <Module Name> [package.json属性名称] // 查看模块的注册信息
npm config set prefix <路径>  // 更改npm全局安装路径

npm who am i  // 查看当前登录的用户
npm login
```

### 版本号定义    
语义版本号分为X.Y.Z三位，分别代表主版本号、次版本号和补丁版本号。当代码变更时，版本号按以下原则更新。   
- 如果只是修复bug，需要更新Z位。    
- 如果是新增了功能，但是向下兼容，需要更新Y位。   
- 如果有大变动，向下不兼容，需要更新X位。   


## yarn

### 常用命令
```bash
yarn init // 初始化项目
yarn add [package]  // 安装包
yarn add [package]@[version]
yarn add [package]@[tag]

yarn // 安装全部依赖，或者用 yarn install

// 分别添加到 devDependencies、peerDependencies 和 optionalDependencies
yarn add [package] --dev
yarn add [package] --peer
yarn add [package] --optional

yarn remove <package>   // 移除包

yarn upgrade [package]    // 升级包
yarn upgrade [package]@[version]
yarn upgrade [package]@[tag]

yarn list // 查看安装的包

```

### 其他命令
```bash
yarn global bin // yarn bin的位置
yarn cache dir  // yarn 全局缓存路径
yarn global dir // 包全局安装路径
yarn cache clean  // 清除全局缓存

// 发布一个包相关，类同于npm
yarn init
yarn login
yarn publish
yarn info [package]

yarn config  set global-folder "D:\Software\yarn\global"  //改变 yarn 全局安装位置
yarn config set cache-folder "你的磁盘路径"   // 改变 yarn 缓存位置
```
