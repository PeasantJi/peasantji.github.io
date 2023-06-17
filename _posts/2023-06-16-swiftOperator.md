---
layout: single
title:  "스위프트 연산자"
excerpt: "스위프트 연산자의 종류와 사용법"
header:
  teaser: /assets/img/operator.jpg
  image: /assets/img/operator.jpg
  caption: "Photo credit: [**ytimg**](https://i.ytimg.com/vi/Svaq3jVy8sU/)"
categories:
  - swiftgrammar
tags:
  - Swift
  - Operators
---

연산자(Operator)
---
- 특정한 문자로 표현한 함수
- 스위프트에서는 부동소수점 타입도 나머지 연산 가능

### 연산자 사용 목적
- 값을 할당하기
- 수학에서 쓰이는 연산자 역할 수행
- 값 비교

### 연산자의 종류
1. 할당/산술 연산자

  |연산자|부호|설명|
  |-----|----|----|
  |할당(대입)연산자|A=B|A에 B 값을 할당|
  |더하기 연산자|A+B|A+B 값을 반환|
  |빼기 연산자|A-B|A-B 값을 반환|
  |곱하기 연산자|A*B|A 곱하기 B 값을 반환|
  |나누기 연산자|A/B|A 나누기 B 값을 반환|
  |나머지 연산자|A%B|A를 B로 나눈 나머지를 반환|

2. 비교 연산자(모두 불리언 값을 반환)

  |연산자|부호|
  |-------|----|
  |값이 같다|A==B|
  |값이 크거나 같다|A>=B|
  |값이 작거나 같다|A<=B|
  |값이 크다|A>B|
  |값이 작다|A<B|
  |값이 같지 않다|A!=B|
  |**참조가 같다|A===B|
  |참조가 같지 않다|A!==B|
  |패턴 매치|A~=B|

  ** A와 B가 참조 타입일 때 같은 인스턴스를 가리키는지 비교하여 불리언 값을 반환

3. 삼항 조건 연산자
- 피연산자가 세 개인 연산자

  |연산자|부호|설명|
  |-----|----|----|
  |삼항 조건 연산자|Question ?A:B|Quesition(불리언 값)이 참이면 A를, 거짓이면 B를 반환|

  - 예시 코드
  ```swift
  var valueA: Int = 3
  var valueB: Int = 5
  
  // valueA가 valueB 보다 크면 valueA값을 반환, 아니면 valueB를 반환
  var biggerValue: Int = valueA > valueB ? valueA : valueB //5
  
  valueA = 0
  valueB =-3
  
  //valueA가 valueB 보다 크면 valueA값을 반환, 아니면 valueB를 반환
  biggerValue = valueA > valueB ? valueA : valueB //0
  
  var stringA: String = ””
  var stringB: String= “String”
  
  //stringA의 값이 비어있으면 1.0을 반환, 아니면 0.0을 반환
  var resultValue: Double = stringA.isEmpty ? 1.0 : 0.0 //1.0
  
  //stringB의 값이 비어있으면 1.0을 반환, 아니면 0.0을 반환
  resultValue = stringB.isEmpty ? 1.0 : 0.0 //0.0
  ```

4. 범위 연산자
- 값의 범위를 나타낼때 사용

  |표현|설명|
  |----|------|
  |A…B|A부터 B까지, A,B포함|
  |A.. <B|A부터 B미만|
  |A…|A이상|
  |…A|A이하|
  |.. <A|A미만|

5. 부울 연산자
- 불리언 값의 논리 연산을 할 때 사용

  |표현|설명|
  |----|------|
  |!B|B(불리언 값)의 참, 거짓을 반전|
  |A && B|A와 B의 불리언 AND 논리 연산|
  |A || B|A와 B의 불리언 OR 논리 연산|
  
6. 비트 연산자

  |표현|설명|
  |----|------|
  |~A|A의 비트를 반전|
  |A & B|A와 B의 비트 AND 논리 연산|
  |A | B|A와 B의 비트 OR 논리 연산|
  |A ^ B|A와 B의 비트 XOR 논리 연산|
  |A >> B, A << B|A의 비트를 B 만큼 비트를 시프트|
  
7. 복합 할당 연산자
- 할당 연산자와 다른 연산자가 하는 일을 한 번에 결합

  |표현|같은 표현|
  |----|------|
  |A += B|A = A + B|
  |A -= B|A = A - B|
  |A *= B|A = A * B|
  |A /= B|A = A / B|
  |A %= B|A = A % B|
  |A <<= N|A = A << N|
  |A >>= N|A = A >> N|
  |A &= B|A = A & B|
  |A |= B|A = A | B|
  |A ^= B|A = A ^ B|
  
9. 기타 연산자

  |연산자|부호|설명|
  |-----|----|-----|
  |nil 병합 연산자|A ?? B|A가 nil이 아니면 A를 반환, A 가 nil이면 B를 반환|
  |부호변경 연산자|A ?? B|A가 nil이 아니면 A를 반환, A 가 nil이면 B를 반환|
  |옵셔널 강제 추출 연산자|O!|O(옵셔널 개체)의 값을 강제로 추출|
  |옵셔널 연산자|V?|V(옵셔널 값)를 안전하게 추출,V(데이터 타입)가 옵셔널임을 표현|

  
  
