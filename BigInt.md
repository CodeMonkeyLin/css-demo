## BigInt
> BigInt 是一种内置对象，可以表示大于 2的53次方 的整数。而在Javascript中，Number 基本类型可以精确表示的最大整数是 2的53次方。BigInt 可以表示任意大的整数。
### 问题
JS 中的Number类型只能安全地表示-9007199254740991 (-(2^53-1)) 和9007199254740991(2^53-1)之间的整数，任何超出此范围的整数值都可能失去精度。
```js
const maxInt = Number.MAX_SAFE_INTEGER;

console.log(maxInt + 1);        

console.log(maxInt + 2);     
```
>JS 提供Number.MAX_SAFE_INTEGER常量来表示 最大安全整数，Number.MIN_SAFE_INTEGER常量表示最小安全整数：

### 解决
```js
const previousMaxSafe = BigInt(Number.MAX_SAFE_INTEGER);
// ↪ 9007199254740991n

const maxPlusOne = previousMaxSafe + 1n;
// ↪ 9007199254740992n
console.log(maxPlusOne);
const theFuture = previousMaxSafe + 2n;
// ↪ 9007199254740993n, this works now!
console.log(theFuture)
```
### 语法
```js
BigInt(value);
```
或者在整数的末尾追加n即可

### 类型信息
```js
typeof 1n === 'bigint'; // true
typeof BigInt('1') === 'bigint'; // true
```
###比较
BigInt 和 Number 不是严格相等的，但是宽松相等的。
```js
0n === 0
// ↪ false

0n == 0
```
Number 和 BigInt 可以进行比较。
```js
1n < 2
// ↪ true

2n > 1
// ↪ true

2 > 2
// ↪ false

2n > 2
// ↪ false

2n >= 2
// ↪ true
```
### 注意点
```js
25 / 10;      // → 2.5
25n / 10n;   

BigInt("10");    // → 10n
BigInt(10);      // → 10n
BigInt(true);    // → 1n

BigInt(10.2);     // → RangeError
BigInt(null);     // → TypeError
BigInt("abc");    // → SyntaxError

1n + 1
```
BigInt 不能与 Number类型互相运算

## 参考
https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/BigInt