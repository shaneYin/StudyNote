### HTML

1. 标签语义化

  * html,body,head,title 基本标签
  * p 段落
  * h1,h2,h3等  标题。 h1只能出现一次
  * ul ol li  有序和无序列表
  * em strong 强调和重点强调

  *<b> <i> <u>* 这些标签并没有语义化，是表象元素。

2. 高级文字排版

  * <blockquote cite="https://xxx.com"></blockquote> 标签用于引用原文，cite属性代表引用地址，是块元素。

  <q cite="https://xxx.com"></q> 标签用于引用原文，cite属性代表引用地址，是行内元素。

  <cite></cite> 标签用来放在引用旁边，常常是人或者书或者来源的名字。

  * <abbr title=""></abbr>  代表缩略词 title属性值是它的全称。 NASA 我伙呆 等。
  * <address></address> 是用来标记编写HTML文档的人的联系方式
  * <sup>是上标 <sub>是下标
  * <time datetime=""></time>用来表示时间， datetime属性是时间的格式化模板

3. 给HTML添加正确的区段标记表示（语义化结构）

  * header 标题栏。 如果是body子元素就是网站全局页眉，如果是字内容的子元素，就是字内容的页眉。
  * nav 导航栏。 页面主导航，不应包含二级链接。
  * main 主内容。 文档中最好只出现一次，并且不要嵌套进除body外的其他元素
  * aside 侧边栏，嵌套在main中。
  * footer 页脚
  * section 和 article 是main中的字内容。一般是section中包含几个 article。
