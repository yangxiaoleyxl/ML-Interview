## Shell Script 八个习惯
- 指定Bash 
    -  

## 常见的Shell脚本 
### 1.选择文件大小大于某个值的文件
有一个文件夹里有若干文件，打印文件大小大于300B的文件名。  

```shell
#!/bin/bash

for file in `ls -l | awk '$5>300 {print $9}'`
do
    echo $file
done
```  