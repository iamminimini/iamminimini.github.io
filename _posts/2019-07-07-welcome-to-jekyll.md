---
layout: post
title:  "[javaScriptScirpt] 이벤트 전달 방식"
date:   2019-07-07 12:49:18 +0900
categories: jekyll update
---

# 이벤트 등록 방법과 이벤트 전달 방식


{% highlight javaScript %}


<input type="button" id="target" value="button" />
<script>
    var t = document.getElementById("target");
    t.addEventListener("click", function(event){
        alert("Hello world, "+event.target.value);
    });
</script>

{% endhighlight %}

addEventListener은 이벤트를 등록하는 가장 권장되는 방식이다. 이 방식을 이용하면 **여러개의 이벤트 핸들러를 등록**할 수 있다.

{% highlight javaScript %}
<input type="button" id="target" value="button" />
<script>
    var t = document.getElementById("target");
    t.addEventListener("click", function(event){
        alert(1);
    });
    t.addEventListener("click", function(event){
        alert(2);
    });
</script>

{% endhighlight %} 


# 이벤트 버블링 (event Bybbling)


엘리먼트에서 이벤트가 감지 되었을 때, 해당 엘리먼트를 포함하고 있는 부모 엘리먼트를 통하여 최상위까지 이벤트가 전달되는 것을 버블링이라고 합니다.


- event.target 
부모의 선언된 이벤트 핸들러는 어디서 이벤트가 발새 했는지 알 수 있습니다.
``event.target``은 최초에 이벤트가 발생한 엘리먼트를 가리키며 ``event.currentTarget``은 실제로 이벤트가 실행되는 엘리먼트를 알려줍니다.

- stopping bubbling
버블링 이벤트는 타킷 엘리먼트에서 위로 올라갑니다. 일반적으로 html 태그까지 올라가며 최종적으로 document객체에 도달합니다. 몇몇 이벤트는 window까지 전달됩니다. 
이를 막기위한 방법으로는 ``event.stopPropagation()``, ``preventDefault()`` 메소드를 제공합니다.


{% highlight javaScript %}
<div onclick="alert("hi")">
  <em onclick="event.stopPropagation()">click</em>
</div>
{% endhighlight %}

처음 코드와 동일하지만 버블링을 막으니 <div>에 선언된 이벤트가 실행되지 않습니다. 만약 엘리먼트에 여러개의 이벤트가 걸려 있다면 ``event.stopImmediatePropagation()``을 통해 전체를 막을 수 있습니다.


# 이벤트 캡쳐링 (event Capturing)


캡쳐링은 위와 반대되는 개념으로 최초 이벤트가 발생한 지점에서 자식요소로 내려가는 과정을 말합니다.   
버블링에 비해 사용빈도가 적으며 addEventListenr()의 세번째 파라미터 (true/false) 를 통해 캡쳐링 or 버블링 단계를 구분할 수 있으며 true이면 캡쳐링이며, false 혹은 인자를 비워두면 버블링이다.


{% highlight javaScript %}
 <script>
document.getElementById("target").addEventListener("click", handler, true);
document.querySelector("fieldset").addEventListener("click", handler, true);
 </script>
{% endhighlight %}


캡쳐링과 버블링이 섞여있을 경우 캡쳐링이 우선시 된다.

# 이벤트 위임

{% highlight javaScript %}
<h1>오늘의 할 일</h1>
<ul class="itemList">
	<li>
		<input type="checkbox" id="item1">
		<label for="item1">이벤트 버블링 학습</label>
	</li>
	<li>
		<input type="checkbox" id="item2">
		<label for="item2">이벤트 캡쳐 학습</label>
	</li>
</ul>

<script>

    var inputs = document.querySelectorAll("input");
    inputs.forEach(function(input) {
        input.addEventListener("click", function(event) {
            alert("clicked");
        });
    });
        
</script> 
{% endhighlight %}


해당 itemList를 클릭했을때 해당 아이템에 대하여 이벤트를 구현할 때 반복문을 이용한 처리는 이벤트가 엄청나게 많을 경우 비효율적일 뿐만 아니라 동적으로 생성된 요소의 이벤트 처리를 해야 할 경우 다시 이벤트처리를 구현해야 하는 번거로움이 존재한다.
"하위 요소에 각각 이벤트를 붙이지 않고 상위 요소에서 하위요소의 이벤트를 제어하는 방식"



{% highlight javaScript %}

// 새 리스트 아이템을 추가하는 코드
    var inputs = document.querySelectorAll("input");
    inputs.forEach(function(input) {
        input.addEventListener("click", function(event) {
            alert("clicked");
        });
    });
        
    var itemList = document.querySelector(".itemList");

    var li = document.createElement("li");
    var input = document.createElement("input");
    var label = document.createElement("label");
    var labelText = document.createTextNode("이벤트 위임 학습");

    input.setAttribute("type", "checkbox");
    input.setAttribute("id", "item3");
    label.setAttribute("for", "item3");
    label.appendChild(labelText);
    li.appendChild(input);
    li.appendChild(label);
    itemList.appendChild(li);
{% endhighlight %}


새로 추가된 리스트 아이템(이벤트 위임 학습)에서 클릭 이벤트가 동작하지 않는 모습을 보입니다.

input 박스에 클릭이벤트 리스너를 추가하는 시점에 리스트 아이템은 두개입니다.
새롭게 추가된 리스트 아이템에는 클릭 이벤트 리스너가 등록되지 않게 됩니다.
리스트의 아이템이 많아지면 많아질수록 이벤트 리스너를 다는 작업 자체가 매우 번거롭습니다. 이 번거로운 작업을 해결할 수 있는 방법이 바로 **이벤트 위임**입니다.


 
{% highlight javaScript %}

// var inputs = document.querySelectorAll("input");
// inputs.forEach(function(input) {
// 	input.addEventListener("click", function() {
// 		alert("clicked");
// 	});
// });

var itemList = document.querySelector(".itemList");
itemList.addEventListener("click", function(event) {
	alert("clicked");
});

// 새 리스트 아이템을 추가하는 코드
// ...
{% endhighlight %}

화면에 모든 인풋 박스에 이벤트 리스너를 추가하는 대신 이제는 인풋 박스의 상위 요소인 ul태그 즉  .itemList에 이벤트 리스너를 달아놓고 하위에 발생한 클릭 이벤트를 감지 합니다. 
앞서 배웠던 이벤트 버블링입니다. 
결과적으로 새로 추가된 리스트 아이템에서 클릭 이벤트가 정상적으로 동작하는 모습을 보실 수 있습니다. 





이벤트 위임은 부모 요소가 자식 요소의 이벤트 처리를 위임받는 것

