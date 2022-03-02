# normalize  vs  reset

브라우저마다 기본적으로 제공하는 element 의 style을 통일 시키기 위해 사용하는 두 `css`에 대해 알아본다.



### reset.css

`reset.css`는 기본적으로 제공되는 브라우저 스타일 전부를 __제거__ 하기 위해 사용된다. `reset.css`가 적용되면 `<H1> ~ <H6>`, `<p>`, `<strong>`, `<em>` 등 과 같은 표준 요소는 완전히 똑같이 보이며 브라우저가 제공하는 기본적인 styling이 전혀 없다.



### normalize.css

`normalize.css`는 브라우저 간 일관된 스타일링을 목표로 한다. `<H1> ~ <H6>`과 같은 요소는 브라우저간에 일관된 방식으로 굵게 표시됩니다. 추가적인 디자인에 필요한 style 만 CSS 로 작성해주면 된다.

즉, `normalize.css` 는 모든 것을 "해제"하기보다는 유용한 기본값을 보존하는 것이다. 예를 들어 , sup 또는 sub 와 같은 요소는 `normalize.css`가 적용된 후 바로 기대하는 스타일을 보여준다. 반면 `reset.css`를 포함하면 시각적으로 일반 텍스트와 구별 할 수 없다. 또한 normalize.css 는 reset.css 보다 넓은 범위를 가지고 있으며 HTML5 요소의 표시 설정, 양식 요소의 글꼴 상속 부족, pre-font 크기 렌더링 수정, IE9 의 SVG 오버플로 및 iOS 의 버튼 스타일링 버그 등에 대한 이슈를 해결해준다.



# 웹팩 (webpack)

프런트엔드 프레임워크에서 가장 많이 사용되는 모듈 번들러다. 모듈 번들러란 웹 애플리케이션을 구성하는 자원 (HTML, CSS, Javascript, Images 등)을 모두 각각의 모듈로 보고 이를 조합해서 병합된 하나의 결과물을 만드는 도구를 의미함.

#### 웹팩에서의 모듈

웹 애플리케이션을 구성하는 모든 자원을 의미합니다. 웹 애플리케이션을 제작하려면 HTML, CSS, Javascript, Images, Font 등 많은 파일들이 필요한데 이 파일 하나하나가 모두 모듈이다.



# 바벨(Babel) & 폴리필

#### 바벨(Babel)

- ES6/7 코드를 ES5 코드로 Transpiling 해주는 Transpiler
- ES5 이전까지는 표준이 없었고 , jquery 가 브라우저 호환성을 해결해줄 수 있기 때문에 필요 없었음
- Babel은 스크립트 자체가 수정되어야 하는 상황으로 새로운 컴파일이 필요할때 사용
- 자바스크립트 스펙으로 아직 확정되지 않은 Proposal 스펙이 5개의 Stage로 구분되어 존재하는데, Babel은 각각의 Stage 에 대해 Preset을 제공함

#### 폴리필(Polyfill)

- 새로 추가된 전역 객체들(Promise, Map, Set)을 사용가능한 객체로 바꾸어주는 개념
- 브라우저 파편화를 해결하기 위해 지원하지 않는 공백을 메꾸는 스크립트나 기타 코드를 끼워넣어줌



#### 차이점

- Babel => Javascript 의 Syntax 가 아닌 것들을 Javascript 에서 사용할 수 있게 만들어준다

- Polyfill => Javascript 의 Syntax 로 읽히지만 정의되어 있지 않은 객체들을 정의해주는 개념

ex ) Promise 객체는 기존에 존재하지 않는 ES6 에서 추가된 객체로, ES6 이전에서 new Promise() 를 하는 경우 Javascript 의 Syntax 이지만 정의되지 않는 function 이라는 의미에서 '__Promise is not a function__' 의 결과를 보여줌. Polyfill 개념을 이용해 Promise 를 사용할 수 있도록 정의해주는 것을 Babel-Polyfill 이 해줄 수 있다.
