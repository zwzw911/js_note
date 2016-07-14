###2 let & constant
1. let：严格遵循先定义，后使用（变量），防止**TDZ(暂时性死区)和变量提升问题**。TDZ也会导致typeof失效（ES5无此问题）。暂时性死区的本质就是，只要一进入当前作用域，所要使用的变量就已经存在了，但是**不可获取**，只有等到声明变量的那一行代码出现，才可以获取和使用该变量。
2. let使得立即执行匿名函数（IIFE）不在需要了（IIFE定义函数变量）
3. ES6也规定，**函数本身的作用域，在其所在的块级作用域之内。**
4. 在for循环中使用let，则每次循环都为一个新变量。
5. const需要立刻赋值，之后赋值错误（strict），或者无效（非strict）。作用域和let一样，都是**块级（{}）**。
6. 对于复合类型（对象，以及数组），const保证**指向的地址不变，但是不能保证其中内容不变**。const a=**Object.freeze**({})可以保证无法**添加新属性**。更近一步，为了无法修改属性，需要写一个函数，freeze所有属性（类型为object）
7. **跨模块const**：**export** const A＝1，然后**import */{A,B} from** './constants'（文件名）
8. ES5，全局变量就是全局对象global的属性。ES6中，var/function还是照此处理，但是let/const/class定义的全局变量不在是global的属性了  

###3 变量的解构
1. 解构需要等号左边是array，**右边的值有iterator接口**（即可以遍历）。   
2. 或者左边是对象，右边也是对象，key相等。{a,b}={a:1,b:2}。应用范围，函数的参数结构。  
3. 
###4 字符串扩展
1. codePointAt(idx)：获得**单个字符（所有）**的**码点**
2. charCodeAt()/charAt():获得单个字符（2字节）的码点/字符。var s=1; s.charCodeAt(0)==>49; s.charAt(0)==>'1'
3. 

###7 数组的扩展
#####Arrar.from
Array.from()接收2个参数，第一个是**类似array的对象**和**可遍历（iterable）对象（set/map）**，第二个是函数(类似数组的map方法)。将第一个参数转换成数组，并对其中每个元素引用第二个参数的处理。
类似数组的对象本质就是有length属性。**ArraY.from({length:3})**
[].slice.call(obj)===>Array.from(obj,mapFunc)
只要有一个原始的数据结构，你就可以先对它的值进行处理，然后转成规范的数组结构，进而就可以使用数量众多的数组方法。
将字符串转为数组，然后返回字符串的长度。因为它能正确处理各种Unicode字符，可以避免JavaScript将大于\uFFFF的Unicode字符，算作两个字符的bug。
#####Arrar.of
用于将一组**值**，转换为数组。ES5中的Array/new Array，参数只有一个，实际指定数组长度。Array.of的行为一致。
#####数组**实例**的copyWithin方法
Array.prototype.copyWithin(target, start = 0, end = this.length)
    target（必需）：从该位置开始替换数据。
    start（可选）：从该位置开始读取数据，默认为0。如果为负值，表示倒数。
    end（可选）：到该位置前停止读取数据，默认等于数组长度。如果为负值，表示倒数。
#####数组**实例**的find()和findIndex
find参数为回调函数，回调函数有3个参数(后2个可以省略)，当前值，当前索引，原始数组。回调函数返回true，find返回对应的**第一个**元素；否则返回undefined。
[1, 5, 10, 15].find((val,idx,arr)=>val=> && idx>1)  ====>   10
findIndex和find类似，只是返回Index或者－1（没有找到）。
[NaN].findIndex((val,idx,arr)=> isNaN(val))
#####数组实例的fill
fill：3个参数，第一个，填充数组的值。第二个和第三个参数，用于指定填充的起始位置和结束位置
#####keys()/values()/entries()
for...of。用于遍历数组。它们都返回一个遍历器对象
#####includes
返回一个**布尔值**，表示某个数组是否包含给定的**值**。ES7支持。
#####空位
**由于空位的处理规则非常不统一，所以建议避免出现空位。**
#####数组推导
ES7支持。


###8 函数的扩展  
1. ES6可以使用默认值，最好放在最后。 
    function的length属性返回**默认参数之前**的参数个数。
2. rest（...）:把剩余参数放入一个数组。`let func=(a,...b)=>{console.log(a);conso.elog(b)}    func(1,2,3,4)===>1 [2,3,4]`  
3. 


###10 Symbol
1. Symbol是非对象，所以不能用new。
2. Symbol无法与其它类型进行运算。
3. **不能使用.运算符作为属性，而必须使用[]**。因为.运算符把属性作为字符处理。a.mySymbol=1===>mySymbol是字符
4. Symbol可以：var a={ERROR:Symbol(),WARN:Symbol(),INFO:Symbol()}。
5. Symbol作为属性名，该属性不会出现在**for...in、for...of**循环中，也**不会**被**Object.keys()、Object.getOwnPropertyNames()**返回。但是，它也不是私有属性，有一个**Object.getOwnPropertySymbols**方法，可以获取指定对象的所有Symbol属性名。
6. **symbol.for()**:它接受一个字符串作为参数，然后搜索有没有以该参数作为名称的Symbol值。如果有，就返回这个Symbol值，否则就新建并返回一个以该字符串为名称的Symbol值。

###14 Iterator和for...of
1. js中，表示'集合'，ES5中有array和object，ES6添加map和set。**字符类似array，所以也有Symbol.iterator属性**。以及Generator对象。  
2. 遍历器（Iterator）就是这样一种机制。它是**一种接口**，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署Iterator接口，就可以完成遍历操作（即依次处理该数据结构的所有成员）。Iterator的作用有三个：一是为各种数据结构，**提供一个统一的、简便的访问接口**；二是使得**数据结构的成员能够按某种次序排列**；三是ES6创造了一种新的遍历命令**for...of**循环，Iterator接口主要供for...of消费。**遍历器对象本质上，就是一个指针对象**。指向当前数据结构的起始位置。调用指针对象的next方法，可以将指针指向数据结构的第一个（下一个）成员，直到结尾。Iterator只是把接口规格加到数据结构之上，所以，**遍历器与它所遍历的那个数据结构，实际上是分开的**，  
2. 遍历器是对象，带有一个next方法（函数），此方法返回对象。{next:function(){return {value,done:}}}。  
2. 默认的Iterator接口部署在数据结构的**Symbol.iterator属性**，或者说，一个数据结构只要具有Symbol.iterator**属性**，就可以认为是“可遍历的”（iterable）。Symbol.iterator本身是一个表达式，返回Symbol对象的iterator属性，这是一个**预定义好的、类型为Symbol的特殊值**，所以要放在方括号内。在ES6中，有三类数据结构原生具备Iterator接口：**数组**、**某些类似数组的对象**、**Set**和**Map**结构。对象（Object）之所以没有默认部署Iterator接口，是因为对象的哪个属性先遍历，哪个属性后遍历是不确定的，需要开发者手动指定。**本质上，遍历器是一种线性处理，对于任何非线性的数据结构，部署遍历器接口，就等于部署一种线性转换**。不过，严格地说，对象部署遍历器接口并不是很必要，因为这时对象实际上被当作Map结构使用，ES5没有Map结构，而ES6原生提供了。
3. 遍历是一个带有**next()，return()/throw()**的对象，必需部署在**[Symbol.iterator]**属性上。next()返回{value:,done}。return()用在for...of循环提前退出时（出错，break），必要的资源清理工作。next()是必须的，return()和throw()是可选的。turow()主要为generator，iterator一般不用。
4. for...in只能获得key，for...of获得value（数组，**key必需为数字**，否则不返回对应的value）。但是通过**entries()或者keys()**属性，也可以遍历key。
5. 对于**Map**，for..of返回是**[key：valeu]数组**;对于set，返回的是值。
6. 比较：for：麻烦；forEach，无法break；for...in:读取key（以字符串的方式），读取原型上的key，顺序不定；for...of：客服所有以上缺点。  
7. 对象默认不能通过for...of进行遍历。可以使用Object.keys()读取key。或者：如果是类似数组的对象（key为length+数字0/1/2...），可以通过Arrary.from()转换成array后使用for...of；如果不是类似array的对象，那么可以

###15 Generator
1. generator函数格式function* func(param){yeild a; yeild b;return c}。  
2. generator函数执行后，**返回一个遍历器对象**。var it=func(); it.next()。Generator函数除了状态机，还是一个遍历器对象生成函数。返回的遍历器对象，可以依次遍历Generator函数内部的每一个状态。next方法返回一个对象，它的value属性就是当前yield语句的值hello，done属性的值false  
3. 任意一个**对象的Symbol.iterator方法，等于该对象的遍历器对象生成函数**，调用该函数会返回该对象的一个遍历器对象   
4. **1. yield句本身没有返回值，或者说总是返回undefined。x=yeild 2，执行next()，返回2（2 是 yeild产生的），但是x=undefined  2. yield不能用在普通函数中。3. yield语句如果用在一个表达式之中，必须放在圆括号里面。**。console.log('Hello' + (yield 123))  
function* gen(){};var g = gen();g\[Symbol.iterator\]() === g  
5. next()方法可以带参数，作为上一次yeild产生的值。但是只能在第二次及之后才能带参数，第一次next()不能带参数。  
6. yeild\*：跟的是遍历器函数或者带有遍历器接口的（例如，array，map/set，string）。yeild*等同于for...of。如果在generator中调用另一个generator，格式为 yeild\* generator1()。如果只是yeild generator，返回的是遍历器对象。  
7. 

###18 class
1. class是语法糖，对ES5的“类”定义进行包装（**类的数据类型是函数**）。constructor()是构造函数（**指向类本生**），类方法无需function关键字，直接函数名+函数体即可（**类方法实际仍然定义在prototype属性上**）。自定义的类方法，无法枚举（Object.keys(class.prototype)===[]），只能通过getOwnPropertyName获得
2. constructor是必须的，如果没有定义，会自动创建一个空构造函数。constructor可以返回其它对象（而不是this）
3. 类的属性，如果不是定义在this上，那么默认是在prototype上。类的所有实例共享一个原型对象。意味着，可以通过更改实例的原型，来更改类的方法定义（不推荐）。
4. 类表达式。const MyClass = class Me {}，或者省略Me。此处类名是MyClass，Me是仅供class内部使用，代指class本身。
5. class没有变量提升（必需先定义，后使用）；class内部默认严格模式。
6. 使用extends进行继承。其中使用super代指父类。构造函数中必需先执行super。super返回this。
7. 子类的__proto__指向父类（构造函数的继承），子类的prototype.__proto__指向父类的__proto__（方法的继承）
8. Object.getPrototypeOf()：从子类获得父类
9. 原生构造函数：Boolean()/Number()/String()/Array()/Date()/Function()/RegExp()/Error()/Object()
10. lass内部可以使用get和set关键字，对某个属性设置存值函数和取值函数，拦截该属性的存取行为
11. 某个方法之前加上星号（*），就表示该方法是一个Generator函数
12. 加上**static**关键字，就表示该方法不会被实例继承，而是直接通过类来调用
13. new.target属性

### 21 编程风格
#####1 块级作用域
1) let取代var，防止变量提升。
2) 全局常量尽量采用const，防止更改，并且复合函数式编程思想
3) 采用严格模式，将代码陷阱变成错误
#####2 字符串
1） 静态字符使用单引号或者反引号，动态字符（字符和变量拼接）采用反引号  
#####3 解构赋值
1） 使用数组成员赋值（即把数组中的元素一个个赋值给变量），采用解构  
2） 如果函数的参数是对象的成员（部分或者全部），采用解构。*代码简洁，解构可以直接获得成员，而无需在函数中再次设置变量获取（var=obj.member）*  
3） 如果函数返回值有多个，采用对象解构获得（部分或者全部）返回值。采用对象解构，便于更改返回值的数量和顺序。  
#####4 对象
1） 对象成员定义，如果多行，最后一行添加逗号，以便之后添加（和CSS类似）；如果是单行定义，**最后不加逗号**。
2） 对象最好是静态（const a={}，如此防止a被无意间改成其它数据），并且成员固定（预先定义成员，值为null，之后可以另行赋值）；如果实在需要动态添加属性，使用（**Object.assign**(a, { x: 3 })）。
3） 如果对象属性名是动态的，使用表达式。const a={[getkey('enable')]:true}。
4） 属性和方法（主要是方法），采用简洁方式
#####5 数组

