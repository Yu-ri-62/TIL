# Django

Django 3.1

`pip list`



### 장고의 흐름

__1. 프로젝트 생성 => 2. 서버 실행하기 => 3. 장고 어플리케이션 생성 => 4. 환경설정 => 5. 사용자가 접근할 수 있는 URL을 정의하고 View함수로 연결 => 6. View 함수에서 데이터를 가공하고, 사용자가 보는 브라우저 화면에 렌더링시킴.__

#### 장고 설치하기

```python
pip install django

# 특정 버전으로 받고 싶다
pip install django==3.0.8
# 설치 확인
pip list
```



#### 장고 시작하기

```
django-admin startproject `프로젝트 이름`   # 프로젝트 생성
```

* `프로젝트 이름`라는  폴더가 생성

  * 여기 안에는 `프로젝트 이름` 폴더와 `manage.py` 생성 되어짐

    * first_webex : 프로젝트 설정 파일들이 들어 있음

    * manage.py : 장고 명령어를 실행하기 위한 파일

      `python manage.py 장고명령어`

  * 가장 바깥에 있는 프로젝트 폴더명은 수정 가능하나, setting 파일이 들어있는 폴더명은 건들이지 말자.

  * `cd 프로젝트 이름` 명령어를 통해 `프로젝트 이름` 폴더 안으로 들어가서 장고 실행!!




#### 장고 실행하기__(명령어를 실행하는 경로에 manage.py가 있는지 반드시 확인)__

```
python manage.py runserver
```

* 서버가 잘 만들어 졌는지 확인하기




* 장고 프로젝트는 Application의 집합체로 동작

  * 실제로 어떠한 역할을 해주는 친구가 바로 app.
  * 하나의 프로젝트는 여러 개의 어플리케이션을 가질 수 있음.
    * 어플리케이션 : 하나의 역할 및 기능 단위로 쪼개진 형태.
      * 회원 관리 / 글 작성, 수정, 삭제 / 데이터를 수집, 분석 / ...
      * 어플리케이션을 이렇게 나뉘어야 한다 같은 기준은 없음.
      * 작은 프로젝트라면 어플리케이션을 따로 나누지 않아도 된다.



#### 어플리케이션 생성 (프로젝트 안에 여러 어플리케이션이 존재하며 어플리케이션은 각각의 역할을 한다)

```
python manage.py startapp 앱이름(복수형)
```

* 해당 앱 이름으로 폴더가 생성됨 (앱폴더)
* 바로 할 일이 있다!!! 
  * `setting.py`에 내가 생성한 app을 등록해야함
  * `INSTALLED_APPS`에 가장 윗줄에 등록해 준다.
  * `LANGUAGE_CODE` = 'ko-kr' 왠만하면 소문자로
  * `TIME_ZONE` = 'Asia/Seoul' 앞에만 대문자!!!!

__*필수! 앱을 생성한 다음에 등록을 해야한다*__



#### 환경설정

* 어플리케이션 사용 등록

  ```
  # 프로젝트폴더/settings.py
  
  INSTALLED_APPS = [
  	'앱이름',
  	...
  ]
  ```

* 언어, 시간 설정

  ```
  # 프로젝트폴더/settings.py
  
  LANGUAGE_CODE = 'ko-kr'
  
  TIME_ZONE = 'Asia/Seoul'
  ```



#### **path('url패턴/', 실행이 되어야 하는 views에 있는 함수.해당 path의 별명)**

* `urls.py`에서 입력하는데, 생성된 app에서 views.py에 있는 함수를 import함
  * `form 앱이름 import views`
  * path('url패턴/', views.호출할함수이름)
* 많이 놓치는 부분 : url패턴 뒤에 슬래쉬


* `views.py` 에서 해야할 일
* 함수를 정의 __(첫번째 인자로 **request 필수**!! => view함수는 url로 들어온 요청을 받아야 하기 때문에)__
  * **return은 꼭 필요!**
    * render : 주로 과 함께 respose 할 때 사용하는 함수
    * `return render(request, '~~~.html')`
* `templates` 에서 해야할 일
* 앱 안에 폴더를 만드는데, 폴더 명은 반드시 `templates` 로 만든다.
  * `templates` 폴더안에 `html파일` 을 생성. __(사용자가 url로 들어왔을 때 보여질 페이지)__



## 여기 까지 기본 수정할 파일들 조작 방법



## 장고 동작 정의 방법



#### MTV (MVC 패턴)

* Model : 장고에서는 Model  => 데이터베이스 관리

* View : 장고에서는 Template => 보여지는 페이지 관리

* Controller : 장고에서는 View => 데이터를 어떻게 처리하고 관리하는지 컨드롤



#### 3대장 : 우리가 가장 밀접하게 수정하여야 하는 파일 명

1) urls.py

2) views.py

3) templates (html 들)



#### 코드의 작성 흐름

* urls.py -> views.pt -> template
* 어디에서 주소를 설정하는지 (urls)
* 요청이 들어오면 어떤 파일을 거치게 되는지
* 어디에서 새로운 페이지를 만들면 되는지 (template 폴더)



#### Template Variable

* html 과 같은 template에서 view.py 에서 준비한 변수를 가져다가 쓰는 방법

* render() 의 세번째 인자로 dictionary형태로 값을 넘겨준다.
  여기에 key에 해당하는 문자열이 template에서 사용 가능한 변수명이 된다.

* dictionary 형태로 직접 전달하는 것 보다 `context`라는 변수를 사용해서 넘기는 것이 일반적.

* render() 세번째 인자로 `{'key':value}`와 같이 딕셔너리 형태로 넘겨주면 Template에서 key를 이용하여 value를 가져올 수 있다.

  ```python
  context = {'key': value}
  return render(request, 'index.html', context)
  ```

  ```html
  {{ key }} 이렇게 value를 보여줄 수 있다.
  ```

   

#### Variable Routing(동적 라우팅)

* 동적 라우팅: URL 주소 일부에 변수처럼 값을 전달하는 동적인 주소를 만드는 것

주소 요청 : `http://127.0.0.1:8000/hello/문자열`

`urls.py`에서

```
path('hello/<str(타입):name(저장되는 변수명)>/', views.hello),
```

* int : 숫자 형식으로 받음.

views.py

```
def hello(request, name(저장되는 변수명):
	print(name)
	context = {
		'name': name,
	}
	return render(request, 'hello.html', context)
```

template(hello.html)

```
<body>
이름은 : {{ name }}  # context 의 key 값을 사용하면 value 를 출력한다.
</body>
```

왜 사용할까?

* hi/justing, hi/john 같이 다양한 사람들과 인사를 하는 함수를 작성할 때 
  * 동적 라우팅을 쓰지 않으면 `urls.py`에 일일히 등록해줘야함.
    * 인원이 많아지거나 누구한테 인사해야할지 모를 때 고정적인 방식은 사용하기 어려움.
  * 동적 라우팅을 사용하면 뒤에 사람이름을 변수화 할 수 있다.
    * `hi/<str:name>` 형식으로 나타낼 수 있음.
    * views.py 에서 함수를 정의할 때 인자로 꼭 variable routing 에서 선언한 변수명을 받아야 함.
  * 변수로 사용할 수 있는 type의 종류
    * 구글에서 django url dispatcher 로 검색하면 확인 가능.



#### Django Template Language(DTL) (tag와 filter)

* django template system에서 사용하는 built-in template system이다.

* 조건, 반복, 치환, 필터, 변수 들의 기능을 제공

* 프로그래밍적 로직이 아니라 프레젠테이션을 표현하기 위한 것.

* 파이썬처럼 if, for를

* 로직을 사용할 때 표현 형식 : `{% %}`

* 값을 표현할 때는 : `{{ }}`

* 주석으로 나타내고 싶을 때는 : `{# #}`or `{% comment %}주석 할 내용 {% endcomment %}`

  ```
  <!--<h1>{#{ i * 2 }#}</h1>-->
  {% comment %}<h1>{{ i * 2 }}</h1>{% endcomment %}
  ```

* for 태그

  * 반복을 위한 태그

    ```
  {% for 임시변수 in iterable 한 객체 %}
    {% endfor %}
    ```

  * for empty

    ```
  {% for 임시변수 in iterable 한 객체 %}
    	값이 하나라도 있으면 여기가 실행
    {% empty %}
    	<p> 메뉴가 없습니다. </p> # 비어있을 때 출력
    {% endfor %}
    ```



* if 태그

  * 조건을 구분하기 위한 태그

    ```
  {% if 조건문 %}
    {% elif 조건문 %}
    {% else %}
    {% endif%}
    ```

* 나머지 기타 유용한 dtl문서를 참고. (구글에서 찾을 때 바로 찾는 키워드 django built in template)

  * 조건 연산자 사용 가능

    ```
    <=
    >=
    ==
    !=
    >
    <
    in
    not in
    is
    ```

    

* Form

  * HTML form tag 의미

  * 입력 받은 데이터를 어딘가로 보낼 때 사용.

    ```html
    <form action="" method="GET">   # action : 보내려는 목표 # method : http                                             # method(get/post)
    <form action="" method"GET">
    
        input 데이터를 입력 받게 적절히 코딩 하면 됨.
    
    	# 오락실 버튼
    	<input type="button">
        
        #미사일 버튼(데이터를 action 으로 전송)
    	<input type="submit">
    	       or
    	<button></button>
    </form>
    ```

  * action: 데이터를 보내려는 목적지 주소

    * action="/catch/": `localhost:8000/catch/`
    * action="catch/": `현재주소/catch/`

  * method : http method (GET, POST)

    * GET: 주소에 query string 형식으로 데이터를 전달하는 방식 (정보를 조회할 때 주로 사용)

      `localhost:8000/catch/?데이터명=데이터값&데이터명1=데이터1값&...`

  * `request`라는 장고 함수 선언할 때 넣어주었던 인자에 유저가 요청한 값이 들어있음.

  * action에 들어가는 목표 url설정 주의 사항!!!

    ```
    action+"/catch"
    => 127.0.0.1:8000/catch?name=asdf
    
    현재 주소 : 127.0.0.1:8000/index
    action="catch/"
    => 127.0.0.1:8000/index/catch?name=asdf
    ```

    
