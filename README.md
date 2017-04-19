# word 文档

### PHP 笔记
  
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
        
        

