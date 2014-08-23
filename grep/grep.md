## grep 资源汇总

### grep 相关教程和资料
- [GNU官网: GNU Grep 2.18](http://www.gnu.org/savannah-checkouts/gnu/grep/manual/grep.html)
- [Grep学习笔记](http://man.chinaunix.net/newsoft/grep/open.htm)
- [linux下grep命令用法实例教程](http://blog.51yip.com/linux/1008.html)  
  测试文件test是个密码文件,内容如下：  
  <pre><code>
  `[root@krlcgcms01 test]# cat test`
  root:x:0:0:root:/root:/bin/bash  
  bin:x:1:1:bin:/bin:/bin/false,aaa,bbbb,cccc,aaaaaa  
  DADddd:x:2:2:daemon:/sbin:/bin/false  
  mail:x:8:12:mail:/var/spool/mail:/bin/false  
  ftp:x:14:11:ftp:/home/ftp:/bin/false  
  &amp;nobody:$:99:99:nobody:/:/bin/false  
  zhangy:x:1000:100:,,,:/home/zhangy:/bin/bash  
  http:x:33:33::/srv/http:/bin/false  
  dbus:x:81:81:System message bus:/:/bin/false  
  hal:x:82:82:HAL daemon:/:/bin/false  
  mysql:x:89:89::/var/lib/mysql:/bin/false  
  aaa:x:1001:1001::/home/aaa:/bin/bash  
  ba:x:1002:1002::/home/zhangy:/bin/bash  
  test:x:1003:1003::/home/test:/bin/bash  
  @zhangying:*:1004:1004::/home/test:/bin/bash  
  policykit:x:102:1005:Po  
  1. 匹配含有root的行  
  `[root@krlcgcms01 test]# grep root test`
  2. 匹配以root开头或者以zhang开头的行，注意反斜杠  
  `[root@krlcgcms01 test]# cat test |grep '^\(root\|zhang\)'`
  3. 匹配以zhang开头，只含有字母  
  `[root@krlcgcms01 test]# echo 'zhangying' |grep '^zhang[a-z]*$'`
  4. 不匹配以bin开头的行,并显示行号  
  `[root@krlcgcms01 test]# cat test|grep -nv bin`
  5. 显示匹配的个数，不显示内容  
  `[root@krlcgcms01 test]#  cat test|grep -c zhang`
  </code></pre>  
- TBD

### grep 书籍
