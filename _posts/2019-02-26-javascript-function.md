---
layout: post
title:  "JavaScript Syntax"
date:   2019-02-26
excerpt: "JavaScript function에 대해 알아보자."
tag:
- JavaScript 
- syntax
- sample
- function
comments: true
---
# JavaScript function
Javascript의 함수는 선언적 함수(함수의 이름이 있다.)와 비선언적 함수로 구분된다. 여러가지 예제를 통해 함수의 성질을 알아보자.

## 선언적 함수
---
{% highlight javascript %}
fn2()
function fn2() { console.log('Hello javascript 1') } function fn2() { console.log('Hello javascript 2') }

function fn(a, b, c) {
console.log(a, b, c);
}
fn() // undefined undefined undefined
fn(10) // 10 undefined undefined
fn(10, 20) // 10 20 undefined
fn(10, 20, 30) // 10 20 30
{% endhighlight %}

- Javascript에서 선언적 함수 호출은 함수 정의 앞에서도 가능하다.
- 매개변수 갯수 check를 안한다.
- <p style="color:green">**선언적 함수는 식별자 검사 단계에서 함수로 인식이 되어 함수 호출이 먼저 나오는 것이 가능하다.**</p>

---
{% highlight javascript %}
//ES6 버전의 디폴트 값 배정 (n=100)
function sum(n=100) {
	if (n == undefined) 
		n = 100; // n = n || 100; 
	var s = 0; 
	for (var i = 0; i <= n; i++) { 
		s += i; 
	} 
	return s; 
}

//가변인자함수
function sumAll() {
	var sum = 0;
	for(var i=0; i<arguments.length; i++) {
		sum += arguments[i];
	}
	return sum;
}

console.log(sumAll(1,2,3,4,5,6,7,8,9))
{% endhighlight %}

- 디폴트 값 설정을 일반적으로는 논리연산자를 이용한 짧은 조건문으로 해결한다.(판단을 내린 시점의 값이 리턴된다.)
- 함수 내부적으로 가지는 arguments변수를 통해 가변인자함수를 사용한다.(java, c++ 에서는 ...으로 가변인수처리를 한다.)

---
{% highlight javascript %}
//javascript의 내부 함수 호출
function outer() { 
	var outvalue = 5678; 
	function inner() { 
		var invalue = 1234; 
		console.log("outvalue = " + outvalue); 
	} 
	inner(); 
	console.log("invalue = " + invalue);// 에러
} 

outer();
{% endhighlight %}

- 내부함수를 만들면 naming충돌을 피할 수 있다. 안쪽 함수에서 바깥 함수의 접근은 가능(scope chain)하지만 바깥 함수에서 안쪽 함수의 접근은 불가능하다.
- 내부함수는 scopechain이 형성된다. 따라서 내부함수는 바깥 scope의 접근이 가능하다.
## 비선언적 함수 
---
{% highlight javascript %}
// fn(); undefined를 호출하여 err가 나타난다.
console.log(fn); //undefined
var fn = function() { 
	console.log('Hello javascript') 
	} 
console.log(fn); // [Function] 
fn(); // Hello javascript
{% endhighlight %}

- Javascript에서 선언적 함수 호출은 함수 정의 앞에서도 가능하다.
- 매개변수 갯수 check를 안한다.
- <p style="color:green">**비선언적 함수는 식별자 검사 단계에서 함수로 인식이 안 되어 함수 호출이 먼저 나오는 것이 불가능하다.**</p>

## 함수 고급
---
함수가 데이터타입(reference type)이라, 매개변수의 전달과 함수의 리턴이 가능하다. 

---
{% highlight javascript %}
function forEach(arr1, fn1) {
	if(!fn1) return; //false인경우 for roop를 돌지 않는다.
	
	for(var i=0; i<arr1.length;i++) {
		fn1(arr[i],i,arr1); //JavaScript에서는 매개변수 갯수를 check하지 않는다.
	}
}

var data = [1,2,3,4,5,6];
var newData = [];

forEach(data, (e,i,arr)=>newData[i]=e*e); //javascript에서의 람다식 표기.
forEach(data, console.log);
{% endhighlight %}

- 함수 매개변수 전달이 가능하다.

---
{% highlight javascript %}
function test(name) {
	var output = 'Hello' + name + '...!';
	return function() {
		console.log(output)
	}
}
test('Javascript')();
{% endhighlight %}

- (일반적인 컴파일 언어에서는 지역변수의 수명은 함수가 끝날 때 사라진다.) JavaScript에서는 stack영역에서 함수 지역 변수들이 할당되는 것이 아니라, <p style="color:green">**scope객체에 대한 참조를 stack에서 관리한다.**</p>
- 일반적으로 함수가 끝나면 scope도 참조가 끝나 사라지지만 이 경우 function이 리턴되고 리턴된 function에서 output을 가리켜 scope가 사라지지 않는다.
- <p style="color:green">**이와 같이 함수를 통해서만 접근 가능한 변수를 closure라 한다.**</p>

---
다음과 같이 closure 변수를 운영체제에서 참조하고 있는 것도 가능하다.

{% highlight javascript %}
function outcount() {
	var count = 0; //closure 변수
	
	setInterval(function() {
		count ++ ;
		console.log(count + "초 지났습니다.");
	},1000); //setInterval(callback함수, 시간간격) 인 비동기함수
}
outcount();

{% endhighlight %}

- JavaScript는 single thread 모델이고 , multi thread를 지원하지 않는다. 따라서 비동기 함수로 처리하여야 한다.
- setInterval은 callback함수를 매개변수로 받는 비동기 함수이다.
- io 작업은 비동기함수(노드)로 처리한다.

---
{% highlight javascript %}
console.log("5! = " + function(n){
	if(n == 1){
		return 1;
	} else {
		return n * arguments.callee(n-1); //argument의 callee필드를 통해 익명함수에서 자기 자신을 호출하는 것이 가능하다.
	}
}(5)); // 익명 함수 정의하고 바로 호출
{% endhighlight %}

- 익명함수에서 재귀 호출을 하기 위해서 arguments.callee 필드를 사용한다.