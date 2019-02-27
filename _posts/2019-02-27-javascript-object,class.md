---
layout: post
title:  "JavaScript Syntax"
date:   2019-02-26
excerpt: "JavaScript object, class에 대해 알아보자."
tag:
- JavaScript 
- syntax
- sample
- object
- prototype
- class
comments: true
---
## JavaScript instnace를 생성하는 방법
---

- 변수에 직접적으로 인스턴스 정의.
- 인스턴스를 return 하는 factory function 정의. (function 안에 instance 변수를 가진다. instance의 소속을 정하지는 않는다).
- new keyword와 생성자 함수 정의. (new는 새로운 인스턴스를 생성하고 function에 this에 인스턴스를 배정한다).
- new keyword와 class keyword


# JavaScript object
JavaScript는 object로 data를 관리하게 된다. 생성된 객체 인스턴스는 heap영역에서 관리된다(객체가 heap영역에 생성될 때 instance라 부른다). 예제를 통하여 JavaScript object의 성질을 알아보자. 

---
{% highlight javascript %}
var dog = {
type: "치와와",
weight: 2,
male: true,

sleep: function() {
console.log(this.type+" 쿨~쿨~");
},
};

dog.sleep();
sleep = dog.sleep;
sleep = dog.sleep.bind(dog);
sleep()
{% endhighlight %}

- Javascript에서 객체의 method는 method area에 위치하는 것이 아니라 heap object instance 안에 위치한다.
- sleep 역시 함수이자 object이기 때문에 bind()를 가진다.
- this. 키워드가 붙은 속성은 heap instance에 위치하고 , 변수들은 scope에서 찾는다.

---
{% highlight javascript %}
var student = { };
student.name = '홍길동';
student.hobby = '악기';
student.special = '프로그래밍';
student.department = '생명공학과';

student.toString = function() {
	var str = '';
	for(var key in this) {
		if(key != 'toString') {
			str += `${key}:${this[key]},` ;
		}
	}
	return str;
}

var str =student.toString();
console.log(str);
console.log(''+student);

delete student.name;
console.log(''+student);
{% endhighlight %}

- Javascript에서 동적으로 속성과 메서드를 추가하는 것이 가능하다.
- student 의 string으로 변환시에 toString()이 사용된다. override한 형태로 출력이 된다.
- delete 키워드로 속성의 삭제가 가능하다.

---
{% highlight javascript %}
var ar = [1,2,3];
delete(ar[1]);
console.log(ar[1]);
console.log(ar);

if(0 in ar) {
	console.log("0번째 요소가 있습니다/");
}
if(1 in ar) {
	console.log("1번째 요소가 있습니다");
}

{% endhighlight %}

- Javascript에서 delete를 하여도 배열의 크기가 줄어드는 것은 아니다.

# prototype 과 상속

---
{% highlight javascript %}
function Student(name) {
	if(!(this instanceof Student)) {
		return new Student(name);
		//변환 함수로 작동
	}
	this.name = name;
}

var student = new Student('Java');
var student2 = Student('JavaScript');

Student.prototype.toString = function(){
	return `${this.name}`;
} //static member로 보면 된다.
{% endhighlight %}

- new keyword 생성자 함수안에 변환 함수를 통해 new keyword 없이 instance생성이 가능하다.
- 과거에는 Javascript에서 생성자 함수를 통한 방식을 class로 사용하였다.
- JavaScript engine의 각 instance는 "__proto__"를 각자 가진다. __proto__속성은 prototype객체를 가리키고 prototype객체 역시 __proto__속성을 가진다.(prototype chain의 최상위는 Object이다.) 
- attribute에서는 읽기 작업과 쓰기 작업이 비대칭이다. 오직 읽기 작업만이 prototype chain을 따라간다.

---
{% highlight javascript %}
function Rectangle(w,h) {
	var width = w;
	var height = h; //private member로 만드는 방법
	
	this.getWidth = function() {return width;}; //closure 변수로 접근하기 위해서 내부적으로 함수가 정의 되어야 한다.
	this.getHeight = function() {return height;};
	
	this.setWidth = function(w) {
		width = w;
	};
	
	this.setHeight = function(h) {
		height = h;
	};
}

Rectangle.prototype.getArea = function () {
	return this.getWidth() * this.getHeight();
	//외부 함수에서 closure객체로 접근은 함수를 통해 가야한다.
};

function Square(length) {
	this.base = Rectangle; //부모 클래스 생성자 함수
	this.base(length,length); //부모 클래스 생성자 함수 호출
	//new 없이 호출하여서 this가 Square의 인스턴스가 된다.
}

Square.prototype = Rectangle.prototype;
Square.prototype.constructor = Square;
{% endhighlight %}

- new keyword 없이 object를 호출시 this의 정보가 현재 object가 된다. 따라서 자식 객체에서 부모 객체를 new없이 호출시 부모 객체의 속성들을 사용가능하다.
- 직관적으로 상속의 모양을 볼 수 없기 때문에 class를 이용한다.

# JavaScript class
JavaScript class를 통하여 직관적으로 상속관계의 객체들을 관리할 수 있다. 같은 속성을 가지는 인스턴스를 생성하고 관리하여, 객체 지향적 프로그래밍을 연습해보자. 

---
{% highlight javascript %}
class Student{
	constructor(name,age) {
		this._name = name; //생성자 안에 객체의 속성을 넣는다
		this.age = age;
	}
	printProfile() {
		console.log(`이름 : ${this.name}, 나이 : ${this.age}`)
	} //static keyword룰 줄 수 있고, 프로토타입 메서드
	
	//getter setter를 나타내는 keyword, 생성시 this.속성시 호출된다. 
	get name() { 
		return this._name; 
	} 
	set name(name) { 
		this._name = name;
	}
	
}
var stu = new Student("lee",27);
stu.printProfile();
{% endhighlight %}

- __속성은 접근가능하지만 내부적으로 쓰겠다를 나타낸다.(접근가능한 private member)
- class는 ES6에서 지원하기 때문에 하위 버전에서 사용시, babel tool을 통해 변환시켜야 한다.

---
{% highlight javascript %}
class Child extends Parent { 
	constructor(name, age) { 
		super(name); 
		this.age = age; 
	} 
	print() { 
		super.print(); 
		console.log("나이 : " + this.age); 
		//상속을 받고 override하였다
	} 
	static sayHello() { 
		console.log('Hello~'); 
	} 
}
{% endhighlight %}

- 생성자 constructor에서 반드시 부모 생성자 super()를 호출하여야 한다.

