# First Day


# 第一个vue应用
1. 使用vue之前要先导入
```
<script src="vue.js" type="text/javascript" charset="utf-8"></script>
```
2. body里面建立视图层，即一个div
```
<div id="app">
	{{ message }}
</div>
```

3. body里面script代码，创建vue对象，并对视图层声明对象进行注册，并且初始化
```
<script type="text/javascript">
	var app1 = new Vue({ //new Vue时，需要传递一个对象作为参数
	el: '#app',  //el即element，用Id选择器选中div
	data:{ //用于保存数据，我们在视图里面声明了什么变量，在这里就要注册什么变量，并进行初始化的赋值
			message:'hello word!',
					
		}
	});
</script>
```

# vue常用数据及方法
1. 第一节中，我们对变量的初始化是在data里面进行，我们也可以申明一个var变量进行初始化
```
var date = {a:1};  //a赋值1
var vm = new Vue({
	el: '#app',
	data: date    //直接将date赋值给data
});
```
2. 对变量a进行修改值时，我们有多种方法
```
date.a = 'hello';  //可以直接这样修改a的值
vm.a = 'hello';  //修改结果和上面相同
```
3. vue暴露一些常用的变量例如```Object.$data```和```Objece.$el```,所以修改变量还可以这样子
```
vm.$data.a = 'hello';
```
4. vue也暴露一些常用的方法

`Object.freeze(）`函数会阻止修改现有属性

`Object.$watch`可以观察一个变量的前后变化值，如：
```
<div id="app">
	{{ a }}
</div>
<script type="text/javascript">
	var date = {a:1};  //a赋值1
	var vm = new Vue({
		el: '#app',
		data: date    //直接将date赋值给data
	});
    vm.$watch('a', function(newval, oldval){
				console.log(newval, oldval);
			});
	vm.$data.a = 'sda';
</script>
```
那么控制台将打印出`sda 1`，即a变量改变后的值和先前的值

# Vue的生命周期
1. beforeCreate函数

在实例初始化之前，数据观测(data obsever)和event/watcher事件配置之前被调用
```
beforeCreate:function(){
				console.log('beforeCreate');
			},
```
2. created

在实例被创建完成后被立即调用,在这一步，实例已经完成以下配置：数据观测(data observer)，属性和方法的运算，watch/event事件回调.然而，挂载阶段还没开始，$el属性目前不可见
```
created:function(){
	console.log('created');
},
```
3. beforeMount

在挂载开始之前被调用，相关的渲染函数首次被调用
```
beforeMount:function(){
	console.log('beforeMount');
},
```
4. mounted

el被新创建的vm.$el替换，挂载成功
```
mounted:function(){
	console.log('mounted');
},
```
5. beforeUpdate

数据更新时调用
```
beforeUpdate:function(){
	console.log('beforeUpdate');
},
```
6. updated

组件DOM已经更新，组件更新完毕
```
updated:function(){
	console.log('updated');
}
```
## 声明周期的综合运用
```
<div id="app">
	{{msg}}
</div>
<script type="text/javascript">
	var vm = new Vue({
		el: '#app',
		data: {
			msg : 'hello vue',	
		},
			
	beforeCreate:function(){
		console.log('beforeCreate');
	},
			
	created:function(){
		console.log('created');
	},
			
	beforeMount:function(){
		console.log('beforeMount');
	},
			
	mounted:function(){
		console.log('mounted');
	},
			
	beforeUpdate:function(){
		console.log('beforeUpdate');
	},
			
	updated:function(){
		console.log('updated');
	}
	});
	setTimeout(function(){
		vm.msg = 'change';
	},3000);
</script>
```
结果如下
```
beforeCreate

created

beforeMount

mounted

Download the Vue Devtools extension for a better development experience:https://github.com/vuejs/vue-devtools

You are running Vue in development mode.

Make sure to turn on production mode when deploying for production.

See more tips at https://vuejs.org/guide/deployment.html

beforeUpdate

updated
```
