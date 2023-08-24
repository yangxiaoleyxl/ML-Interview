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

### 3.字符串判空 
```shell 
#!/bin/bash

test_str=""

if [ "$test_str" = "" ];then
    echo "NULL!"
fi

if [ x"$test_str" = x ];then
    echo "NULL!"
fi

if [ -z "$test_str" ]; then
    echo "NULL!"
fi 
```