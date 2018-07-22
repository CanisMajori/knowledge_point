call bind apply

在JS中，这三者都是用来改变函数的this对象的指向的，他们有什么样的区别呢。在说区别之前还是先总结一下三者的相似之处：

1. 都是用来改变函数的this对象的指向的。
2. 第一个参数都是this要指向的对象。
3. 都可以利用后续参数传参。

例子1：

```js
var xw={
    name: "小王",
    gender: "男",
    age: 24,
    say: function(){
        alert(this.name+" , "+this.gender+" ,今年"+this.age);
    }
}
var xh={
    name: "小红",
    gender: "女",
    age: 18
}
xw.say();
```

本身没什么好说的，显示的肯定是小王 ， 男 ， 今年24。那么如何用xw的say方法来显示xh的数据呢：：：：

```js
xw.say.call(xh);//使用say方法，改变了this指向 小红，
xw.say.apply(xh);
xw.say.bind(xh)();
```

如果直接写xw.say.bind(xh)是不会有任何结果的。call和apply都是对函数的直接调用，而bind方法返回的仍然是一个函数，因此后面还需要再加一个()来进行调用

例子2

```js
var xw={
    name: "小王",
    gender: "男",
    age: 24,
    say: function(school,grade){
        alert(this.name+" , "+this.gender+" ,今年"+this.age+" ,在"+school+"上"+grade);
    }
}
var xh={
    name: "小红",
    gender: "女",
    age: 18
}
```

可以看到say方法多了两个参数，我们通过call/apply的参数进行传参。

```js
xw.say.call(xh,"实验小学","六年级");   //call，参数要一个一个写出来
xw.say.apply(xh,["实验小学","六年级"]);	//apply后续参数要以数组形式表示
xw.say.bind(xh,"实验小学","六年级")();		//bind的两个括号都可以传参数；
xw.say.bind(xh)("实验小学","六年级");
```

