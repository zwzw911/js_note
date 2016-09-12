####  
1. 在$scope中设置数据，不要直接赋值，而是最好放在一个Object中。`$scope.test=1`不好，`$scope.test={test:1}`

####radio  
1. 可以使用`ng-checked`设置**初始**状态，但是无法通过`ng-checked`来传递选中状态到angular，因为它只是**单向绑定**，并且选中或者不选中，不会修改`ng-checked`的值。  
2. 若要判断选中状态，需要为radio设置value值，并通过`ng-model`进行双向绑定。*选中时，会返回value的值，通过value判断选中了哪个radio*。  


####select  
1. select通过ng-options选项获得options的内容。ng-options对应的是数组。    
2. ng-model对应的ng-options中的一个对象（ng-options对应的数组的一个元素）  
