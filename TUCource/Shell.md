## Shell script Summary
- [Variables](#variables)
- [Math Relation](#math-relation)
- [If Else](#if-else)
- [For](#for)
- [Case](#case)
- [redirect](#redirect)
- [While](#while)
- [$?](#\#?)
- [read](#read)


### Variables
- 系统定义变量: set命令查看
- 用户定义变量：echo$<变量名>  

### Math Relation
- -eq 相等
- -ne 不等
- -gt 大于
- -lt 小于
- -ge 大于等于
- -le 小于等于

### If Else
- **if** condition **then** ... fi


### For 
- for var in {} do ... done   

### Case 
- case var in ... ;; esac   

### redirect 
- command >file, 输出重定向到 file (注意>和file之间不能有空格)
- command >>file, 输出重定向到file (注意>和file之间不能有空格) 
- command >file 2>&1，以覆盖方式，将正确输出和错误信息都输出到同一文件file中
- command >>file 2>&1, 以追加方式，将正确输出和错误信息都输出到同一文件file中 

### While 
- while [condition] do {} done  

### $? 
- 获取上一个命令的退出状态
- 获取函数的返回值 

### read 
- 若没有重定向，则从标准输入中读取 
- 选项
    - -n num 读取num个字符, 而非整行
    - -a array 将读取的内容赋值给数组
    - -p 显示提示信息 

