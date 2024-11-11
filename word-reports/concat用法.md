
# concat 用法

一直只是知道 concat  是拼接数组，但是但对于其返回值和参数具体要求是什么，一直没有清晰的认识，所以特意查了一下文档，如果能立刻得出下面代码的结果，那就不需要看这篇笔记了

```js
var arr = [1];
arr.concat() === arr;  // ?

[1].concat(2);
[1].concat([2], 3);
[1].concat([[2]]);

var arrB = [];
arrB[2] = 3;
[1].concat(arrB);

Array.prototype.concat.call([1], 2);
Array.prototype.concat.call(1, [2]);
Array.prototype.concat.call(1, {1:1, 2:2});

```

concat 不会修改原数组与参数，每次都会返回新数组，如果没有参数，则会返回原数组的浅拷贝。
即
```js
var arr = [1];
arr.concat() === arr; // false
```


## 执行过程

- 首先创建新数组；
- 使用调用他的对象中的元素将新数组填充；
- 依次将参数执行以下操作；
  - 如果参数是 `[Symbol.isConcatSpreadable]` 属性为真的数组或类数组，则会打平填充，**不会递归打平**；
  - 否则直接填充；
- 返回新数组；

如果源数组或参数数组中有稀疏数组即不连续数组，新数组中会保留空(empty)。

```js
[1 ,,3].concat([, 4]);  // [1, Empty, 3, Empty, 4]
```

::: details 此方法是通用的数组方法。

<!--@include: ./通用数组方法.md-->
:::


this 值和参数会执行相同的判断，除了一点，this 会先转为对象，再执行数组填充

```js
Array.prototype.concat.call(1, [2]); // [Number {1},  2]

```

## [Symbol.isConcatSpreadable] 特性

如果数组或类数组的 `[Symbol.isConcatSpreadable]` 属性为真，则会打平填充，否则不会被打平；

```js
var arr = [1];
arr[Symbol.isConcatSpreadable] = false;
arr.concat([2, [3]]); // [[1], 2, 3]

var fakeArr = {
  0: 1,
  2: 3,
  length: 3,
  [Symbol.isConcatSpreadable]: true,
};

[1].concat(fakeArr); // [1, 1, empty, 3]


```

## String.prototype.concat 

可以接受多个参数，效果与字符串的 + 操作符相似，用于拼接字符串，不同之处是 + 操作符会将参数转为基本类型然后转为字符串，而 concat 会直接转为字符串。

```js
var a = {
  toString() {
    return 1;
  },
  valueOf() {
    return 2;
  },
}

"" +  a;  // "2"

"".concat(a);  // "1"

```



## 本文中的 vitepress 和 md 特殊方法


```md
::: details 此方法是通用的数组方法。
<!-- detail 折叠 内容 -->
:::
```
::: raw
\<!--@include:./通用数组方法.md--\>
:::









