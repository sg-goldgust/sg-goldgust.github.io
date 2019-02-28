---
layout: post
title:  "JavaScript Syntax"
date:   2019-02-26
excerpt: "JavaScript Array에 대해 알아보자."  
tag:
- JavaScript 
- syntax
- sample
- Array
comments: true
---

# JavaScript Array

JavaScript에서의 Array는 linked-list로 사용되고, script언어 특성상 type이 달라도 같은 arr에 위치하는 것이 가능하다. Java 마찬가지로 배열을 동적으로 메모리상에서 관리한다. 배열은 key index인 object다. 여러가지 예제를 통해 array의 특성을 알아보자.

---
{% highlight javascript %}
var ar =[1,2,5,,,,9,15];

for (var i =0; i<ar.length; i++){
	console.log("ar["+i+"]="+ar[i]);
}
console.log("==============================");
ar.length = 3; //java와 다르게 length가 상수가 아니다. 나머지 값들이 undefined로 배정된다.
for (var i =0; i<ar.length; i++){
	console.log("ar["+i+"]="+ar[i]);
}
console.log("==============================");
ar.length = 10;
for (var i =0; i<ar.length; i++){
	console.log("ar["+i+"]="+ar[i]);
}
console.log("==============================");
ar[20] = 0; //사이 값들이 undefined로 배정된다.
for (var i =0; i<ar.length; i++){
	console.log("ar["+i+"]="+ar[i]);
}
console.log("==============================");
for(var i in ar) {
	console.log("ar["+i+"]="+ar[i]);
}
//실제 데이터가 있는 element에 key i 가 할당 된다.
{% endhighlight %}

- Javascript에서 java와 다르게 length가 상수가 아니다. length 대입시 나머지 값들이 undefined로 배정된다.
- for-in roop의 경우 실재값이 있는 것에 key를 배정하고 roop를 순회한다.

---
{% highlight javascript %}
var ar = [0,1,2,3];
delete ar[1];
console.log("ar[1] =" + ar[1]);

ar["korea"]=4;
console.log('ar["korea"]=' + ar["korea"], ar.length);
console.log('ar["korea"]=' + ar.korea, ar.length);

//ar.length로 for roop 순회시 4번돌지만, for in 으로 순회시 5번 돈다.
for(var i in ar) {
	console.log("ar["+i+"]="+ar[i]);
}


ar[-3.14] = 5;
console.log("ar[-3.14] =" + ar[-3.14], ar.length);
{% endhighlight %}

- Javascript에서 숫자가 아닌 다른 값으로도 배열의 키를 만들 수 있다.
- delete : 배열의 값을 삭제한다.