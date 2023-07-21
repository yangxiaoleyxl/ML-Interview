## Shell script Summary
- [1.Stream管理](#1stream管理)
- [2.StreamJob管理](#2streamjob管理)
- [2.Application管理](#2application管理)

### Variables
- 系统定义变量: set命令查看
- 用户定义变量：echo$<变量名>  
- 

### Math Relation
- -eq 相等
- -ne 不等
- -gt 大于
- -lt 小于
- -ge 大于等于
- -le 小于等于

### If Else
- **if** condition **then** ... fi
- ** ** 

### For 
- for var in {} do ... done   

### Case 
- case var in ... ;; esac   

### redirect 
- command >file, 输出重定向到 file (注意>和file之间不能有空格)
- command >>file, 输出重定向到file (注意>和file之间不能有空格) 
- command >file 2>&1，以覆盖方式，将正确输出和错误信息都输出到同一文件file中
- command >>file 2>&1, 以追加方式，将正确输出和错误信息都输出到同一文件file中

