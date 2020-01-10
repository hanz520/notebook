##  1. 开始   

  为了简化开发过程，避免繁杂的webpack配置项，先用`cli2.0`创建一个简化版webpack的vue项目   
  ```bash
  vue init webpack-simple test-publish-component
  ```   
  >如果cli版本已经升级到了3.0，请看下面：    

  Vue CLI >= 3 和旧版使用了相同的 vue 命令，所以 Vue CLI 2 (vue-cli) 被覆盖了。如果你仍然需要使用旧版本的 vue init 功能，你可以全局安装一个桥接工具：
  ```bash
  npm install -g @vue/cli-init
  ```
  创建好的项目目录很简单，如下图：    

  ![Image text](/01.jpg)    

  安装好相关依赖，并且对目录进行调整，简化`App.vue`的内容，删除`assets`目录，如下图：   

  ![Image text](/02.jpg)    

  此时，准备工作基本告一段落

## 2. 编写一个组件  

  主要是为了记录发布一个组件到npm，这里仅仅编写一个最简单的vue组件--myComponent.vue，如下：   
  ```html
    <template>
      <div>显示传进来的文字{{msg}}</div>
    </template>

    <script>
    export default {
      name: 'myComponent',
      props: {
        msg: {
          type: String,
          default: '默认值'
        }
      }

    }
    </script>
  ```   
  `App.vue`引用该组件测试，测试该组件是否可用   
  ```html
  <template>
    <div id="app">
      显示最简单的文字
      <myComponent msg="文字来自App" />
    </div>
  </template>

  <script>
  import myComponent from './myComponent.vue'
  export default {
    name: 'app',
    components: {
      myComponent,
    },
    data () {
      return {
      }
    }
  }
  </script>
  ```     
  到此为止，和日常的vue开发没有区别，项目也是能够跑起来的。   

## 3. 编写打包组件时候的入口文件，修改webpack配置  
  在根目录创建`entry.js`，内容如下：    
  ```js
  import myComponent from './src/myComponent.vue'

  // 安装组件
  const install = (Vue) => {
    Vue.component(myComponent.name, myComponent)
  }

  myComponent.install = install

  // 供直接html引用vuejs使用
  if (typeof window !== 'undefined' && window.Vue) {
    install(window.Vue)
  }

  export default myComponent

  ```     
  修改`webpack.config.js`如下：
  ```js
  var path = require('path')
  var webpack = require('webpack')

  module.exports = {
    // entry: './src/main.js',
    // 如果是开发环境从main.js进，如果是打包构建生产环境，从entry.js进
    entry: process.env.NODE_ENV == 'development' ? './src/main.js' : './entry.js',
    output: {
      path: path.resolve(__dirname, './dist'),
      publicPath: '/dist/',
      // filename: 'build.js',
      filename: process.env.NODE_ENV == 'development' ? 'build.js' : 'testPublishComponent.min.js',  // 组件打包后生成的文件名
      libraryTarget: 'umd'   //  将组件暴露为所有的模块定义下都可运行的方式
    },
    module: {
      rules: [
        {
          test: /\.css$/,
          use: [
            'vue-style-loader',
            'css-loader'
          ],
        },      {
          test: /\.vue$/,
          loader: 'vue-loader',
          options: {
            loaders: {
            }
            // other vue-loader options go here
          }
        },
        {
          test: /\.js$/,
          loader: 'babel-loader',
          exclude: /node_modules/
        },
        {
          test: /\.(png|jpg|gif|svg)$/,
          loader: 'file-loader',
          options: {
            name: '[name].[ext]?[hash]'
          }
        }
      ]
    },
    resolve: {
      alias: {
        'vue$': 'vue/dist/vue.esm.js'
      },
      extensions: ['*', '.js', '.vue', '.json']
    },
    devServer: {
      historyApiFallback: true,
      noInfo: true,
      overlay: true
    },
    performance: {
      hints: false
    },
    devtool: '#eval-source-map'
  }

  if (process.env.NODE_ENV === 'production') {
    module.exports.devtool = '#source-map'
    // http://vue-loader.vuejs.org/en/workflow/production.html
    module.exports.plugins = (module.exports.plugins || []).concat([
      new webpack.DefinePlugin({
        'process.env': {
          NODE_ENV: '"production"'
        }
      }),
      new webpack.optimize.UglifyJsPlugin({
        // sourceMap: true,
        sourceMap: false,   // 禁用sourceMap
        compress: {
          warnings: false
        }
      }),
      new webpack.LoaderOptionsPlugin({
        minimize: true
      })
    ])
  }


  ```

## 4. 打包组件，并试用    
  经过上述的步骤之后，此时通过`npm run build`就可以构建出组件的压缩包了。再`dist`目录可以找到`testPublishComponent.min.js`文件。   
  这个组件现在可以引用到其他项目中，进行全局注册，局部注册，或者是html直接引入vue.js下引入该js文件直接使用，如下：      
  - 全局注册或局部注册使用    
  ```html 
  <template>
    <div id="app">
      显示最简单的文字
      <myComponent msg="文字来自App" />
    </div>
  </template>

  <script>
  // import myComponent from './myComponent.vue'
  // 修改路径为构建过的组件
  import myComponent from '../dist/testPublishComponent.min.js'
  import Vue from 'vue'
  Vue.use(myComponent)

  export default {
    name: 'app',
    // components: {
    //   myComponent,
    // },
    data () {
      return {
      }
    }
  }
  </script>
  ```     
  - html下直接引入使用    
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="utf-8">
  </head>
  <body>
  <div id="app">
    <my-component :msg="propData" />
  </div>
  <script src="https://unpkg.com/vue/dist/vue.js"></script>
  <script src="./dist/testPublishComponent.min.js"></script>
  <script>
    new Vue({
      el: '#app',
      data: function() {
        return {
          propData: 'html版本'
        }
      },
      methods: {
      }
    })
  </script>
  </body>
  </html>
  ```     

## 5. 发布到npm      
  1.  修改package.json文件。在文件中新增一个main入口为构建好的js文件，如下：    
  ![Image text](/03.jpg)      
  2. npm官网创建一个npm账户，并且启动命令行登录
  ![Image text](/04.jpg)    
  3. 登录成功后，运行`npm publish`发布即可。package.json里面的name名不能与已经发布的包同名。    
    在发布之前，可以先通过`npm pack`打包一个本地`test-publish-component-1.0.0.tgz`包，在其他项目中你可以通过`npm install 绝对路径/test-publish-component-1.0.0.tgz`安装，试用可行性。
  4. 发布完了之后，就可以通过npm去安装开发的组件了。


  [源码链接](https://github.com/hanz520/test-publish-component)