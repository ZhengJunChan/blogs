## in和hasOwnProperty的共同点和区别

首先，我们来看一下它们的语法和概述：
> [in](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/in "in")

语法：key in objectName

概述：如果指定的属性存在于指定的对象中，则 in 运算符会返回 true。
 
> [hasOwnProperty](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty "hasOwnProperty")

语法：obj.hasOwnProperty(key)

概述：所有继承了 Object 的对象都会继承到 hasOwnProperty 方法。这个方法可以用来检测一个对象是否含有特定的自身属性；和 in 运算符不同，该方法会忽略掉那些从原型链上继承到的属性。

> 举个栗子，看看他们的共同点

    var arr = ['a', 'b'],
	    obj = {
	        a: 'a',
	        b: 'b'
	    };

    // in
    console.log('1 in arr:' + (1 in arr));        //true
    console.log('"a" in arr:' + ('a' in arr));    //false
    console.log('1 in obj:' + (1 in obj));        //false
    console.log('"a" in obj:' + ('a' in obj));    //true
    
    // hasOwnProperty
    console.log('arr.hasOwnProperty(0):' + arr.hasOwnProperty(0));      //true
    console.log('arr.hasOwnProperty("a"):' + arr.hasOwnProperty('a'));  //false
    console.log('obj.hasOwnProperty(0):' + obj.hasOwnProperty(0));      //false
    console.log('obj.hasOwnProperty("a"):' + obj.hasOwnProperty('a'));  //true

从上面的栗子中我们可以看出，key指的是对象的索引，in和hasOwnProperty都能检查对象是否含有指定属性。

> 再举个栗子，看看它们的区别

    function Fruits(price) {
		this.price = price;
    }
    
    Fruits.expiryDate = '2018-03-21';
    Fruits.prototype.type = 'Fruits';
    
    var apple = new Fruits(3.5);
    
    console.log(apple);
    console.log('type' in apple);               //true
    console.log(apple.hasOwnProperty('type'));  //false
    console.log('price' in apple);              //true
    console.log(apple.hasOwnProperty('price')); //true

打印apple出来看：

    Fruits {
	    price: 3.5,
	    __proto__: {
		    type: "Fruits",
		    constructor: function Fruits(price),
		    __proto__: Object
	    }
    }

从apple的结构我们可以看出，in能访问到__proto__对象下的属性，而hasOwnProperty不能访问到。

**总结：综上所述，in和hasOwnProperty都可以访问对象下面的属性，且访问方式是以索引的方式，in能访问_proto_对象下的属性，但hasOwnProperty却不能**