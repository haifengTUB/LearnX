## Markdown 资源汇总

### Markdown 相关教程和资料
- [Markdown 官网](https://daringfireball.net/projects/markdown/basics)
- [Markdown - 引领未来科技写作的博客利器](http://ux.etao.com/posts/620)
- [Markdown 语法说明 快速入门](http://wowubuntu.com/markdown/basic.html)
- [Markdown 语法说明](http://wowubuntu.com/markdown/index.html)
- [怎样使用Markdown](http://www.ituring.com.cn/article/23)
- [使用Ghost写文章](http://docs.ghost.org/zh/usage/writing/)
- [献给写作者的 Markdown 新手指南](http://jianshu.io/p/q81RER)
- [Markdown指南](http://zipperary.com/2013/05/22/introductio-to-markdown/)
- [如何在Linux下使用Markdown进行文档工作](http://www.ituring.com.cn/article/10044)
- [Markdown,重拾码字乐趣](http://jianshu.io/p/5d8529c97b29)
- [马克飞象](http://maxiang.info)
- TBD

### Markdown 编辑器
- Windows: [MarkdownPad](http://markdownpad.com/)
- Linux: [ReText](http://sourceforge.net/p/retext/home/ReText/)
- Mac: [Mou](http://mouapp.com/)
- Chrome: [MaDe](https://chrome.google.com/webstore/detail/oknendfeeopgpibecfjljjfanledpbkog?hl=en)
- Online:
 + [Dillinger](http://dillinger.io/)
 + [Dillinger Github](https://github.com/joemccann/dillinger/)
 + [StackEdit](https://stackedit.io/)
 + [Markable](http://markable.in/)
 + [markdowntutorial](http://www.markdowntutorial.com/)

### Win7 下破解 MarkdownPad 2
**以下破解步骤参考[破解 Windows 下Markdown 编辑器 MarkdownPad 2][1]**

我的破解过程记录如下：

1. 安装如下软件
 - [最新MarkdownPad 2](http://markdownpad.com/download/markdownpad2-setup.exe), 安装完后使用其高级功能，"File"->"Export"->"Export PDF"提示要升级到专业版才能使用.
 - .Net 反编译器 ILSpy
[ILSpy官网](http://ilspy.net/)
[ILSpy下载](http://sourceforge.net/projects/sharpdevelop/files/ILSpy/2.0/ILSpy_Master_2.1.0.1603_RTW_Binaries.zip/download)
 - 反汇编工具IDA
[IDA官网](https://hex-rays.com/products/ida/index.shtml)
[IDA试用版本](https://www.hex-rays.com/products/ida/support/download_demo.shtml)
[IDA试用版本Windows](http://out7.hex-rays.com/files/idademo65_windows.exe)
 - 十六进制编辑器 [HxD](http://mh-nexus.de/en/hxd/) 但我用的是Notepad++
2. 使用 ILSpy 反编译 MarkdownPad 出源文件，找到其验证授权的函数
使用 ILSpy 打开 MarkdownPad2 安装目录下的 MarkdownPad2.exe 文件，在 MarkdowPad2.Licensing 命名空间下找到 LicenseEngine 类的 VerifyLicense 方法,这个函数是用来验证你所填写的邮箱 email 和 许可证 licenseKey 是否合法，函数首先判断 email 和 licenseKey 是否为空，若有一个为空则直接返回 false，即验证不通过； 若均不为空，那么下面进行其它逻辑的验证。我们并不关心它是如何验证用户所填的 email 和 licenseKey 是否能匹配上，我们只需要将第一步判断若 email 或 licenseKey 为空返回 false 改为 返回 true，那么，就直接通过验证了。下面就是要使用 IDA 工具找到该代码片段的二进制代码的位置。
3. 使用 IDA 反汇编 Markdown，找到验证授权函数的汇编代码,使用 IDA 打开 MarkdownPad2 安装目录下的 MarkdownPad2.exe 文件，左侧点击 Function name，按 ALT+T 键搜索VerifyLicense 函数名，没有查到，左侧函数列表中也只有一个函数start，
正如[第七条留言](http://www.cnblogs.com/hazir/p/unlocking_markdownpad2.html#2873744)所反映的情况一样。我最后是通过搜索十六进制串"00 0a 2c 02"共匹配到四处，第一处位于0x00002e70，
和[第十三条留言](http://www.cnblogs.com/hazir/p/unlocking_markdownpad2.html#2888088)所反映的位置基本一致。我把位于0x00002e80处的0x16改成0x17后就能正常使用Export PDF功能了。另外三处的暂时没有修改，等遇到功能限制时再试。

4. 扩展阅读:IDA专栏文章
 - [IDA反汇编/反编译静态分析iOS模拟器程序](http://blog.csdn.net/column/details/ios-ida.html)
 - [《IDA Pro权威指南》读书笔记](http://blog.csdn.net/hursing/article/details/8754296)
 - [（一）话说IDA](http://blog.csdn.net/hursing/article/details/8920487)
 - [（二）加载文件与保存数据库](http://blog.csdn.net/hursing/article/details/8923748)
 - [（三）函数表示与搜索函数](http://blog.csdn.net/hursing/article/details/8926315)
 - [（四）反汇编的符号信息与改名](http://blog.csdn.net/hursing/article/details/8929401)
 - [（五）F5反编译](http://blog.csdn.net/hursing/article/details/8935697)
 - [（六）交叉引用](http://blog.csdn.net/hursing/article/details/8939392)
 - [（七）识别类的信息](http://blog.csdn.net/hursing/article/details/8997776)
 - [（八）IDA for Mac](http://blog.csdn.net/hursing/article/details/9019651)
 - [（九）block](http://blog.csdn.net/hursing/article/details/9021941)

[1]:http://www.cnblogs.com/hazir/p/unlocking_markdownpad2.html
