#ES6新增语法
##数组
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

####2. `Array.prototype.find` 方法用于找出第一个符合条件的数组成员。它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出第一个返回值为` true `的数组项，然后返回该数组项。如果没有符合条件的数组项。则返回`undefined        `
```
[1, 2, 3, 4, 5].find((item, i) => i === 3) 

// <- 4

let arr = [{name: 'aa', age: 15}, {name: 'bb', age: 18}];

arr.find( (obj) => {
        return obj.name == 'bb';
    })
结果返回最后一个对象
```
- 另外这种方法的回调函数可以接受三个参数，依次为当前的值、当前的位置和原始数组。
                                                                                    
                              

####2. `箭头函数 =>` 语法
```
function (msg) {
console.log(msg)
}

转换成箭头函数就是：
msg=>console.log(msg)

var fn=function (str,str1) {
   console.log(str)
}
转换成箭头函数就是：
var fn=(str,str1)=>console.log(str)
```
- 只能在匿名函数或者函数表达式中使用箭头函数，不能再具名函数中使用，也就是函数声明格式