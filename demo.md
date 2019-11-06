

### 数组

* `Array.isArray()` : 判断数组
* `Array.from()` : 从一个类数组或可迭代对象重生成一个浅拷贝数组实例
* `Array.of()` : 创建一个具有可变数量参数的新数组实例
```javascript
Array.of(7);       // [7] 
Array.of(1, 2, 3); // [1, 2, 3]

Array(7);          // [ , , , , , , ]
Array(1, 2, 3);    // [1, 2, 3]
```
* `Array.prototye.concat()` : 用于合并两个或多个数组。此方法不会更改现有数组，而是返回一个新数组。返回一个浅拷贝（引用）。
* `Array.prototype.entries()` : 返回一个新的 `Array Iterator` 对象，该对象包含数组中每个索引的键/值对
```javascript
// 二维数组按行排序
function sortArr(arr) {
  var goNext = true;
  var entries = arr.entries();
  while (goNext) {
    var result = entries.next();
    if (result.done !== true) {
      // 排序算法可以按照内容进行修改
      result.value[1].sort((a, b) => a - b);
      goNext = true;
    } else {
      goNext = false;
    }
  }
  return arr;
}

var arr = [[1,34],[456,2,3,44,234],[4567,1,4,5,6],[34,78,23,1]];
sortArr(arr);
=>
[
  [1,34],
  [2,3,44,234,456],
  [1,4,5,6,4567],
  [1,23,34,78]
]
```
* `Array.prototype.every()` : 测试数组内的所有元素是否都能通过某个指定函数的测试
* `Array.prototype.some()` : 测试数组内是不是至少有1个元素通过指定函数的测试
* `Array.prototype.fill()` : 用来填充数组的值
```javascript
// 初始化数组元素
var a = Array(5);
console.log(a); // [empty × 5]
a.fill(0, 0); // [0, 0, 0, 0, 0]
```
* `Array.prototype.filter()` : 创建一个数组，返回通过所提供函数的条件的所有元素
* `Array.prototype.map()` : 创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果
* `Array.prototype.reduce()` : 对数组中的每个元素执行一个由您提供的reducer函数(升序执行)，将其结果汇总为单个返回值
```javascript
// 叠加
var sum = [0, 1, 2, 3].reduce(function (accumulator, currentValue) {
  return accumulator + currentValue;
}, 0); // 6

// 数组扁平化
var flattened = [[0, 1], [2, 3], [4, 5]].reduce(function(a, b) {
  return a.concat(b);
}, []);
// flattened is [0, 1, 2, 3, 4, 5]

// 数组去重
var myArray = ['a', 'b', 'a', 'b', 'c', 'e', 'e', 'c', 'd', 'd', 'd', 'd'];
var myOrderedArray = myArray.reduce(function (accumulator, currentValue) {
  if (accumulator.indexOf(currentValue) === -1) {
    accumulator.push(currentValue);
  }
  return accumulator
}, [])
```
* `Array.prototype.reduceRight()` : 接受一个函数作为累加器（accumulator）和数组的每个值（从右到左）将其减少为单个值
```javascript
[[0, 1], [2, 3], [4, 5]].reduceRight(
  (accumulator, currentValue) => accumulator.concat(currentValue)
); // [4, 5, 2, 3, 0, 1]
```
* `Array.prototype.flat()` : 返回一个指定深度递归的数组，并将所有元素与遍历到的子数组元素合并成一个新数组返回
```javascript
[1, 2, [3, 4, [5, 6]]].flat(); // 默认递归深度为 1
// [1, 2, 3, 4, [5, 6]]

[1, 2, [3, 4, [5, 6, [7, 8, [9, 10]]]]].flat(Infinity); // 完全扁平化
```
* `Array.prototype.flatMap()` : 使用映射函数映射每个元素，然后将结果压缩成一个新数组。它与 `map` 连着深度值为 `1` 的 `flat` 几乎相同
* `Array.prototype.join()` : 将一个数组（或一个类数组对象）的所有元素连接成一个字符串并返回这个字符串
* `Array.prototype.keys()` : 返回一个包含数组中每个索引键的 `Array Iterator` 对象
* `Array.prototype.values()` : 返回一个新的 `Array Iterator` 对象，该对象包含数组每个索引的值
* `Array.prototype.reverse()` : 将数组中元素的位置颠倒，并返回该数组，该方法会改变原数组
* `Array.prototype.shift()` : 删除数组第一个元素，并返回该元素的值，会改变原数组
* `Array.prototype.pop()` : 删除数组最后一个元素，并返回该元素的值，会改变原数组
* `Array.prototype.slice()` : 返回一个新的数组元素，`end < 返回数组 <= begin`，返回包括 begin 不包括 end 的原数组的浅拷贝，原数组不会变化
* `Array.prototype.splice()` : 通过删除或替换现有元素或者原地添加新的元素来修改数组，并以数组形式返回被修改的内容。此方法会改变原数组
```javascript
// ["angel", "clown", "drum", "sturgeon"]
['angel', 'clown', 'drum', 'mandarin', 'sturgeon'].splice(3, 1);
```
* `Array.prototype.find()` : 返回数组中满足条件的（所提供函数）的第一个元素的值
* `Array.prototype.findIndex()` : 返回数组中满足提供的测试函数的第一个元素的索引

### 字符串

* `String.prototype.slice()` : 提取某个字符串的一部分，并返回一个新的字符串，且不会改动原字符串
* `String.prototype.split()` : 使用指定的分隔符字符串将一个 `String` 对象分割成子字符串数组，以一个指定的分割字串来决定每个拆分的位置
* `String.prototype.charAt()` : 从一个字符串中返回指定的字符，如第一个字符 `'Hello'.charAt(0) => 'H'`
* `String.prototype.substring()` : 返回一个字符串在开始索引到结束索引之间的一个子集, 或从开始索引直到字符串的末尾的一个子集
* `String.prototype.trim()` : 字符串两端删除空白字符，类似方法还有 `String.prototype.trimLeft()` 和 `String.prototype.trimRight()`
* `String.prototype.startsWith()` : 用来判断当前字符串是否以另外一个给定的子字符串开头，支持两个参数，一个是要搜索的字符串，一个是开始搜索的位置