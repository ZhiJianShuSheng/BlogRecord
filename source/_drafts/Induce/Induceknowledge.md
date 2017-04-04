知识归纳



### 背景图片的使用：
通常情况下，我们会只用背景图片，但是由于不同设备的屏幕尺寸不同，为了实现全屏显示，这时候我们会让背景图片全屏填充。

解决方案：
由于移动端、PC端的不同，通常情况下两者一个有选择90度的效果。
通常




### 前端优化：

```
网站重构：在不改变外部行为的前提下，简化结构、添加可读性，而在网站前端保持一致的行为。
也就是说是在不改变UI的情况下，对网站进行优化，在扩展的同时保持一致的UI。

对于传统的网站来说重构通常是：

表格(table)布局改为DIV+CSS
使网站前端兼容于现代浏览器(针对于不合规范的CSS、如对IE6有效的)
对于移动平台的优化
针对于SEO进行优化
深层次的网站重构应该考虑的方面

减少代码间的耦合
让代码保持弹性
严格按规范编写代码
设计可扩展的API
代替旧有的框架、语言(如VB)
增强用户体验
通常来说对于速度的优化也包含在重构中

压缩JS、CSS、image等前端资源(通常是由服务器来解决)
程序的性能优化(如数据读写)
采用CDN来加速资源加载
对于JS DOM的优化
HTTP服务器的文件缓存

```
### 你有用过哪些前端性能优化的方法？

```
1. 减少http请求次数：
CSS Sprites, JS、CSS源码压缩、图片大小控制合适；网页Gzip，CDN托管，data缓存 ，图片服务器。
2. 前端模板 JS+数据，减少由于HTML标签导致的带宽浪费，前端用变量保存AJAX请求结果，每次操作本地变量，不用请求，减少请求次数
3. 用innerHTML代替DOM操作，减少DOM操作次数，优化javascript性能。
4. 当需要设置的样式很多时设置className而不是直接操作style。
5. 少用全局变量、缓存DOM节点查找的结果。减少IO读取操作。
6. 避免使用CSS Expression（css表达式)又称Dynamic properties(动态属性)。
7. 图片预加载，将样式表放在顶部，将脚本放在底部  加上时间戳。
8. 避免在页面的主体布局中使用table，table要等其中的内容完全下载之后才会显示出来，显示比div+css布局慢。
对普通的网站有一个统一的思路，就是尽量向前端优化、减少数据库操作、减少磁盘IO。向前端优化指的是，在不影响功能和体验的情况下，能在浏览器执行的不要在服务端执行，能在缓存服务器上直接返回的不要到应用服务器，程序能直接取得的结果不要到外部取得，本机内能取得的数据不要到远程取，内存能取到的不要到磁盘取，缓存中有的不要去数据库查询。减少数据库操作指减少更新次数、缓存结果减少查询次数、将数据库执行的操作尽可能的让你的程序完成（例如join查询），减少磁盘IO指尽量不使用文件系统作为缓存、减少读写文件次数等。程序优化永远要优化慢的部分，换语言是无法“优化”的。
```

### 对算法,数据结构有一定了解

```
算法:

图搜索 （广度优先、深度优先）,深度优先特别重要
排序
动态规划
匹配算法和网络流算法
正则表达式和字符串匹配

额外推荐:

贪婪算法
概率方法
近似算法

数据结构:

图 （树尤其重要）
Map
堆
栈/队列
Tries | 字典树
 

上面是 Arjun Nayini 的推荐，下面是 Ken George 的推荐

注：下面这个没有特定优先级

算法:

三路划分-快速排序
合并排序（更具扩展性，复杂度类似快速排序）
DF/BF 搜索 （要知道使用场景）
Prim  / Kruskal （最小生成树）
Dijkstra （最短路径算法）
选择算法

数据结构:

HashMap （真的要知道所有哈希结构）
图和树（红黑树很好学） (red-black trees are good to learn)
堆（优先级队列）
栈/队列（必须知道的基础内容）
Tries | 字典树

A *和遗传算法也很有趣。
```