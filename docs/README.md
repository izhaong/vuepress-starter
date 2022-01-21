---
title: vue element-ui 换肤功能开发
date: 2021-12-30 15:50:34
permalink: /pages/037c03/
categories:
  - 大前端
  - Vue
tags:
  - 

---



此功能基于

> vue 2.6
>
> element-ui 2.13.2

实现

快速切换主题 使用命令行主题工具进行深层次的主题定制



## 实现原理

- 主题的css通过`public/index.html`中的link标签中引入
- 切换事件中就切换link标签中的css地址即可
  - 避免加载缓慢的问题，提前构建好主题css文件，放置在`src/assets`或者`public`文件夹下
- 结果：

![image-20220112165109453](https://cdn.jsdelivr.net/gh/izhaong/izhaong.com-oss/blogImg/014020.vue%20element-ui%20%E6%8D%A2%E8%82%A4%E5%8A%9F%E8%83%BD%E5%BC%80%E5%8F%91/2022/01/12/16-51-10-1501f8fd057642eb9855ce6c4488ff35-image-20220112165109453-5580b9.png)

## 开始实现

使用官方的深度主题构建工具[element-theme](https://github.com/ElementUI/element-theme)

- 克隆仓库 `git clone https://github.com/ElementUI/element-theme.git`

- node版本切换到10;   我用的10.24.1

- 安装好依赖 `npm i`

- 安装主题包 `npm i element-theme -D`

- 增加npm脚本

  - ```json
    "scripts": {
        ...
        "et": "node_modules/.bin/et",
        "et:init": "node_modules/.bin/et -i",
       	...
      },
    ```

- 初始化变量文件

  - `npm run et:init`

  就可以看到多出一个 element-variables.css的文件

- 然后只需要调整好几个颜色变量即可，[使用官方在线构建](https://element.eleme.cn/#/zh-CN/theme)更准确如果是暗黑模式，就需要把颜色反过来。如

  - ![image-20220112135601646](https://cdn.jsdelivr.net/gh/izhaong/izhaong.com-oss/blogImg/014020.vue%20element-ui%20%E6%8D%A2%E8%82%A4%E5%8A%9F%E8%83%BD%E5%BC%80%E5%8F%91/2022/01/12/13-56-08-4246a53186d4934c20070cb368c773b2-image-20220112135601646-302e1e.png)

  - 然后下载，把其中的json文件中颜色值替换到element-variables.css

  - ```scss
    /* Color
    -------------------------- */
    /// color|1|Brand Color|0
    $--color-primary: #50D6FF !default;
    /// color|1|Background Color|4
    $--color-white: #121B33 !default;
    /// color|1|Background Color|4
    $--color-black: #243666 !default;
    $--color-primary-light-1: mix($--color-white, $--color-primary, 10%) !default; /* 53a8ff */
    $--color-primary-light-2: mix($--color-white, $--color-primary, 20%) !default; /* 66b1ff */
    $--color-primary-light-3: mix($--color-white, $--color-primary, 30%) !default; /* 79bbff */
    $--color-primary-light-4: mix($--color-white, $--color-primary, 40%) !default; /* 8cc5ff */
    $--color-primary-light-5: mix($--color-white, $--color-primary, 50%) !default; /* a0cfff */
    $--color-primary-light-6: mix($--color-white, $--color-primary, 60%) !default; /* b3d8ff */
    $--color-primary-light-7: mix($--color-white, $--color-primary, 70%) !default; /* c6e2ff */
    $--color-primary-light-8: mix($--color-white, $--color-primary, 80%) !default; /* d9ecff */
    $--color-primary-light-9: mix($--color-white, $--color-primary, 90%) !default; /* ecf5ff */
    /// color|1|Functional Color|1
    $--color-success: #16EE9F !default;
    /// color|1|Functional Color|1
    $--color-warning: #F7D230 !default;
    /// color|1|Functional Color|1
    $--color-danger: #FE5858 !default;
    /// color|1|Functional Color|1
    $--color-info: #B2BFD9 !default;
    
    $--color-success-light: mix($--color-white, $--color-success, 80%) !default;
    $--color-warning-light: mix($--color-white, $--color-warning, 80%) !default;
    $--color-danger-light: mix($--color-white, $--color-danger, 80%) !default;
    $--color-info-light: mix($--color-white, $--color-info, 80%) !default;
    
    $--color-success-lighter: mix($--color-white, $--color-success, 90%) !default;
    $--color-warning-lighter: mix($--color-white, $--color-warning, 90%) !default;
    $--color-danger-lighter: mix($--color-white, $--color-danger, 90%) !default;
    $--color-info-lighter: mix($--color-white, $--color-info, 90%) !default;
    /// color|1|Font Color|2
    $--color-text-primary: #DEE7FF !default;
    /// color|1|Font Color|2
    $--color-text-regular: #BED0FF !default;
    /// color|1|Font Color|2
    $--color-text-secondary: #919AB3 !default;
    /// color|1|Font Color|2
    $--color-text-placeholder: #8091BE !default;
    /// color|1|Border Color|3
    $--border-color-base: #414D6E !default;
    /// color|1|Border Color|3
    $--border-color-light: #4E5C7F !default;
    /// color|1|Border Color|3
    $--border-color-lighter: #EBEEF5 !default;
    /// color|1|Border Color|3
    $--border-color-extra-light: #647092 !default;
    
    // Background
    /// color|1|Background Color|4
    $--background-color-base: #243666 !default;
    ```

- 然后就是构建主题包了 `npm run et`

![element](https://cdn.jsdelivr.net/gh/izhaong/izhaong.com-oss/blogImg/014020.vue%20element-ui%20%E6%8D%A2%E8%82%A4%E5%8A%9F%E8%83%BD%E5%BC%80%E5%8F%91/2021/12/31/14-33-29-840e8a7316157b438fc2342415e2cc38-element-4e1dee.gif)

- 构建完成后把包放到 `public/theme/[名称]` 下面

- 最后用函数去手动引入就好了

  ```js
  themeColorChangeHandle (val) {
        var styleList = [
          {
            id: 'J_elementTheme',
            url: `${process.env.BASE_URL}element-theme/${val}/index.css?t=${new Date().getTime()}`
          },
        ]
        for (var i = 0; i < styleList.length; i++) {
          var el = document.querySelector(`#${styleList[i].id}`)
          if (el) {
            el.href = styleList[i].url
            continue
          }
          el = document.createElement('link')
          el.id = styleList[i].id
          el.href = styleList[i].url
          el.rel = 'stylesheet'
          document.querySelector('head').appendChild(el)
        }
      }
  ```

  ### 问题

- 出错：ReferenceError: primordials is not defined

  - node版本过高， 降级node到10就差不多了

  - （不想降级node可使用这个方案）

    - 根目录下新建`npm-shrinkwrap.json`, 其内容如下

    - ```json
      {
        "dependencies": {
          "graceful-fs": {
              "version": "4.2.2"
           }
        }
      }
      ```







