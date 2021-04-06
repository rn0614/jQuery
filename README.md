# jQuery

> jQuery 는 일종의 패키지로 javaScript를 쉽게 쓰기 위한 라이브러리



## jQuery 실행하는 법

1. jQuery 파일 다운로드 후 사용:`<script src="jquery-3.6.0.min.js"></script>`

2. CDN 호스트 이용하는 방식 : `<script src="https://jquery.com/jquery-3.6.0.min.js"></script>`



## jQuery 구조

기본구조 : `$(선택자).메서드(매개변수);`형태를 가진다.

$: jQuery의 요약어

`선택자` : 적용할 대상

`메서드` : 이벤트 문구로 매개변수의 값을 통해 상황을 제어



var 변수 = $("선택자").메소드(); 으로 정의하고 변수.메소드(); 사용 가능



보통 메서드는 매개변수들이 정해져 있는데

.ready(실행할 문장) -> 그냥 안에 ready 하면 자동으로 실행될 문장만 필요

.on('이벤트', 실행할 문장) -> 어떤 '이벤트' 상황과 실핼할 문장 필요

.css({속성:속성값}) -> 어떤 속성(목적)과 해당 속성값(변수)가 필요



## 선택자

> 선택자는 적용하는 주체를 뜻함.

- 전체 선택자 :  $(document) 

- 직접 선택자 
  1. `태그` : $("태그명") 
  2. `id` : $("#id명")
  3. `class` : $(".class명") 
- 인접 관계 선택자
  - 자식(바로 한칸 아래) : $("선택자1 > 선택자2")
  - 후손(아래이기만 하면 전부) : $("선택자1 선택자2") 
  - 형제(+는 하나만 ~ 는 모두) : $('#객체 + 속성'); // $('#객체 ~ 속성');
- 필터 선택자
- 속성 선택자 : 요소[속성 = 값]  ex) input[type="text"]



전체 문서를 뜻하는 `document`, 윈도우 창을 뜻하는 `window`, 상위 선택자를 뜻하는`this` 가 추가로 있음. 





## jQuery 변수(선택자가 복수일 때 적용)

> 여러개를 찾을 경우 변수명을 선언하여 코드를 줄임

`var $변수명 = $('선택자');`  : `var tds = document.getElementsByTagName('td');` 와 동일

해당 선택자들은 변수의 배열로 선언됨

- each(인덱스) : 인덱스+1 번째 선택자 /인덱스는 0부터 시작한다
- hover(마우스 올렸을 때 실행, 마우스 뗐을 때 실행 )



## 메소드(이벤트)

> 특정 상황을 나타내는 요소
>
> on이용시 여러 이벤트 동시 실행 가능 `$('선택자').on('이벤트 유형1 2 3...', 실행함수)`

1. 윈도우 이벤트 ( `ready`/ `resize`/ `scroll`/ `load`/ `unload` )
2. 입력 양식 이벤트( `submit`/ `reset`/ `change`/ `focus`/ `blur`)
3. 마우스 이벤트
4. 키보드 이벤트( `keyup`/ `keydown`/ `keypress`)



#### on 사용법(복수 이벤트 사용을 위한)

1. 선택자.on(이벤트1).on(이벤트2)
2. 선택자.on(이벤트1, 이벤트2)



#### 동적 연결 이벤트(이벤트 실행 후 추가 연속이벤트)

$(document).on("이벤트", "이벤트 발생 객체(새로 생성된 객체)", 실행함수);





### 1. 윈도우 이벤트

- ready : 문서 객체 요소(DOM 요소)가 모두 로드됐을 때 발생 (상시 이벤트에 사용)

``` javascript
//행동 시 선택자가 문장을 실행함.
$(document).ready(function(){
    $(선택자).on('행동', function(){
        행동하면 실행할 문장
    });
});
```

- resize : 윈도우 창 크기 변경 시 발생

``` javascript
//윈도우 창 크기 변경시 사진크기 변경
$(document).ready(function(){
	imgResize();	//초기 리사이징
	$(window).on('resize',function(){		// 리사이징하면 실행
		imgResize(); // 화면 변할때 리ㅅ이징
	});
			
	function imgResize(){
		//윈도우 가로 길이
		var winWidth=$(window).width();
		// 윈도우 세로 길이
		var winHeight= winWidth * 세로크기(px)/가로크기(px);
		
		//이미지의 가로길이 세로길이 설정
		$('#topImg').css({'width':winWidth,'height':imgHeight});
	}
});
```

- css : 요소의 스타일(CSS) 변경

```javascript
$(document).ready(function(){
				//여러 속성을 한 번에 적용
				$('선택자').css({
					float:'정렬방향',
					background:'배경색',
					color:'글자색',
					width:'너비',
					height:'높이'
				});
```

- scroll : 스크롤 내릴 때 발생
- load : 문서가 객체 요소(리소스,이미지 음악포함) 모두 로드 됐을 때 발생 
- unload : 문서 객체를 닫을 때 발생





### 2. 키보드 이벤트

- keydown : 키를 누를 때 발생
- keypress : 글자가 입력될때 발생(영어, 숫자 입력만 인식)
- keyup : 키에서 손을 땔 때 발생



### 3.입력 양식 이벤트

- submit : submit 버튼 누를 때
- reset : reset 버튼 누를 때
- change : 내용을 변경할 때
- focus : 초점을 맞출 때
- blur : 커서를 잃었을 때





### 동적 방식 처리(이벤트 1로 이벤트2가 생겼을 때 이벤트 2 실행방법)

``` javascript
$(document).ready(function(){
	//버튼 클릭했을 때 : 새버튼을 2개 생성
	$('기존생성자').on('click',function(){ //이벤트1
		$(this).after(이벤트1)
	});
    
    $(document).on('click','새로 생긴 생성자',function(){ //이벤트2
		이벤트2
	});
});
```









#### 입력란에서 엔터치면 다음 입력란으로 넘어가는 법

> 입력란 -> 엔터([ENTER]의 아스키코드값(13) 출력) -> 인식하면 다음 입력란으로 focus 하기



4월/6일

9-10(select-change-event) : 선택시 문자 변환 &가격시 계산해서 합계 출력

``` javascript
// 선택한 select의 value 값을 출력할 위치에 출력함
$(document).ready(function(){
	$('select 선택자').on('change',function(){
		$('출력할 곳 선택자').text($(this).val());
	})
});
```



``` javascript
$(document).ready(function(){
	var price=4500000;
	var amount,chkAmount=0, optAmount=0;
	var $checkBox=$(':checkBox');
	
	// 주문액을 계산, 출력하는 함수
	function showAmount(){
		amount = price + optAmount+chkAmount;				
        $('#amount').text(amount.toLocaleString()+"원") //toLocaleString: 천 단위 구분(,)
	}
				
	//select 태그의 option 변경 시 기본 옵션 금액 계산
	$('#basicOption').on('change',function(){
		optAmount = parseInt($(this).val()); // parseInt를 통해서 정수화
		showAmount();
	})
    
	//checkbox 클릭시 선택 옵션 계산(checkAmount)
	$checkBox.on('click',function(){
		chkAmount=0;
					
	// 각 체크박스마다 체크 되었는지 확인(변수 배열) : 배열의 각 요소마다 체크 유무 확인
		$checkBox.each(function(){
			if($(this).is(':checked')){
           		chkAmount += parseInt($(this).val());
			}
		});	
		showAmount(); // 다 한후 showAmount 실행
	});
});
```

10-11 이벤트 stop, prevent로 이벤트 실행 취소



text, html

prepend,append,before, after,empty,remove를 통한 추가 위치 결정



11-12  

attr  : `var 변수 = $('선택자').attr('속성');` 선택자의 속성을 추출하는 메소드

addClass, removeClass,toggleClass

slideDown, slideUp

show, hide, toggle

fadeIn, fadeOut, fadeToggle, fadeTo



1-2 애니메이션



jQuery로 가능한 시각적 효과
- Basic 효과 : hide() / show() / toggle()
- Sliding 효과 : slideDown() / slideUp() / slideToggle()
- Fading 효과 : fadeIn() / fadeOut() / fadeToggle() / fadeTo()
- Animate 효과 : animate(속성) 



공통 인수
- duration :효과 진행 속도(slow / normal / fast / 3000)
- callback : 효과 완료 후에 수행할 함수 
- easing : 전체 애니메이션의 적용 시간 비율을 원하는 진행 비율로 매핑
  - swing : 사이곡선 (느리게 시작해서 빠르게 진행되다가 나중에 다시 느려지는 효과)
  - linear : 선형 (일정 속도로 진행)

