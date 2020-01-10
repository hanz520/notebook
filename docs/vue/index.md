## vue  

1.data里不显示声明对象的属性，之后添加属性时正确的做法时用 `vm.$set()` 方法,否则vue检测不到数据的变化

## vue中JSX使用
1. 绑定变量和传参
```jsx
let timer = 300
return (
  <el-tooltip open-delay={timer} enterable={false}  content="删除测试用例" placement="top" effect="light">
    <el-button>按钮一个</el-button>
  </el-tooltip>
)
```
2. 绑定方法
```jsx
let clickFn = () => {}
return (
  <el-button on-click={() => {clickFn()}}></el-button>
）
```
3. 实现循环   
  - 方法一    
  ```jsx
  let tags = ['标签A', '标签B']
  return (
    <span>
      {
        tags.map(tag =>{
          return <el-tag class="mr5">{tag}</el-tag>
        })
      }
    </span>
  )
  ```     
  - 方法二，因为`return`里面只能包含表达式，所以如果用for循环遍历的话，只能用以下方法，先生成一个`VNode`list，然后放到`return`返回    
  ```jsx
  let tags = arrToLabel(this.DB.testType, val)
  let list = []
  for(let i=0; i<tags.length; i++) {
    list.push(<el-tag class="mr5">{tags[i]}</el-tag>)
  }
  return (
    <span>
      { list }
    </span>
  )
  ```   


## vue-cli    

### 如何用vue-cli.3.x创建创建2.0项目      
Vue CLI >= 3 和旧版使用了相同的 vue 命令，所以 Vue CLI 2 (vue-cli) 被覆盖了。如果你仍然需要使用旧版本的 vue init 功能，你可以全局安装一个桥接工具：
```bash
npm install -g @vue/cli-init
```   

