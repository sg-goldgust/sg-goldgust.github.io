---
layout: post
title:  "JavaScript Syntax"
date:   2019-02-26
excerpt: "JavaScript ES(syntex)에 대해 알아보자. 이후 jQuery를 통해 DOM, BOM에 대해 알아보자"
tag:
- JavaScript 
- syntax
- sample
- test
comments: true
---

# JavaScript Elements

다른 언어와 다르게 변수의 scope에 따라 선언의 키워드가 달라지게 된다. 블록 범위 변수 선언(let keyword) 과 함수 범위 변수 선언(var keyword)에 대해 살펴보자

## scope 객체 
---
{% highlight javascript %}
var global = "전역";
function func() {
	globe = "글로벌" ; 
	//전역변수, main() scope 객체에서 식별자로 인식된다.

	var local = "로컬"; //지역변수
	console.log("함수안 local = " + local);
	console.log("함수안 global = " + global);
}
func();
console.log("함수밖 local = " + local);
//함수의 scope 객체가 사라지고 undefined가 출력된다.
console.log("함수밖 global = " + global);
console.log("함수밖 globe = " + globe);
{% endhighlight %}

- Javascript에서 함수나 전역변수 실행 전 현재 scope에서 운영되는 식별자를 찾는다. 현재 level에서 없는 변수는 자기의 상위 scope에서 찾게 된다.(scope chain)
- "use strict" 선언으로 변수 선언 안할 시 err처리가 가능하다.



## let keyword 객체 
---
다른 언어에서의 변수와 scope가 동일하다.
(let, const는 explore에서 지원하지 않는다.)

## 특수한 값
---
- null : reference가 없음을 나타내는 값
- undefined : 변수 선언시 초기화 되는 값
- NaN : 숫자가 아님을 나타내는 값
- infinite

	undefined의 경우 type으로도 사용된다.<br>
	null, undefined, Nan, 0, "" -> False


## Casting 
---
- 암묵적 casting : + 연산자는 *string* 우선되고, 나머지 연산자는 "num"가 우선시 된다. 

- 명시적 casting : 
	Number(),String(),parseInt(),parseFloat()<br/>
	**Number(), String()** 은 class의 생성자이고 , javascript에서 new없이 사용시 함수로 사용되고 type의 변환을 가져온다.<br/><br>	
 Javascript에서는 연산자 실행 전에 type casting이 먼저 일어난다. (비교연산자 주의!!)<br>
 *'==='연산자를 통해 type부터 비교연산을 하게 된다.*