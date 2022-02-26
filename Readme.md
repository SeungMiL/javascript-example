# 자바스크립트 잘 쓰는 문구 예제정리

## 블록문

```js
// 블록문
{
  var foo = 10;
}

// 제어문
var x = 1;
if (x < 10) {
  x++;
}

// 함수 선언문
function sum(a, b) {
  return a + b;
}
```

---

## 조건문

1
```js
if(조건식){
    // 조건식이 참이면 이 코드 블록이 실행된다
} else {
    // 조건식이 거짓이면 이 코드 블록이 실행된다
}
```
2
```js
if(조건식1){
    // 조건식1이 참이면 이 코드 블록이 실행된다
} else if (조건식2){
    // 조건식2이 참이면 이 코드 블록이 실행된다
} else {
    // 조건식1과 조건식2가 모두 거짓이면 이 코드 블록이 실행된다.
}
```

**활용 예제**
```js
// x가 짝수이면 result 변수에 문자열 '짝수'를 할당하고, 홀수이면 문자열 '홀수'를 할당한다.
var x = 2;
var result;

if (x % 2) { // 2 % 2는 0이다. 이때 0은 false로 암묵적 강제 변환된다.
  result = '홀수';
} else {
  result = '짝수';
}

console.log(result); // 짝수
```

바로 위 예제를 삼항 조건 연산자로 바꿔 쓸때

```js
var x = 2;

// 0은 false로 취급된다.
var result = x % 2 ? '홀수' : '짝수';
console.log(result); // 짝수
```
---

## switch문

```js
switch(표현식){
    case 표현식1:
      switch 문의 표현식과 표현식1이 일치하면 실행될 문;
      break;
    case 표현식2:
      switch 문의 표현식과 표현식2이 일치하면 실행될 문;
      break;
    default:
      switch 문의 표현식과 일치하는 case 문이 없을 때 실행될 문;
}
```
**활용 예제**
```js
// 월을 영어로 변환한다. (11 → 'November')
var month = 11;
var monthName;

switch (month) {
  case 1: monthName = 'January';
    break;
  case 2: monthName = 'February';
    break;
  case 3: monthName = 'March';
    break;
  case 4: monthName = 'April';
    break;
  case 5: monthName = 'May';
    break;
  case 6: monthName = 'June';
    break;
  case 7: monthName = 'July';
    break;
  case 8: monthName = 'August';
    break;
  case 9: monthName = 'September';
    break;
  case 10: monthName = 'October';
    break;
  case 11: monthName = 'November';
    break;
  case 12: monthName = 'December';
    break;
  default: monthName = 'Invalid month';
}

console.log(monthName); // November
```

---

## 반복문

### 1. for문( 반복 횟수가 명확할 때 주로 사용)

```js
for(변수 선언문 또는 할당문; 조건식; 증감식){
    조건식이 참인 경우 반복 실행될 문;
}
```
**활용 예제**

```js
for (var i = 0; i < 2; i++) {
  console.log(i);
}
```
중첩 반복문 활용예제

```js
for (var i = 1; i <= 6; i++) {
  for (var j = 1; j <= 6; j++) {
    if (i + j === 6) console.log(`[${i}, ${j}]`);
  }
}
```
### 2. while문( 반복 횟수가 불명확할 때 주로 사용)

```js
var count = 0;

// count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
while (count < 3) {
  console.log(count); // 0 1 2
  count++;
}
```
**활용 예제**
```js
var count = 0;

// 무한루프
while (true) {
  console.log(count);
  count++;
  // count가 3이면 코드 블록을 탈출한다.
  if (count === 3) break;
} // 0 1 2
```
### 2-1. do...while문
코드블록을 먼저 실행하고 조건식을 평가한다. 따라서 코드블록은 무조건 한번 이상 실행된다.

**활용예제**
```js
var count = 0;

// count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
do {
  console.log(count);
  count++;
} while (count < 3); // 0 1 2
```

---

### break 문
레이블 문, 반복문, switch문의 코드 블록을 탈출하며 그 외에 break 문을 사용하면 SyntaxError(문법에러)가 발생한다.

레이블 문이란? 식별자가 붙은 문을 뜻함. 
중첩된 for 문 외부로 탈출할 때 유용하지만 그 밖의 경우에는 일반적으로 권장하지 않는다.-> 이유: 프로그램 흐름이 복잡해져서 가독성이 나빠지고 오류를 발생시킬 가능성이 높아지기 때문

**활용 예제-특정 문자의 인덱스(위치) 검색**
```js
var string = 'Hello World.';
var search = 'l';
var index;

// 문자열은 유사배열이므로 for 문으로 순회할 수 있다.
for (var i = 0; i < string.length; i++) {
  // 문자열의 개별 문자가 'l'이면
  if (string[i] === search) {
    index = i;
    break; // 반복문을 탈출한다.
  }
}

console.log(index); // 2

// 참고로 String.prototype.indexOf 메서드를 사용해도 같은 동작을 한다.
console.log(string.indexOf(search)); // 2
```

---

### continue 문
반복문의 코드 블록 실행을 현 지점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동시킨다. break 문처럼 반복문을 탈출하지는 않는다.

```js
var string = 'Hello World.';
var search = 'l';
var count = 0;

// 문자열은 유사배열이므로 for 문으로 순회할 수 있다.
for (var i = 0; i < string.length; i++) {
  // 'l'이 아니면 현 지점에서 실행을 중단하고 반복문의 증감식으로 이동한다.
  if (string[i] !== search) continue;
  count++; // continue 문이 실행되면 이 문은 실행되지 않는다.
}

console.log(count); // 3

// 참고로 String.prototype.match 메서드를 사용해도 같은 동작을 한다.
const regexp = new RegExp(search, 'g');
console.log(string.match(regexp).length); // 3
```

활용예제
```js
// continue 문을 사용하지 않으면 if 문 내에 코드를 작성해야 한다.
for (var i = 0; i < string.length; i++) {
  // 'l'이면 카운트를 증가시킨다.
  if (string[i] === search) {
    count++;
    // code
    // code
    // code
  }
}

// continue 문을 사용하면 if 문 밖에 코드를 작성할 수 있다.
for (var i = 0; i < string.length; i++) {
  // 'l'이 아니면 카운트를 증가시키지 않는다.
  if (string[i] !== search) continue;

  count++;
  // code
  // code
  // code
}
```