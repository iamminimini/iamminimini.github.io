---
layout: post
title:  "[JavaScirpt] 클로저(Closure)"
date:   2019-06-30 16:49:18 +0900
categories: jekyll update
---

# 클로저(Closure)


함수 밖에서 선언된 변수를 함수 내부에서 사용할 때 클로저 발생한다.     
일반적으로 함수가 종료되면 메모리에서 소멸하기 때문에 function을 재호출해도 변수에 할당했던 값은 소멸하여 호출이 불가하게 됩니다.    
하지만  **클로저는 이러한 외부 변수와 같은 환경 자체를 통째로 기억하는 공간을 형성합니다**  


{% highlight java %}
var global_name = "테스트";

function Name()
{  
    var outer_name = "홍길동";

    function printName(){
        var inner_name = "김병장";

        console.log(global_name);
        console.log(outer_name);
        console.log(inner_name);
        
    }

    return printName;

    -- 출력 -- 
    // 테스트
    // 홍길동
    // 김병장
}

var print = Name();

print();

{% endhighlight %}

Name() 함수를 반환 하여 var print 변수에 저장합니다. 
print 변수에 저장한 것이 함수이므로 print도 함수입니다. 
그러므로 print()로 실행할 수 있습니다.

`` var print = Name(); `` 로 반환받은 것이 클로저 입니다.   
Name() 함수 내에서 정의된 지역 변수인 outer_name이 자신의 수명이 끝나는 Name()을 호출 후에 print(); 호출에도 살아 있다는 것입니다.



- Closure는 function 안에 function이 있게 되면 기본적으로 생성된다.
- Closure는 scope chain이 생성됐을 때의 변수 값들을 보존하고 기억하게 된다.
- 함수가 메모리에서 없어질 때까지 따라다니게 된다.

