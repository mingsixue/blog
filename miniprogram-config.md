小程序配置
========

全局配置
-------
app.json 是小程序的全局配置，包括了小程序所有页面路径、界面表现、网络超时实际、底部 tab 等。

    {
        // 页面路径列表 String[]
        "pages": [
            "pages/index/index"
        ],

        // 全局默认窗口表现 Object
        "window": {
            // 导航栏背景颜色，如#000000，HexColor，默认#000000
            "navigationBarBackgroundColor": "#fff",

            // 导航栏标题颜色，仅支持 black / white，默认 white
            "navigationBarTextStyle": "black",

            // 导航栏标题文字内容，String
            "navigationBarTitleText": "Title",

            // 导航栏样式，仅支持 default 默认样式 / custom 自定义导航栏
            "navigationStyle": "default",

            // 窗口的背景色，默认#ffffff，HexColor
            "backgroundColor": "#ffffff",

            // 下拉 loadinng 的样式，仅支持 dark / light，默认 dark
            "backgroundTextStyle": "light",

            // 顶部窗口的背景色，仅 IOS 支持，默认#ffffff，String
            "backgroundColorTop": "#ffffff",

            // 底部窗口的背景色，仅 IOS 支持，默认#ffffff，String
            "backgroundColorBottom": "#ffffff",

            // 是否开启全局的下拉刷新，默认 false，Boolean
            "enablePullDownRefresh": false,

            // 页面上拉触底事件触发时距页面底部距离，单位为 px，Number
            "onReachBottomDistance": 50,

            // 屏幕旋转设置，支持 auto / portrait / landscape，默认 portrait
            "pageOrientation": "portrait"
        },

        // 底部 tab 栏的表现 Object
        "tabBar": {
            // tab 上的文字默认颜色，仅支持十六进制颜色，必填
            "color": "",

            // tab 上的文字选中的颜色，仅支持十六进制颜色，必填
            "selectedColor": "",

            // tab 的背景色，仅支持十六进制颜色，必填
            "backgroundColor": "",

            // tabbar 上边框的颜色，仅支持 black / white，默认 black
            "borderStyle": "black",

            // tab 的列表，最少2项，最多5项，Array
            "list": [{
                // 页面路径，必须在 pages 中先定义，String，必填
                "pagePath": "pages/index/index",

                // tab 上按钮文字，String，必填
                "text": "首页"

                // 图片路径，icon 大小限制为 40kb，建议尺寸为 81px * 81px，不支持网络图片，当 position 为 top 时，不显示 icon，String
                "iconPath": "",

                // 选中时的图片路径，icon 大小限制为 40kb，建议尺寸为 81px * 81px，不支持网络图片，当 position 为 top 时，不显示 icon，String
                "selectedIconPath": ""
            }, {
                "pagePath": "pages/my/index",
                "text": "我的"
            }],

            // tabBar 的位置，仅支持 bottom / top
            "position": "bottom",

            // 自定义 tabBar，默认 false，Boolean
            "custom": false
        },

        // 网络超时时间 Object
        "networkTimeout": {
            // wx.request 的超时时间，单位：毫秒，默认 60000，Number
            "request": 60000,

            // wx.connectSocket 的超时时间，单位：毫秒，默认 60000，Number
            "connectSocket": 60000,

            // wx.uploadFile 的超时时间，单位：毫秒，默认 60000，Number
            "uploadFile": 60000,

            // wx.downloadFile 的超时时间，单位：毫秒，默认 60000，Number
            "downloadFile": 10000
        },

        // 是否开启 debug 模式，默认关闭，Boolean
        "debug": true,

        // 是否启用插件功能页，默认关闭，Boolean
        "functionalPages": true,

        // 分包结构配置 Object[]
        "subpackages": [
            // 分包根目录，String
            "root": "packageA",

            // 分包别名，分包预下载的时候可以使用，String
            "name": "pack1",

            // 分享页面路径，相对于分包根目录，String[]
            "pages" : [{
                "pages/cat",
                "pages/dog
            }, {
                "root": "packageB",
                "name": "pack2",
                "pages": [
                    "pages/apple",
                    "pages/banana"
                ]
            }],

            // 分包是否是独立分包，Boolean
            independent: false
        ],

        // Woker 代码放置的目录 String
        "workers": "",

        // 需要在后台使用的能力，如「音乐播放」，String[]
        "requiredBackgroundModes": [
            "audio", // 后台音乐播放
            "location" // 后台定位
        ],

        // 使用到的插件 Object
        "plugins": {
            "myPlugin": {
                "version": "1.0.0",
                "provider": "appid"
            }
        },

        // 分包预下载规则，Object
        "preloadRule": {
            // 页面路径
            "pages/index": {
                // 指定网络下预下载，可选值为：all不限网络 wifi仅wifi下
                "network": "all",

                // 进入页面后预下载分包的 root 或 name。 __APP__ 表示主包
                "packages": ["important", "__APP__"]
            }
        },

        // iPad 小程序是否支持屏幕旋转，默认关闭，Boolean
        "resizable", false,

        // 需要跳转的小程序列表，String[]
        "navigateToMiniProgramAppIdList": [
            "wxe5f52902cf4de896"
        ],

        // 全局自定义组件配置，Object
        "usingComponents": {
            "componentsName": "componentsPath"
        },

        // 小程序接口权限相关设置，Object
        "permission": {
            // 用户信息
            "scope.userInfo": {
                "desc": "描述文案" // 最长 30 个字符
            },

            // 地理位置
            "scope.userLocation": {
                "desc": "" 
            },

            // 后台定位
            "scope.userLocationBackground": {
                "desc": ""
            },

            // 通讯地址
            "scope.address": {
                "desc": ""
            },

            // 发票抬头
            "scope.invoiceTitle": {
                "desc": ""
            },

            // 获取发票
            "scope.invoice": {
                "desc": ""
            },

            // 微信运动步数
            "scope.werun": {
                "desc": ""
            },

            // 录音功能
            "scope.record": {
                "desc": ""
            },

            // 保存到相册
            "scope.writePhotosAlbum": {
                "desc": ""
            },

            // 摄像头
            "scope.camera": {
                "desc": ""
            }
        },

        // 指明 sitemap.json 的位置，String
        "sitemapLocation": "",

        // 指定使用升级后的 weui 样式，String
        "style": "",

        // 指定需要引用的扩展库，Object
        "useExtendedLib": {
            "kbone": true,
            "weui": true
        },

        // 微信消息用小程序打开，Object
        "entranceDeclare": {
            "locationMessage": {
                "path": "pages/index/index",
                "query": "foo=bar"
            }
        }
    }

`pages` 字段，用于描述当前想程序所有页面路径，每一项对应一个页面的路径，文件名不需要写文件后缀，框架会自动去寻找。数组的第一项代表小程序的初始页面（首页），新增/减少页面，都需要对 pages 数组进行修改，在 app.json 中添加。

<pre><code>├── app.js
├── app.json
├── app.wxss
├── pages
│&nbsp;&nbsp; │── index
│&nbsp;&nbsp; │   ├── index.wxml
│&nbsp;&nbsp; │   ├── index.js
│&nbsp;&nbsp; │   ├── index.json
│&nbsp;&nbsp; │   └── index.wxss
│&nbsp;&nbsp; └── my
│&nbsp;&nbsp;     ├── my.wxml
│&nbsp;&nbsp;     └── my.js
└── utils
</code></pre>

`window` 字段，定义小程序所有页面的顶部背景颜色、文字颜色等

![Window](https://res.wx.qq.com/wxdoc/dist/assets/img/config.344358b1.jpg)

[官网链接]：[Window 配置](https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/app.html#%E5%85%A8%E5%B1%80%E9%85%8D%E7%BD%AE)

`tabBar` 字段，如果小程序是一个多 tab 应用（客户端窗口的底部或顶部有 tab 栏可以切换页面），可以通过 tabBar 配置项指定 tab 栏的表现，以及 tab 切换时显示的对应页面。

![tabBar](https://res.wx.qq.com/wxdoc/dist/assets/img/tabbar.ce1b3c5b.png)

[官网链接]：[tabBar 配置](https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/app.html#tabBar)

`debug` 字段，可以在开发者工具中开启 debug 模式，在开发者工具的控制台面板，调试信息以 info 的形式给出，其信息有 Page 的注册，页面路由，数据更新，事件触发等。可以帮助开发者快速定位一些常见的问题。

`functionalPages` 字段，插件所有者小程序需要设置这一项来启动插件功能页。

`subpackages` 字段，声明项目分包结构，写成 subPackages 也支持。开发者将小程序划分成不同的子包，用户在使用时按需进行加载。每个使用分包的小程序必定含有一个主包。在小程序启动时，默认会下载主包并启动主包内页面，当用户进入分包内某个页面时，客户端把对应分包下载下来，下载完成后再进行展示。分包有大小限制，整个小程序分包大小不超过 8M，单个分包/主包大小不超过 2M。

<pre><code>├── app.js
├── app.json
├── app.wxss
├── packageA
│&nbsp;&nbsp; └── pages
│&nbsp;&nbsp;     ├── cat
│&nbsp;&nbsp;     └── dog
├── packageB
│&nbsp;&nbsp; └── pages
│&nbsp;&nbsp;     ├── apple
│&nbsp;&nbsp;     └── banana
├── pages
│&nbsp;&nbsp; ├── index
│&nbsp;&nbsp; └── logs
└── utils
</code></pre>

打包原则
* 声明 subpackages 后，将按 subpackages 配置路径进行打包，subpackages 配置路径外的目录将被打包到 app（主包）中
* app（主包）也可以有自己的 pages（即最外层的 pages 字段）
* subpackage 的根目录不能是另一个 subpackage 内的子目录
* tabBar 页面必须在 app（主包）内

引用原则
* packageA 无法 require packageB JS 文件，但可以 require app、自己 package 内的 JS 文件
* packageA 无法 import packageB 的 template，但可以 require app、自己 package 内的 template
* packageA 无法使用 packageB 的资源，但可以使用 app、自己 package 内的资源

`workers` 字段，在 app.json 中可配置 Worker 代码放置的目录，目录下的代码将被打包成一个文件。

<pre class="language-text"><code>├── app.js
├── app.json
├── project.config.json
└── workers
    ├── request
    │   ├── index.js
    │   └── utils.js
    └── response
        └── index.js
</code></pre>

`requiredBackgroundModes` 字段，申明需要后台运行的能力，目前支持 audio 后台音乐播放 / location 后台定位，在此处申明了后台运行的接口，开发版和体验版上可以直接生效，正式版还需要通过审核。

`plugins` 字段，可以包含多个插件声明，每个插件声明以一个使用者自定义的插件引用名作为标识，并指明插件的 appid（provider字段） 和需要使用的版本号。myPlugin 名称由使用者定义，无需和插件开发者保持一致或开发者协调。

<pre class="language-json"><code>{</span>
  "plugins": {
    "myPlugin": {
      "version": "1.0.0",
      "provider": "wxidxxxxxxxxxxxxxxxx"
    }
  }
}
</code></pre>

也可以在分包内引入插件代码包，但使用有限制，仅能在这个分包内使用该插件；同一个插件不能被多个分包同时引用；如果基础库版本低于 2.9.0，不能从分包外的页面直接跳入分包内的插件页面，需要先跳入分包内的非插件页面、再跳入同一分包内的插件页面。

<pre class="language-json"><code>{
  "subpackages": [
    {
      "root": "packageA",
      "pages": [
        "pages/cat",
        "pages/dog"
      ],
      "plugins": {
        "myPlugin": {
          "version": "1.0.0",
          "provider": "wxidxxxxxxxxxxxxxxxx"
        }
      }
    }
  ]
}
</code></pre>

`preloadRule` 字段，预下载分包行为在进入某个页面时触发，key 是页面路径，value 是进入此页面的预下载配置。

`resizable` 字段，在 iPad 上不能单独配置某个页面是否支持屏幕旋转，在屏幕旋转时，小程序将随之旋转，显示区域尺寸也会随着屏幕旋转而变化。对于不同尺寸的显示区域，页面的布局会有所差异，此时可以使用 media query 来解决大多数问题。

`navigateToMiniProgramAppIdList` 字段，当小程序要跳转到其它小程序时，需要先在配置文件中声明需要跳转的小程序 appId 列表，最多允许填写 10 个。

`usingComponents` 字段，在这里声明的自定义组件视为全局自定义组件，在小程序内的页面或自定义组件中可以直接使用而无需再声明。

`permission` 字段，小程序接口权限相关设置，一旦用户明确同意或拒绝过授权，其授权关系会记录在后台，直到用户主动删除小程序。

`sitemapLocation` 字段，指明 sitemap.json 的位置，默认为 sitemap.json 即在 app.json 同级目录下名字的 sitemap.json 文件。

`style` 字段，微信客户端7.0开始，UI界面进行了大改版。小程序也进行了基础组件的样式升级，可使用 v2 表明启用新版的组件样式。

`useExtendedLib` 字段，指定需要引用的扩展库，目前支持 kbone:多端开发框架、weui:WeUI组件库。指定后相当于引入了对应扩展库相关的最新版本的 npm 包，同时也不占用小程序的包体积。目前不支持分包中引用。

`entranceDeclare` 字段，聊天位置消息用打车类小程序打开，IOS不支持。

页面配置
-------
每一个小程序页面可以使用同名 .json 文件来对本页面的窗口表现进行配置，页面中配置项会覆盖 app.json 的 window 中相同的配置项。

    {
        // 导航栏背景颜色，如#000000，HexColor，默认#000000
        "navigationBarBackgroundColor": "#000000",

        // 导航栏标题颜色，仅支持 black / white，默认 white
        "navigationBarTextStyle": "white",

        // 导航栏标题文字内容，String
        "navigationBarTitleText": "Title",

        // 导航栏样式，仅支持 default 默认样式 / custom 自定义导航栏
        "navigationStyle": "default",

        // 窗口的背景色，默认#ffffff，HexColor
        "backgroundColor": "#ffffff",

        // 下拉 loadinng 的样式，仅支持 dark / light，默认 dark
        "backgroundTextStyle": "dark",

        // 顶部窗口的背景色，仅 IOS 支持，默认#ffffff，String
        "backgroundColorTop": "#ffffff",

        // 底部窗口的背景色，仅 IOS 支持，默认#ffffff，String
        "backgroundColorBottom": "#ffffff",

        // 是否开启全局的下拉刷新，默认 false，Boolean
        "enablePullDownRefresh": false,

        // 页面上拉触底事件触发时距页面底部距离，单位为 px，Number
        "onReachBottomDistance": 50,

        // 屏幕旋转设置，支持 auto / portrait / landscape，默认 portrait
        "pageOrientation": "portrait",

        // 设置为 true 则页面整体不能上下移动，只在页面配置中有效，无法在 app.json 中设置，Boolean
        "disableScroll": false,

        // 页面自定义组件配置，Object
        usingComponents: {
            "component-tag-name": "path/to/the/custom/component"
        }
    }