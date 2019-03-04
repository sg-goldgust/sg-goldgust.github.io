---
layout: post
title:  "JavaScript Syntax"
date:   2019-02-26
excerpt: "JavaScript 내장 객체에 대해서 알아보자"
tag:
- JavaScript 
- syntax
- sample
- inner object
comments: true
---
<h1> JavaScript Object </h1>
	<p>JavaScript 내장 모듈의 literal 표현과 method를 살펴보자, 또한 html wrapping 함수를 만들어 보자(자주 사용하는 메서드만 표시하엿다.)</p>
<h2> String Object </h2>
<hr/>
- charAt()
- indexOf(searchvalue,start)
- concat(s1,s2)
- toLowerCase()
- replace(searchvalue,newvalue) : 반복이 있을 경우 첫 번째 value값만 변환이 된다.
- slice(start,end)
- split(separator,limit)
- trim()
- link() : html <a> tag로 mapping 시켜준다.
<p><br/>replace method를 정규표현식을 통해 모든 value의 변환이 가능하고, function을 배정하는 것이 가능하다. </p>
{% highlight javascript %}
var links = {
		'네이버' : 'https://www.naver.com',
		'다음' : 'https://www.daum.net',
}
var str = "네이버와 다음은 한국의 대표적인 포털사이트입니다.";
console.log(str);

var result = str.replace(/(네이버|다음)/g,function(site) {
	return site.link(links[site]);
	//새창을 띄우게 하기 위해서
	//return `<a href = "${links[site]}" target="_blank">${site}</a>`;
});

console.log(result);

//네이버 다음이 아닌 패턴을 동적으로 만들기 위해서 literal이 아닌 new로 객체를 생성하여야 한다.
var filter = Object.keys(links).join('|');

var reg = new RegExp(filter,"g");
var result = str.replace(reg,function(site) {
	return site.link(links[site]);
});
{% endhighlight %}

<h2> Math Object </h2>
<hr/>
- abs()
- floor()
- ceil()
- round()
- pow()
- random()
<p><br/>html wrapping method를 만들어 보자</p>
{% highlight javascript %}
var tours = require('./tour.js');
const perPage = 8;

function range(end){
	var arr = [];
	for (var i =0; i<end ; ++i) {
		arr.push(i)
	}
	return arr;
}

function random(start,end) {
	return Math.floor(Math.random()*end + start);
}

var totalPage = Math.ceil(tours.length/perPage);
var page = random(1,totalPage);
console.log(totalPage,page);

function toPageItem(e) {
	if(e == page) {
		return `<li class = "page-item active">
		<a class = "page-link" href = "#">${e}</a></li>`
	} else {
		return `<li class = "page-item">
		<a class = "page-link" href = "#">${e}</a></li>`
	}
}

function toPagination(items) {
	return `<ul class = "pagination">\n${items}\n</ul>`;
}

var items = range(totalPage)
			.map(toPageItem)
			.join('\n')
			
var pagenation = toPagination(items);
console.log(pagenation);


//html wrapping 을 일반화 하기 위해서 !!
function wrapHtml(tag,item,attrs={}) {
	var arr=[];
	
	for(var a in attrs) {
		arr.push(`${a} = "${attrs[a]}"`);
	}
	var attrstr = arr.join(' ');
	return `<${tag} ${attrstr}>\n ${item}\n</${tag}>`;
}

var pagination = wrapHtml('ul',items,{'class':'pagination'});
console.log(pagination);
{% endhighlight %}

<h2> Date Object </h2>
<hr/>
- toDateString()
- toTimeString()	
<p><br/>1자리 숫자의 경우 '0'을 앞에 두는 메서드를 만들어보자</p>
{% highlight javascript %}
function twoDigitStr(n) {
	return n<10 ? '0'+n : n;
}
{% endhighlight %}

<h2> RedExp Object </h2>
<hr/>

<h2>  JavaScript Object Notation </h2>
<hr/>
eval() 함수에 의한 html 해석은 보안에 취약하기 때문에 JSON 객체로 처리한다.
- parse(string) : JSON객체로 변환
- stringify(JSON object) : string 으로 변환