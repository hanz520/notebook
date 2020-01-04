## vue  

1.data里不显示声明对象的属性，之后添加属性时正确的做法时用 `vm.$set()` 方法,否则vue检测不到数据的变化


## vue-cli  

### 如何用vue-cli.3.x创建创建2.0项目    
Vue CLI >= 3 和旧版使用了相同的 vue 命令，所以 Vue CLI 2 (vue-cli) 被覆盖了。如果你仍然需要使用旧版本的 vue init 功能，你可以全局安装一个桥接工具：
```bash
npm install -g @vue/cli-init
```