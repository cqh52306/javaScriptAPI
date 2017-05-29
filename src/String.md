# JavaScript系列之String

## JavaScript中创建字符串有两种方式

1. 使用 String 构造函数：

```js
var str1 = new String(); //创建一个空字符串
var str2 = new String("张三"); 
```
2. 使用字符串字面量表示法(常用)：

```js
var str1 = ''; //创建一个空字符串 或者双引号
var str2 = "张三"; 
```
## 鉴别字符串

可以通过 instanceof(构造函数创建) Array去判断

```js
//自定义方法实现
var is_string = function (value) {
    return Object.prototype.toString.apply(value) === '[object String]';
}
```

## 字符串常用方法

* fromCharCode()
* charAt()和charCodeAt()
* slice()
* substr()和substring()
* indexOf()和 lastIndexOf() 
* replace()
* search() 
* concat()
* split() 
* toLowerCase() 和toUpperCase()


1. fromCharCode()
```js
String.fromCharCode([code1[,code2...]]); 从一些Unicode字符串中创建一个字符串，  
```
```js
String.fromCharCode(65,66,112); //ABp
``` 

2. charAt()和charCodeAt()
```js
charAt方法返回指定索引位置处的字符。如果超出有效范围的索引值返回空字符串。
charCodeAt方法返回一个整数，代表指定位置字符的Unicode编码。  
```
```js
var str = "ABC"; 
str.charAt(1); //B
var str = "ABC"; 
str.charCodeAt(0); //65
``` 

3. slice()
```js
slice方法返回字符串的片段
strObj.slice(start[,end]) 
start下标从0开始的strObj指定部分其实索引。如果start为负，将它作为length+start处理，
此处length为字符串的长度。 
end小标从0开始的strObj指定部分结束索引。如果end为负，将它作为length+end处理，
此处length为字符串的长度。 
```
```js
var str = "ABCDEF"; 
str.slice(2,4); //CD
``` 

4. substr()和substring()
```js
substr方法返回一个从指定位置开始的指定长度的子字符串。
strObj.substr(start[,length]) 
--start所需的子字符串的起始位置。字符串中的第一个字符的索引为0。 
  length在返回的子字符串中应包括的字符个数。 
substring方法返回位于String对象中指定位置的子字符串。 
strObj.substring(start,end) 
--start指明子字符串的起始位置，该索引从0开始起算。 
  end指明子字符串的结束位置，该索引从0开始起算。 
  substring方法使用start和end两者中的较小值作为子字符串的起始点。
  如果start或end为NaN或者为负数，那么将其替换为0。 
```
```js
var str = "ABCDEF"; 
str.substring(2,4); // 或 str.substring(4,2); 
//CD
var str = "ABCDEF"; 
str.substr(2,4); //CDEF 
``` 

5. indexOf()和 lastIndexOf() 
```js
indexOf方法放回String对象内第一次出现子字符串位置。如果没有找到子字符串，则返回-1。
strObj.indexOf(substr[,startIndex]) 
--substr要在String对象中查找的子字符串。 
  startIndex该整数值指出在String对象内开始查找的索引。如果省略，则从字符串的开始处查找。  
lastIndexOf方法返回String对象中字符串最后出现的位置。如果没有匹配到子字符串，则返回-1。 
strObj.lastIndexOf(substr[,startindex]) 
--substr要在String对象内查找的子字符串。 
  startindex该整数值指出在String对象内进行查找的开始索引位置。如果省略，则查找从字符串的末尾开始。 
```
```js
var str = "ABCDECDF"; 
str.indexOf("CD"，1); // 由1位置从左向右查找 123... 
//2 
var str = "ABCDECDF"; 
str.lastIndexOf("CD",6); // 由6位置从右向左查找 ...456 
//5 
``` 

6. replace()
```js
replace该方法将字符串中第一个出现的searchValue子字符串替换为replaceValue，
并返回新的字符串。原有的字符串不受影响。
replace(searchValue,replaceValue)
```
```js
var str1="aaaa";
var str2=str1.replace("a","b");
alert(str2);//输出"baaa"
alert(str1);//输出"aaaa"
``` 

7. search()
```js
search方法返回与正则表达式查找内容匹配的第一个字符串的位置。
strObj.search(reExp) 
```
```js
var str = "ABCDECDF"; 
str.search("CD"); // 或 str.search(/CD/i); 
//2 
``` 