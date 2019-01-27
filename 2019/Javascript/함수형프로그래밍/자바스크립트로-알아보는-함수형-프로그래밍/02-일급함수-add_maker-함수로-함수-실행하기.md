**함수형 프로그래밍 개요**  
**[일급함수, add_maker, 함수로 함수 실행하기]**

일급함수

함수를 값으로 다룰 수 있는 개념

```
자바스크립트는 변수에 함수를 담을 수 있다.

var f1 = function(a) {return a*a; };
console.log(f1); // 함수의 내용이 보임

var f2 = add;
console.log(f2);  // 함수의 내용이 보임

새로 작성한 익명함수건 미리 선언해둔 함수건 변수에 담을 수 있다는 것이 중요한 개념이다.
```

```
function f3(f) {
	return f();
}

f3(function() {return 10;}); // 10
f3(function() {return 20;}); // 20
```

이러한 일급함수의 개념과 순수함수라는 특징을 이용해서 함수의 **조합성**을 높여나가는 것이 함수형 프로그래밍.

언제 평가해도 상관없는 순수함수들을 많이 만들고, 그 순수함수들을 **값**으로 들고다니면서 필요한 시점, 가장 적절한 시점마다 평가를 하는 방식으로 **다양한 로직**을 만들어 나가는 것이 함수형 프로그래밍.

```
add_maker: 일급함수 + 클로저의 개념이 담긴 예제

function add_maker(a) {
	return function(b) {
		return a + b;
	} // 클로저면서 순수함수.
}

var add10 = add_maker(10); // a에 10 할당.

add10(20); // 30

var add5 = add_maker(5);
var add15 = add_maker(15);

add5(10); // 15
add15(10); // 25

add_maker 는 이런식(!)으로 사용하는 함수

```

```
function f4(f1, f2, f3) {
	return f3(f1() + f2());
}

f4(
	function() {return 2;},
	function() {retrun 1;},
	function(a) {return a*a;}
); // (2+1)*(2+1) = 9

이와 같은 '형태' 의 프로그래밍 방식.

순수함수들(f1,f2,f3,...)을 만들고 순수함수를 조합(f4)하여 큰 로직을 만들어나가는 프로그래밍.
```








