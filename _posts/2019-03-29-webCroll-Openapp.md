

---
layout: post
title:  "웹 크롤링과 스크레이핑"
date:   2019-03-29
excerpt: "머신러닝, 딥러닝 실전 개발 입문"
tag:
- 웹 크롤링
- 머신러닝, 딥러닝 실전 개발
- BeautifulSoup
- Selenium
- Open Api
comments: true
---



<h1>웹 크롤링과 스크레이핑 </h1>

<p>머신러닝 딥러닝을 위한 자동차 이미지 데이터를 네이버에서 제공하는 Open Api를 사용하여 사진 파일을 저장해 보자</p>



<p> urllib.request :

 get요청으로 request객체를 얻거나(urlopen) , request body를 지정한 파일 경로로 저장할 때 사용한다.(urlretrieve)

 즉 app에서 dom 객체를 얻거나, 파일로 저장할 때 사용한다. </p>



 <p>requests : session, rest방식의 request를 지원한다. </p>



<p> beautifulsoup : html dom을 분석하여, 원하는 객체를 추출가능하다.

JQuery처럼 사용한다. (마치 dom의 특정 태그를 추출하여 조작한다는 점에서 유사하다. 물론 JQuery는 일반적으로 event handle을 위해 사용하지만..) 

생성한 soup객체는 soup.find() , soup.select(CSS 선택자 가능) 형식으로 사용하게 된다.</p>



<p> urllib.parse : url parameter encoding , 절대경로 변환, urlparse()로 url객체를 얻을 때 사용한다. </p>



<hr/>



<p>app에서 response를 얻는 경우, 페이지에서의 script 실행이 불가능하다. 즉 ajax, script실행시 write되는 dom부분에 대해서는 접근이 불가능하다. 또한 네이버 로그인과 같이 입력값에 hidden이 많은 경우, 적절한 request를 보내는 것이 쉽지가 않다..</p>



<p>이를 해결하기 위해!!, 웹 브라우져 자체를 원격조정하여 해당 데이터의 실시간 내용을 읽을 수 있다. python module selenium을 사용한다. selenium사용시 어떠한 브라우져를 사용할지 정하여야 한다. 크롬드라이버, phantomjs지원을 한다.</p>



<p>browser dom객체에서 find_element_by를 통해 원하는 객체를 선택하고, send_keys와 같은 조작을 한다. </p>



<p>Open api를 각 검색엔진들은 지원하고 있다. </p>



{% highlight python%}

import os

import sys

import urllib.request

print("print ok")

{% endhighlight %}



<form action="">

    search keyword : <input type ="text"> <br>

    save file : <input type = "text">

</form>