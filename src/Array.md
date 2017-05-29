# JavaScript系列之Array

## JavaScript中创建数组有两种方式

1. 使用 Array 构造函数：

```js
var arr1 = new Array(); //创建一个空数组
var arr2 = new Array("张三","李四","王二麻子"); //创建一个包含3个字符串的数组
```
2. 使用数组字面量表示法：

```js
var arr1 = []; //创建一个空数组
var arr2 = ["张三","李四","王二麻子"]; //创建一个包含3个字符串的数组
```
## 鉴别数组

ES5之前，可以通过 instanceof Array去判断，但是instanceof 操作符的问题在于，它假定只有一个全局执行环境。
JavaScript的值可以在同一个网页的不同框架之间传来传去，每个页面拥有自己的全局上下文，这就造成了instanceof无法识别

ES5 新增了 Array.isArray()方法。这个方法的目的是最终确定某个值到底是不是数组，无论该值来自哪里。

## 数组方法

* join()
* push()和pop()
* shift() 和 unshift()
* sort()
* reverse()
* concat()
* slice()
* splice()
* indexOf()和 lastIndexOf() （ES5新增）
* forEach() （ES5新增）
* map() （ES5新增）
* filter() （ES5新增）
* every() （ES5新增）
* some() （ES5新增）
* reduce()和 reduceRight() （ES5新增）
* Array.from（ES6新增）
* Array.of（ES6新增）
* copyWithin（ES6新增）
* fill（ES6新增）
* find和findIndex（ES6新增）
* keys、values和entries（ES6新增）
* includes（ES6新增）
* 数组的空位（ES7新增）


1. join()
```js
join(separator): 将数组的元素组起一个字符串，以separator为分隔符，  
省略的话则用默认用逗号为分隔符，该方法只接收一个参数：即分隔符。
```
```js
var arr = [1,2,3];
console.log(arr.join()); // 1,2,3
console.log(arr.join("-")); // 1-2-3
console.log(arr); // [1, 2, 3]（原数组不变）
``` 
```js
通过join()方法可以实现重复字符串，只需传入字符串以及重复的次数，就能返回重复后的字符串，函数如下：
```
```js
function repeatString(str, n) {
    return new Array(n + 1).join(str);
}
console.log(repeatString("abc", 3)); // abcabcabc
console.log(repeatString("Hi", 5)); // HiHiHiHiHi
```

2. push()和pop()
```js
push(): 可以接收任意数量的参数，把它们逐个添加到数组末尾，并返回修改后数组的长度。  
pop()：数组末尾移除最后一项，减少数组的 length 值，然后返回移除的项。  
```
```js
var arr = ["Lily","lucy","Tom"];
var count = arr.push("Jack","Sean");
console.log(count); // 5
console.log(arr); // ["Lily", "lucy", "Tom", "Jack", "Sean"]
var item = arr.pop();
console.log(item); // Sean
console.log(arr); // ["Lily", "lucy", "Tom", "Jack"]
```
3. shift() 和 unshift()
```js
shift()：删除原数组第一项，并返回删除元素的值；如果数组为空则返回undefined 。 
unshift:将参数添加到原数组开头，并返回数组的长度 。
这组方法和上面的push()和pop()方法正好对应，一个是操作数组的开头，一个是操作数组的结尾。
```
```js
var arr = ["Lily","lucy","Tom"];
var count = arr.unshift("Jack","Sean");
console.log(count); // 5
console.log(arr); //["Jack", "Sean", "Lily", "lucy", "Tom"]
var item = arr.shift();
console.log(item); // Jack
console.log(arr); // ["Sean", "Lily", "lucy", "Tom"]
```

4. sort()
```js
默认是按升序排列，排序过程中会调用每个数组项的 toString()方法，所以比较的是字符串
```
```js
//完美解决方案
function compare(value1, value2) {
    if (value1 < value2) {
        return -1;
    } else if (value1 > value2) {
        return 1;
    } else {
        return 0;
    }
}
var arr = [1, 12, 2, 22];
console.log(arr.sort(compare)); // [1, 2, 12, 22]
```

5. reverse()
```js
反转数组项的顺序
```
```js
var arr = [13, 24, 51, 3];
console.log(arr.reverse()); //[3, 51, 24, 13]
console.log(arr); //[3, 51, 24, 13](原数组改变)
```

6. concat()
```js
concat() ：将参数添加到原数组中。这个方法会先创建当前数组一个副本，
然后将接收到的参数添加到这个副本的末尾，最后返回新构建的数组。
在没有给 concat()方法传递参数的情况下，它只是复制当前数组并返回副本。
```
```js
var arr = [1,3,5,7];
var arrCopy = arr.concat(9,[11,13]);
console.log(arrCopy); //[1, 3, 5, 7, 9, 11, 13]
console.log(arr); // [1, 3, 5, 7](原数组未被修改)
```
```js
从上面测试结果可以发现：传入的不是数组，则直接把参数添加到数组后面，
如果传入的是数组，则将数组中的各个项添加到数组中。但是如果传入的是一个二维数组呢？
```
```js
var arrCopy2 = arr.concat([9,[11,13]]);
console.log(arrCopy2); //[1, 3, 5, 7, 9, Array[2]]
console.log(arrCopy2[5]); //[11, 13]
```
```js
上述代码中，arrCopy2数组的第五项是一个包含两项的数组，
也就是说concat方法只能将传入数组中的每一项添加到数组中，
如果传入数组中有些项是数组，那么也会把这一数组项当作一项添加到arrCopy2中。
```

7. slice()
```js
slice()：返回从原数组中指定开始下标到结束下标之间的项组成的新数组。
slice()方法可以接受一或两个参数，即要返回项的起始和结束位置。在只有一个参数的情况下， 
slice()方法返回从该参数指定位置开始到当前数组末尾的所有项。如果有两个参数，
该方法返回起始和结束位置之间的项——但不包括结束位置的项。
```
```js
var arr = [1,3,5,7,9,11];
var arrCopy = arr.slice(1);
var arrCopy2 = arr.slice(1,4);
var arrCopy3 = arr.slice(1,-2);
var arrCopy4 = arr.slice(-4,-1);
console.log(arr); //[1, 3, 5, 7, 9, 11](原数组没变)
console.log(arrCopy); //[3, 5, 7, 9, 11]
console.log(arrCopy2); //[3, 5, 7]
console.log(arrCopy3); //[3, 5, 7]
console.log(arrCopy4); //[5, 7, 9]
```

8. splice()
```js
删除：可以删除任意数量的项，只需指定 2 个参数：要删除的第一项的位置和要删除的项数。
插入：可以向指定位置插入任意数量的项，只需提供 3 个参数：起始位置、 0（要删除的项数）和要插入的项。
替换：可以向指定位置插入任意数量的项，且同时删除任意数量的项，只需指定 3 个参数：起始位置、要删除的项数和要
插入的任意数量的项。插入的项数不必与删除的项数相等。  
splice()方法始终都会返回一个数组，该数组中包含从原始数组中删除的项，如果没有删除任何项，则返回一个空数组。
```
```js
var arr = [1,3,5,7,9,11];
var arrRemoved = arr.splice(0,2);
console.log(arr); //[5, 7, 9, 11]
console.log(arrRemoved); //[1, 3]
var arrRemoved2 = arr.splice(2,0,4,6);
console.log(arr); // [5, 7, 4, 6, 9, 11]
console.log(arrRemoved2); // []
var arrRemoved3 = arr.splice(1,1,2,4);
console.log(arr); // [5, 2, 4, 4, 6, 9, 11]
console.log(arrRemoved3); //[7]
```

9. indexOf()和 lastIndexOf()
```js
indexOf()：接收两个参数：要查找的项和（可选的）表示查找起点位置的索引。其中， 从数组的开头（位置 0）开始向后查找。 
lastIndexOf：接收两个参数：要查找的项和（可选的）表示查找起点位置的索引。其中， 从数组的末尾开始向前查找。
```
```js
var arr = [1,3,5,7,7,5,3,1];
console.log(arr.indexOf(5)); //2
console.log(arr.lastIndexOf(5)); //5
console.log(arr.indexOf(5,2)); //2
console.log(arr.lastIndexOf(5,4)); //2
console.log(arr.indexOf("5")); //-1
```

10. forEach()
```js
forEach()：对数组进行遍历循环，对数组中的每一项运行给定函数。这个方法没有返回值。参数都是function类型，
默认有传参，参数分别为：遍历的数组内容；第对应的数组索引，数组本身。
```
```js
var arr = [1, 2, 3, 4, 5];
arr.forEach(function(x, index, a){
console.log(x + '|' + index + '|' + (a === arr));
});
// 输出为：
// 1|0|true
// 2|1|true
// 3|2|true
// 4|3|true
// 5|4|true
```

11. map()
```js
map()：指“映射”，对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组。
```
```js
var arr = [1, 2, 3, 4, 5];
var arr2 = arr.map(function(item){
    return item*item;
});
console.log(arr2); //[1, 4, 9, 16, 25]
```

12. filter()
```js
filter()：“过滤”功能，数组中的每一项运行给定函数，返回满足过滤条件组成的数组。
```
```js
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
var arr2 = arr.filter(function(x, index) {
    return index % 3 === 0 || x >= 8;
}); 
console.log(arr2); //[1, 4, 7, 8, 9, 10]
```

13. every()
```js
every()：判断数组中每一项都是否满足条件，只有所有项都满足条件，才会返回true。
```
```js
var arr = [1, 2, 3, 4, 5];
var arr2 = arr.every(function(x) {
    return x < 10;
}); 
console.log(arr2); //true
var arr3 = arr.every(function(x) {
    return x < 3;
}); 
console.log(arr3); // false
```

14. some()
```js
some()：判断数组中是否存在满足条件的项，只要有一项满足条件，就会返回true。
```
```js
var arr = [1, 2, 3, 4, 5];
var arr2 = arr.some(function(x) {
return x < 3;
}); 
console.log(arr2); //true
var arr3 = arr.some(function(x) {
return x < 1;
}); 
console.log(arr3); // false
```

15. reduce()和 reduceRight()
```js
这两个方法都会实现迭代数组的所有项，然后构建一个最终返回的值。reduce()方法从数组的第一项开始，逐个遍历到最后。
而 reduceRight()则从数组的最后一项开始，向前遍历到第一项。这两个方法都接收两个参数：一个在每一项上调用的函数
和（可选的）作为归并基础的初始值。
传给 reduce()和 reduceRight()的函数接收 4 个参数：前一个值、当前值、项的索引和数组对象。
这个函数返回的任何值都会作为第一个参数自动传给下一项。第一次迭代发生在数组的第二项上，因此第一个参数是数组的第一项，
第二个参数就是数组的第二项。
下面代码用reduce()实现数组求和，数组一开始加了一个初始值10。
```
```js
var values = [1,2,3,4,5];
var sum = values.reduceRight(function(prev, cur, index, array){
    return prev + cur;
},10);
console.log(sum); //25
```

16. from()
```js
Array.from方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象
（包括ES6新增的数据结构Set和Map）。任何有length属性的对象，都可以通过Array.from方法转为数组
PS:扩展运算符（...）也可以将某些数据结构(遍历器接口Symbol.iterator)转为数组
```
```js
let arrayLike = {
    '0': 'a',
    '1': 'b',
    '2': 'c',
    length: 3
};
// ES5的写法
var arr1 = [].slice.call(arrayLike); // ['a', 'b', 'c']
// ES6的写法
let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']
```
```js
Array.from()的另一个应用是，将字符串转为数组，然后返回字符串的长度
```
```js
function countSymbols(string) {
  return Array.from(string).length;
}
//同时提供map功能
Array.from({ length: 2 }, () => 'jack')
// ['jack', 'jack']
```
17. of()
```js
Array.of方法用于将一组值，转换为数组，总是返回参数值组成的数组。如果没有参数，就返回一个空数组。
```
```js
Array.of() // []
Array.of(undefined) // [undefined]
Array.of(1) // [1]
Array.of(1, 2) // [1, 2]
```
```js
//Array.of方法可以用下面的代码模拟实现。
function ArrayOf(){
  return [].slice.call(arguments);
}
```

18. copyWithin()
```js
数组实例的copyWithin方法，在当前数组内部，将指定位置的成员复制到其他位置（会覆盖原有成员），
然后返回当前数组。也就是说，使用这个方法，会修改当前数组。
它接受三个参数。
+ target（必需）：从该位置开始替换数据。
+ start（可选）：从该位置开始读取数据，默认为0。如果为负值，表示倒数。
+ end（可选）：到该位置前停止读取数据，默认等于数组长度。如果为负值，表示倒数。
```

```js
//表示将从3号位直到数组结束的成员（4和5），复制到从0号位开始的位置，结果覆盖了原来的1和2
[1, 2, 3, 4, 5].copyWithin(0, 3);//[4, 5, 3, 4, 5]
```

19. fill()
```js
fill方法使用给定值，填充一个数组。fill方法用于空数组的初始化非常方便。
数组中已有的元素，会被全部抹去。
fill方法还可以接受第二个和第三个参数，用于指定填充的起始位置和结束位置。
```

```js
['a', 'b', 'c'].fill(7);// [7, 7, 7]

new Array(3).fill(7);// [7, 7, 7]

['a', 'b', 'c'].fill(7, 1, 2);// ['a', 7, 'c']
```

20. find()和findIndex()
```js
数组实例的find方法，用于找出第一个符合条件的数组成员。它的参数是一个回调函数，
所有数组成员依次执行该回调函数，直到找出第一个返回值为true的成员，然后返回该成员。
如果没有符合条件的成员，则返回undefined。
```
```js
[1, 4, -5, 10].find((n) => n < 0);// -5
[1, 5, 10, 15].find(function(value, index, arr) {
  return value > 9;
}) // 1
```
```js
数组实例的findIndex方法的用法与find方法非常类似，返回第一个符合条件的数组成员的位置，
如果所有成员都不符合条件，则返回-1。
```
```js
[1, 5, 10, 15].findIndex(function(value, index, arr) {
  return value > 9;
}) // 2
```
```js
这两个方法都可以接受第二个参数，用来绑定回调函数的this对象。
另外，这两个方法都可以发现NaN，弥补了数组的IndexOf方法的不足。
```
```js
[NaN].indexOf(NaN)// -1
[NaN].findIndex(y => Object.is(NaN, y))// 0
```

21. 数组实例的entries()，keys()和values()
```js
ES6提供三个新的方法——entries()，keys()和values()——用于遍历数组。
它们都返回一个遍历器对象（详见《Iterator》一章），可以用for...of循环进行遍历，
唯一的区别是keys()是对键名的遍历、values()是对键值的遍历，entries()是对键值对的遍历。
```
```js
for (let index of ['a', 'b'].keys()) {
  console.log(index);
}
// 0
// 1
```
```js
for (let elem of ['a', 'b'].values()) {
  console.log(elem);
}
// 'a'
// 'b'
for (let [index, elem] of ['a', 'b'].entries()) {
  console.log(index, elem);
}
// 0 "a"
// 1 "b"
```
```js
如果不使用for...of循环，可以手动调用遍历器对象的next方法，进行遍历。
```
```js
let letter = ['a', 'b', 'c'];
let entries = letter.entries();
console.log(entries.next().value); // [0, 'a']
console.log(entries.next().value); // [1, 'b']
console.log(entries.next().value); // [2, 'c']
```

22. 数组实例的includes()
```js
Array.prototype.includes方法返回一个布尔值，表示某个数组是否包含给定的值，
与字符串的includes方法类似。该方法属于ES7，但Babel转码器已经支持。
该方法的第二个参数表示搜索的起始位置，默认为0。如果第二个参数为负数，则表示倒数的位置，
如果这时它大于数组长度（比如第二个参数为-4，但数组长度为3），则会重置为从0开始。
```
```js
[1, 2, 3].includes(2);     // true
[1, 2, 3].includes(4);     // false
[1, 2, NaN].includes(NaN); // true
[1, 2, 3].includes(3, 3);  // false
[1, 2, 3].includes(3, -1); // true
```