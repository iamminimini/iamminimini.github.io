---
layout: post
title:  "[JavaScirpt] 호이스팅(Hoisting)"
date:   2019-06-30 16:49:18 +0900
categories: jekyll update
---

# 호이스팅(Hoisting)
 호이스트(hoist)의 사전적 의미는 `끌어올리다.` 혹은  `들어올리다` 이며,    
 JavaScript에서 호이스팅이란 코드에 사용된 **변수나 함수들의 최상위로 끌어올리는 것**을 의미한다.
 단 선언 부분만 위로 끌어올려지는 것이고 대입하는 부분은 그대로 남겨져 있다.

 함수 내에서 선언한 함수 범위 (local scope)의 변수는 해당 함수 최상위로
 함수 밖에서 선언한 전역 범위(global scope)의 변수는 해당 스크립트의 최상위로 끌여올려진다. 

{% highlight java %}
function Name()
{  
  console.log("First Name :" + name);  
  var name = "Lee";  
  console.log("Last Name :"+ name);  
}

Name();

// First Name : undefined  
// Last Name : Lee  

{% endhighlight %}
다른 프로그래밍 언어의 경우라면 name이 선언되지 않았는데 사용하려고 하기 때문에 에러를 발생시킨다.
하지만 JavaScirpt는 호이스팅 통해 변수 name의 선언을 가장 먼저 해주기 때문에 에러 없이 동작한다.

{% highlight java %}
function Name()
{  
  var name;  // name 변수는 호이스팅된다. 할당은 이후에 발생한다.
  console.log("First Name :" + name);  
  var name = "Lee";  // <- 이때 name에 값이 할당
  console.log("Last Name :"+ name);  
}

Name();

// First Name : undefined  
// Last Name : Lee  

{% endhighlight %}


호이스트 되었을 때 함수와 변수의 이름이 같다면 함수 선언은 변수 선언을 덮어씌운다.

{% highlight java %}

var Name;  // <- 변수 선언

function Name()
{  
  console.log("my name is hong");
}

console.log("typeof :" + typeof myName);      // typeof : function   

{% endhighlight %}



하지만 변수에 값이 할당되었을 경우는 변수 선언이 함수 선언을 덮어 쓰게 된다.

{% highlight java %}

var Name; = "hong"; 

function Name()
{  
  console.log("my name is hong");
}

console.log("typeof :" + typeof myName);      // typeof : String   

{% endhighlight %}
