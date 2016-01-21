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
5. Symbol作为属性名，该属性不会出现在**for...in、for...of**循环中，也**不会**被**Object.keys()、Object.getOwnPropertyNames()**返回。但是，它也不是私有属性，有一个**Object.getOwnPropertySymbols**方法，可以获取指定对象的所有Symbol属性名
