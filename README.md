# word 文档

## PHP 笔记
### 内存处理
#### 使用生成器
  
  生成一个范围内的数据(错误的方式)

``` <?php
    // 生成范围内的数据
    function makeRange($length){
            $dataset =array();
            for($i=0;$i<$length;$i++){
                $dataset[]=$i;
            }
            return $dataset;
        }
        
    // 调用 
    $customRange =  makeRange(100000);
    foreach($customRange as $i){
        echo $i,PHP_EOL;
     }   

```  

 正确的方式：

``` <?php

function makeRange($length){
     for($i = 0 ;$i<$length;$i++){
         yield $i;
     }
 }

foreach(makeRange(10000) as $i){
     echo $i,PHP_EOL;
} 
```

总结：虽然两种方式都能产相同的效果！但是上面一种定义一个数组占用分配内存，而后面一种是：一次只会为一个整数分配内存
        
    
#### 使用生成器处理CSV文件


```<?php

    function getRow($file){
        $handl = fopen($file,'rb');
        if($handl === false){
             throw new Exception();
         }
         while(feof($handl) === false){
            yield fgetcsv($handl);
        }
          fclose($handl);
    }


    foreach(getRow('/Users/costa92/Code/wx_user.csv') as $row){
       print_r($row);
    }
```
 总结：在PHP处理文件大小只允许1GB的内存！如果小于1GB的文件，可以使用普通方法，读取全部文件！再循环处理，但是如果超过1GB，只能使用上面一种方式处理。

