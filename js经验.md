##### 原型
1.  js中**万物皆对象**。对象分成2类：**普通对象**和**函数对象**。Object,Function是内置的**函数对象**。
2.  使用function/new Function建立的对象为**函数对象**，其它皆为**普通对象**。
3.  **函数对象**有prototype属性，其为原型对象（普通对象）；而所有对象（普通和函数），都有**_proto_**属性。
4.  对象的_proto_指向创建它的**函数对象**的prototype。
