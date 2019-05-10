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
