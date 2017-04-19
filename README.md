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
 
 
### 创建闭包
 
 **简单闭包例子：**
    
   
``` <?php
        $closure = function($name){
           return sprintf("Hello %s",$name);
        };

        echo $closure("costa92");
```

这个一种是闭包函数与普通的函数相似，使用也有相同，不过匿名函数没有名称


**在array_map()函数使用闭包**

  
``` <?php
        $numbersPlusOne  = array_map(function($number){
             return $number+1;
        },[1,2,3]);

        print_r($numbersPlusOne);
```

  传统的使用方式：
    
    
```<?php
         //实现具名回调
        function incrementNumber($number){
            return $number+1;
        }
        
        //使用具名回调
        $numbersPlusOne = array_map('incrementNumber',[1,2,3]);
        print_r($numbersPlusOne);
```
            
    总结：在没有出现闭包之前，只能使用传统的方式，但是效率没有使用闭包那么高！
    
    
 **附加状态**
      
      使用use关键附加闭包的状态
      
    
```  <?php
        
            function enclosePerson($name){
               return function($doCommand) use ($name){
                   return sprintf('%s,%s',$name,$doCommand);
                 };  
            }

            $clay = enclosePerson('Clay');
            echo $clay("get me sweet tea");
```
                 

