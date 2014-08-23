## sed 资源汇总

### sed 相关教程和资料
- [GNU官网: sed, a stream editor](http://www.gnu.org/software/sed/manual/sed.html)
- [酷壳: sed 简明教程](http://coolshell.cn/articles/9104.html)
- [Linux下sed简易教程](http://www.chinabin.cn/language/shell/2150.html)  
简单示例:
  1. 删除空行，^匹配开头，$匹配结尾  
    `sed -e '/^$/d' file.name`
  2. 替换每一行的第一个出现的abc为def  
  	`sed -e 's/abc/def/' file.name`
  3. 替换所有的abc为def  
  	`sed -e 's/abc/def/' file.name`
  4. shell脚本中的用法，注意是双引号而不是单引号  
  	`sed -e 's/abc/def/' file.name`
  5. 删除当前目录中文件名中包含特殊字符的文件，如 +,{,;,\等  
  	<pre><code>
	for filename in *
	do 
	  badname=!echo "$filename" | sed -n /[\+\{\;\"\\\=\?\~\(\)\<\>\&\*\|\$\]/p!
	done
	</code></pre>
  	当然，也可以使用find语句，如下：  
	`find . -name '*[+{;"\\=?~()<>&*|$ ]*' -exec rm -f '{}' \;`
- [SED单行脚本快速参考](http://sed.sourceforge.net/sed1line_zh-CN.html) | [英文](http://sed.sourceforge.net/sed1line.txt)
- [Unix sed实用教程系列](http://www.cnblogs.com/lazycoding/p/3248289.html)
  1. [Unixsed实用教程开篇](http://leaver.me/archives/3162.html)
  2. [[译]Unixsed实用教程第一篇-向文件中增加一行](http://leaver.me/archives/3169.html)
  3. [[译]Unixsed实用教程第二篇-替换文件内容](http://leaver.me/archives/3174.html)
  4. [[译]Unixsed实用教程第三篇-读写文件](http://leaver.me/archives/3176.html)
  5. [[译]Unixsed实用教程第四篇-选择性打印](http://leaver.me/archives/3179.html)
  6. [[译]Unixsed实用教程第五篇-替换文件内容续](http://leaver.me/archives/3183.html)
  7. [[译]Unixsed实用教程第六篇-删除文件内容](http://leaver.me/archives/3186.html)
  8. [[译]Unixsed实用教程第七篇-输出文件内容(10Demo)](http://leaver.me/archives/3191.html)
  9. [[译]Unixsed实用教程第八篇-CSV文件操作](http://leaver.me/archives/3194.html)
- [sed简明入门教程](http://www.ourunix.org/post/375.html)
- TBD

### sed 书籍
- [sed与awk](http://book.douban.com/subject/1236944/)
- TBD