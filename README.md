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

# 변경 가능한 데이터 구조를 가진 언어에서 불변성 유지하기
* 액션을 동작으로 번역하기 시작함
1. 카피-온-라이트 원칙 세 단계
    1. 복사본 만들기
    2. 복사본 변경하기
    3. 복사본 리턴하기
   --> 불변성을 유지하면서 값을 바꿈
   --> 이렇게 하면 쓰기를 읽기로 바꿀 수 있음

```javascript
// 아래와 같은 일반화된 메서드가 중요
const removeItems = (array, idx, count) => {
	const copy = [...array];
	copy.splice(idx, count);
	return copy
}

```
	* 120쪽 연습문제
```javascript
const addContact = (list, email) => [...list, email];

const submitFormHandler = event => {
	const email = event.target.elements['email'].value;
	mailingList = addContact(mailingList, email)
}
```

3. 쓰면서 읽기도 하는 함수 분리하기
	* 많은 메서드들이 읽기/쓰기를 동시에 하는 경우가 많음 (js 말고 다른 언어도 흔하다)
	* 읽기용 메서드 / 쓰기용 메서드로 구분하는 것이 좋음
	* 125쪽 연습문제
```javascript
const last = (list) => list[list.length-1];
const dropLast = (list) => [...list].slice(0, list.length-1);
const pop = (list) => {last:last(list), array:dropLast(list)}
```
	* 128~130쪽
```javascript
const push = (array, elem) => [...array, elem];
const addContact = (list, email) => push(list, email);
const arraySet = (array, idx, value) => {
	const result = [...array];
	result[idx] = value;
	return result;
}
```
4. 객체에 대한 카피온 라이트
	{...object} --> 이렇게 하면 됨
	* 136~144쪽
```javascript
const objectSet = (object, key, value) => ({
	...object,
	[key]: value
})

const setPrice = (item, newPrice) => objectSet(item, 'price', newPrice);
const setQuantity = (item, newQuantity) => objectSet(item, 'quantity', newQuantity);
const objectDelete = (object, key) => {
	const result = {...object};
	delete result[key];
	return result;
}

const setQuantityByName = (cart, name, quantity) => cart.map(item=>{
	if(item.name === name) {
		return setQuantity(item, quantity);
	}
	return item;
})
```

# 7. 신뢰할 수 없는 코드를 쓰면서 불변성 지키기
1. 방어적 복사
	1. 데이터가 안전한 코드에서 나갈 때 복사(deep copy)
	2. 안전한 코드로 데이터가 들어 올때 복사(deep copy)
	3. 복사-비신뢰 코드-복사 ==> 함수로 분리
	4. 154~155쪽

```javascript
const deepCopy = (target) => {
	if(Array.isArray(target)) {
		return target.map(item=>({...item}));
	}
	return {...target};
}
// R.clone
const payrollCalcSafe = (employees) => {
	const copy = deepCopy(employees);
	const payrollChecks = payrollCalc(copy);
	return deepCopy(payrollChecks);
}	
// R.pipe(deepCopy, payrollCalc, deepCopy)
``` 
2. 161 연습문제
	1: DC, 2: SC, 3: SC, 4: DC, 5: DC
3. 163 연습문제
	1:DC 2:CW 3:~~DC~~ DC와CW 4:~~DC~~CW 5:~~DC~~CW 6:DC 7:DC 8:CW 9:DC 10:DC 

# 8/9 계층형 설계
1. 소프트웨어 설계
	코드를 만들고, 테스트하고, 유지보수하기 쉬운 프로그래밍 방법을 선택하기 위해 미적 감각을 사용하는 것 
2. 계층형 설계
	소프트웨어를 계층으로 구성하는 기술
	각 계층에 있는 함수는 바로 아래 계층에 있는 함수를 이용해 정의
3. 계층형 설계 패턴
	1. 직접 구현
	2. 추상화 벽
	3. 작은 인터페이스
	4. 편리한 계층

### 1. 직접 구현
1. 비슷한 구체화 수준에서 작동하도록 함
2. 다양한 계층의 함수를 호출한다면 구체화 수준이 같지 않다는 증거

178쪽 연습문제
	사이에 새로운 계층일듯함. 가장 낮은 계층에 removeItem(index), findIndex(item)이 있을 거고 removeItemByName이 이 함수들을 사용해 생성될 것 같다 --> 188쪽에 나온다 괜히 기분좋음

190-195쪽 연습문제
```javascript
const isInCart = (cart, name) => indexOfItem(cart, name) !== null;
const setPriceByName = (cart, name, price) => {
	const index = indexOfItem(cart, name);
	if(index === null) {
		return cart;
	}
	const copy = [...cart];
	copy[index] = setPrice(copy[index], price);
	return copy;
}	
// 연습문제의 답에서는 무조건 얕은 복사한 리스트를 반환한다. 
// 난 아무것도 안 바뀌면 값을 복사할 필요가 없다고 생각하는데, 이건 경우에따라서 다를듯. 
// 변환된 코드의 경우 사실 원래 동작과 살짝 바뀌는 문제도 존재한다. 
// name이 동일한 제품이 있으면 동작에 버그 발생, 전재조건으로 이름이 동일한 제품은 없다고 되어있을듯함

const setPriceByName = (cart, name, price) => {
	const index = indexOfItem(cart, name);
	if(index === null) {
		return cart;
	}
	return arraySet(cart, idx, setPrice(copy[index], price)
}
```
 
197쪽 기억하세요
	1. 배열인덱스 쓰기 
		1. 별생각없이 쓸 수 있다.
		2. 코드 내용대로 동작하니까 
	2. 함수 쓰기
		1. 나중에 수정사항있을때 고치기가 너무너무 좋아진다. (캐싱, 전후이벤트 추가, 이름변경등)
		2. 그냥 이거다

// 기타 - 무의식중에 하는 것들을 이렇게 연구해서 상세하게 설명하다니.. 부럽

### 2. 추상화 벽
1. 세부구현을 감추고 인터페이스를 제공
2. 언제쓸까?
	1. 쉽게 구현을 바꾸기 위해 - 결국은 인터페이스를 먼저 만드는 것으로 보임
	2. 코드를 읽고 쓰기 쉽게 만들기 위해
	3. 팀 간에 조율할 것을 줄이기 위해
	4. 주어진 문제에 집중하기 위해
	--> 신경쓸것과 아닌것을 구분
 * 우리 프로젝트 
	1. 폴더내 index만 접근하게 하는 룰
	2. 파스는 파스클라우드에서만 사용

### 3. 작은 인터페이스 
1. 추상화 벽에 만든 함수를 인터페이스라고 생각하면 됨
2. 추상화벽이라는 계층의 크기를 작게 만듦

### 4. 편리한 계층
1. 언제 그만 멈출까?
	1. 코드가 편리하다고 느껴지면 (??)
2. 적용 시점
	1. 구체적인 것을 너무 많이 알아야 하는 시점
	2. 코드가 지저분 하다고 느껴지면 (??)

## 호출 그래프
1. 알수 있는 것
	1. 유지보수성
		- 그래프의 상단에 위치할 수록 고치가 쉬움 
	2. 테스트
		- 그래프의 하단에 위치할 수록 테스트가 중요
		- 위쪽은 코드가 더 많이 바뀔 것이므로, 테스트의 수명이 짧아짐 
	3. 재사용 
		- 아래쪽이 재사용하기가 편함 

# 10/11. 일급함수
1. 함수 이름에 있는 암묵적 인자 
    1. 특징 
        1. 함수 구현이 거의 똑같음
        2. 함수 이름의 구현의 차이를 만듦
    2. 리팩터링 
        1. 함수 이름에 있는 암묵적 인자 확인
        2. 명시적 인자 추가
        3. 하드 코딩된 값을 새로운 인자로 변경
        4. 함수 호출부분 수정
		==> 필드명 문자열로 보내는 것 어떻게 처리할지 (아마도 enum 비슷한 걸로??)
```
2. 명시적 인자가 추가된 함수 생성
3. 기존 함수에서 명시적 인자가 추가된 함수 호출 (어디서 이 함수를 쓸지 모름)
4. 기존 함수가 필요없다면, 함수 호출하는 곳에서 직접 수정
```

2. 일급
	1. 값으로 처리 될 수 있는 모든 것 (변수에 할당, 인자, 리턴값 등등 )
	2. 일급이 아닌 것을 일급으로 바꿀 수 있어야 됨

3. 필드명을 문자열로 받아 처리
	1. typescript 같은 type으로 처리
	2. 런타임에 예외처리 추가 
	==> 런타임 예외처리가 크게 의미가 있는지 모르겠다. 
		비정상 동작을 하지 않게 아얘 에러처리한다는 것이 중요하다면 의미가 있지만,
		그게 아니라면, 함수명을 유지하는게 실수방지에는 좋을 것 같다. 

4. 반복문을 일급으로 변경
	1. 반복문을 설명할 수 있는 이름의 함수로 변경 (코드를 함수로 감싸기)
	2. 반복문내 지역변수를 일반적인 이름으로 변경 (더 일반적인 이름으로 바꾸기)
	3. 함수이름의 암묵적 인자를 명시적 인자로 변경 (암묵적 인자 드러내기)
	4. 반복문내 본문을 함수로 분리  (함수 추출하기)
	5. 반복문이 포함된 함수를 일반적 이름으로 바꾸고, 반복문내 함수를 인자로 변경 (암묵적 인자 드러내기)
	==> 결국 FP 라이브러리에서 제공하는 함수를 만드는 것
	==> 함수 본문을 콜백으로 바꾸기 (replace body with callback)

5. 배열에 대한 카피-온-라이트
연습문제 273 - 278
``` javascript
const push = (array, elem) => withArrayCopy(array, (copy)=>copy.push(elem));
const dropLast = (array) => withArrayCopy(array, (copy)=>copy.pop());
const dropFirst = (array) => withArrayCopy(array, (copy)=>copy.shift());

const withObjectCopy = (object, modify) => {
	const result = {...object};
	modify(result);
	return result;
}

const objectSet = (object, key, value) => withObjectCopy(object, (copy)=>copy[key]=value);
const objectDelete = (object, key) => withObjectCopy(object, (copy)=>delete copy[key]);

const tryCatch(execute, errorHandler) => {
	try {
		execute();
	} catch(error) {
		errorHandler(error);
	}
}

const IF = (test, then, else) => {
	if(test()) {
		return then();
	}
	return else();
}

```

6. 함수를 리턴하는 함수
	이쪽은 처음에는 많이 어려울 듯. wrapLogging이란 함수를 변경하는 과정 한번더 확인해보자
	add1, add10 이런 예제가 쉬울 것 같다.
연습문제 285 - 286
``` javascript
const wrapErrorHandler = (f, errorHandler=()=>null) => (...params) => {
	try {
		return f(...params);
	} catch (err) {
		return errorHandler(err);
	}
}

const makeAdder = (adder) => (input) => input+adder;
```

!! 287쪽 내용 아주 중요. 결국은 함수형을 쓰면 좋은 코드가 나오는 것이 아님. 좋은 코드를 만들기 위해, 필요하면 함수형을 사용하는 것. 연습할때는 함수형의 극한(?)까지 가도 좋지만, 실무에서는 남들도 읽기쉽고, 고치기도 쉬운 코드를 만들어야 함을 명심

# 12. 함수형 반복
1. map
	* forEach를 사용하는 경우자체가 중복이라는 관점
연습문제 299
``` javascript
const result = _.map(({firstName, lastName, address})=>({firstName, lastName, address}))(customer);
const result = _.map(_.pick(['firstName','lastName','address']))(customer);
```
2. filter
연습문제 304
``` javascript
const testGroup = _.filter(({id}) => id%3 === 0)(customers);
const nonTestGroup = _.filter(({id}) => id%3 !== 0)(customers);
```
3. reduce
연습문제 309 - 312
``` javascript
const sum = (numbers) => reduce(numbers, 0, (result, number)=>result+number);
const product = (numbers) => reduce(numbers, 1, (result, number)=>result*number);
const min = (numbers) => reduce(numbers, Number.MAX_VALUE, (result, number)=>number<result?number:result  );
const max = (numbers) => reduce(numbers, Number.MIN_VALUE, (result, number)=>number>result?number:result  );
[] / [] / init / 같은 array / 같은 array / []
```
	* reduce로 할 수 있는 것들
		1. 실행 취소/실행 복귀
		2. 테스트할 때 사용자 입력을 다시 실행하기
		3. 시간 여행 디버깅
		4. 회계 감사 추적
			==> 모든 명령이 계산이고 그것들을 array로 저장후 다시 돌리는 개념인 듯
연습문제 314
``` javascript
const map = (arr, f) => reduce(arr, [], (result, item) => [...result, f(item)]);
const filter = (arr, f) => reduce(arr, [], (result, item) => f(item)?[...result, f(item)]:result);
```

# 13. 함수형 도구 체이닝
1. 체인을 명확하게 만들기
	1. 단계에 이름 붙이기
	2. 콜백에 이름 붙이기
		==> 다른 곳에서 사용되는지 여부에 따라서 둘중 어느것을 쓸지 결정하면 될 것 같다 
2. 스트림 결합
	1.  map, filter, reduce 체인을 최적화 하는 것
	2. 병목이 생겼을 때만 쓰고, 대부분의 경우에는 여러 단계를 사용하는 것이 읽기에 편함 
3. 반복문을 함수형 도구로 리팩토링
	1. 데이터 만들기
	2. 배열 전체를 다루기
	3. 작은 단계로 나누기 
```  javascript
const shoesAndSocksInventory = (products) => {
	const shoesAndSocks = filter(product=>product.type === 'shoes' || product.type === 'socks');
	return reduce(shoesAndSocks, 0, (result, item)=>result+item.numberInInventory);
```
연습문제 348-352
``` javascript
const roster = reduce(evaluations, {}, (result, evaluation)=>{
	const {position, name} = evaluation;
	if(result[postion]) {
		return result;
	}
	return {
		...result,
		[position]: name
	}
})

const recommendations = map(employeeNames, (name)=> ({name, positon: recommendPosition(name)})); 

```

# 14. 중첩된 데이터에 함수형 도구 사용하기
1. 연습문제

``` javascript
const user = {
	firstName: "Joe",
	lastNmae: "Nash",
	email: "JOE@EXAMPLE.COM"
};
update(user, "email", lowercase);

const item = {
	name: "shoes",
	price: 7,
	quantity: 2
};
const tenXQuantity = (item) => update(item, "quantity", (quantity) => quantity * 10);

16 / ~~14~~ / CINDY

```

2. 연습문제
``` javascript
const incrementSizeByName = (cart, name) => nestedUpdate(cart, [name, 'option', 'size'], size=>size+1);
```

387 - 했던 얘기가 나오긴 함. 그대로 안 쓰고 한번 감싸서 쓰는것 
