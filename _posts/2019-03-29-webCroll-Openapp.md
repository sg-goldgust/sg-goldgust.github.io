<script> 
$(function(){ 
     $('p').html('내용을 <b>변경</b>한다.'); 
    document.write("읽은 내용 : " + $('p').html()); });
</script>
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

<p> beautifulsoup : html dom을 분석하여, 원하는 객체를 추출가능하다.
JQuery처럼 사용한다. (마치 dom의 특정 태그를 추출하여 조작한다는 점에서 유사하다. 물론 JQuery는 일반적으로 ) 
생성한 soup객체는 soup.find() , soup.select(CSS 선택자 가능) 형식으로 

</p>
{% highlight python%}

{% endhighlight %}