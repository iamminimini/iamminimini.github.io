---
layout: post
title:  "[Jekyll] Jekyll Themes 적용 방법 "
date:   2019-07-02 10:49:18 +0900
categories: jekyll update
---


[http://jekyllthemes.org/](http://jekyllthemes.org/)

위에 홈페이지에서 jekyll 테마를 한눈에 볼 수 있다. 
맘에 드는 테마를 발견했다면 

![이미지 이름](/image/1.png)
- 홈페이지 클릭 ->  fork- > download 후 사용
- 다운로드 사용 후 내 블로그에 옮겨서 사용


두 가지 방법으로 간단하게 테마를 적용할 수 있다.  
첫번째 방법으로 테마를 적용해보자  


1. 홈페이지로 이동을 하게 되면 해당 테마의 github로 이동을 하게 된다
![이미지 이름](/image/2.png)
2. 오른쪽 상단 Fork를 클릭하게 되면 
![이미지 이름](/image/3.png)
3. 내 Repository 추가 된다.
![이미지 이름](/image/4.png)
4. github Desktop을 이용하거나 git명령어를 사용하여 로컬에 받은 후
5.  bundle install --path vendor/bundle 명령어 입력
6. jekyll server 입력

![이미지 이름](/image/6error.png)
의 에러가 나온다면 bundle exec jekyll serve으로 다시 실행하자
![이미지 이름](/image/7finish.png)

![이미지 이름](/image/5.png)

