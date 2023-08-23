## Shell Script 八个习惯
- 指定Bash 
    -  

## 常见的Shell脚本 
### 1.选择文件大小大于某个值的文件
有一个文件夹里有若干文件，打印文件大小大于 300B 的文件名。  

```shell
#!/bin/bash

for file in `ls -l | awk '$5>300 {print $9}'`
do
    echo $file
done
```   

### 2.某个文件夹中找到.py结尾的文件取10个，并取所有文件的第一行  

```shell 
#! bin/shell 
for file in `find dir -type f -name "*.py" | head -n 10`  
do 
    sed -n '1p' $file >> result_file
done 
```  

### 3.打印fileB中有fileA中没有的行
方法1:用awk的方法  

```
awk 'NR==FNR{a[$0]++} NR>FNR{if(!($0 in a)) print $0}' file1 file2
``` 

### 4.Shell 封装 MySQL 查询 
```shell
#!/bin/bash

host=xxx
user=xxx
password=xxx
port=xxx
dbname=xxx

sql_conn_str="-h${host} -P${port} -u${user} -p${password} $dbname"

function select_from_mysql()
{
	sql="xxxxxx"
	echo "$sql" | mysql -s $sql_conn_str >resultfile
}

select_from_mysql
```   
上面的代码就可以满足我们的需求。注意的几个小点：  
1.实际使用时候，将数据库各配置项，以及具体的sql查询语句替换成实际配置项即可。  
2.mysql -s选项表示查询输出的结果不带字段名称，如果不加-s选项会输出字段名称。  
3.将resultfile换成你最终结果文件存储的地址。 

### 处理空行 
- 查看空行行号
```shell  
grep -n '^\s*$' xxx  
``` 

```shell  
awk '/^\s*$/{print NR}' xxx  
``` 

```shell  
sed -n '/^\s*$/=' xxx 
```