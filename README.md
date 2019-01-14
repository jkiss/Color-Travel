# React 多页应用模版

## DOC:

### 一、 📦 打包方式分为生产和线上：
> 所有打包后的文件都在 build/ 目录下，可以直接将 build/ 部署到线上环境
```javascript
npm run dev
npm run build

// 打包环境
node v8.9.4
webpack v4.23.1
```

1. src/ 业务文件夹目录结构：
```javascript
./src
├── fonts
│   └── roboto-thin.styl
│
├── htmlTemplates
│   └── app.ejs
│
├── modules            // 通用模块组件（js&css module）
│   ├── com
│   │   ├── Loading
│   │       ├── index.js
│   │       └── css.styl
│   ├── res            // 通用的静态资源，比如 favicon 图标等
│   │   ├── copy       // 直接 copy 到 build 里面
│   │   │   └── thumb.jpg
│   │   ├── 1.jpg
│   │
│   ├── style
│   │   ├── nk-player.styl
│   │   └── reset.styl
│   └── utils
│       └── index.js
│
├── pages              // 采用DDD（domain drive design）组织结构方式
│   ├── about
│   │   ├── Slide      // presentational component
│   │   │   ├── index.js
│   │   │   └── css.styl
│   │   ├── Video      // presentational component
│   │   │   ├── index.js
│   │   │   └── css.styl
│   │   └── index.js   // container component
│   │
│   └── home           // 业务组件都放在同一路由文件夹
│       ├── Page1      // presentational component
│       │   ├── index.js
│       │   └── css.styl
│       ├── Page2      // presentational component
│       │   ├── index.js
│       │   └── css.styl
│       └── index.js   // container component
│
└── vendor
    └── SplitText.min.js
```

2. webpack/ 打包配置目录：
```javascript
├── entry.js    // 配置js入口文件
├── loaders.js
├── plugins.js  // 每个html文件根据config配置，自动生成
└── resolve.js
```

3. config.js 文件：
```javascript
// webpack发布路径，以及其他一些分享信息，统一配置
{
    // Deploy
    public_path: 'webpack发布路径'
    ,port: 9000
    ,plugin_url: ''

    // multi-pages
    ,pages: [
        {
            title: '标题'
            ,desc: '描述'
            ,image: '预览图（16:9）'
            ,url: 'html页面完整url'
            ,thumb: '微信分享方图（1:1）'

            // htmlWebpackPlugin parameters 
            ,filename: 'index.html'
            ,entry: 'home/index'
        },{
            title: ''
            ,desc: ''
            ,image: ''
            ,url: ''
            ,thumb: ''

            // htmlWebpackPlugin parameters
            ,filename: 'about/index.html'
            ,entry: 'about/index'
        }
    ]
}
```

### 二、🔧 集成的基础插件和功能插件：

   1. [**jquery**](https://jquery.com/): $ 已暴露为全局变量，可以引用jQuery插件；
   
   2. [**jquery.html5loader**](https://github.com/GianlucaGuarini/jquery.html5loader): 传统的预加载所有图片，在展示网页之前；
   
   3. [**fullpage.js**](https://alvarotrigo.com/fullPage/)：全屏滚动插件；
   
   4. [**lodash**](https://lodash.com/)：js基础功能函数封装（utility library）；
   
   5. [**lazysizes**](https://github.com/aFarkas/lazysizes)：具有丰富的图片懒加载方式；
   
   6. [**gsap**](https://greensock.com/gsap)：动画库；
   
   7. [**stylus**](http://stylus-lang.com/): TJ大神出品的css预编译语言，底层node；
   
   8. [**nib**](http://tj.github.io/nib/): 配合stylus的css3扩展函数；

