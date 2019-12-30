1. 克隆一份代码到本地，并选择好需要安装的版本  
```bash
git clone https://github.com/vuejs/vue-devtools.git
```

2. 安装依赖  
```bash
npm install 或者 yarn install
```

3. 构建  
```bash
npm run build 或者 yarn run build
```

4. 打开`shells/chrome/src/manifest.json`, 把`persistent: false `设置成`true`    
  新版本路径`packages/shell-chrome/manifest.json`
  `5.2`版本后官方取消了`shells`目录

5. 安装到浏览器
  打开浏览器扩展插件，把`chrome`文件夹拖过去就得了，新版的`shell-chrome`