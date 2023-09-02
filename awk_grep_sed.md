# Linux 文本三剑客 
## awk 
- `awk [option] 'pattern[action]' file` 即通过**单引号**中的条件动作进行文本格式化 
- `action动作场景` 
    - `$0` 代表整行
    - `$NF` 代表分割后的最后一列
    - `$(NF-1)`代表分割后的倒数第二列  

- `awk '{print $1}' filename` 使用 awk 打印文件第一列 
- `awk 'END {print NR}' filename` 统计文件行数 
- `awk {sum += $1} END {print sum} filename` 如何计算某一列的总和   

## sed 
#### sed 语法 
`sed [options] 'OPERATION' filename`   
- options
    - -n: Suppresses the default behavior of printing the pattern space to the console after processing.
    - i: Changes the original file instead of outputting the changes to stdout. 
- OPERATION
    - s: Replaces the first occurrence of a regex pattern with another regex pattern.
    - y: Translates a set of characters into another set of characters.
    - d: Deletes the pattern space without printing it.
    - p: Prints the pattern space to stdout.
    - g: Replaces all occurrences of the regex pattern with another regex pattern.
    - a: Appends text to the output stream.
    - i: Inserts text to the output stream.
    - r: Reads text from the file and appends it to the output stream. 

#### 内容替换 
`sed '/s/old/new/g' filename`  
#### 删除行列 
`sed 'Nd;Md' file.txt`  

#### 打印指定行 
`sed 'a,bp' file.txt`

## grep 
- `grep    [options]    pattern     [file]` 
-  '命令'    '参数'     '匹配模式'    '文件' 
#### 末尾参数
- i：忽略大小写进行匹配。
- v：反向查找，只打印不匹配的行。
- n：显示匹配行的行号。
- E 或 --extended-regexp : 将样式为延伸的正则表达式来使用。
- q 或 --quiet或--silent : 不显示任何信息。
- o 或 --only-matching : 只显示匹配PATTERN 部分 

#### grep例子 
- `grep "xx" /tmp/passwd.txt -n` 找到与 xx 有关的行并显示行号 
- `grep  "xx" /tmp/passwd.txt -v` 找到与 xx 无关的行 
- `grep 'xx' /tmp/passwd.txt -c` 统计含有 xx 的行数 
- `grep '^m' /tmp/passwd.txt` 找到以 m 开头的行   


### 综合例子 
- 写一个 bash脚本以实现一个需求，去掉输入中含有this的语句，把不含this的语句输出
```shell 
$awk '!/this/ {print $0}' filename  
$grep -v 'this' 
$sed '/this/d' filename  
```

- 打印第5行 
```shell
$sed -n 5p 
``` 

- 统计每个单词出现的次数
```shell
cat nowcoder.txt | xargs -n1 | sort | uniq -c | sort -n | awk '{print $2, $1}' 
# cat 访问文件 
# xargs 转为单行输出 
# sort 结果按字符大小排序 
# uniq 统计重复行 
# sort 对第一列统计结果排序 
# awk 交换列位置输出
``` 

