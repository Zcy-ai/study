# shell脚本语言

## 参数 parameter

变量: a, path

位置参数: 0,1,12

特殊变量: #,?

$ 获取参数的值

$#: 获取参数的个数

$*: 将命令中的所有参数当作一个参数来保存

$@: 使用时加引号, 将命令中的所有参数当作一个字符串列表中的多个独立参数

假设在脚本运行中写入三个参数1，2，3。$* 等价于"1 2 3", $@等价于"1""2""3"

$?: 显示命令最后的退出状态。0表示没有错误，其余值代表有错误

🌰
```shell
x=bon
y=jour
echo $x
x=$x$y
echo $x
```
输出结果: bon, bonjour

变量赋值可使用shell内部命令read
read -p [ var1 var2 ….], 其中-p选项用于显示输入提示
```shell
read x y
echo $x$y
```



## 正则表达式 reguler expression
.: 替换正则表达式中的任意单个字符（除换行符）

[]: 指定一定值范围内的单个字符

🌰
* [Ff]raise 表示 « Fraise » ou « fraise »
* [1-3-] 表示 « 1 », « 2 », « 3 » et « - »
* [a-cI-K1-3] 表示 « a », « b », « c », « I », « J », « K », « 1 », « 2 », « 3 »
* [^0-9] 表示除数字以外的所有字符

^: 行的开头

$: 行的结尾

🌰
* « ^chaîne » 表示待匹配的表达式必须由 « chaîne » 开头
* « chaîne$ » 表示待匹配的表达式必须由 « chaîne » 结尾

*: 前导字符出现0次或多次

🌰
* « a* » 表示待匹配表达式包含0次或多次 « a »

+: 前导字符匹配一次或多次

?: 前导字符匹配0次或1次

|: r1|r2表示匹配r1或r2

( r ) : une expression régulier peut être mise entre 
parenthèses pour grouper des expressions :

\\{n\\}: 前导字符重复几次

🌰
* ab{3}c 表示 abbbc

\\{n,\\}: 前导字符至少重复n次

\\{n,m\\} 前导字符重复n至m次

### 正则表达式在grep中的运用

``` shell
# 找到/etc/passwd文件中所有以csh为结尾的行
grep 'csh$' /etc/passwd 
```

``` shell
# ls -l 输出结果中所有以d为开头的行（目录）
ls –l | grep '^d' 
```

``` shell
# ls -l 输出结果中所有不以d为开头的行（也就是不是目录）
ls –l | grep '^[^d] '
```

``` shell
# 一个数字+空格+Mar  比如 《1 Mar》
$ ls –l | grep '[0-9] Mar' 
```

``` shell
# 匹配paule 或 pauline
egrep 'paul(e|ine)' /etc/passwd
```


1. 下列正则表达式分别匹配了什么字符串
* a*b+c?[^c]
* a.*b

2. 下列的字符串
aabbbb, accbbac, bbabbab, abbdaac, abbdbca, 
分别匹配了下面哪个正则表达式
* [ac]*b+
* [^c]*ba?.$ 
* ^a[bd]\\{1,3\\}[ac]*$  grep和egrep区别 ⚠️

3. 现有下列字符串
aabbbb, accbbac, bbabbab, abbdaac, abbdbca, 编写正则表达式 : 
- 匹配含有连续两个b的字符串 b\{2\}
- 开头和结尾字符相同的字符串 ^\(.\)*\1$

4. 
* Afficher les lignes d’un fichier qui commencent par une majuscule et finissent par un point
bon[^j][^o][^u][^r]*
* Afficher les lignes d’un fichier qui ne contiennent pas trois lettres a
* Afficher les lignes d’un fichier qui contiennent bon mais pas bonjour

### sed

#### 简介
sed "过滤器（流编辑器）是一种可编程过滤器。sed "过滤命令应用于文件，即默认的标准输入；处理结果发送到标准输出。
sed "命令搜索字符串或正则表达式的实例，并将其替换为另一个字符串或正则表达式。它不会修改处理过的文件，只会将结果写入标准输出

#### 用法
sed -option 
常用选项:
* -r 使用扩展正则表达式
* -e 命令行上
* -i 直接对文件内容作出修改
* -n 取消默认输出,sed会默认输出所有文本内容,使用-n仅输出处理过的行
* -f

sed命令选项:
* a: 追加，即在匹配行后插入内容
* s: 替换
* p: 打印
* i: 插入，向匹配行前插入内容
* d: 删除
* c: 更改匹配行内容
* g: 全局替换

🌰
``` shell
# 全局替换所有小写的u和a为大写
sed –e 's/u/U/g' –e 's/a/A/g' file
```

``` shell
# 假设prog 有s/u/U/g, 我们可以将prog脚本命令用于file文件
sed –f prog file
```

``` shell
# 文件中的所有toto都替换成tata
sed 's/toto/tata/g' file
```

``` shell
# 删除（不显示）带有toto的行
sed –e '/toto/d' file
```

``` shell
# 使用-n仅输出处理过的行, 这边只打印文件的最后一行
sed -n '$p' filepath
```

``` shell
# 打印文件的5-10行
sed -n '5,10p' filepath
```

``` shell
# 打印所有le开头的行
sed -n '/^le/p' filepath
```

``` shell
# 打印所有filtre结尾的行
sed '/filtre$/p' filepath
```

``` shell
# 添加 « ligne : » 至文件的每一行
sed 's/^/ligne :/' filepath
```

``` shell
# « filtre » 置于括号内，其中&用于保存查找到的字符串以便在替换中使用
sed 's/filtre/(&)/g' filepath
```

``` shell
# 假设文件中的一行为: one,two,three
# 输出的结果为 one:three
# \1 表示第一个()中的正则表达式匹配的内容
# \2 表示第二个()中的正则表达式匹配的内容
sed 's/\(.*\),.*,\(.*\)/\1:\2/' fich
```

``` shell
# 假设文件中的一行为:0412 shenjiahyi
# 输出的结果为: shenjiayi0412(注意shenjiayi前有一个空格)
# \1 表示第一个()中的正则表达式匹配的内容
# \2 表示第二个()中的正则表达式匹配的内容
sed 's/^\(....\)\(.*\)$/\2\1/' fich
```

``` shell
sed 's/\([0-9][0-9]*\)/aa\1aa/g'
```

``` shell
# 删除文件所有sujet开头的行
sed '/^sujet/d’ fichier
```

``` shell
# 不显示文件的1-10行, 删除1-10行
sed '1,10d' fichier
```

``` shell
# 打印文件中所有以x或X结尾的行
sed -n '/[xX]$/p' file
```

``` shell
# 打印A开头或者L开头的行,注意\是转义字符没有含义
sed -n '/^A\|^L/p' file
```

``` shell
# 
sed 's/[^,]*,//' file
```

``` shell
# 正则表达式匹配 《 任意长度字符串+逗号+数字结尾》
# sed语义为打印所有上述正则表达式匹配的所有行
sed -n '/.*,[0-9]$/p' file
```

``` shell
# 文件中所有行的开头添加A,
# &代表正则表达式匹配的内容在这也就是任意的字符串
sed 's/.*/A,&/' file
```

``` shell
# 文件中所有行的结尾添加,A
# &代表正则表达式匹配的内容在这也就是任意的字符串
sed 's/.*/&,A/' file
```

``` shell
# 在file1的每一行后都插入file2的内容
sed 'r file2' file1
```

``` shell
# 在file1的第一行后插入file2的内容
sed '1r file2' file1
```

``` shell
# 在file1中含有banana的行后插入file2的内容
sed '/banana/r file2' file1
```

``` shell
# 在file1的最后一行后插入file2的内容
sed '$r file2' file1
```

``` shell
# file1的2-4行写入file2（覆写）
sed -n '2,4w file2' file1
```

``` shell
# file1的3-最后一行写入file2（覆写）
sed -n '3,$w file2' file1
```

``` shell
# file1的含apple的行-含mango的行写入file2（覆写）
sed -n '/apple/,/mango/w file2' f
```


#### exercice
* 删除文件中的所有空行
* 删除文件中所有的空格
* 删除文件中所有注释
* 用 "19NN "替换倒数第二位数字，其中 N 是文件中每一行的倒数第二位数字
* 《 sed –e '/^[^a-zA-Z0-9]$/d' 》的作用
* 《 sed –e '3,5s/\([a-z]\)[a-z]*\([a-z]\)/\1*\2/g' file 》的作用
* 《 sed –e '/d.\ {3\ }t/,/f.n/s/a/b/' file 》的作用