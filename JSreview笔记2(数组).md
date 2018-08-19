# JS复习笔记2（数组）

将数组长度设为0之后，会删除数组所有元素

```js
var arr = ['h', 'q', 'y', '', '', 'j', '', ''];
console.log(arr.length);
arr.length = 0; 
console.log(arr);//空数组[]
```

### 添加元素：

```js
var arr = ['h', 'q', 'y', 'j'];
arr[4] = 'five'; //指定索引，添加元素
arr.push('one');//在末尾添加元素
arr.push('two_1', 'two_2');
arr.unshift('first');//在开头添加元素
arr.unshift('first_1', 'first_2');//两个元素一次加入
```

### 删除元素

```js
var arr = ['h', 'q', 'y', 'j'];
delete arr[2]; //删除一个指定元素，注意和下面的区别
console.log(arr);
arr.pop();//删除最后一个元素
console.log(arr); 
arr.shift();//删除第一个元素
console.log(arr); 
delete arr[0]; //删除一个指定元素
console.log(arr);
```

### 数组方法

join()：数组中的元素转换成字符串并连接在一起；默认是逗号(,)连接，可以指定连接符号；

```js
var students = [
                ['张三', 20],
                ['李四', 21],
                ['王五', 22],
                ['小六', 23]
            ];
console.log(students.join());//默认以逗号连接
console.log(students.join('|'));//指定以|连接
```

reverse()：把数组中的元素顺序反转；

sort()：对数组中的元素排序并返回排序后的值；
没有参数时按字母排序，会把元素转换成字符串；

```js
var a = [1, 23, 9, 12, 80];
a.sort(function (a,b) {
    /* 从小到大，a在前面，返回负值 */
    // return a-b;
    /*从大到小*/
    return b-a;
});
console.log(a);
```

concat()：数组连接，连接后返回一个新数组

slice()：截取数组，两个参数，指定开始和结束位置
参数支持负数，表示从后面往前面数，第一个-1, 依次-2,-3...；

```js
var a = ['h', 'q', 'y', 'j'];
console.log(a.slice(0, 2));
console.log(a.slice(2, 2));//[]
console.log(a.slice(2));//
console.log(a.slice(-2));
console.log(a.slice(-2, -1));
console.log(a.slice(-2, -3));//[]
```

splice()：插入、删除元素的通用方法，哎哟，这么牛逼，好怕；
感觉插入、删除元素的其他方法可以去死了；
会直接修改元数组
参数1：操作起始位置；
参数2：操作元素个数，为空表示到结尾，为0表示插入元素，大于0表示替换元素；<br>
参数n：新的元素，代表要插入的元素

```
var a = ['h', 'q', 'y', 'j'];
a.splice(2); //从下标2开始删除
console.log(a);
a.splice(2, 0, 1, 2, 3);//从下标2开始添加元素
console.log(a);
a.splice(2, 1, 'y', 'j');//从下标2开始添加元素
console.log(a);
a.splice(1, 0, ['H5', '嵌入式']);//这里插入数组元素会怎么样那？
console.log(a);
```

toString():将数组的所有元素转换成字符串，并用逗号连接起来并输出;

join();



### 数组新方法

forEach():遍历数组元素，并调用指定的函数；
forEach调用的函数的三个参数依次为数组元素、元素索引、数组本身
forEach不支持break；

```js
var a = ['h', 'q', 'y', 'j'];
//打印每一个元素
a.forEach(function (value) {
    console.log(value);
});
//修改每一个元素的值
a.forEach(function (value, i, arr) {
    arr[i] = value + arr[i+1];
});
console.log(a);
```

map():类似forEach，为每个元素调用指定函数，该操作返回一个新数组，不会修改原始数组

```js
var a = ['h', 'q', 'y', 'j'];
var b = a.map(function (v) {
    return v + v;
});
console.log(a);
console.log(b);
```

filter():返回数组的子集，是否返回当前元素是根据调用的函数来判断的

```js
var a       = [1,2,23,34,5,6,78,98,9];
var oddnum  = evennum = [];
//奇数
oddnum = a.filter(function(v) {
    return v%2!=0;
});
//偶数
evennum = a.filter(function(v) {
    return v%2 == 0;
});
console.log(a);
console.log(oddnum);
console.log(evennum);
```

every()和some():对数组的所有元素执行函数检查; 区别：
every()：当每个元素都返回true是才返回true；
some()：当有一个元素都返回true就返回true；

```js
var a       = [1,2,23,34,5,6,78,98,900];
var oddnum  = evennum = 0;
//检查是不是都小于100
oddnum = a.every(function(v) {
    return v < 100;
});
//至少有一个大于100
evennum = a.some(function(v) {
    return v > 100;
});
console.log(oddnum); //false
console.log(evennum); //true
```

reduce和reduceRight（从后向前）：使用指定的函数对数组元素进行组合，生成一个值；
参数1：要执行的函数，有返回值；
参数2：传递给函数的默认值，可忽略

```js
var a       = [1,2,23,34,5,6,78,98,900];
//求和，默认值为0
//运算过程：
var n = a.reduce(function (x, y) {
    return x + y;
}, 0);
console.log(n);

//求积
var m = a.reduce(function (x, y) {
    return x*y;
} ,1);
console.log(m);
//求最大值，可以不设置默认值
var max = a.reduce(function (x, y) {
    return x>y?x:y;
});
console.log(max);
```

indexOf()和lastIndexOf：搜索指定的元素并返回其索引，不存在返回-1

传入值 返回下标  lastindexof返回倒着的下标

```js
var a       = [1,2,23,34,5,6,78,98, 23,900];
var n = a.indexOf(23);//返回下标2
console.log(n);
var m = a.indexOf(23, 3);//从下标3开始搜索，返回下标8
console.log(m);
var p = a.lastIndexOf(23);//返回下标8
console.log(p);
```

### 将字符串看做数组操作

```js
var str = 'hqyjhyn';
    console.log(str[4]); //charAt()：指定位置的字符
    console.log(str.charAt(4));//中括号的方式访问起来更方便
	//数组的方法可以劫持过来使用在字符串上，这就很帅了；
    //劫持数组的方法来使用
    var b = Array.prototype.map.call(str, function (v) {
        return v+v;
    });
    console.log(str);
    console.log(b);
```