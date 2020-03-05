1. dependencies   
  应用能够正常运行所依赖的包。这种 dependencies 是最常见的，用户在使用 npm install 安装你的包时会自动安装这些依赖。
2. devDependencies    
  开发应用时所依赖的工具包。通常是一些开发、测试、打包工具，例如 webpack、ESLint、Mocha。应用正常运行并不依赖于这些包，用户在使用 npm install 安装你的包时也不会安装这些依赖。
3. peerDependencies   
  应用运行依赖的宿主包。最典型的就是插件，例如各种 jQuery 插件，这些插件本身不包含 jQeury，需要外部提供。用户使用 npm 1 或 2 时会自动安装这种依赖，npm 3 不会自动安装，会提示用户安装。
4. bundledDependencies    
  发布包时需要打包的依赖，似乎很少见。
5. optionalDependencies   
  可选的依赖包。此种依赖不是程序运行所必须的，但是安装后可能会有新功能，例如一个图片解码库，安装了 optionalDependencies 后会支持更多的格式。

  