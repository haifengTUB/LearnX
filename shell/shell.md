## Linux shell 资源汇总

### Shell 入门
- [Learn UNIX in 10 minutes](http://freeengineer.org/learnUNIXin10minutes.html) **推荐**
- [Learn X in Y minutes Where X=bash](http://learnxinyminutes.com/docs/bash/) | [中文版](http://learnxinyminutes.com/docs/zh-cn/bash-cn/)
- [Shell脚本编程30分钟入门](https://github.com/qinjx/30min_guides/blob/master/shell.md)
- [Linux Shell脚本教程：30分钟玩转Shell脚本编程](http://see.xidian.edu.cn/cpp/shell/)
- [Bash脚本15分钟进阶教程](http://www.vaikan.com/bash-scripting/) | [英文: Better Bash Scripting in 15 Minutes](http://robertmuth.blogspot.com/2012/08/better-bash-scripting-in-15-minutes.html)
- [Linux Shell编程入门](http://www.cnblogs.com/suyang/archive/2008/05/18/1201990.html)
- [Shell编程基础](http://wiki.ubuntu.org.cn/Shell%E7%BC%96%E7%A8%8B%E5%9F%BA%E7%A1%80)
- TBD

### Shell 书籍
- [Bash Guide for Beginners](http://tldp.org/LDP/Bash-Beginners-Guide/html/index.html) | [英文版PDF下载](http://tldp.org/LDP/Bash-Beginners-Guide/Bash-Beginners-Guide.pdf)
- [Advanced Bash-Scripting Guide](http://tldp.org/LDP/abs/html/) | [英文版PDF下载](http://tldp.org/LDP/abs/abs-guide.pdf) | [中文版 : 高级Bash脚本编程指南](http://book.douban.com/subject/3010746/) 
- [Shell脚本学习指南](http://book.douban.com/subject/3519360/)
- [Linux Shell脚本攻略](http://book.douban.com/subject/6889456/)
- TBD

### Shell 相关教程和资料
- [入门bash Shell脚本](http://wtlucky.github.io/geekerprobe/blog/2013/05/02/start-write-shell/)
- [Shell 字符串处理汇总（查找，替换等等）](http://blog.chinaunix.net/uid-124706-id-3475936.html)
- [Bash Shell字符串操作小结](http://my.oschina.net/aiguozhe/blog/41557)
<pre><code class="bash">
str="abcdef"
expr substr "$str" 1 3  # 从第一个位置开始取3个字符， abc
expr substr "$str" 2 5  # 从第二个位置开始取5个字符， bcdef 
expr substr "$str" 4 5  # 从第四个位置开始取5个字符， def

echo ${str:2}           # 从第二个位置开始提取字符串， bcdef
echo ${str:2:3}         # 从第二个位置开始提取3个字符, bcd
echo ${str:(-2)}        # 从倒数第二个位置向左提取字符串, abcde
echo ${str:(-2):3}      # 从倒数第二个位置向左提取3个字符, cde

str="abbc,def,ghi,abcjkl"
echo ${str#a*c}         # ,def,ghi,abcjkl  一个井号(#) 表示从左边截取掉最短的匹配 (这里把abbc字串去掉）
echo ${str##a*c}        # jkl，             两个井号(##) 表示从左边截取掉最长的匹配 (这里把abbc,def,ghi,abc字串去掉)
echo ${str#"a*c"}       # 空,因为str中没有子串"a*c"
echo $[str##"a*c"}      # 空,同理
echo ${str#d*f)         # abbc,def,ghi,abcjkl, 
echo ${str#*d*f}        # ,ghi,abcjkl   

echo ${str%a*l}         # abbc,def,ghi  一个百分号(%)表示从右边截取最短的匹配 
echo ${str%%b*l}        # a             两个百分号表示(%%)表示从右边截取最长的匹配
echo ${str%a*c}         # abbc,def,ghi,abcjkl  
</code></pre>
- [Linux shell脚本编写基础](http://blog.csdn.net/fpmystar/article/details/4183678)
- [Shell 教程（上）](https://github.com/widuu/linux_course/blob/master/shell.md)  
- [shell-learn](https://github.com/singlepig/shell-learn)
- [shell基础十二篇](http://bbs.chinaunix.net/thread-452942-1-1.html)
- TBD