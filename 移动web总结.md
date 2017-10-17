##  移动web开发  使用手机上网的用户多 但是 开发人员缺少

## 准备工作

##  屏幕 

1.   英寸 3.5 4.0 5.5 
2.   分辨率  1366*768（PC 1366 是宽度 768高度）  960（高度） * 640（宽度）  1920*1080  480 * 320
3.   DPI PPI（像素密度） 1英寸 所容纳的像素点 1英寸 容纳 宽度163px 高度 163px  PPI(163)
          PPI 326  宽度 326px 高度326px   像素的高的平方 和 像素的宽的平方 开根号 除以 英寸
          屏幕尺寸固定时，当PPI 越大，像素的实际大小就会越小，当PPI越小，像素实际大小就越大
4.   DIP (设备独立像素) PC 1366*768  1px 就等于 1设备独立像素 1dp = 1px
          960 * 480（分辨率）  480*320(真实像素)  1设备独立像素 = 2 分辨率像素  1dp = 2px
5.   物理像素(分辨率像素)和CSS像素(真实像素) 

## 远程调试(真机调试)

  1. 手机和电脑要链接同一个wifi
  2. 电脑开启服务器 (localhost) 把localhost换成ip地址
  3. 把地址发给手机 或者 使用二维码扫描

## 视口

  1. 什么是视口 (浏览器的可视窗口) 在手机端和屏幕大小一样
  2. 视口在PC端没有效果 移动端页面默认的视口宽度 980 (造成网页缩放)
  3. 解决视口宽度默认980的问题 设置视口的宽度等于 设备的宽度 width=device-width
  4. 视口的其他设置 初始化缩放 最大 最小 是否允许缩放。。。
  5. 快捷键 meta:vp + tab 生成标准化视口配置

##  移动端的站点和浏览器 

  1. 手机淘宝 手机京东 (上面)轮播图 (中间)导航 (下面)商品列表
  2. 移动浏览器 移动端主流浏览器都是谷歌是webkit内核 不用考虑兼容性问题

## JD项目 
  1. 样式初始化
  2. box-sizing:border-box;  防止出滚动条
      1.     -webkit-tap-highlight-color: transparent; 清除 a标签的点击高亮
  3. 网页结构 分为多少块 顶部搜索 轮播图 导航条 商品列表
  4. 布局容器 layout
      1. 最大宽度 640px
      2. 最小宽度 320px
      3. 居中
  5. 构建顶部搜索块
      1. 左右两边固定宽度 中间自适应的布局
          1. 使用margin（不推荐） 给中间的盒子加上margin-left：xxpx; margin-right:xxpx 这种方式的中间的盒子不能加width:100%
          2. 推荐使用padding 盒模型box-sizing:border-box; 把中间的内容挤小
      2. 精灵图缩放(移动端精灵图都会要缩放) background-size:200px 200px;

  6. 轮播图的制作
      1. 写结构 ul > li > img 
      2. 写样式: 1 先写布局 ：给ul设置宽度 800%  里面的每个li的宽度 1/8 12.5%(相对ul所以相当于就是banner的宽度)  左浮动 
      3. 小圆点 ul li  ul要定位居中 水平居中 距离底部10px left:50% margin-left:-60px 
         transform:translateX(-50%);
  7. 导航条的制作
      1. 写结构 ul > li > a >  img + p
      2. 分析布局 li设置宽度25% 浮动
      3. 调整a的字体 行高 文本居中... 
      4. 背景色默认只能看到一截 给ul加清除浮动
  8. 图片距离块级元素底部3px的间距 

      1. 给图片转块
      2. 设置文字大小0
      3. 设置vertical-align: middle/bottom;



## 京东超市商品块的布局

  1. 标题 和内容的一个布局
  2. 内容的流式布局 50% 浮动
  3. 边框和宽度50%的公共样式的使用
  4. 使用障眼法解决左边图片高度不够的问题 背景色填充

## 秒杀块的布局

  1. 标题和内容的布局
  2. 标题的左右两边浮动
  3. nth-of-type(3n) 选中两个冒号
  4. 秒杀商品内容 流式布局 33.33% 给li加
  5. 秒杀商品图片 60%百分比

## 头部搜索JS特效

  1. 获取banner轮播图容器的高度
  2. 添加滚动条滚动事件 获取滚动条滚动的距离
  3. 计算透明度 滚动条距离/banner的高度
  4. 把透明度拼接到rgba设置到搜索框上
  5. 判断如果滚动条距离超过了轮播图容器的高度 就计算透明度和设置

## 移动端的滑动事件

  1. touchstart  手指触摸的时候会触发
  2. touchmove 手指在屏幕上滑动的时候会触发
  3. touchend 手指离开时会触发
  4. touchcancel (了解) 触摸中断会触发(突然来电话)
  5. 注意 滑动事件的的元素 需要有宽高 

## 滑动事件里面的事件源对象 (touchevent)

  1. touches 表示获取屏幕上的手指对象(数组)
  2. targetTouches 表示获取元素上的手指对象
  3. changedTouches 表示获取手指改变后的手指对象
  4. touches  和 targetTouches 是一样的  通常用在 touchstart 和 touchmove 事件里面获取手指对象
  5. changedTouches 通常用在 touchend 事件里面 获取手指离开一瞬间的手指对象

## touch 对象 (手指对象)

  1. clientX  手指相对于视口左上角的X轴的位置  clientY  手指相对于视口左上角Y轴的位置 
  2. pageX 手指相对于页面左上角的X轴的位置  pageY 手指相对于页面左上角Y轴的位置
  3. screenX  手指相对于屏幕左上角X轴的的位置 screenY  手指相对于屏幕左上角的Y轴的位置
  4. 当页面没有滚动条的时候 clientX pageX clientY pageX 是一样 有滚动条建议使用pageX

## 拖拽操作

  1. 注册滑动事件 touchstart touchmove
  2. 获取开始的时候的X 和 Y轴的位置 clientX
  3. 获取滑动中的时候 X Y 轴的位置
  4. 用 滑动中的X 和 Y轴的位置 减去开始的X 和 Y  求到滑动的距离
  5. 把滑动的距离作为位移设置到div上

## 轮播图的滑动

1.   注册滑动事件 touchstart   touchmove touchend
2.   获取滑动开的的X轴的位置 记录到startX 
3.   滑动开始的时候把 定时器清除 滑动的时候是不需要自动播
4.   touchmove记录滑动中的X轴的位置 moveX
5.   计算滑动的距离 distanceX =  moveX - startX
6.   把滑动的距离设置到imgBox上  
7.   同时要清除过渡 原因 就是滑动的时候 已经很慢 不在需要过渡
8.   设置位移的时候 除了 distanceX  还要加上当前轮播图已经到达的位置 
          (-index+bannerWidth +distanceX)+'px';


## 轮播图的切换

1. 判断滑动的距离有没有超过100  注意 给 distanceX加上绝对值 Math.abs(distanceX) > 100
2. 判断  distanceX 是正值 （从左往右）切换到上一张 index --  
         还是负值  (从右往左) 切换到下一张 index++ 
         设置 imgBox的位移 -index+bannerWidth  加上过渡
3. 如果没有超过100做回弹  Math.abs(distanceX) > 0  (防止没有滑动的时候也执行代码)
          设置 imgBox的位移 -index+bannerWidth  加上过渡
4. 加上定时器


## 过渡完成事件 transitionend   webkitTransitionEnd （当一个元素过渡完成的时候会触发的事件）
  1. 在过渡完成里判断index  index == count-1  index = 1  设置位移 清除过渡
  2. 判断index == 0  ；index = count-2 设置位移和清除过渡

## 节流阀

  1. 定义一个是否过渡完成的变量 isEnd= true
  2. 在 touchmove里面判断 如果isEnd== true 才计算移动的距离和设置位移 
  3. 在touchend里面 isEnd=false  因为 滑动结束的时候 会切图 或者 回弹 都会有过渡 
  4. 在过渡完成事件里面 isEnd = true 
  5. 注意 在 touchend事件里面要把 distanceX清空
  6. 当滑动完毕 把定时器设置回去(在过渡完成事件里面加)

## 点标记实现 
  1. 清空所有li的active
  2. 给当前index-1（因为图片索引从1开始 点标记是从0 开始）的li添加active
  3. 注意点标记的清空和添加 过渡完成后添加

## zepto的基本介绍
  1. 和JQ一样 定位于移动端
  2. zepto是分模块 主模块里面 只包含了基本的5个模块 

## 使用zepto实现 轮播图的自动播
1. zepto的使用和JQ一样 但是一些东西需要引入单独的模块
2. 选择器模块 eq()  selector.js
3. 动画模块 animate()的使用   fx.js
4. animate()的使用 
        animate({
          属性:值
        },时间，速度函数，动画执行的回调函数)
        动画执行的回调函数相当于（transitionend）


## zepto 滑动事件 

  1. swipeLeft 左滑动事件 (从右往左滑会触发的事件)
  2. swipeRight 右滑动事件 (从左往右滑会触发的事件)
  3. 注意 使用滑动事件需要引入touch.js包

## zepto的定制(把模块合到一个包方便引入)

  1. 安装nodeJS环境 双击node.msi 一路next 不要选目录
  2. 下载zepto  zepto-master文件夹
  3. 在zepto-master文件夹里面的上面搜索框输出cmd进入当前目录的命令行
  4. 修改make文件 大概41行左右  modules = (env['MODULES'] || 'zepto event ajax form ie fx selector touch').split(' ') 把想要的包在括号里面添加
  5. 编译定制的zepto  npm run-script dist

## 真机调试

  1. 联网 手机和电脑连接同一个wifi (或者电脑开wifi手机连接 或者 手机开热点电脑连接)
  2. 电脑开启网页服务器 
    1. 打开sublime（我的）
    2. 把项目拖进sublime里面
    3. 点击tools > sublimeserver > start sublimeserver
    4. 在html文件右键  view in sublimeserver
  3. 查看wifi的ip
  4. 把 网址的localhost换成192.168.191.1

## 分类页面的布局 全屏布局(没有滚动条的页面)
1. 设置宽度100%高度100% 使用padding把内容挤小 （要把所有元素的盒模型设置成border-box）
2. 左边固定宽度右边自适应的布局 左边的宽度固定100px 要加float:left 右边元素设置margin-left:100px 

## 头部的两个图标 background-size  origin clip position 盒模型 box-sizing:border-box 和搜索框  box-sizing:border-box 

## 左侧的布局 右边的布局

## 左侧滑动  使用滑动事件 touchstart touchmove touchend 获取Y轴的坐标值 clientY

1. 设置位移 top  往下滑是正 往上滑是负

2. 滑动的距离 要每次加上上一次的滑动距离 在滑动结束后累计 currentY += distanctY

3. 判断滑动的位置 有没有超出最大的静止定位位置 和最小的静止定位位置  

4. 最大的静止定位位置 超过了0px 就要位移到0px

5. 最小的静止定位位置 400px-800px  就是超过了 -400px 就要位移到-400px


## 点击切换  移动端的点击事件 移动端click事件有300ms左右的延迟 所以使用 自己封装的点击事件才执行单击操作

1. 通过使用touchstart 和touchend事件 才判断 如果单击的事件 如果小于150ms 并且只有一个手指单击 认为是单击操作
2. 执行切换的业务逻辑

## 点击事件封装成一个tap函数 itcast对象上的 对象上的函数（便于扩展）
函数有两个参数 tap(需要注册tap事件的dom元素,触发事件后需要执行的回调函数(e))

## 点击切换的业务逻辑

1. 点击切换到时候 切换active 把所有li的active类名清空 
2. 给当前点击的Li添加active e.target.parentNode
3. 设置点击的位移 当前li的索引*一个li的高度   
4. 给所有的li添加一个索引 lis[i].index = i;
5. 设置位移的距离 加过渡  判断 如果当前li的索引*li的高度 超过了最小的静止定位位置 就设置成最小静止定位的位置

6. 给当前的currentY = 位移的位置（当前li的索引*一个li的高度 ）/ 最小的静止定位位置

## 使用zepto的tap事件的使用

$('选择器').on('tap',function(e){

})

注意 zepto和 自己封装的tap事件都有一个共同的问题  点透的问题

## 解决移动端的点击事件 延迟 并且点透的问题 引入fastclick来解决点击事件的问题
1. 引入faskclick的包
2. $(function() {
        FastClick.attach(document.body);
    }); 给页面的所有元素都添加faskclick事件的绑定
3. 用原生 或者jq的方式 直接注册click

## iScroll.js插件的使用  
1.  作用: 是解决滑动操作的插件 (分类页面左侧和右侧的滑动,轮播图也可以用)
2.  使用步骤 
    1.  引包 引入 <script src="./js/iscroll.js"></script>
    2.  书写页面结构
        1. 要有一个父容器(固定宽高 切overflow:hidden)
        2. 要有一个子容器 子容器的内容要比父元素高 或者宽
    3.  创建iscroll对象 实现滑动操作
            var myScroll = new IScroll('#wrapper',{
                 mouseWheel: true,
                 scrollbars: true
             });
             创建对象里面的第一个参数是父容器的选择器 第二个参数就是配置的对象

## swipe插件的使用 (轮播图插件)

  1. 引包 把 swipe.js引入
  2. 创建页面结构
    1. 有个父容器 隐藏溢出
    2. 有个子容器 很多张图
    3. 类名可以自己定义
    4. 注意每张图就是100%
       3.调用JS创建swipe对象
        var mySwipe = Swipe(document.querySelector(".jd_banner"),{
        auto:2000
       });
       注意 传入的是DOM元素

## swiper 插件的使用 (轮播图插件)

1.  引包 
2.  引入 css swiper.css
    1. 引入 JS  swiper.js
3.  创建页面结构
         ​```
          <div class="swiper-container" id="swiper0">
             <!--图片-->
             <ul class="swiper-wrapper">
                 <li class="swiper-slide">
                     <a href="javascript:;">
                         <img src="./uploads/l1.jpg" alt="">
                     </a>
                 </li>
             </ul>
         </div>
         ​```
         
         注意 使用swiper插件的结构要和官方要求的一样 类名要一样
         父容器.swiper-container
         子容器.swiper-wrapper
         每一张图的 .swiper-slide
4.  创建swiper插件对象
       var mySwiper = new Swiper ('.swiper-container',{
           autoplay: 2000,
           direction : 'vertical'
       });
       注意 传入的是选择器(父容器)
       参数配置  autoplay 定时器 loop 循环 loop:true

## 响应式的概念   (一个页面适配多个终端)


## 媒体查询 

@media screen and (min-width:xxpx)  屏幕宽度大于等于值
@media screen and (max-width:xxpx)  屏幕宽度小于等值

@media (min-width:xxpx)  屏幕宽度大于等于值
@media (max-width:xxpx)  屏幕宽度小于等值

min-width 判断条件要从小到大写  先写小的条件判断 768  > 992 > 1200
max-width 判断条件要从大到小写  先写大的条件判断 1200  > 992 > 768


## 响应式开发框架 妹子UI  framework7 Bootstrap（重点）

## Bootstrap框架的介绍

  1. 当前前端最流行的框架
  2. 快速开发响应式网站 
  3. 提供了很多丰富的组件

## Bootstrap框架的基本使用

  1. 下载Bootstrap （生产环境的包）
  2. 使用Bootstrap的基本模块  (首页 》 起步 》基本模块 )
  3. 理解基本模板的内容 (引包)
      1. 引入CSS文件   <link href="css/bootstrap.min.css" rel="stylesheet">
      2. 引入jquery  <script src="//cdn.bootcss.com/jquery/1.11.3/jquery.min.js"></script>
      3. 引入Bootstrap的JS文件  <script src="js/bootstrap.min.js"></script>
      4. 条件注释 :  <!--[if lt IE 9]> 条件成立执行的代码  <![endif]-->
          1. 条件注释只是针对IE浏览器生效
          2. 作用解决IE浏览兼容问题
          3. 当if条件成立的时候 条件里面 的代码就会执行 当条件不成立的时候 代码就是注释不执行
          4. 快捷键 cc:ie6
  4. 框架通常放在lib(library)文件夹里面 注意 这里面的东西是只用不改

## 布局容器

  1. container 固定宽度且居中的容器 (媒体查询判断 改变容器在不同屏幕下的宽度)
  2. container-fluid 全屏100%撑满的容器

## 栅格系统  (流式布局的栅格系统)

1.    栅格系统 在行.row里面 
2.    一行默认分为12份
3.    栅格系统有多个屏幕的档次
      1. col-xs  在任意档次都可以生效 通常会在w<768
      2. col-sm  768 - 992
      3. col-md 992 -1200
      4. col-lg w> 1200
      5. 注意 这个档次也是会向上兼容和向下覆盖
4.    常见的布局写法
          ​```
            <div class="row">
              <div class="col-xs-12"></div>
              <div class="col-xs-12 col-sm-6 col-md-4 col-lg-3"></div>
              <div class="col-xs-12 col-sm-6 col-md-4 col-lg-3"></div>
              <div class="col-xs-12 col-sm-6 col-md-4 col-lg-3"></div>
            </div>
          ​```


## 栅格系统的其他特性 
1.    列偏移 (col-md-offset-2)  
2.    列排序  .col-md-pull-2 .col-md-pull-2
3.    列嵌套 列里面嵌套一行
            <div class="row">
              <div class="col-md-4">
                <div class="row">
                  <div class="col-sm-6">1</div>
                  <div class="col-sm-6">1</div>
                </div>
              </div>
            </div>
            栅格系统是流式布局 也就是百分比
            col-sm-6 的50% 是相对于 col-md-4 的一半
4.    隐藏列  hidden-sm xs.. 在某个屏幕隐藏  visible-xs sm 在某个屏幕显示  注意这个屏幕档次是固定的 不会向上兼容和向下覆盖 原因是条件里面 @media (min-width: 768px) and (max-width: 991px) 
      1. col-xs  在任意档次都可以生效 通常会在w<768
      2. col-sm  768 - 992
      3. col-md 992 -1200
      4. col-lg w> 1200


##  less

1.    less编译 
      1. 安装node js
      2. 把 less.cmd等文件 放到Nodejs的安装目录 或者 AppData里面的npm目录
      3. 在webstrom实现编译 
          1. 创建less文件  右键 new file  填写 aa.less  （自己写后缀名.less）
          2. 右上角有一个add watch 选择program 的less.cmd目录 点ok
          3. 在less文件写代码 实现即时编译
2.    less语法

      1. 定义变量 @变量名:变量值;
      2. 混入 (定义函数)   .radius(@r:10px){border-radius:@r;}
      3. 嵌套  
          .row > div > a{}
          .row{
              &
              >div{
                  &
                  >a{
                      &
                 }
              }
          }

          & 符号 表示当前所在大括号的元素  相当于 JS里面 this

          通常会用在 伪类 伪元素 交集选择器
         ```css
                    a:hover{

                    }
                    a{
                      &:hover{

                      }
                    }

                    div::before{

                    }

                    div{
                      &::before{

                      }
                    }

                    li.active a{

                    }
                    li{
                      &.active{
                        a{
                        
                        }
                      }
                    }
         ```

## 微金所顶部通栏

1. 版心容器 container
2. 栅格系统  col-md-2  5 2 3
3. 隐藏类 hidden-xs hidden-sm
4. 字体图标 使用字体图对应的类名
5. 图片定位水平居中 盖住边框
6. 右边的按钮的样式重置

## 导航条的使用

1. 版心容器  container
2. 把表单 下拉菜单删掉
3. 修改文字内容
4. 修改导航条样式 
    1. 修改导航条的高度 注意不能给最外面的导航条加高度80因为移动端的高度是自适应
    2. 给导航条的子元素加高度 navbar-header 或者 navbar-collapse
    3. 修改 navbar-header 里面 的 navbar-brand的行高 行高是50原因是navbar-brand默认有上下15px padding所以行高要减掉padding
    4. 导航条内容样式修改 调整行高 a的行高 也是50 因为也有padding 字体大小
    5. 调整.active a的背景色去掉 加上底部边框
    6. 调整a hover 和 foucs 的字体颜色 加上底部边框
    7. 调整 navbar-brand里面的图标 换成logo text 分别设置图标的字体大小和颜色
    8. 调整 navbar-toggle 的上边距
    9. 在sm屏幕隐藏 navbar-nav hidden-sm

## 轮播图的使用

1. 轮播图插件在 JS 插件里面的carousel
2. 轮播图的结构 小圆点carousel-indicators    轮播图项carousel-inner  控制器 carousel-control
3. 轮播图的轮播项里面的 item  就是每一张轮播图 往图片标签插入图片 但是注意 item有一个active 类名表示当前正在显示的图片 有且只能有一个
4. 实现微金所的响应式轮播图
    1. 实现思路 分成两个轮播图来实现
        1. 移动端展示的轮播图 使用图片标签的方式 给图片标签设置宽度100% 因为移动端的图比较小需要可以自动适应(可以自动改变宽高)
        2. PC端展示的轮播图  由于图片比较大 2000px的宽度 PC屏幕通常是1366 展示2000展示不完会触滚动条 或者 设置100%宽度 宽高会缩小 
           解决方案就是PC端使用背景图 实现轮播图的显示 给每一个item里面的a添加一个行内样式背景图 (因为每一张图都不一样)同时给所有a添加高度410 背景定位居中 背景大小cover
    2. 把大图和小图结合到一起 实现响应式轮播
        1. 把大图小图的a都放到item里面 
        2. 根据屏幕宽度控制大图和小图的显示隐藏 
            1. 小图 在 sm md lg都隐藏 或者 visible-xs 只在xs显示
            2. 大图 在 xs 隐藏
               3.但是这种响应式轮播图有缺点(资源请求浪费 在什么屏幕都要加载所有的图片)

## 引入文件

1. 引入第三方的文件 bootstrap jquery这种
    1. 引入bootstrap css第三方
    2. 引入jq 第三方
    3. 引入bootstrap js第三方
2. 引入公共样式文件 base.css初始化 或者字体图标的样式...
3. 引入自己的文件
    1. index.css
    2. index.js

## JS 实现响应式轮播图

1. 分析实现原理 是通过添加resize事件 判断屏幕宽度 加载不同的图片
2. 加载图片的图片路径不一样 分别存储到了 item的自定义属性上 data-large-image data-small-image
3. 循环变量所有item分别设置每个item里面的a的图片 大图就获取 大图路径 小图就获取小图路径
4. 注意 大图背景图style不能直接插入 要使用css方法先设置到标签上在html进去 或者style里面不带 引号
5. resize事件默认不能触发 trigger('resize') 事件注册完了马上触发一次

## 轮播图滑动

1. 获取手指开始位置
2. 获取结束手指的位置
3. 结束-开始判断滑动的方向 正 从左到右 上一张  负 从右到左 下一张
4. 实现上一张 prev()  下一张 next()
5. 导航条底部20px边距

## 信息块

1. 版心容器 container
2. 栅格系统  col-md-4 col-sm-6
3. 组件》媒体对象 media
4. 给最外层盒子加padding 分别给里面的row里面的每一个列 盒子再加margin-top 父元素和子元素直接的距离用padding 子元素子元素之间的距离用margin
5. hidden-xs

## 预约块

1. 版心容器 container
2. 栅格系统 col-sm-9 col-sm-3
3. 图标 和 字体颜色..
4. 高度行高 60px
5. hidden-xs

## 标签页 商品块

1.  标题和 内容是靠 href的选择器 和 data-toggle="tab" 起作用
2.  标签页标题样式修改
    1. 产品设置整体背景色
    2. 修改高度 修改 li里面的a的行高 50px
    3. 去掉li>a的边框 和背景色
    4. 去掉active > a的边框背景色
    5. li默认有-1px的margin-bottom 去掉边框0px
    6. 给active> a 和 a:hover 加上自己的border-bottom
    7. 给li加左右padding 15px

3.  标签页面板样式修改
    1. 栅格系统划分 col-md-4 col-sm-6 col-xs-12
    2. 左边自适应 右边固定 左边maring-right:100px 右边width：100px的定位到右边 给父元素加相对定位
    3. 栅格的列嵌套  在左侧里面嵌套一个row > .col-xs-6
    4. 右边块加上左虚线边框
    5. 处理上下的小半圆 小半圆的背景色和最外的大盒子一样 定位到上面和下面 圆角 阴影

4.  工具提示的使用

    1. JS插件 》 工具提示
    2. 起作用的是 data-toggle="tooltip" data-placement="top" title="微金宝"  和 元素 样式没关 
    3. 但是要初始化   $('[data-toggle="tooltip"]').tooltip();
    4. 注意 给宝和北的父元素 加上100%不然工具提示信息不能在一行显示

5.  active样式添加

    1. 给第一个wjs_box添加active类名
    2. 当有active类名 的盒子背景色 主题色 文本是白色
    3. 给左边加一个伪元素设置伪元素的content是图标编码 设置字体颜色 是wjs 调整位置字体大小

6.  实现标签页标题的滑动

    1. 有一个结构 父元素和子元素 并且子元素的宽度要比父元素宽 父元素设置overflow:hidden;
    2. 通过JS获取ul里面的所有Li元素的宽度(每个标题的宽度) li是有padding的获取的时候要用innerWidth()
    3. 设置到ul元素上 同时在ul外面在嵌套一个 tabs_parent 元素设置overflow:hidden;
    4. 引入isScroll.js 在Index前面引入 因为Index依赖iscroll
    5. 创建iscroll
        ```
          var myScroll = new IScroll('.tabs_parent',{
              /*设置水平滑动，不允许垂直滑动*/
              scrollX: true, scrollY: false
          });
        ```
        注意 如果要支持水平滑动要设置 scrollX = true 默认是不支持水平滑动


## 新闻块制作

1. 版心容器 container
2. 栅格系统 2(offset-2偏移2)  1 7 
3. 1份的列 放 标签页的标题 
4. 7份的列 放 标签也的内容
5. 调整标签页标题的样式
    1. 调整每个a 边框去掉 
    2. active > a 边框背景色去掉  加上主题背景色
    3. a:hover的边框背景色去掉  加上主题背景色
    4. 依次放 new01-04
    5. 调整图标的字体大小  
    6. 调整a的圆角 50%
    7. 调整红色的虚线 不能用伪元素 伪元素高度100%需要父元素也有固定高度 定位到中间
6. 响应式标题
    1. md 的时候默认 下边距
    2. sm 左边距要 30px margin 手写媒体查询 判断条件 768 - 992px  要and
    3. xs 每个li占25% 手写媒体查询 判断 max-width:768px
7. 右侧调整Li的行高 60px

## 合作伙伴 

1. 版心容器 
2. ul转行内块居中

## 定制Bootstrap

1. 进官网 右侧有一个定制
2. 找到需要定制的组件和样式 修改 例如栅格系统 修改成15列
3. 改完之后下载 
4. 也可以修改源码


## em 和 rem

1. em ： element 元素 指的是当前元素的字体大小 1em= 1倍当前字体大小
2. rem : root element 根元素 指的是根元素的字体大小  1rem = 1倍根元素的字体大小
3. rem相对于em更灵活


## rem适配

1. 份数的方式 640屏幕分成 20份 每份占32px 640屏幕的html字体大小32px
2. 量页面元素宽高的时候 比如24  24/32rem  求得24px占20份里面的多少份

## rem 工具的使用

1. 按照设计稿量多少写多少
2. 设置工具的设计稿宽度 和基础字体值(也就是html 字体大小)
3. 勾上媒体查询 自动生成媒体查询
4. 点击px 转 rem 生成 转好的rem单位


## 字体图标生成过程  https://icomoon.io/

1. 进入 https://icomoon.io/ 网站
2. 点击右上角 icomoonApp
3. 点击左上角 import icons
4. 选中所有导入的图标
5. 点击右下角 generate font
6. 点击左上角 preferences 设置字体名称 和 类名前缀
7. 点击download
8. 解压生成好的压缩包 里面有demo.html
9. 打开demo.html能够查看图标对应类名
10. 使用 的时候 把 fonts文件夹放到项目 并且引入style.css（这里面就定义了那些图标的类名）

## 翻墙和插件


1. 拿到之后解压greenvpn 解压的目录不能有中文
2. 打开greenvpn.exe 点击免注册使用
3. 点击右上角免费领取
4. 任意选路双击链接
5. 蓝灯 直接双击 蓝灯的exe就可以

## 装google插件 

1. Anything to QRcode 二维码插件
2. Bootstrap resize tool bootstrap响应式工具
3. WEB前端助手(FeHelper) 前端工具 格式化代码 压缩 混淆等等
4. 广告终结者 去除视频广告的插件
5. 有道词典Chrome划词插件 翻译和划词翻译