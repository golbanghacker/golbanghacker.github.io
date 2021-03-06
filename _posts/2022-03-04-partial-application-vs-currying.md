---
title: "부분 적용과 커링"
date: 2022-03-05 11:40:00 +0900
categories: blog
tags: programming
---

# 부분 적용과 커링

부분 적용(partial application)은 함수의 매개변수 값을 처음부터 고정시켜 항수(arity, 인수(parameter, 매개변수) 개수)가 더 작은 함수를 생성하는 기법이다. 쉽게 말해, 매개변수가 5개인 함수가 있을 때 3개의 값을 제공하면 나머지 두 매개변수를 취할 함수가 생겨난다.

커링(currying)처럼 부분 적용도 함수의 길이를 직접 줄이는 임무를 수행하지만 방법은 조금 다르다. 커리된 함수가 사실상 부분 적용된 함수라서 두 기법을 혼동하는 사람들이 많다. 가장 주된 차이점은 매개변수를 전달하는 내부 메커니즘이다.

커링은 부분 호출할 때마다 단항 함수를 중첩 생성하며, 내부적으로는 이들을 단계별로 합성하여 최종 결과를 낸다. 커링은 여러 인수를 부분 평가하는 식으로도 변용할 수 있어서 개발자가 평가 시점과 방법을 좌지우지할 수 있다.

```jsx
// 커링
var curriedFn = function(a) {
	return function(b) {
		return function(c) {
			return a + ", " + b + ", " + c + "는 좋은 친구들입니다.";
		}	
	}
}
```

반면, 부분 적용은 함수 인수를 미리 정의된 값으로 묶은(할당한) 후, 인수가 적은 함수를 새로 만든다. 이 결과 함수는 자신의 클러저에 고정된 매개변수를 갖고 있으며, 후속 호출 시 **이미 평가를 마친** 상태이다.

```jsx
// 부분 적용
var partialAppliedFn = function(a) {
	return function(b, c) {
		return a + ", " + b + ", " + c + "는 좋은 친구들입니다.";		
	}
}
```

부분 적용과 커링은 모두 유익한 기법으로, 어느 기법을 택하든지, 함수를 여러 단항 훔수들로 몸집을 줄이는 동시에, 맘대로 자신의 스코프 밖에 위치한 객체에 접근하지 못하게끔 적정한 개수의 인수를 공금하는 효과가 있다. 필요한 데이터를 얻는 로직을 분리하면 재사용 가능한 함수로 만들 수 있다. 무엇보다, 함수의 합성을 단순화한다는 장점이 있다.

참고 : 루이스 아텐시오, <<함수형 자바스크립트>>
