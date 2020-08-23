## HTML(Hyper Text Markup Language)

* 웹 페이지를 작성하기 위한(구조를 잡기 위한)언어

* 웹 컨텐츠의 의미와 구조를 정의

* HTML의 기본 구조

  ```
  <!DOCTYPE html>   # html 문서 정의
  <html>            # html문서의 최상위 요소로 문서의 root를 뜻한다.
    <head> </head>  # 해당 thml문서의 정보를 담고 있다.
                    # (제목, 문자의 인코딩, 외부 로딩 파일 지정)
                    # 브라우저에는 나타나지 않음
  
    <body> </body>  # 브라우저 화면에 실질적으로 나타나는 정보
  </html>
  ```

  * DOM tree: 부모, 형제 관계
  * 요소(element): 태그와 컨텐츠로 구성

    * 태그 별로 속성이 있는데 각 태그마다 사용하는 속성은 다르다.
    * 시멘틱 태그: 의미론적 요소를 담은 태그(HTML5에서)
                            개발자 및 사용자 뿐만 아니라 검색엔진 등에 의미있는 정보의 그룹으로 표현 가능.
      * header: 문서 전체나 섹션의 헤더(머릿말 부분)
      * nav: 내비게이션
      * aside: 사이드에 위치한 공간, 메인 컨텐츠와 관련성이 적은 컨텐츠
      * section: 문서의 일반적인 구분, 컨텐츠의 그룹을 표현
      * article: 문서, 페이지, 사이트 안에서 독립적으로 구분되는 영역
      * footer: 문서 전체나 섹션의 푸터(마지막 부분)
    * 그룹 컨텐츠:
      * p: 문단을 구분지을 때
      * hr: 윗쪽 그룹과 아래쪽 그룹을 나눌 때
      * ol, ul, li: 리스트로 구성을 나누고 싶을 때
      * pre: 미리 작성된 텍스트를 있는 그대로 표시. 블록 형태로 사용
      * blockquote: 인용문을 넣을 수있음
      * div: 박스 형태로 영역이 설정되고 그 안에 정렬됨.
    * 텍스트 관련 컨텐츠:
      * a: 링크
      * b, strong: 굵게, 굵게하면서 강조
      * i, em: 이텔릭체, 이텔릭체 강조
      * span: 줄 단위로 영역이 설정됨. inline속성
      * br: 줄 바꿈
      * img: 이미지
    * 테이블 관련:
      * tr: 표의 가로줄을 만드는 역할
      * td: 셀을 만드는 역할
      * th: 표의 제목을 쓰는 역할
      * thead:
      * tbody:
      * tfoot:
      * caption: 표의 제목을 나타냄.
      * colspan:  열 단위로 합침.
      * rowspan: 행 단위로 합침.
    * form: 서버에 처리 될 데이터를 제공하는 역할
      * action: 어디로 보낼지
      *  method: GET, POST
    * input: 다양한 타입을 가지는 입력 데이터 필드
      * name, placeholder, required, autofocus
      * type: text, radio, checkbox, date, passward, ...
      * label 태그: 서식 입력 요소의 캡션





## CSS(Cascading Style Sheets)

* 스타일, 레이아웃 등을 통해 문서(HTML)를 표시하는 방법을 지정하는 언어

* CSS 적용 방법

  1. inline: 관리하기가 힘듦. (for test)
     `<div style="background-color: red;"></div>`
  2. 내부 참조 방식: 하나의 html에서만 적용. (for study, test)
     `<style>h1 { color: red; }</style>`
  3. 외부 참조 방식: css정의를 파일 단위로 묶어서 필요한 html문서 마다 적용이 가능. 유지보수가 쉬움. but 파일을 따로 만들어서 관리를 해야하기 때문에 css파일을 잘 챙겨야 한다.

* CSS 정의하는 방법

  ```
  h1 {                   # h1은 선택자
    color: blue;         # 선언
    font-size: 15px;     # 속성: 속성값;
  }
  ```

* 선택자: 특정한 요소를 선택하여서 스타일링을 하기 위해 반드시 필요함.

  * 기초 선택자

    * 타입(요소, 태그)선택자

      ```
      h2{ 
        color: orange; 
      }
      ```

    * 아이디 선택자: 문서에서 한번만 사용할 수 있고 한 태그에 단일 아이디 값만 사용할 수 있다.

      ```
      #purple {
        color: purple;
      }
      
      <li id="purple"></li>    적용할 태그
      ```

      

    * 클래스 선택자: 해당 클래스가 적용될 모든 문서를 선택하여 바꿀 수 있다

      ``` 
      .green{ 
        color:green; 
      } 
      .blue{
        clolr:blue;
      }
      
      <h1 class="green"></h1>    적용할 태그 
      <h1 class="green blue"></h1>  여러개의 클래스를 받고 싶을 때, green blue를 적은 순서대로 적용되는 것이 아니라 마지막으로 선언된 것이 적용되기 때문에 blue가 적용된다.
      ```

    * 전체 선택자: * { color: red; }

      ```
       * { 
        color: red; 
        }
      ```

      
  * 고급 선택자
    * 자손 선택자: 하위의 모든 요소를 선택함 (띄어쓰기로 구분)
      선택자1 선택자2 { 속성: 속성값; } `article p { color: red; }`
    * 직계 자손 선택자: 바로 아래의 요소만 선택함 ( > 로 구분)
      선택자1 > 선택자2 { 속성: 속성값; } `div > p { color: blue; }`
    * 형제 요소 선택자: 같은 레벨에 있는 요소를 선택함 (~로 구분)
      선택자1 ~ 선택자2 { 속성: 속성값; } `p ~ section { color: yellow; }`
    * 인접 형제 요소 선택자: 바로 붙어 있는 형제 요소를 선택함(+로 구분)
      선택자1 + 선택자2 { 속성: 속성값; } `div + p { color: purple; }`

* CSS 적용 우선순위

  1. 중요도: !important로 나타냄. 디버깅이 어려울 수 있기 때문에 사용시 주의

  2. 우선순위:

     1. 인라인: 태그에 직접 스타일을 적용한 것
     2. 아이디 선택자
     3. 클래스 선택자
     4. 속성 선택자
        * 셀렉터[속성]: 해당 속성을 가진 요소를 선택
        * 셀렉터[속성=속성값]: 해당 속성값을 가진 요소를 선택
     5. 수도 클래스 선택자
        * 셀렉터 hower: 해당 셀렉터 위에 마우스를 오버했을 때
     6. 요소(타입, 태그)선택자

     > 범용(*) 선택자, ('', +, ~, >) 결합자는 우선 순위에 영향을 미치지 않음

* CSS 상속

  * CSS는 상속을 통해 부모 요소의 속성을 자식에게 상속한다.__(모두는 아님)__
    * text관련 요소는 상속되지만 box model, position 관련요소는 상속되지 않는다.

  1. __코드에 정의된 순서__

  * px, %(기준 사이즈에서 배율), em(상속받은 사이즈에서 배수), rem(root사이즈(최상위 요소html의 사이지를 기준으로)에서 배수)
  * vw(뷰포트 너비의 1%), vh(뷰포트 높이의 1%), vmin(뷰포트에서 가로세로 중에서 가장 짧은 쪽의 1%), vmax(뷰포트에서 가로세로 중에서 가장 긴 쪽에서 1%)
  * Hex(#), rgb, hsl, rgba, hsla

* Box Model

  ![box model](15_HTML_CSS.assets/box%20model-1598174834408.PNG)

  * margin: 테두리 바깥의 외부 여백. 배경색을 지정할 수 없다.
  * border: 테두리 영역
  * padding: 테두리 안쪽의 내부 여백. 요소에 적용된 배경색, 이미지는 padding까지 적용.
  * content: 글이나 이미지 증 요소의 실제 내용
  * box-sizing
    * content-box: default값, 콘텐츠 영역의 크기, padding을 제외한 순수 contents 영역만을 box로 지정
    * border-box: 박스 모델 테두리 기준으로 크기 조절. (border까지의 너비)

![box sizing](15_HTML_CSS.assets/box%20sizing.PNG)

* 마진 상쇄
  * 블록요소에 탑이나 바텀 마진이 결합이 될 때 큰 마진으로 덮어씌어진다.
  * 수직 간의 형제 요소에서 주로 발생
  * margin 대신 padding을 이용해서 해결 가능
* CSS Display

  * block:  줄바꿈이 일어나는 요소. 화면 크기 전체의 가로 폭을 차지한다. 블록 레벨 요소 안에 인라인 레벨 요소가 들어갈 수 있음.
    * div, ul, ol, li, p, hr, form
  * inline: 줄 바꿈이 일어나지 않는 행의 일부 요소. content 너비만큼 가로 폭을 차지한다. 
    * span, a, img, input, label, b, em, i, strong
    * 컨텐트의 너비 만큼 공간을 차지
    * width, height, margin-top, margin-bottom 은 지정할 수 없음
    * 상하여백은 line-height로 지정한다.
  * inline-block: inline처럼 한 줄에 표시 가능하며, block처럼 width, height, margin 속성을 모두 지정할 수 있다.
    * 컨텐트 너비 만큼 공간을 차지
    * width, height, margin-top, margin-bottom 을 지정 가능.
  * none: 공간을 없애 버림. 화면에 표시하지 않는다.
    * visibility: hidden 은 공간은 차지하나 화면에 표시만 안함.

![속성에따른수평정렬](15_HTML_CSS.assets/%EC%86%8D%EC%84%B1%EC%97%90%EB%94%B0%EB%A5%B8%EC%88%98%ED%8F%89%EC%A0%95%EB%A0%AC.PNG)

* CSS Position: 모든 요소는 네모(박스모델)이고, 어떻게 보여지는지(display)에 따라 문서에서의 배치가 달라질 수있다.

  * static: 디폴트 값(기준 위치)
    * 기본적인 요소의 배치 순서에 따름(좌측 상단)
    * 부모 요소 내에서 배치될 때는 부모 요소의 위치를 기준으로 배치 된다.
  * 아래는 좌표 프로퍼티(top, bottom, left, right)를 사용하여 이동이 가능하다.(음수 값도 가능)
    * relative: static 위치를 기준(자기 자신의 과거 위치)으로 이동(상대 위치)
    * absolute: static이 아닌 가장 가까이 있는 부모/조상 요소를 기준으로 이동(절대 위치)
    * fixed: 부모 요소와 관계 없이 브라우저를 기준으로 이동(고정 위치)
      * 스크롤 시에도 항상 같은 곳에 위치

