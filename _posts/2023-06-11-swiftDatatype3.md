---
layout: single
title:  "스위프트 심화 데이터 타입(2)"
excerpt: "데이터타입 열거형 사용법"
header:
  image: /assets/img/Swift-Enum.jpg
  caption: "Photo credit: [**becodable**](https://becodable.com/swift-enum/)"
toc: true
toc_label: "목차"
toc_sticky: true
toc_icon: "tasks"
categories:
  - swiftgrammar
tags:
  - Swift
  - Enum

---
열거형
---
- 열거형은 연관된 항목들을 묶어서 표현하는 타입
- 배열과 딕셔너리와 다르게 정의해준 항목 값 외에는 추가/수정 불가

### 열거형 사용 목적
1. 제한된 선택지 제작
2. 정해진 값 외에는 입력받고 싶지 않을때
3. 예상된 입력 값이 한정되어 있을 때

### 열거형 선언
```swift
// 각 항목 자체가 고유의 값을 가짐
enum School {
  case primary, elementary, middle, high, college, university, graduate
}
```

School 열거형 변수의 생성 및 값 변경
```swift
var highestEducationLevel: School = school.university
//같은 표현
var highestEducationLevel: School = .university

// 같은 타입은 School 내부의 항목으로만 highestEducationLevel의 값을 변경
highestEducationLevel = .graduate
```

열거형의 각 항목은 자체로도 하나의 값이지만 항목의 원시 값(raw value)도 가질 수 있다
```swift
enum School: String {
  case primary = "유치원"
  case elementary = "초등학교"
  case middle = "중학교"
  case high = "고등학교"
  case college = "대학"
  case university = "대학교"
  case graduate = "대학원"
}

let highestEducationLevel: School = School.university
print("저의 최종학력은 \(highestEducationLevel.rawValue) 졸업입니다. ") // 저의 최종학력은 대학교 졸업입니다. 

//원시 값을 통한 열거형 초기화
let primary = School(rawValue: "유치원") //primary
let graduate = School(rawValue: "석박사") //nil

//연관 값을 갖는 열거형
enum MainDish {
    case pasta(taste: String)
    case pizza(dough: String, topping: String)
    case chicken(withSauce: Bool)
    case rice
}

var dinner: MainDish = MainDish.pasta(taste: "크림") //크림 파스타
dinner = .pizza(dough: "치즈크러스트", topping: "불고기") //불고기 치즈크러스트 피자
dinner = .chicken(withSauce: true)
dinner = .rice //밥
```

여러 열거형의 응용
```swift
enum PastaTaste {
    case cream, tomato
}
enum PizzaDough {
    case cheeseCrust, thin, original
}

enum PizzaTopping {
    case pepperino, cheese, bacon
}

enum MainDish2 {
    case pasta(taste: PastaTaste)
    case pizza(dough: PizzaDough, topping: PizzaTopping)
    case chicken(withSauce: Bool)
    case rice
}

var dinner: MainDish2 = MainDish2.pasta(taste: PastaTaste.tomato)
dinner = MainDish.pizza(dough: PizzaDough.cheeseCrust, topping: PizzaTopping.bacon)
```

### 항목 순회
- 열거형이 포함된 모든 케이스를 알아야할 때 사용
- 열거형의 이름 뒤에 콜론(:)을 작성하고 한 칸 띄운 뒤 CaseIterable 프로토콜을 채택
- allCases 이름의 타입 프로퍼티를  통해 모든 케이스의 컬렉션을 생성

CaseIterable 프로토콜을 활용한 열거형의 항목 순회
```swift
enum School: CaseIterable {
    case primary
    case elementary
    case middle
    case high
    case college
    case university
    case graduate
}
let allCases: [School] = School.allCases
print(allCases) 
// [School.primary, School.elementary, School.middle, School.high, School.college, School.university, School.graduate]
```

available 속성을 갖는 열거형의 항목 순회
```swift
enum School: String, CaseIterable {
  case primary = "유치원"
  case elementary = "초등학교"
  case middle = "중학교"
  case high = "고등학교"
  case university = "대학교"
  @available(iOS, obsoleted: 12.0)
  case graduate = "대학원"
  
  static var allCases: [School] {
    let all: [School] = [.primary,
                         .elementary,
                         .middle,
                         .high,
                         .university]
    #if os(iOS)
    return all
    #else
    return all + [.graduate]
    #endif
  }
}

lett allCases: [School] = School.allCases
print(allCases)
// 실행환경에 따라 다른 결과
```

### 순환 열거형
열거형 항목의 연관 값이 열거형 자신의 값이고자 할 때 사용
특정 항목에 순환 열거형 항목 명시: case 키워드 앞에 indirect 붙이기 
열거형 전체에 적용: enum 키워드 앞에 indirect 붙이기
```swift
//특정 항목에 순환 열거형 항목 명시
enum ArithmeticExpression {
  case number(Int)
  indirect case addition(ArithmeticExpression, ArithmeticExpression)
  indirect case multiplication(ArithmeticExpression, ArithmeticExpression)
}

//열거형 전체에 순환 열거형 명시
indirect enum ArithmeticExpression {
  case number(Int)
  case addition(ArithmeticExpression, ArithmeticExpression)
  case multiplication(ArithmeticExpression, ArithmeticExpression)
}
//ndirect 키워드는 이진 탐색 트리 등의 순환 알고리즘을 구현할 때 사용
```

비교 가능한 열거형
Comparable 프로토콜을 준수하는 연관 값만 갖거나 연관 값이 없는 열거형을 비교, 앞에 위치한 케이스가 더 작은 값이 됨
```swift
enum Condition: Comparable {
  case terrible
  case bad
  case good
  case great
}

let myCondition: Condition = Condition.great
let yourCondition: Condition = Condition.bad
if myCondition >= yourCondition {
    print("제 상태가 더 좋군요")
} else {
print("당신의 상태가 더 좋아요")
}
// 제 상태가 더 좋군요

```
