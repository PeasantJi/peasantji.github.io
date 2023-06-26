---
layout: single
title:  "스위프트 기본 데이터 타입"
header:
  teaser: /assets/img/swift2.jpg
  image: /assets/img/swift2.jpg
categories:
  - swiftgrammar
---

# 스위프트 기본데이터 타입

## Int와 UInt
1. Int:  
 - +, - 부호를 포함한 정수, Int의 최댓값 이상 UInt의 최댓값 미만을 사용할때 선택
```swift
var integer: Int = -100
print("Int 최댓값: \(Int.max), Int 최솟값: \(Int.min)")
//Int 최댓값: 9223372036854775807, Int 최솟값: -9223372036854775808
```

2. UInt: 
 - - 부호를 포함하지 않는 0을 포함한 양의 정수
```swift
let unsignedInteger: UInt = 50
print("UInt 최댓값: \(UInt.max), Int 최솟값: \(UInt.min)")
//UInt 최댓값: 18446744073709551615, Int 최솟값: 0
```
3. 진수에 따라 정수 28을 표현하는 방법
- 10진수
```swift
let decimalInteger: Int = 28
```
- 2진수: 접두어 0b
```swift
let binaryInteger: Int = 0b11100
```
- 8진수: 접두어0o
```swift
let octalInteger: Int = 0o34
```
- 16진수 : 접두어 0x
```swift
let hexadecimalInteger: Int = 0x1C
```

## Bool: 
 - 참(true) 또는 거짓(false)만 값으로 가지는 자료형
```swift
var boolean: Bool = true
let isEarthFlat: Bool = false
```
## Float: 
 - 32비트의 부동소수 표현, 6자리의 숫자까지만 표현
```swift
var floatValue: Float = 123456.1
```
## Double: 
 - 64비트의 부동소수 표현, 최소 15자리의 십진수를 표현
```swift
var doulbValue: Double = 1234567890.1
```

## Character: 
 - 단 하나의 문자를  의미, 스위프트는 유니코드 9문자를 사용함. 영어는 물론 유니코드에서 지원하는 모든 언어 및 특수기호 등을 사용 가능
```swift
let alphabetA: Character = "A"
//값에 유니코드 문자를 사용가능
let commandCharacter: Character = "❤" 
let 한글변수이름: Character = "ㄱ"
```

## String: 
 - 문자의 나열인 문자열, character와 마찬가지로 유니코드 9문자를 사용하며 앞뒤에 큰따옴표를 사용하여 표현

```swift
//문자열 타입으로 선언
let name: String = "Jisung"
//이니셜라이저로 빈 문자열 생성
var introduce: String = String()
//append() 메서드를 사용하여 문자열 이어 붙이기
introduce.append("제 이름은")
// + 연산자를 통해서 문자열 이어 붙이기
introduce = introduce + " " + name + "입니다."
print(introduce)
//문자의 수 세기
print("name의 글자 수:\(name.count)")
//빈 문자열인지 확인
print("introduce가 비어있습니까?\(introduce.isEmpty)")
//메서드를 통한 접두어, 접미어 확인
// - 접두어 확인
var hasPrefix: Bool = false
hasPrefix = name.hasPrefix("Ji")
print(hasPrefix) // true
// - 접미어 확인
var hasSuffix: Bool = false
hasSuffix = name.hasSuffix("Ji")
print(hasSuffix) //false
//메서드를 통한 대소문자 변환
var convertedString: String = ""
//대문자로 변환
convertedString = name.uppercased()
print(convertedString) // JISUNG
//소문자로 변환
convertedString = name.lowercased()
print(convertedString) // jisung

//프로퍼티를 통한 빈 문자열 확인
let greeting = "안녕"
var isEmptyString: Bool = false
isEmptyString = greeting.isEmpty
print(isEmptyString) // false

//프로퍼티를 이용해 문자열 길이 확인
print(greeting.count) //2
```

## 특수문자(제어문자) : 
 - 백슬레쉬에 특정한 문자를 조합하여 사용
\n : 줄바꿈 문자
\\ : 문자열 내에서 백슬래시 표현
\" : 문자열 내에서 큰따옴표 표현
\t : 탭 문자. 키보드의 탭키
\0 : 문자열이 끝났음을 알리는 null 문자

```swift
print("문자열 안에서 \n 이런 \"특수문자\"를\t사용하면 이런 결과를 볼 수 있습니다.")
"""
문자열 안에서
 이런 "특수문자"를    사용하면 이런 결과를 볼 수 있습니다
"""
print(#"문자열 안에서 특수문자 사용이 싫다면 문자열 앞, 뒤에서 #을 붙여주세요."#)
// 문자열 안에서 특수문자 사용이 싫다면 문자열 앞, 뒤에서 #을 붙여주세요.
let number: Int = 100
print(#"특수문자를 사용하지 않을 때도 문자열 보간법을 사용하고 싶다면 이렇게 \#(number) 해보세요"#)
```

## Any, AnyObject, nil
- Any : 스위프트의 모든 데이터 타입을 사용할 수 있다는 뜻상수의 데이터타입이 Any로 지정되면 변수 또는 상수 어떤 데이터 타입이든지 상관없이 할당
- AnyObject : 클래스와 인스턴스만 할당할 수 있음.
- nil : 특정타입이 아니라 ‘없음’을 나타내는 스위프트의 키워드, nil값을 접근하면 잘못된 메모리 접근으로 런타입 오류 발생
- Never : 특정 함수의 반환 타입으로 사용, 종료되지 않는 함수
```swift
var someVar: Any = "jisung"
someVar = 50
someVar = 100.1
```
Any, AnyObject 타입은 처음엔 편할 수 있으나 나중에 타입확인 및 변환을 매번 해줘야되어 불편, 되도록이면 타입을 명시해주는 것이 좋음
