## 关于call和apply

call和apply这两个方法的极为相似，唯一的区别在于传参不同
> [call](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/call "call")

**语法**：fun.call(object[, arg1[, arg2[, ...]]])
> [apply](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply "apply")

**语法**：fun.apply(object, [argsArray])

**参数**：
	
- object：在fun运行时this指向的值。需要注意的是，object并不一定是该函数执行时真正的this值。如果这个函数处于非严格模式下，object为null和undefined时，this值会自动指向全局对象(浏览器中就是window对象)，同时值为原始值(数字，字符串，布尔值)的this会指向该原始值的自动包装对象。。
- arg是传入fun的传参(arguments)。

**概述**：在调用一个存在的函数时，你可以为其指定对象，使this指向该对象。 this 指当前对象，你可以只写一次这个方法然后在另一个对象中继承它，而不用在新对象中重复写该方法。

> 举个栗子，瞅瞅它们的基本用法 ：

    var apple = {};

    function fruit(name) {
        this.name = name;
    }

    function appleCall() {
        // fruit中的this指向apple
        fruit.call(apple, "appleCall")
    }

    appleCall();
    console.log(apple.name);                 // appleCall

    function appleApply() {
        // fruit中的this指向apple
        fruit.apply(apple, ["appleApply"])
    }

    appleApply();
    console.log(apple.name);                 // appleApply

> 再举个栗子，瞅瞅它们使用场景 —— 继承：


    function Food(name, price) {
        this.name = name;
        this.price = price
    }

    function Fruit(name, price, unit) {
        this.unit = unit;
        Food.apply(this, [name, price]);                    // 相当于Food.call(this, name, type)
    }

    let apple = new Fruit("apple", "3块", "个");

    console.log(apple.name + apple.price + 1 + apple.unit);  // apple3块1个

> 再举个栗子，瞅瞅它们更多的使用场景 —— 多重继承：

    function Food(name, price) {
        this.name = name;
        this.price = price;
    }

    function Fruit(isPeel) {
        this.isPeel = isPeel;
    }

    function TropicalFruit(name, price, isPeel) {
        Food.apply(this, [name, price]);                       // 相当于Food.call(this, name, price);
        Fruit.apply(this, [isPeel]);                           // 相当于Food.call(this, isPeel);
    }

    let mango = new TropicalFruit('mango', '8块', false);

    console.log(mango);                                        // {name: "mango", price: "8块", isPeel: false}

**总结：关于call跟apply，唯一的区别就是传参方式不同。call和apply的作用是将调用该方法的函数上下文指向传入的对象（如果该对象在当前作用域存在）**
