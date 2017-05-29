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