[TOC]
#Mobile web app重构说明文档
—— 2014/11/14 update

适用于：

- Andorid客户端 v4.x 所有页面
- iOS客户端v3.11-v4.x详情页、嗅探页、活动列表页
- Andorid&iOS客户端功能不完全一致，以Andorid项目为优先参考

##项目架构
- `mod_*.html` 公用模块示例，`detail_*.html` 详情页，`search_*.html` 搜索页，`user_*.html` 个人中心
- `mixin.scss`通用变量及功能函数，`reset.scss` reset样式，`btn.scss` 按钮样式
- `common.scss` 基础类名，项目通用模块（文本、图标、提示、布局）

##分辨率适配
- 采用rem为布局单位；
- 安卓以720x1280设计稿为准切图，基础font-size:30px，以等比缩放作适配; 
- iOS以640x960设计稿为准切图，基础font-size:20px，iPhone等比缩放适配，iPad以内容展现适配；
- iPhone6+分辨率适配细节需与设计沟通验证完善 ——2014.11
- 跨平台页面未做响应式设计统一采取等比缩放适配方案，对低设备比例高分辨率调低基础字号。

###渲染声明
- 安卓对支持 `target-densitydpi=device-dpi` 声明的设备采取实际分辨率渲染，分辨率适配精度高；
- 外链页面请勿使用 `target-densitydpi=device-dpi` 会导致浏览器以实际比例渲染未做适配的页面；
- iPad客户端webview宽度有540/500两种，需加入viewport声明，eg.`width=540`

##布局说明
###mixin.scss
- 包括：通用颜色、间距定义，常用mixin函数
- sprite使用`目录名`+`sprites`，单独调用时以图片名赋值，eg.`@include sprite($ico-sprites,ico_search)`
- sprite-position可单独定义，eg.`@include sprite-position($ico-sprites,ico_search)`

### 多状态类名
- 点击态，添加类名  `.hover` 
- 不可点击态，添加类名  `.disabled`
- 已操作态，添加类名 `classname` +`_done` 
- tab切换选中，添加类名  `.on` 

### 单类名，可单独调用
- `.textline` 单行文本截断
- `.text2line` 两行文本截断
- `.text3line` 三行文本截断

###ico
- 纯色ico使用font-face制作，[demo](mod_ico.html)
- 其余ico使用图片，目录images/ico
- `ico_play.png`为(种子解析页面)(seed.html)使用，不限于手雷客户端内嵌，先做成图片 v4.4

###Button [demo](mod_ico.html)
- `.obtn` 通用操作按钮(蓝色边框-v4.0)
- `.fbtn` 通用操作按钮(蓝色背景-v4.4)
- `.bbtn` 搜索页操作按钮(灰色渐变背景-v3.x+)
- `.btn_play` 透明悬浮播放按钮
- `classname` +`classname_full` 操作按钮【通栏样式】 eg.`.obtn.obtn_full`  [demo](report.html)

### tips提示区域
- 通用类名`.tip_none`
- 扩展类名：[无评论](detail_fun_joke.html)`tip_nocomment`，[搜索无结果](search_no_result.html) `tip_noresult`

### loading
- 通用结构：`.loadmore > .loading + text`
- `.pageload`控制在页面内居中布局
- `.loadding_type2`为浅色杂边透明底，用于]嗅探页](sniffer.html)。

###导航
- `.nav` 搜索导航
- `.tab_nav` 内容切换导航
- `.episode_nav` 分集导航（横向滑动）

###列表
- `.filter_list` 过滤列表：
	- 下载页 【格式选择】 [demo](detail_movie_list_down.html#layer_filter_box)
	- 举报页 【原因选择】 [demo](report.html)
- 文本链接列表：
	- `.episode_list` 剧集【综艺】
	- +`.episode_gird_list` 剧集【数字】（布局似网格）
- 文本列表：
	- 	`.prev_list` 文字、行内图片【字段】


### 海报模块
- `.prev_picbox` 默认竖版图片【详情、相关推荐】
- +`.prev_picbox_land` 横版图片版式
- 相关推荐的扩展类名 `.recom_item`



###详情页底部通栏
- `.detail_footer` 外框，基础类名
- `.detail_footer_comment` 底部评论栏
- `.detail_footer_button` 纯操作按钮（安卓v4.0无此样式）

### 整体布局
- 详情页`body`统一添加 `.detail_page` 
- 搜索页`body`统一添加 `.search_page` 
- 个人中心`body`统一添加 `.user_page` 
- 嗅探页`body`统一添加 `.sniffer_page` 
- 非固定区域滚动的详情页在`body`或第一个子div上添加`.detail_page_nofixed`


----------

**Author:** *Wanfor*   
**E-Mail:** *wanfor.h@gmail.com*