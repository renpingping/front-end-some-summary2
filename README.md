
[JavaScript数组循环的几种写法](#JavaScript数组循环的几种写法)

[使用slice和concat对数组的深拷贝和浅拷贝](#使用slice和concat对数组的深拷贝和浅拷贝)

# JavaScript数组循环的几种写法

利用Javascript map(),reduce()和filter()数组方法可以帮助您编写更加声明性、流畅的风格代码。

而不是积累起来for循环和嵌套来处理列表和集合中的数据，您可以利用这些方法更好地将逻辑组织成功能的构建块，然后将它们链接起来以创建更可读和更易于理解的实现。

ES6还为我们提供了一些更好的数组方法，比如.find,.findIndex,.of和for..of循环！

## 数组循环
	var officers = [
	    { id: 20, name: 'Captain Piett' },
	    { id: 24, name: 'General Veers' },
	    { id: 56, name: 'Admiral Ozzel' },
	    { id: 88, name: 'Commander Jerjerrod' }
	];
	// What you need
	// [20, 24, 56, 88]

## for循环
使用率最高，也是最基本的一种遍历方式

	var officersIds = [];
	for(var i=0,len=officers.length;i<len; i++){
	    officersIds.push(officers[i].id);
	}
	console.log(officersIds); // [20,24,56,88]

## forEach循环
forEach中传入要执行的回调函数，函数有三个参数。第一个参数为数组元素(必选)，第二个参数为数组元素索引值(可选)，第三个参数为数组本身(可选)

	var officersIds = [];
	officers.forEach(function (officer,index,array) {
	    console.log(index); //0,1,2,3,
	    console.log(officer); //{id: 20, name: "Captain Piett"},{id: 24, name: "General Veers"},{id: 56, name: "Admiral Ozzel"},{id: 88, name: "Commander Jerjerrod"}
	    officersIds.push(officer.id);
	});
	console.log(officersIds); //[20,24,56,88]
## for in循环
for...in循环可用于循环对象和数组,推荐用于循环对象,可以用来遍历JSON

	var officersIds = [];
	for(var key in officers){
	    console.log(key); // 0 1 2 3 返回数组索引
	    console.log(officers[key]); //{id: 20, name: "Captain Piett"},{id: 24, name: "General Veers"},{id: 56, name: "Admiral Ozzel"},{id: 88, name: "Commander Jerjerrod"}
	    officersIds.push(officers[key].id);
	}
	console.log(officersIds); //[20,24,56,88]
## for of循环
可循环数组和对象，推荐用于遍历数组。

for...of提供了三个新方法：

key()是对键名的遍历；
value()是对键值的遍历；
entries()是对键值对的遍历；

	let arr = ['科大讯飞', '政法BG', '前端开发'];
	for (let item of arr) {  
	  console.log(item); //  科大讯飞  政法BG  前端开发
	}
	// 输出数组索引
	for (let item of arr.keys()) {  
	  console.log(item);  // 0 1 2
	}
	// 输出内容和索引
	for (let [item, val] of arr.entries()) {  
	  console.log(item + ':' + val); //  0:科大讯飞  1：政法BG  2：前端开发
	}
	var officersIds = [];
	for (var item of officers) {
	    console.log(item); //{id: 20, name: "Captain Piett"},{id: 24, name: "General Veers"},{id: 56, name: "Admiral Ozzel"},{id: 88, name: "Commander Jerjerrod"}
	    officersIds.push(item.id); 
	}
	console.log(officersIds); // [20,24,56,88]
	// 输出数组索引
	for(var item of officers.keys()){
	    console.log(item); // 0 1 2 3
	}
	// 输出内容和索引
	for (let [item, val] of officers.entries()) {
	    console.log(item) // 0 1 2 3 输出数组索引
	    console.log(val);//{id: 20, name: "Captain Piett"},{id: 24, name: "General Veers"},{id: 56, name: "Admiral Ozzel"},{id: 88, name: "Commander Jerjerrod"}
	    console.log(item + ':' + val); 
	}
## map循环
map() 会返回一个新数组，数组中的元素为原始数组元素调用函数处理后的值。
map() 方法按照原始数组元素顺序依次处理元素。

map 不修改调用它的原数组本身。

map()中传入要执行的回调函数，函数有三个参数。第一个参数为数组元素(必选)，第二个参数为数组元素索引值(可选)，第三个参数为数组本身(可选)

	var arr = [
	    {name:'a',age:'18'},
	    {name:'b',age:'19'},
	    {name:'c',age:'20'}
	];
	arr.map(function(item,index) {
	    if(item.name == 'b') {
		console.log(index)  // 1
	    }
	})
数组加一

	var officersIds = officers.map(function (officer) {
	    return officer.id
	});
	console.log(officersIds); //[20,24,56,88]
	reduce
	array.reduce(function callback(accumulator, currentValue, currentIndex, array){

	}[, initialValue])

	var peoples = [
	  {
	    id: 10,
	    name: "Poe Dameron",
	    years: 14,
	  },
	  {
	    id: 2,
	    name: "Temmin 'Snap' Wexley",
	    years: 30,
	  },
	  {
	    id: 41,
	    name: "Tallissan Lintra",
	    years: 16,
	  },
	  {
	    id: 99,
	    name: "Ello Asty",
	    years: 22,
	  }
	];
输出他们的年龄总数

	var totalYears = peoples.reduce(function (total, people) {
	    console.log(total);
	    console.log(people);
	    return total + people.years;
	}, 0);
	// const totalYears = people.reduce((acc, people) => acc + people.years, 0);
	console.log(totalYears); //30
求年龄最大的那个人

	var oldest = peoples.reduce(function (oldest, people) {
	    return (oldest.years || 0) > people.years ? oldest : people;
	}, {});
	console.log(oldest); //{id: 2, name: "Temmin 'Snap' Wexley", years: 30}
	console.log(oldest.years); //82

## filter
filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素。

	array.filter(function(currentValue,index,arr){

	}, thisValue)
演示

	var designer = peoples.filter(function (people) {
	    return people.job === "designer";
	});
## 组合使用
	var totalScore = peoples
	    .filter(function (person) {
		return person.isForceUser;
	    })
	    .map(function (choose) {
		return choose.mathScore + choose.englishScore;
	    })
	    .reduce(function (total, score) {
		return total + score;
	    }, 0);
    
## Array.from()
	var divs = document.querySelectorAll('div.pane');  
	var text = Array.from(divs, (d) => d.textContent);  
	console.log("div text:", text);
	// Old, ES5 way to get array from arguments
	function() {  
	  var args = [].slice.call(arguments);
	  //...
	}

	// Using ES6 Array.from
	function() {  
	  var args = Array.from(arguments);
	  //..
	}
	var filled = Array.from([1,,2,,3], (n) => n || 0);  
	console.log("filled:", filled);  
	// => [1,0,2,0,3]
	
著作权归作者所有。
商业转载请联系作者获得授权,非商业转载请注明出处。
链接:http://caibaojian.com/for-loop.html
来源:http://caibaojian.com


# 使用slice和concat对数组的深拷贝和浅拷贝

## 一、数组浅拷贝

在使用JavaScript对数组进行操作的时候，我们经常需要将数组进行备份.

如下代码，如果只是简单才用赋值的方法，那么我们只要更改其中的任何一个，然后其他的也会跟着改变，这就导致了问题的发生

var arr1 = ["red","yellow","black"];
var arr2 = arr1;
arr2[1] = "green";
console.log("数组的原始值：" + arr1 );
console.log("数组的新值：" + arr2);

测试结果如下


 

像上面的这种直接赋值的方式就是数组的浅拷贝，浅拷贝改变其中一个数组，另外一个数组也会跟着改变。很多时候，这不是我们想要的。

## 二、数组深拷贝方法

（1）js的slice方法

复制代码
对于array对象的slice函数，返回一个数组的一段。（仍为数组）
arrayObj.slice(start, [end])

参数：
arrayObj 必选项。一个 Array 对象。
start 必选项。arrayObj 中所指定的部分的开始元素是从零开始计算的下标。
end可选项。arrayObj 中所指定的部分的结束元素是从零开始计算的下标。

说明：
slice 方法返回一个 Array 对象，其中包含了 arrayObj 的指定部分。
slice 方法一直复制到 end 所指定的元素，但是不包括该元素。
如果 start 为负，将它作为 length + start处理，此处 length 为数组的长度。
如果 end 为负，就将它作为 length + end 处理，此处 length 为数组的长度。
如果省略 end ，那么 slice 方法将一直复制到 arrayObj 的结尾。
如果 end 出现在 start 之前，不复制任何元素到新数组中。
复制代码
测试例子：

var arr1 = ["1","2","3"];
var arr2 = arr1.slice(0);
arr2[1] = "9";
console.log("数组的原始值：" + arr1 );
console.log("数组的新值：" + arr2 );
测试结果：



如测试结果显示，通过JS的slice方法，改变拷贝出来的数组的某项值后，对原来数组没有任何影响。

（2）js的concat方法

concat() 方法用于连接两个或多个数组。该方法不会改变现有的数组，而仅仅会返回被连接数组的一个副本。
语法：arrayObject.concat(arrayX,arrayX,......,arrayX)
说明：返回一个新的数组。该数组是通过把所有 arrayX 参数添加到 arrayObject 中生成的。如果要进行 concat() 操作的参数是数组，那么添加的是数组中的元素，而不是数组。
测试例子:

var arr1 = ["1","2","3"];
var arr2 = arr1.concat();
arr2[1] = "9";
console.log("数组的原始值：" + arr1 );
console.log("数组的新值：" + arr2 );
测试结果:



如测试结果显示，通过JS的concat方法，改变拷贝出来的数组的某项值后，对原来数组没有任何影响。

(3)js遍历数组的方法

测试例子：

复制代码
var arr1 = [1,2,3];//原来数组
var arr2 = [];//新数组

function deepCopy(arry1, arry2){
　　var length = arry1.length;
　　for(var i = 0;i<length;i++){
　　　　arry2[i] = arry1[i];
　　}
}

deepCopy(arr1, arr2);
arr2[0] =5;
console.log(arr1);
console.log(arr2);

复制代码
测试结果：



 

 ## 三、slice,concat方法的局限性

测试例子1

var arr1 = [{"name":"weifeng"},{"name":"boy"}];//原数组
var arr2 = [].concat(arr1);//拷贝数组
arr1[1].name="girl";
console.log(arr1);// [{"name":"weifeng"},{"name":"girl"}]
console.log(arr2);//[{"name":"weifeng"},{"name":"girl"}]
测试结果：



 

测试例子2

复制代码
var a1=[["1","2","3"],"2","3"],a2;
a2=a1.slice(0);
a1[0][0]=0; //改变a1第一个元素中的第一个元素
console.log(a2[0][0]);  //影响到了a2

var b1=[["1","2","3"],"2","3"],b2;
b2=b1.slice(0);
b1[0][0]=0; //改变a1第一个元素中的第一个元素
console.log(b2[0][0]);  //影响到了a2
复制代码
测试结果：



 

从上面两个例子可以看出，由于数组内部属性值为引用对象，因此使用slice和concat对对象数组的拷贝，整个拷贝还是浅拷贝，拷贝之后数组各个值的指针还是指向相同的存储地址。

因此，slice和concat这两个方法，仅适用于对不包含引用对象的一维数组的深拷贝

 
