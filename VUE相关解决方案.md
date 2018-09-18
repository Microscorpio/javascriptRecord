项目所用到的技术：（各个技术所用到的版本号查看package.json）
1. vue : https://cn.vuejs.org/
2. vue-router :  http://router.vuejs.org/zh-cn/api/router-link.html
3. vue-resource : 传参数用params 官网https://github.com/pagekit/vue-resource
4. ui库（ElementUI）：http://element.eleme.io/#/zh-CN/component/installation
5. 字体图标库（阿里图标库）： http://www.iconfont.cn/   892425640@qq.com  tycc..1993
   [没有版本号，是从阿里图标库中直接下载下来手动放到src/assets/font]
6.我们还使用了ElementUI的主题配置（改变ElementUI的主题颜色只需要执行命令就行）
：http://element.eleme.io/#/zh-CN/component/custom-theme
7.src/assets/common.less里面设置了我们自己项目的主题颜色
项目相关描述：（默认去首页是在src/pages/content.vue设置的重定向）
1. 安装淘宝镜像  npm install -g cnpm --registry=https://registry.npm.taobao.org （cnpm install安装依赖速度比npm install快）
2. http://cn.vuejs.org/v2/guide/installation.html                vue自定义项目的脚手架命令行工具安装
3. http://blog.csdn.net/u013778905/article/details/53864289         项目结构说明
4. https://segmentfault.com/q/1010000005138038               WebStorm ES6 语法支持设置
5. https://github.com/chimurai/http-proxy-middleware 【代理服务器中间件，解决跨域config/index.js】
6. http://blog.csdn.net/hongchh/article/details/55113751     webpack配置文件说明（build下的文件）
7. http://www.tuicool.com/articles/rYRBbiA     babel配置   Node.js神器之babel-preset-env：http://www.tuicool.com/articles/YbEfEzz
8. https://segmentfault.com/q/1010000005596587?from=singlemessage&isappinstalled=1      babel-runtime "transform-runtime"避免编译重复的代码在各个代码块里  .babel配置文件中的解释
9. http://blog.csdn.net/larry_lee88/article/details/38538123  （生产环境） 打包gzip , 前端gzip打包之后，服务端要加配置才能用，【这样js文件请求才能以gzip的方式去加载请求】
10. 安装elementui主题需要安装全局的 npm i element-theme -g    执行et命令行才有效果
11.  elementui 按需加载插件babel-plugin-component
     element主题样式是利用babel-plugin-component配置在.babelrc文件中，详情参考：
     i. http://element.eleme.io/#/zh-CN/component/quickstart
     ii. http://element.eleme.io/#/zh-CN/component/custom-theme
12. 安装基于Chrome的devtools http://www.cnblogs.com/lolDragon/p/6268345.html
13. 打包到生产环境后的manifest.js vendor.js app.js的解说：
  https://segmentfault.com/q/1010000009276145/a-1020000009279643
 14. 生产环境环境和测试环境接口请求对应配置：
 http://blog.csdn.net/fungleo/article/details/54574049
 15.        .editorconfig文件 => 该文件定义项目的编码规范，编辑器的行为会与.editorconfig 文件中定义的一致，并且其优先级比
    编辑器自身的设置要高，这在多人合作开发项目时十分有用而且必要。

    root = true

    [*]    // 对所有文件应用下面的规则
    charset = utf-8                    // 编码规则用utf-8
    indent_style = space               // 缩进用空格
    indent_size = 2                    // 缩进数量为2个空格
    end_of_line = lf                   // 换行符格式
    insert_final_newline = true        // 是否在文件的最后插入一个空行
    trim_trailing_whitespace = true    // 是否删除行尾的空格
16. webstorm的node_modules忽略打开：http://www.cnblogs.com/chengwb/p/6183440.html



Title: 我眼中的Vue。
Vote:1
Comment:0条评论
https://zhuanlan.zhihu.com/p/30620860
================ 
Title: 有没有前端大佬，帮忙看个问题。???
Vote:1
Comment:0条评论
https://www.zhihu.com/question/263827671/answer/273420037
================ 
Title: 天了噜，程序猿要毁童年了！
Vote:46
Comment:​14 条评论
https://zhuanlan.zhihu.com/p/25993645
================ 
Title: 学Python Django学得很迷茫，怎么办？
Vote:2
Comment:0条评论
https://www.zhihu.com/question/26235428/answer/227096890
================ 