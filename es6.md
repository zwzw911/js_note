### let & constant
1. let：严格遵循先定义，后使用（变量），防止TDZ(暂时性死区)和变量提升问题。TDZ也会导致typeof失效（ES5无此问题）。暂时性死区的本质就是，只要一进入当前作用域，所要使用的变量就已经存在了，但是**不可获取**，只有等到声明变量的那一行代码出现，才可以获取和使用该变量。
2. let使得立即执行匿名函数（IIFE）不在需要了（IIFE定义函数变量）
3. ES6也规定，**函数本身的作用域，在其所在的块级作用域之内。**
4. 在for循环中使用let，则每次循环都为一个新变量。
5. const需要立刻赋值，之后赋值错误（strict），或者无效（非strict）。作用域和let一样，都是**块级（{}）**。
6. 对于复合类型（对象，以及数组），const保证**指向的地址不变，但是不能保证其中内容不变**。const a=**Object.freeze**({})可以保证无法**添加新属性**。更近一步，为了无法修改属性，需要写一个函数，freeze所有属性（类型为object）
7. **跨模块const**：**export** const A＝1，然后**import */{A,B} from** './constants'（文件名）
8. ES5，全局变量就是全局属性global的属性。ES6中，var/function还是照此处理，但是let/const/class定义的全局变量不在是global的属性了  

### 解构

### 字符
1. codePointAt(idx)：获得**单个字符（所有）**的**码点**
2. charCodeAt()/charAt():获得单个字符（2字节）的码点/字符。var s=1; s.charCodeAt(0)==>49; s.charAt(0)==>'1'
3. 

###Symbol
1. Symbol是非对象，所以不能用new。
2. Symbol无法与其它类型进行运算。
3. **不能使用.运算符作为属性，而必须使用[]**。因为.运算符把属性作为字符处理。a.mySymbol=1===>mySymbol是字符
4. Symbol可以：var a={ERROR:Symbol(),WARN:Symbol(),INFO:Symbol()}。
5. Symbol作为属性名，该属性不会出现在**for...in、for...of**循环中，也**不会**被**Object.keys()、Object.getOwnPropertyNames()**返回。但是，它也不是私有属性，有一个**Object.getOwnPropertySymbols**方法，可以获取指定对象的所有Symbol属性名。
6. **symbol.for()**:它接受一个字符串作为参数，然后搜索有没有以该参数作为名称的Symbol值。如果有，就返回这个Symbol值，否则就新建并返回一个以该字符串为名称的Symbol值。

###Iterator
1. js中，表示'集合'，ES5中有array和object，ES6添加map和set。遍历器（Iterator）就是这样一种机制。它是**一种接口**，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署Iterator接口，就可以完成遍历操作（即依次处理该数据结构的所有成员）。Iterator的作用有三个：一是为各种数据结构，**提供一个统一的、简便的访问接口**；二是使得**数据结构的成员能够按某种次序排列**；三是ES6创造了一种新的遍历命令**for...of**循环，Iterator接口主要供for...of消费。**遍历器对象本质上，就是一个指针对象**。指向当前数据结构的起始位置。调用指针对象的next方法，可以将指针指向数据结构的第一个（下一个）成员，直到结尾。Iterator只是把接口规格加到数据结构之上，所以，**遍历器与它所遍历的那个数据结构，实际上是分开的**，
2. 默认的Iterator接口部署在数据结构的**Symbol.iterator属性**，或者说，一个数据结构只要具有Symbol.iterator**属性**，就可以认为是“可遍历的”（iterable）。Symbol.iterator本身是一个表达式，返回Symbol对象的iterator属性，这是一个**预定义好的、类型为Symbol的特殊值**，所以要放在方括号内。在ES6中，有三类数据结构原生具备Iterator接口：**数组**、**某些类似数组的对象**、**Set**和**Map**结构。对象（Object）之所以没有默认部署Iterator接口，是因为对象的哪个属性先遍历，哪个属性后遍历是不确定的，需要开发者手动指定。**本质上，遍历器是一种线性处理，对于任何非线性的数据结构，部署遍历器接口，就等于部署一种线性转换**。不过，严格地说，对象部署遍历器接口并不是很必要，因为这时对象实际上被当作Map结构使用，ES5没有Map结构，而ES6原生提供了。
