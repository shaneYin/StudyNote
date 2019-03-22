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

4. figure标签

  figure标签是对重要内容添加的说明，说明性文字用 figcaption标签包裹

  ```
    <figure>
      <img />
      <figcaption>对图片、音频、方程等内容的说明性文字</figcaption>
    </figure>
  ```

5. img图片和CSS中的background背景图使用区别：

    使用CSS中的background属性设置图片是为了装饰网页，提升视觉效果。

    而使用img元素插入图片是为了让内容有意义，图片也是内容的一部分。

6. video标签

    * src属性：资源地址
    * controls属性： 对视频的控制，暂停快进等
    * 标签内可以有段落文字存在，是在浏览器不支持video标签时显示的。
    * 不同的浏览器会兼容不同的视频格式，比如 FireFox 和 Chrome支持WebM格式，Internet Explorer 和 Safari 支持MP4

      同时针对此，video标签中可以嵌套source标签，来供可支持浏览器的选择。

      ```
        <video controls>
          <source src="rabbit320.mp4" type="video/mp4">
          <source src="rabbit320.webm" type="video/webm">
          <p>你的浏览器不支持 HTML5 视频。可点击<a href="rabbit320.mp4">此链接</a>观看</p>
        </video>
      ```

7. track标签可以给视频添加字幕，字幕文件为.vtt结尾的文件

    ```
    <video controls>
      <source src="example.mp4" type="video/mp4">
      <source src="example.webm" type="video/webm">
      <track kind="subtitles" src="subtitles_en.vtt" srclang="en">
    </video>
    ```

8. 
