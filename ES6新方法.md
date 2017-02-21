##ES6新增语法
 ####1. `...` 语法

- 求多个数组中的最大值

```
   var arr1=[1,2,3];
   
   var arr2=[6];
   
   var max=Math.max(...arr1,...arr2);
   
```
- 将arguments或者NodeList转换成数组

```
var likeArr=document.querySelectorAll('div');

var arr=[...likeArr];

```