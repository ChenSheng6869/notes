# JavaScript

## 1 函数及面向对象

### 1.1 函数定义及变量作用域

> 定义方式一

```javascript
function abs(x) {
            if (x >= 0){
                return x;
            } else {
                return -x;
            }
        }
```

> 定义方式二

```javascript
var abs = function () {
            if (x >= 0){
                return x;
            } else {
                return -x;
            }
        }
```

> 调用方式

```javasript
javascript可以任意传参
```

> 存在多个参数 arguments

`arguments`是一个JS免费赠送的关键词

```javascript
function abs(x) {
            if (typeof x != 'number'){
                throw 'Not a number';
            }
            for (let i =0; i < arguments.length; i++){
                console.log(arguments[i]);
            }
            if (x >= 0){
                return x;
            } else {
                return -x;
            }
        }
```

`arguments`包含所有的参数，如果使用多余的参数进行附加操作，需要排除已有参数

### 1.2 变量的作用域

> 规范

将自己代码全部放入自己定义的唯一空间名字中。（减少全局命名冲突冲突的问题）

```javascript	
//唯一全局变量
var chen = {};
//定义全局变量
var chen.add = function(a,b) {
    return a+b;
}
```

> 常量 const

### 1.3 方法



### 1.3 闭包



### 1.4 箭头函数



### 1.5 创建对象



### 1.6 class继承（新特性）



### 1.7 原型链继承（难）



## 2 常用对象

## 3 操作Dom元素

## 4 操作Dom元素



