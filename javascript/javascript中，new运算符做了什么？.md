## javascript中，new运算符做了什么？

首先，我们来看一下它们的语法和概述：
> [new](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/new "new")

**语法**：new constructor[([arguments])]

**参数**：
	
- 构造函数(constructor)：一个指定对象实例的类型的函数。
- 传参(arguments)：一个用来被构造函数调用的参数列表。

**概述**：创建一个用户定义的对象类型的实例或具有构造函数的内置对象类型之一。

当代码 new foo(...) 执行时，new的执行步骤：

1. 创建一个新对象，并将这个对象的_proto_指向构造函数foo的prototype
2. （如果有参数，传参并）执行构造函数foo，同时this会指向这个新的实例。如果没有参数new foo等同new foo()
3. 如果构造函数返回了一个对象，那么这个对象会取代new出来的对象，反之，会返回步骤1中创建的对象

> 举个栗子：

    function Fruits(price) {
		this.price = price;
    }
    
    Fruits.expiryDate = '2018-03-21';
    Fruits.prototype.type = 'Fruits';
    
    var apple = new Fruits(3.5);

用代码来实现上述代码中 new Fruits(3.5) 中new的执行步骤：

    var obj = {};                                          // 创建新对象

    obj._proto_ = Fruits.prototype;                        // 将这个对象的_proto_指向Fruits的prototype
    
    var res = Fruits.call(obj, 3.5);                       // 执行构造函数foo，同时this会指向这个新的实例
    
    return typeof res === 'object' ? res : obj;            // 如果构造函数返回了一个对象，那么这个对象会取代new出来的对象，反之，会返回步骤1中创建的对象

> 明白了new的原理，现在来看看代码里面要怎么去使用：

    function car(make, model, year) {
       this.make = make;
       this.model = model;
       this.year = year;
    }

在创建2个实例：

    var potatoCar = new car("Fiat", "500c", 2010);
    var pandaCar = new car("Geely", "yuanjing x1", 2017);

    alert(potatoCar.make);         // "Fiat"
    alert(pandaCar.make);          // "Geely"

如果想同时给这两个实例添加同一属性：

    car.prototype.color = "blue";

    alert(pandaCar.color);         // "blue"
    alert(potatoCar.color);        // "blue"
