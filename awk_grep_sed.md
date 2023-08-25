# Linux 文本三剑客 
### awk 
- `awk [option] 'pattern[action]' file` 即通过**单引号**中的条件动作进行文本格式化 
- `action动作场景` 
    - `$0` 代表整行
    - `$NF` 代表分割后的最后一列
    - `$(NF-1)`代表分割后的倒数第二列  

- `awk '{print $1}' filename` 使用 awk 打印文件第一列 
- `awk 'END {print NR}' filename` 统计文件行数

### sed 


### grep 
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
