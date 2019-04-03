# javascriptbasic3
1.1.关于this的指向
1.1.1.全局上下文
所有函数外部的this是全局上下文，代表的是window
1.1.2.函数上下文
对象方法中的this指的是该方法所属的对象

1.1.3.构造函数中
当一个函数被作为构造函数使用时（前面加new关键字），new关键字会让this的指向改变，并让其成为当前函数的返回值
this指的是通过构造函数创建的对象。
1.2.批量创建对象
1.2.1.工厂模式创建对象
为什么要优化创建对象的方式
因为对象在项目中被大规模的使用，所以每一点小小的改进都会对项目整体效率带来很大的提升，现阶段同学们还不可能有深刻的体会，只是让大家了解一下，后面讲项目大家自然就明白了。
工厂模式创建对象
同类型对象，只是一些属性的值不同，通过对象字面量创建对象每次都要写那么多东西很费劲，我们可以将创建对象的过程封装进一个函数，只把发生变化的属性作为参数传入，从而简化对象创建的过程。
但是工厂模式只是创建出来一个普通的对象并将其返回，因此无法判断实例的具体类型。

function createStudent(name, age, sex, score) {
    var stu = new Object();
    stu.name = name;
    stu.age = age;
    stu.sex = sex;
    stu.score = score;
    stu.sayHi = function () {
        console.log("大家好，我是" + this.name);
    };
    return stu;
}
var s1 = createStudent("zs", 18, 1, 90);
var s2 = createStudent("ls", 20, 0, 100);


1.2.2.构造函数创建对象
@this和new
利用new 关键字可以声明新的对象。new 关键字可以让构造函数中this的指向改变，并让构造函数把this返回。
构造函数:
构造函数也是函数，只不过构造函数的目的是为了创建新对象，为新对象进行初始化(设置对象的属性、方法)。
function Student(name, age, sex, score) {
    this.name = name;
    this.age = age;
    this.sex = sex;
    this.score = score;
    this.sayHi = function () {
        console.log("大家好，我是" + this.name);
    };
}
var s2 = new Student("ls", 20, 0, 100);

new 关键字可以让构造函数中this的指向改变。this指的是，通过当前构造函数创建的对象（s2）。
Student：类（一类事物，学生这一类事物）

构造函数创建对象:
通过构造函数创建对象更方便（不需要创建对象并返回）。更重要的是可以通过instanceof来判断实例的类型了。
//A instanceof B A是不是一个通过B创建出来的实例
console.log(s2 instanceof Student);//true

实例，也叫对象。

1.3.基本类型和复杂类型
1.3.1.分类
简单数据类型（值类型、基本数据类型）：直接存储值
number、string、boolean、undefined、null
复杂数据类型（引用类型）：存储引用
object
1.3.2.基本类型的复制

在栈中复制一份变量值，然后赋值给num2；
1.3.3.复杂类型的复制

将栈中存储的地址值复制一份，赋值给p2。
但是这俩地址是一样的，都指向的是同一个堆中的对象。
1.3.4.基本类型参数

第一步，传递参数

此时f1的形参num的值是50；
第二步，执行方法内部代码num=60;

此时形参num的值是60；
此时实参num的值没变，还是50；

总结：值类型作为参数，修改形参值后，不会影响实参值。因为值类型作为参数，是将值复制一份给形参。


1.3.5.复杂类型参数

具体逻辑如下：



总结：引用类型作为参数，修改形参值后，会影响实参值。因为引用类型作为参数，虽然讲地址复制一份传给形参，但是指向的都是同一个堆中的对象。

1.4.数组的方法
1.4.1.转换数组
valueOf() //返回数组对象本身
var arr = [1, 2, 3, 4, 5]; 
    console.log(arr);//[1, 2, 3, 4, 5]
    console.log(arr.valueOf());//[1, 2, 3, 4, 5]
    
arr.valueOf()相当于arr。

toString() //把数组转换成字符串
console.log(arr.toString());//1,2,3,4,5

join() //把字符串中的每一项进行拼接
console.log(arr.join());//1,2,3,4,5
console.log(arr.join("-"));//1-2-3-4-5
console.log(arr.join(""));//12345

join()方法内部实现原理：
var arr = ["刘备", "张飞", "关羽"];
function join(arr, sep) {
    var str = arr[0];
    for (var i = 1; i < arr.length; i++) {
        str = str + sep + arr[i];
    }
    return str;
}
console.log(join(arr, "|"));


1.4.2.检测数组
arr instanceof Array

Array.isArray() //ES5方法，低版本浏览器不兼容

console.log(arr instanceof Array);//true
console.log({} instanceof Array);//false
console.log(Array.isArray(arr));//true
console.log(Array.isArray({}));//false

1.4.3.数组的增删方法
从后边增删：push()、pop()   
从前面增删：unshift() 、shift()  
var arr = [1, 2, 3, 4, 5];
console.log(arr);
console.log(arr.push(0));//从后面添加元素 返回新数组的长度
console.log(arr.pop());//从后面删除元素 返回被删除的元素
console.log(arr.shift());//从前面删除元素 返回被删除的元素
console.log(arr.unshift(0));//从前面添加元素 返回新数组的长度

1.4.4.数组反转
reverse() //翻转数组
var arr = ["a", "b", "c", "d"];
console.log(arr.reverse());

反转原理：
function reverse(arr) {
    var newArr = [];
    for (var i = arr.length - 1; i >= 0; i--) {
        newArr.push(arr[i]);
    }
    //console.log(newArr);
    return newArr;
}
console.log(reverse(arr));

第二种方式：
function reverse(arr) {
    for (var i = 0; i < arr.length / 2; i++) {
        //0 arr.length-1-0
        //1 arr.length-1-1
        //2 arr.length-1-2
        //i arr.length-1-i
        var temp = arr[i];
        arr[i] = arr[arr.length - 1 - i];
        arr[arr.length - 1 - i] = temp;
    }
    //console.log(arr);
    return arr;
}

1.4.5.数组迭代方法filter
迭代方法 （ES5中的新方法，不会修改原数组）
every()、filter()、forEach()、map()、some()

这里主要介绍filter，过滤：
 //工资的数组[1500,1200,2000,2100,1800]把工资大于等于2000的删除
    var arr = [1500, 1200, 2000, 2100, 1800];
    console.log(arr);
//    迭代方法：filter，过滤。迭代：会遍历当前数组每个元素（迭代相当于遍历）
    //filter(参数function：此方法用于定义过滤规则)
//filter不会对数组本身过滤，会将过滤结果作为新数组返回
    var newArr = arr.filter(function (element, index, array) {
        //console.log(element);//当前迭代的元素
        //console.log(index);//当前迭代索引
        //console.log(array);//当前数组
        if (element > 2000) {
            return false;//删除该元素
        }

        return true;//保留该元素
    });
    console.log(newArr);

1.4.6.数组位置
indexOf()  //寻找指定项目在数组中的位置
lastIndexOf()   //如果没找到返回-1

indexOf(searchElement,fromIndex)
indexOf(“a”,fromIndex);  a为要查找的元素。fromIndex是从哪开始找（包含fromIndex本身）
lastIndexOf(“a”,fromIndex);参数与indexOf一样。

//["c", "a", "z", "a", "x", "a"]找到数组中第一个a出现的位置
//["c", "a", "z", "a", "x", "a"]找到数组中最后一个a出现的位置
var arr = ["c", "a", "z", "a", "x", "a"];
console.log(arr.indexOf("a"));//1
console.log(arr.lastIndexOf("a"));//5

第一个参数：searchElement，搜索的元素
第二个参数：fromIndex，从哪个索引开始找。（注意：包含fromIndex）
这个包含fromIndex也好理解，也好记忆。如果我们调用indexOf(“c”)，不传第二个参数，默认从0开始找，那我找的是第0个的元素c，如果不包含fromIndex，肯定找不到。找不到的话，这个方法设计的就有问题了。
1.4.7.练习-统计元素出现的次数
要求：["c", "a", "z", "a", "x", "a"]获取数组中每个元素出现的次数
结果：c:1 a:3 z:1 x:1  以这种形式输出

//["c", "a", "z", "a", "x", "a"]获取数组中每个元素出现的次数
var arr = ["c", "a", "z", "a", "x", "a"];
var o = {};// c:1 a:3 z:1 x:1
for (var i = 0; i < arr.length; i++) {
    var item = arr[i];
    if (o[item]) {
        o[item] = o[item] + 1;
    } else {
        o[item] = 1;
    }
}
console.log(o);
for (var k in o) {
    console.log(k + "出现了" + o[k] + "次");
}

首先确定，存储的数据格式为键值对：c:1 a:3 z:1 x:1，所以确定用对象存储。
注意：这里的o[item]，是操作对象属性的第二种方式 对象[“属性名”]。
这里为什么item不用加双引号，是因为item是变量，而不是字符串。

1.4.8.数组其他方法
1.4.8.1.slice()
 slice():从数组中截取一部分内容。
 var arr = [4, 6, 7, 8, 3, 46, 8];
    console.log(arr);
//    1开始 2结束 [start,end) 开始能取到 结束取不到
    console.log(arr.slice(0, 2));//slice 不会改变原数组

1.4.8.2.splice()
splice()：删除或替换数组中的一部分
//1开始 2个数 3要加入的元素
console.log(arr.splice(0, 2));//会对原数组进行修改

注意第二个参数是：个数
1.4.8.3.forEach()
forEach()遍历数组：
var arr = [4, 6, 7, 8, 3, 46, 8];
for (var i = 0; i < arr.length; i++) {
    console.log(arr[i]);
}
arr.forEach(function (e) {//e代表当前元素
    console.log(e);
});
//1.当前元素；2.当前索引；3.当前数组
arr.forEach(function (element, index, array) {
    console.log(element);
    console.log(index);
    console.log(array);
});

1.4.8.4.如何清空数组
清空数组的最简单方式？
arr = [];

其他两种方式：arr.splice(0,arr.length);
		     arr.length = 0;
1.5.补充知识点
1.5.1.函数、工厂函数、构造函数的区别？
函数：
function fn() {
    console.log("表示很多代码");
    console.log("做了很多事情");
}
函数就是封装了一段普通的逻辑。

工厂函数 : 可以传入不同参数，返回相同类型对象的函数。
工厂模式：批量创建对象的模式。
function createStudent(name, age, sex, score) {
    var stu = new Object();
    stu.name = name;
    stu.age = age;
    stu.sex = sex;
    stu.score = score;
    stu.sayHi = function () {
        console.log("大家好，我是" + this.name);
    };
    return stu;
}
工厂函数，是用来批量创建对象的。他是用来创建对象的普通函数。


构造函数：
function Student(name, age, sex, score) { 
    this.name = name;
    this.age = age;
    this.sex = sex;
    this.score = score;
    this.sayHi = function () {
        console.log("大家好，我是" + this.name);
    }; 
}
构造函数，是专门用来创建对象的，并且默认返回this。内部的逻辑，仅仅就是给属性、方法赋值。
调用时，构造函数必须使用new Student();
函数和工厂函数，都是普通函数，所以直接调用即可。
1.5.2.对象与构造函数？
对象：万物皆为对象，人，电脑，自行车等等。
构造函数，是用来创建对象的。

function Student(name, age, sex, score) { 
    this.name = name;
    this.age = age;
    this.sex = sex;
    this.score = score;
    this.sayHi = function () {
        console.log("大家好，我是" + this.name);
    }; 
}

利用构造函数，创建对象：
var s = new Student("ls", 20, 0, 100);
这里的s就是对象，属于Student对象。
这个Student我们可以理解为类，Student类，表示一类事务，表示所有学生。
而s就是一个学生，一个对象，一个Studeng学生实例。

使用new Function构造函数的方式创建的实例都是对象。

1.5.3.js中的方法，怎么知道需不需要参数传递？  ***
1.5.3.1.普通情况
看webstorm的提示（参数提示：ctrl+P）

将光标，放到方法括号内，按下快捷键：ctrl+p

中括号内部的第一块内容是参数类型（可能是Number，string等），第二块内容是optional可选，代表当前参数可以不传
第一个参数：start开始索引
第二个参数：end结束索引

无参数：

如果是无参数，则会提示无参数。
1.5.3.2.泛型与可变参数
泛型”T”：代表任意数据类型
可变参数”…”：参数个数可变，可以不传，也可以传多个

中括号中的…代表的是可变参数。
T代表的是参数类型不确定，可指任意数据类型。
那既然参数类型可以任意写，并且可以传多个参数，那么如下：
console.log(arr.push(0, "abc", true));

再看indexOf()方法：

这里的参数searchElement类型也是T，说明我们可以查找任意数据类型的元素。
比如”a”、1、false

1.5.4.写代码不要强制写，根据webstorm提示写
js的方法，方法名是安装驼峰命名法定义的。js.indexOf();O必须大写。（注意，这里不要自己强制写代码，要根据代码提示写）

出现代码提示时，敲回车即可，根据代码提示写点，可以大大降低错误率。

1.5.5.typeof null 是object的解释
爱民是按照他的理解来讲解，而不是按照spec来照本宣科的，况且他写绿皮书时ES5/ES6还没有出来，而ES5之前的ES规范其实都写得比较烂。
你也发现他是以typeof运算符的返回值作为“基础类型”。这是站在语言使用者的角度来揣摩语言的内在逻辑。所以他讲的并不符合spec的定义，但这确实是一种角度。
按照spec，JS的数据类型就是以下七（六）种：
Undefined 类型；
Null 类型；
Boolean 类型；
String 类型；
Symbol 类型（此为ES6规范所新增）；
Number 类型；
Object 类型。

且按照spec，typeof只是一个运算符，其返回值并不能作为JS类型系统的依据。
我先说下如何理解typeof的返回值。
现在比较普遍的认知是，typeof null返回“object”是一个历史错误（JS的发明者Brendan Eich自己也是这样说的），只是因为要保持语言的兼容性而维持至今。从ES5制定开始就有动议将typeof null改为返回“null”（如启动node加上“--harmony_typeof”参数，即是如此），但是当前ES6标准草案仍然维持了原样。

