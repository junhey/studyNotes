#PHP面试刷题

- 表单提交get和post有何区别？

答：get的方式是把数据在地址栏中发送，get传送的数据量较小，不能大于2KB。post传送的数据量较大，一般被默认为不受限制。但理论上，IIS4中最大量为80KB，IIS5中为100KB。

- 用PHP打印出前一天的时间格式是2006-5-10 22:21:21

echo date("Y-m-d H:i:s",time()-(3600*24));或echo date("Y-m-d H:i:s",strtotime("-1 day"));

- php中include和require的区别？

这两种结构除了在如何处理失败之外完全一样。include() 产生一个警告而 require() 则导致一个致命错误。换句话说，如果你想在遇到丢失文件时停止处理页面就用 require()。include() 就不是这样，脚本会继续运行。

- echo(),print(),print_r()的区别

echo可以接多个参数,print只能接一个参数,它们都是PHP的语言结构,print_r是递规打印,用来打印数组或对象

- 能够使HTML和PHP分离开使用的模板

smarty,phplib,SmartTemplate

- 你如何理解MVC模式？

首先说一下框架，框架:就是别人把一些底层,常用操作.比如数据操作(增,删,改,查)写好.你来直接用.其它的功能要自己来做。MVC:设计模式,M模型,V显示,C控制.现在许多框架都是基于MVC来做的把逻辑和显示分开.比如你要换页面,只需要改V里面的东西并不需要再去变动程序!（详细的东西可以 上网上查一下）

- 如何实现PHP、JSP交互？

PHP提供了支持JAVA的类库文件,或者通过HTTP协议来交互数据

- 使用哪些工具进行版本控制？

Git，SVN

- 如何实现字符串翻转？

不考虑中英文混合,不是最优算法,不用php库函数翻转字符串:
```
function   str_to_reverse($str){  
    for($length=0;$str[$length]!=null;$length++){;}  
  	$strlength=$length-1;  
  	unset($length);
	for($start=0,$end=$strlength;$start<$end;$start++,$end--){  
	  	$temp = $str[$start];  
	  	$str[$start] = $str[$end];  
	  	$str[$end] = $temp;  
	}  
  	unset($temp,$start,$end,$strlength);  
  	return $str;  
}
```
如果PHP库函数的话这样
```
$str=strrev("Junhey");
echo $str;
```



- 优化MYSQL数据库的方法。

1） 将where中用的比较频繁的字段建立索引,联合索引。
2） 保证单表数据不超过200W，适时分割表。
3） 避免使用长连接。
4） 修改my.cnf里面的各项参数，比如最大连接数，查询缓存等。根据你的服务器内存来最大化调节那些配置参数。
5） 针对需求，使用正确的表引擎，是myisam或是innodb。

- 用PHP写出显示客户端IP与服务器IP的代码

echo $_SERVER['REMOTE_ADDR'] //客户端ip
echo $_SERVER['SERVER_ADDR'] //服务器端ip

- apache+mysql+php实现最大负载的方法

1）问的太笼统,生成静态html页面,squid反向代理,apache,mysql的负载均衡。
2）可以采取数据缓存的方法，我们通常在统计数据的时候，需要在原始数据的基础上经过计算等一系列操作，才会得到最终的结果，如果每做一个查询都需要这样一系 列操作，当数据量大时，势必会带来很多问题。可以建立一个结果表，写一个脚本，用crontab定时触发脚本去原始表取数据，计算，写入到结果表，前端查 询从结果表取数据，这也是比较常用的一种做法。
3）采用分布式，多个apache，多个mysql，其实就是dns负载均衡，dns根据当前用户解析几个ip的ping值，将用户转移到某一台最快的服务器，或者平均分配。
4）money不是问题的话,可以考虑F5硬件负载均衡!
5）可以使用Microsoft Windows Server系统的负载均衡设置

- 优化MYSQL数据库的方法

(1)选取最适用的字段属性,尽可能减少定义字段长度,尽量把字段设置NOT NULL,例如’省份,性别’,最好设置为ENUM
(2)使用连接（JOIN）来代替子查询:
(3)使用联合(UNION)来代替手动创建的临时表
(4)事务处理:保证数据完整性,例如添加和修改同时,两者成立则都执行,一者失败都失败
	mysql_query(”BEGIN”);
	mysql_query(”INSERT INTO customerinfo (name) VALUES (’$name1′)”;
	mysql_query(”SELECT * FROM `orderinfo` where customerid=”.$id”);
	mysql_query(”COMMIT”);
(5)锁定表,优化事务处理:我们用一个 SELECT 语句取出初始数据，通过一些计算，用 UPDATE 语句将新值更新到表中。包含有 WRITE 关键字的 LOCK TABLE 语句可以保证在 UNLOCK TABLES 命令被执行之前，不会有其它的访问来对 inventory 进行插入、更新或者删除的操作
	mysql_query(”LOCK TABLE customerinfo READ, orderinfo WRITE”);
	mysql_query(”SELECT customerid FROM `customerinfo` where id=”.$id);
	mysql_query(”UPDATE `orderinfo` SET ordertitle=’$title’ where customerid=”.$id);
	mysql_query(”UNLOCK TABLES”);
(6)使用外键,优化锁定表
(7)建立索引
(8)优化查询语句:最好在相同字段进行比较操作,在建立好的索引字段上尽量减少函数操作
	SELECT * FROM order WHERE YEAR(orderDate)<2008;(慢)
	SELECT * FROM order WHERE orderDate<"2008-01-01";(快)
	SELECT * FROM order WHERE addtime/7<24;(慢)
	SELECT * FROM order WHERE addtime<24*7;(快)
	SELECT * FROM order WHERE title like "%good%";
	SELECT * FROM order WHERE title>=”good” and name<"good";
	
- 实现中文字串截取无乱码的方法
```
$str = "我是一串比较长的中";
echo "mb_substr:" . mb_substr($str, 0, 6, "utf-8");
echo "mb_strcut:" . mb_strcut($str, 0, 6, "utf-8");
```
打印结果：
		mb_substr：我是一串比较
		mb_strcut：我是

mb_substr是按字来切分字符，而mb_strcut是按字节来切分字符，但是都不会产生半个字符的现象



- 在PHP中，当前脚本的名称（不包括路径和查询字符串）记录在预定义变量中；而链接到当前页面的URL记录在预定义变量中

```
echo $_SERVER["PHP_SELF"];
echo $_SERVER["HTTP_REFERER"];
```

- 如下代码

```
	$null = NULL;
	$bool = FALSE;
	$notSet;
	$array = array();
	
	//以下是问题
	$a = "hello";
	$b = &$a;
	unset($b);
	//答案为:hello
	echo $a;
	$b = "world";
	//答案为:hello
	echo $a;
	
	//以下是问题
	$a = 1;
	$x = &$a;
	$b = $a++;
	//答案为:1
	echo $b;
	
	//以下是问题
	$x = empty($array);
	//答案为:1
	echo $x;
	//答案为:true
	echo $x?"true":"false";
```
- 表单中 get与post提交方法的区别

get是发送请求HTTP协议通过url参数传递进行接收,而post是实体数据,可以通过表单提交大量信息

- session与cookie的区别

session:储存用户访问的全局唯一变量,存储在服务器上的php指定的目录中的（session_dir）的位置进行的存放
cookie:用来存储连续訪問一个頁面时所使用，是存储在客户端，对于Cookie来说是存储在用户WIN的Temp目录中的。
两者都可通过时间来设置时间长短

- 数据库中的事务是什么

事务（transaction）是作为一个单元的一组有序的数据库操作。如果组中的所有操作都成功，则认为事务成功，即使只有一个操作失败，事务也不成功。如果所有操作完成，事务则提交，其修改将作用于所有其他数据库进程。如果一个操作失败，则事务将回滚，该事务所有操作的影响都将取消

- MYSQL取得当前时间的函数是 

now()

- 格式化日期的函数是 

date()

- 语句include和require的区别是什么

require->require是无条件包含也就是如果一个流程里加入require,无论条件成立与否都会先执行require
include->include有返回值，而require没有(可能因为如此require的速度比include快)

- 如何修改SESSION的生存时间

将php.ini中的session.gc_maxlifetime设置为9999重启apache
或:
	$savePath = “./session_save_dir/”;
	$lifeTime = 小时 * 秒;
	session_save_path($savePath);
	session_set_cookie_params($lifeTime);
	session_start();
	
- 有一个网页地址，比如http://www.murray.cn/,如何得到它的内容

```
$readcontents = fopen(”http://www.murray.cn/”, “rb”);
$contents = stream_get_contents($readcontents);
fclose($readcontents);
echo $contents;
```
或
```
echo file_get_contents(”http://www.murray.cn/”);
```


- 在HTTP 1.0中，状态码401的含义是 未被授权

如果返回“找不到文件”的提示，则可用 header 函数，其语句为 header(”Location:www.murray.cn”);


- 请说明php中传值与传引用的区别。什么时候传值什么时候传引用?

按值传递：函数范围内对值的任何改变在函数外部都会被忽略
按引用传递：函数范围内对值的任何改变在函数外部也能反映出这些修改
优缺点：按值传递时，php必须复制值。特别是对于大型的字符串和对象来说，这将会是一个代价很大的操作。
按引用传递则不需要复制值，对于性能提高很有好处。

- 在PHP中error_reporting这个函数有什么作用

设置错误级别与错误信息回报

- 请写一个函数验证电子邮件的格式是否正确

$pregEmail = "/([a-z0-9]*[-_\.]?[a-z0-9]+)*@([a-z0-9]*[-_]?[a-z0-9]+)+[\.][a-z]{2,3}([\.][a-z]{2})?/i";
return preg_match($pregEmail,$email);

- 如何得到当前执行脚本路径，包括所得到参数

```
$script_name = basename(__file__);
print_r($script_name);
```

- JS表单弹出对话框函数是

alert(),prompt(),confirm();
获得输入焦点函数是focus();

- 如何声明一个名为”myclass”的没有方法和属性的类

class myclass{} 

如何实例化一个名为”myclass”的对象
new myclass()

如何访问和设置一个类的属性
$object = new myclass();
$newstr = $object->test;
$object->test = “info”;

- 可以打开一个文件，以对文件进行读和写操作: 

fopen()

- 以下的输出结果

```
$num = 10;
function multiply(){
	$num = $num * 10;
}
multiply();
echo $num;
//输出:10
```

- 写一个函数，尽可能高效的，从一个标准 url 里取出文件的扩展名
function getExt($url){
	$arr = parse_url($url);
	$file = basename($arr["path"]);
	$ext = explode(”.”,$file);
	return $ext[1];
}

- PHP5权限控制修饰符

public(公共),private(私用),protected(继承)

- session与cookie的区别?

答:session:储存用户访问的全局唯一变量,存储在服务器上的php指定的目录中的（session_dir）的位置进行的存放
   cookie:用来存储连续訪問一个頁面时所使用，是存储在客户端，对于Cookie来说是存储在用户WIN的Temp目录中的。 
   两者都可通过时间来设置时间长短
   
- 数据库中的事务是什么?

答:事务（transaction）是作为一个单元的一组有序的数据库操作。如果组中的所有操作都成功，则认为事务成功，即使只有一个操作失败，事务也不成功。如果所有操作完成，事务则提交，其修改将作用于所有其他数据库进程。如果一个操作失败，则事务将回滚，该事务所有操作的影响都将取消。

- 实现中文字串截取无乱码的方法。

答:
```
function GBsubstr($string, $start, $length) {
    if(strlen($string)>$length){
		$str=null;
		$len=$start+$length;
		for($i=$start;$i<$len;$i++){
			if(ord(substr($string,$i,1))>0xa0){
				$str.=substr($string,$i,2);
				$i++;
			}else{
				$str.=substr($string,$i,1);
			}
		}
		return $str.'...';
	}else{
		return $string;
   }
}
```
- 对于大流量的网站,您采用什么样的方法来解决访问量问题?

答:确认服务器硬件是否足够支持当前的流量,数据库读写分离,优化数据表,
   程序功能规则,禁止外部的盗链,控制大文件的下载,使用不同主机分流主要流量

- 请写一个函数验证电子邮件的格式是否正确 (2分)

答:
```
function checkEmail($email){
	$pregEmail = "/([a-z0-9]*[-_\.]?[a-z0-9]+)*@([a-z0-9]*[-_]?[a-z0-9]+)+[\.][a-z]{2,3}([\.][a-z]{2})?/i";
	return preg_match($pregEmail,$email);  
}
```

- 你如何访问和设置一个类的属性? 

```
答:$object = new myclass();
   $newstr = $object->test;
   $object->test = "info";
```


- 变量的作用范围问题！

```
<?PHP
  $num = 10;//这个是全局变量
  function multiply(){
     $num=$num*10;//这个是局部变量
  }
  multiply();//你调用这个函数对于全局变量的$num变量没有任何影响！
  echo $num;//这个是全局变量,输出的结果是10
?> 

<?PHP
  $num = 10;
  function multiply(&$num){//引用方式调用全局变量
     $num=$num*10;
  }
  multiply($num);
  echo $num;//这样就可以是100了！
?> 

<?PHP
//需要改变外部变量的值,需要在参数上加&,表示引用.这样
function multiply(&$var){
	$var = $var * 10;
}
	multiply($num);
	echo $num;//这样就可以是100了！
?> 
```

- 使用php写一段简单查询，查出所有姓名为“张三”的内容并打印出来
　　
表名User
　　Name Tel           Content Date
　　张三 13333663366  大专毕业 2006-10-11
　　张三 13612312331  本科毕业 2006-10-15
　　张四 021-55665566 中专毕业 2006-10-15

　　请根据上面的题目完成代码：
　　$mysql_db=mysql_connect("local","root","pass");
　　@mysql_select_db("DB",$mysql_db);
    $result = mysql_query("SELECT * FROM `user` WHERE name='张三'");
    while($rs = mysql_fetch_array($result)){
		echo $rs["tel"].$rs["content"].$rs["date"];
    } 
	
	(a) 有一新记录(小王 13254748547 高中毕业 2007-05-06)请用SQL语句新增至表中
    mysql_query("INSERT INTO `user` (name,tel,content,date) VALUES 
    ('小王','13254748547','高中毕业','2007-05-06')")

　　(b) 请用sql语句把张三的时间更新成为当前系统时间
    $nowDate = date("Y-m-d");
    mysql_query("UPDATE `user` SET date='".$nowDate."' WHERE name='张山'");

　　(c) 请写出删除名为张四的全部记录
    mysql_query("DELETE FROM `user` WHERE name='张四'");

- 请写出数据类型(int char varchar datetime text)的意思; 请问varchar和char有什么区别

答:int是数字类型,char固定长度字符串,varchar实际长度字符串,datetime日期时间型,text文本字符串
   char的场地固定为创建表设置的长度,varchar为可变长度的字符
   
- 检测一个变量是否有设置的函数是否?是否为空的函数是?

答:isset($str),empty($str);


取得查询结果集总数的函数是?(1分)
答:mysql_num_rows($result);

- $arr = array('james', 'tom', 'symfony'); 请打印出第一个元素的值

答:echo $array[0];

- 请将41题的数组的值用','号分隔并合并成字串输出

答:for($i=0;$i<count($array);$i++){ echo $array[$i].",";}

- $a = 'abcdef'; 请取出$a的值并打印出第一个字母

答:echo $a{0} 或 echo substr($a,0,1)

- PHP可以和sql server/oracle等数据库连接吗?

答:当然可以

- 请写出PHP5权限控制修饰符

答:public(公共),private(私用),protected(继承)

- 请写出php5的构造函数和析构函数

答:__construct , __destruct

- 完成以下:

(一)创建新闻发布系统，表名为message有如下字段
　　id 文章id
　　title 文章标题
　　content 文章内容
　　category_id 文章分类id
    hits 点击量
	
答:CREATE TABLE 'message'(
   'id' int(10) NOT NULL auto_increment,
   'title' varchar(200) default NULL,
   'content' text,
   'category_id' int(10) NOT NULL,
   'hits' int(20),
   PRIMARY KEY('id');
   )ENGINE=InnoDB DEFAULT CHARSET=utf8;

(二)同样上述新闻发布系统：表comment记录用户回复内容，字段如下

　　comment_id 回复id
　　id 文章id，关联message表中的id
　　comment_content 回复内容
　　现通过查询数据库需要得到以下格式的文章标题列表,并按照回复数量排序，回复最高的排在最前面
　　文章id 文章标题 点击量 回复数量
　　用一个SQL语句完成上述查询，如果文章没有回复则回复数量显示为0

答:SELECT message.id id,message.title title,IF(message.`hits` IS NULL,0,message.`hits`) hits,
   IF(comment.`id` is NULL,0,count(*)) number FROM message LEFT JOIN 
   comment ON message.id=comment.id GROUP BY message.`id`;

(三)上述内容管理系统，表category保存分类信息，字段如下

　　category_id int(4) not null auto_increment;
　　categroy_name varchar(40) not null;
　　用户输入文章时，通过选择下拉菜单选定文章分类
　　写出如何实现这个下拉菜单

答:
```
function categoryList()
{
    $result=mysql_query("select category_id,categroy_name from category")
            or die("Invalid query: " . mysql_error());
    print("<select name='category' value=''>\n");
    while($rowArray=mysql_fetch_array($result))
    {
       print("<option value='".$rowArray['category_id']."'>".$rowArray['categroy_name']."</option>\n");
    }
    print("</select>");
}
```


- 写一个函数，尽可能高效的，从一个标准 url 里取出文件的扩展名
   例如: http://www.sina.com.cn/abc/de/fg.php?id=1 需要取出 php 或 .php

答案1:
```
function getExt($url){
   $arr = parse_url($url);   
   $file = basename($arr['path']);
   $ext = explode(".",$file);
   return $ext[1];
}
```
答案2:
```
function getExt($url) {
    $url = basename($url);
    $pos1 = strpos($url,".");
    $pos2 = strpos($url,"?");
    if(strstr($url,"?")){
         return substr($url,$pos1 + 1,$pos2 - $pos1 - 1);
    } else {
      return substr($url,$pos1);
    }
}
```


- 写一个函数，算出两个文件的相对路径

　　如 $a = '/a/b/c/d/e.php';
　　$b = '/a/b/12/34/c.php';
　　计算出 $b 相对于 $a 的相对路径应该是 ../../c/d将()添上

答:

```
function getRelativePath($a, $b) {   
    $returnPath = array(dirname($b));   
    $arrA = explode('/', $a);   
    $arrB = explode('/', $returnPath[0]);   
    for ($n = 1, $len = count($arrB); $n < $len; $n++) {   
        if ($arrA[$n] != $arrB[$n]) {   
            break;   
        }    
    }   
    if ($len - $n > 0) {   
        $returnPath = array_merge($returnPath, array_fill(1, $len - $n, '..'));   
    }   
       
    $returnPath = array_merge($returnPath, array_slice($arrA, $n));   
    return implode('/', $returnPath);   
}
echo getRelativePath($a, $b);  
```


- 写一个函数，能够遍历一个文件夹下的所有文件和子文件夹。

答:
```
function my_scandir($dir)
{
     $files = array();
     if ( $handle = opendir($dir) ) {
         while ( ($file = readdir($handle)) !== false ) {
             if ( $file != ".." && $file != "." ) {
                 if ( is_dir($dir . "/" . $file) ) {
                     $files[$file] = scandir($dir . "/" . $file);
                 }else {
                     $files[] = $file;
                 }
             }
         }
         closedir($handle);
         return $files;
     }
}
```

- 以下哪一个函式可以把浏览器转向到另一个页面？

redir()这不是一个 PHP 函式，会引致执行错误。
header()这个是正确答案，header() 用来插入卷头资料，可以用来使浏览器转向到另一个页面，例如：
header("Location: http://www.search-this.com/");
location()这不是一个 PHP 函式，会引致执行错误。
redirect()这不是一个 PHP 函式，会引致执行错误。

- 以下哪一个函式可以用来开启档案以便读／写？

fget()这不是一个 PHP 函式，会引致执行错误。
file_open()这不是一个 PHP 函式，会引致执行错误。
fopen()这是正确答案，fopen() 可以用来开启档案以便读／写，事实上这个函式还有很多选项，详细资料请参阅 php.net。 
open_file()这不是一个 PHP 函式，会引致执行错误。


- 请说明 PHP 中传值与传引用的区别。什么时候传值什么时候传引用?

答:传值只是把某一个变量的值传给了另一个变量，而引用则说明两者指向了同一个地方。

- 请举例说明在你的开发过程中用什么方法来加快页面的加载速度

答：要用到服务器资源时才打开，及时关闭服务器资源，数据库添加索引，页面可生成静态，图片等大文件单独服务器。使用代码优化工具啦

- echo count("abc"); 输出什么？

答："1"

- MySQL数据库，一天一万条以上的增量，怎么优化？

答：我们曾做过短信SP的东西，有个短信发送的日志表，每天增量也很大，
处理的方法是按月进行分表，因为是日志表，主要操作是insert操作，所以每月初自动生成新的数据表，
数据插入到对应月份的那张数据表。[比如表明前缀是cdb_smslog 后面加200910 及时cdb_smslog_200910]
其他优化方式暂时想不起来，对于myISAM, 考虑容量的话，也有优化的方案
但是对于那种查询操作的表的话，我的思路是根据作者的发布时间存储到不同的表里面
所以对sina那种海量数据的处理很感兴趣，很好奇他们的处理方法，[以前同事说sina的首页同时操作10多个数据库]


- 写出一种排序算法（要写出代码），并说出优化它的方法。

答：
```
//冒泡排序
function maopao($arr) {
	$count = count($arr);
	for($i=0; $i<$count-1; ++$i) {
		for($j=0; $j<$count-$i-1; ++$j) {
		if($arr[$j] > $arr[$j+1]) {
			$temp = $arr[$j];
			$arr[$j] = $arr[$j+1];
			$arr[$j+1] = $temp;
		}
	}
}
	return $arr;
}
```

```
//顺序排序
function shunxu($arr) {
	$count = count($arr);
	for($i=0; $i<$count-1; ++$i) {
	$p = $i;
	for($j=$i+1; $j<$count; ++$j) {
		$p = $arr[$p] > $arr[$j] ? $j : $p;
	}
	if($p != $i) {
		$tvalue = $arr[$i];
		$arr[$i] = $arr[$p];
		$arr[$p] = $tvalue;
	}
}
	return $arr;
}
```
ps:有人说加个监控，计算数组交换的频度[这对冒泡], 比如冒泡的第一次操作频度为0，则无需操作，直接返回，因为已经是排好序的数组


- 一群猴子排成一圈，按1，2，...，n依次编号。然后从第1只开始数，数到第m只,把它踢出圈，从它后面再开始数，再数到第m只，在把它踢出去...，如此不停的进行下去，直到最后只剩下一只猴子为止，那只猴子就叫做大王。要求编程模拟此过程，输入m、n, 输出最后那个大王的编号。

答：
yuesefu环问题，PPC有很多针对这个问题的处理，我的就不上啦
```
function yuesefu($n,$m) {
	$r=0;
	for($i=2; $i<=$n; $i++) {
		$r=($r+$m)%$i;
	}
	return $r+1;
}
print_r(yuesefu(3,3));
```

- 写5个不同的自己的函数，来截取一个全路径的文件的扩展名，允许封装php库中已有的函数。

答：
```
$path = str_replace('\\', '/',__FILE__);
echo $path.'<br />';
function extname1($path) {
	return strrchr($path, '.');
}

function extname2($path) {
	$position = strrpos($path, '.');
	return substr($path, $position);
}

function extname3($path) {
	$arr = explode('.', $path);
	return $arr[count($arr) - 1];
}

function extname4($path) {
	preg_match_all('/[\w\/\:\-]+\.([\w]+)$/', $path, $out);
return $out[1][0];
}

function extname5($path) {
	return preg_replace('/^[^\.]+\.([\w]+)$/', '${1}', basename($path));
}

print_r(extname5($path));
```

- 写个函数用来对二维数组排序。

答：
```
function array_sort_by_any_row($array_name, $row_id, $order_type){
	$array_temp=array();
	foreach($array_name as $key=>$value){
		$array_temp[$key]=$value[$row_id];
	}
	if($order_type==="ASC"){ //顺序
		asort($array_temp);
	} else {
		arsort($array_temp);
	}
	$result_array=array();
	foreach($array_temp as $key=>$value){
		$result_array[$key]=$array_name[$key];
	}
	return $result_array;
}
	$arr = array(array('num'=>5, 'value'=>6),
	array('num'=>2, 'value'=>39),
	array('num'=>36, 'value'=>29)
);
$sortarr = array_sort_by_any_row($arr, 'num', 'DESC');
print_r($sortarr);
```