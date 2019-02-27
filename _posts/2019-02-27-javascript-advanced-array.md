---
layout: post
title:  "JavaScript Syntax"
date:   2019-02-26
excerpt: "JavaScript array에 대한 심화 자료입니다."
tag:
- JavaScript 
- syntax
- sample
- array
comments: true
---
# JavaScript advanced-array

## 배열 메서드
---
array 객체의 prototype method를 알아보자

- join("between tag") : 원본의 변화는 없다.
- reverse()
- indexOf(value)
- push(value), pop(), unshift(value), shift()
- splice(바꿀 위치, 삭제 갯수, 나머지는 삽입)
- slice() : 원본의 변화는 없다. defalut로 쓸 경우 복사할 수 있다.
- concat() : 원본의 변화는 없다.
- sort(function) : default는 문자열로 정렬한다. compare함수를 전달하여 정렬방식을 지정할 수 있다.
- foreach(function) : value, idx, arr이 함수에 전달된다.
- map(function) : 원본의 변화는 없다.
- filter()

---
array shuffle 예제

{% highlight javascript %}
var test = [0,1,2,3,4,5,6,7]

function shuffle(arr) {
	function swap(a,b) {
		var temp = arr[a];
		arr[a] = arr[b];
		arr[b] = temp;
	}
	
	for(var i = arr.length; 0 < i; --i){
		var random = parseInt(Math.random()*i);
		swap(i-1,random);
	}
}
shuffle(test);
console.log(test);

//배열 객체의 shuffle 이라는 속성을 대입
Array.prototype["shuffle"] = function(){  //Array.prototype.shuffle을 써도 동일하다.
	shuffle(this);
}
var test2 = [0,1,2,3,4,5,6,7]
test2.shuffle();
console.log(test2);

Object.defineProperty(
		Array.prototype,"shuffle",{enumerable:false}
); //for-in roop 순회시 key의 접근을 막는다.

{% endhighlight %}

- shuffle algorithm : array의 마지막 값을 랜덤 index value와 swap한다.
- 기본적으로 object의 prototype은 enumerable:false 처리가 되어있다.