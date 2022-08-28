# 1. 쏙쏙 들어오는 함수현 코딩에 오신 것을 환영합니다
1. 함수형 프로그래밍
	* 학문적 정의 : 부수효과가 없는 순수 함수를 사용하는 프로그래밍  
        	* 문제점 : 부수효과가 없으면 개발의 의미가 없음  
	* 실제 : 함수형 프로그래밍에서도 비순수함수를 **잘** 다루는 기술을 사용
2. 코드 분류
	* 액션 : 부수효과를 발생시키거나 호출의 결과가 계속 바뀌는 함수
	* 계산 : 같은 입력이면 항상 같은 결과를 주는 함수
	* 데이터

# 2. 현실에서의 함수형 사고
1. 변경 가능성에 따라 코드 나누기
	* 계층형 설계 (stratified design)              
	
	변경 가능성 | 레이어              | 의존성 | 수정난이도 |
	|:------------: | :---------------: | :-------: | :------------: | 
	높음               |비즈니스 규칙 | 낮음      | 낮음             |
	                       | 도메인 규칙 |||
	낮음               | 기술 스택        | 높음       | 높음             |  
2. 분산 시스템 타임라인으로 시각화
	* **!!--소스 만들기와 반죽펴기를 바꿔야 할듯--!!**
	* 분산 시스템의 서로 다른 타임 라인의 순서보장 필요
	* 타임라인 커팅
		* 타임라인 중 독립적으로 동작해도 되는 부분을 분리하는 방식인 듯
		* 그래서 액션들의 올바른 순서를 보장하게 만듦
	
## 감상  
보통 비/순수함수란 단어를 사용한다. 비순수는 부정적, 순수는 긍정적이라는 어감이라 받아들일 때의 감정이 다르다. 반면 액션/계산이라는 단어를 사용하니 둘다 대등한 느낌을 주게 만들어, 좀더 객관적이고 균형있게 바라볼수 있게 만들어 준다. 그리고 함수형 프로그래밍이 아니라 함수형 사고란 단어를 사용한다. 이렇게 새로운 단어를 도입해서 기존의 생각패턴을 바꾸어 내용을 이해하게 만드는게 작가의 의도중 하나일 것 같다.
# 3. 액션과 계산, 데이터의 차이를 알기
1. 개발과정에서
	1. 문제에 대해 생각할때
		* 주의할 부분 - 액션
		* 데이터로 처리할 부분
		* 결정을 내려야할 부분 - 계산
	2. 코딩할 때
		* 액션에서 계산을 분리, 계산에서 데이터를 분리
		* 액션을 계산으로, 계산을 데이터로 변경
	3. 코드를 읽을 때
		* 액션, 계산, 데이터로 구분
		* **숨어 있는 액션**까지도 찾아냄
2. 현실에서
	1. 액션은 호출시점과 횟수에 의존 
	2. 액션의 단계를 나눠서, 계산과 데이터를 분리
	3. 계산은 더 작은 계산과 데이터로 나누고 연결
	4. 계산단계는 찾기가 어려움 - 사고과정에 녹아 있어서 무의식적으로 처리하는 부분
3. 데이터의 장점
	1. 직렬화 가능
	2. 동일성 비교 가능
	3. 자유로운 해석

* 연습문제
	* 쿠폰독 마케팅에 필요한 것들
		* 친구 추천 - A
		* 친구 추천 10회이상 여부 - C
		* 등급별 쿠폰 얻기 - D 
		* 이메일 보내기 - A
	* 쿠폰독 팀의 목록
		* 이메일 보내기 - A
		* 데이터 베이스에서 구독자 가져오기 - A
		* 쿠폰에 등급 매기기 -  ~~C~~ D  
		* 데이터 베이스에서 쿠폰 읽기 - A
		* 이메일 제목 - D
		* 이메일 주소 - D
		* 추천 수 - ~~C~~ D
		* 어떤 이메일이 쿠폰을 받을지 결정하기 - C
		* 구독자 DB 레코드 - D
		* 쿠폰 DB 레코드 - D
		* 쿠폰 목록 DB 레코드 -D
		* 구족자 목록 DB 레코드 - D
		* 이메일 본문 - D
4. 쿠폰독
	* 액션의 사용을 최소화
	* 액션을 계산으로 최대한 변경
		--> 쉽게 테스트 가능
	* 데이터를 계산해서 다른 데이터를 생성
	* 결과적으로 나온 데이터를 액션에서 사용

### 쉬는시간
	Q. 	대용량 데이터인 경우, 비효율적이지 않나?
	A. 	메모리 부족으로 동작하지 않을수도 있다. 하지만 실행하기전에 최적화는 좋지 않다.
		최적화를 위해 수정할 때, 계산은 바꿀 필요가 없다.
		액션만 바꾸면 되기에, 수정이 편리하다.		
* 계산
	* 액션보다 좋은점
		* 테스트 쉽다
		* 기계적/정적 분석이 쉽다
		* 조합하기 좋다
	* 걱정하지 않아도 되는 점
		* 동시에 실행
		* 과거에 실행했던 것이나 미래에 실행할 것
		* 실행횟수 
* 액션
	* 다루기 어려움
	* 소프트웨어 실행하는 이유
	* 잘 사용하는 방법
		1. 최소한으로 사용
		2. 작게 만듦
		3. 외부와 상호작용하는 것을 제한 (????)
		4. 호출 시점에 의존하는 것을 제한

# 4. 액션에서 계산 빼내기
1. 더 쉬운 테스트를 위한 조건
	1. DOM 업데이트와 비즈니스 규칙 분리
	2. 전역변수는 없어야 함
2. 더 쉬운 재사용을 위한 조건
	1. 전역변수 없어야 함
	2. DOM 사용을 가정하면 안 됨
	3. 함수가 결괏값을 리턴
	
```
특이점
전역변수도 액션으로 생각함
일반적으로 생각하면 데이터라고 할 것 같은데, 사용하는 시점에 따라 값이 바뀔 수 있기 때문에 액션으로 판단하는 것 같음
```
3. 계산 추출 단계리팩토링
	1. 함수 추출 - 계산 코드를 찾아서 빼낸다
	2. 암묵적 입력과 출력을 찾는다
	3. 암묵적 입력은 인자로, 출력은 리턴값으로 변경
* 연습문제 1
	* 전역변수는 안 없앤것 같음 (shopping_cart가 여전히 있다.)

* 연습문제 2

```javascript
function getTex(total) {
	return total * 0.10;
}

function update_tax_dom() {
	set_tax_dom(getTex(shopping_cart_total));
}
```

* 연습문제 3
	* 이건 몽창 맞음

* 연습문제 4

```javascript
const isFreeShipping = (item, total) => item.price+total >= 20;

function updateShippingIcons() {
	const buyButtons = getBuyButtonsDom();
	for(var i=0; i<buyButtons; i++) {
		const button = buyButtons[i];
		const item = button.item;
		if(isFreeShipping(item, shoppingCartTotal)) {
			button.showFreeShippingIcon();
		} else {
			button.hideFreeShippingIcon();
		}
	} 
}
```

* 연습문제 5
	* 이것도 과연 전역변수가 없다고 할 수 있을까? (shoppingCartTotal)

# 5. 더 좋은 액션 만들기
1. 쉬는 시간
	1. 라인 수가 늘어나도, 작은 함수의 사용으로 이해하기 쉽고 재사용이 쉬워짐
	2. 배열 복사로 자원을 더 사용하지만, 런타임에서 메모리를 효율적으로 사용. 필요시 나중에 최적화
2. 암묵적 입력과 출력은 최소화
	1. 암묵적 입력/출력을 줄이면 테스트가 쉽고 재사용이 편리
	2. 연습문제     
	
```javascript
	const addItemToCart = (name, price, cart) => {
		const newCart = addItem(cart, name, price);
		calcCartTotal(newCart);
		return newCart;
	}
	
	const calCartTotal = (cart) => {
		const total = calcTotal(cart);
		setCartTotalDom(total);
		updateShippingIcons(cart);
		updateTaxDom(total);
	} 
	
	const setCartTotalDom = (cart) => { ... }	
	const updateShippingIcons = (cart) => { ... }
	
	consgt updateTaxDom = (total) => {
		setTexDom(calcTax(total));
	}
```
3. 설계는 엉켜있는 코드를 푸는 것
	1. 장점 - 재사용 / 유지보수 / 테스트가 쉬워진다.
	2. 일반화된 함수 사용
		1. addItem(cart, item) ==> addElementLast(array, elem)
4. 연습문제

```javascript
const setShowButtonIcon = (button, isShow) => {
	if(isShow) {
		button.showFreeShippingIcon();
	} else {
		button.hideFreeShippingIcon();
	}
}

const isFreeShippingWithItem = (cart, item) => {
	const newCart = addItem(cart, item);
	return getsFreeShipping(newCart);
}

const updateShippingIcons = (cart) => {
	getBuyButtonsDom()		
		.map(button=>[button, isFreeShippingWithItem(cart, button.item)])
		.forEach(([button, isIconShow])=>setShowButtonIcon(button, isIconShow))
}
```		
