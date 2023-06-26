---
layout: single
title:  "스위프트 심화 데이터 타입(1)"
header:
  teaser: /assets/img/swift.png
  image: /assets/img/swift.png
categories:
  - swiftgrammar
---
스위프트의 데이터 타입 특징
===
1. 옵셔널(Optional): 값이 있을 수도, 없을 수도 있다는 표현을 옵셔널(Optional) 콘셉트를 채용하여 런타임 오류 발생을 최소화
2. 타입캐스팅(Type-Casting): 서로 다른 데이터 타입에서의 데이터 교환은 꼭 타입캐스팅(Type-Casting)을 거치게 설계
3. 컴파일단에서 부터 데이터 타입을 확인하여 타입이 맞지않으면 컴파일 오류를 발생하여 여러 타입을 섞어 사용할 때 발생할 수 있는 런타임 오류를 최소화
4. 타입 추론: 변수나 상수를 선언할 때 특정 타입을 명시하지 않아도 컴팡닐러가 할당된 값을 기준으로 변수나 상수의 타입을 결정
5. 타입 별칭: 데이터 타입에 임의로 다른 이름(별칭)을 부여가능

타입추론
---
변수, 상수 선언할 때 타입을 명시하지 않아도 컴파일러가 할당된 값을 기준으로 타입 결정
```swift
var name =  "jisung" // 타입추론을 통하여 name은 String타입으로 선언
name = 100 // 앞서 추론에 의해 String 타입입으로 오류
```

타입 별칭
---
이미 존재하는 데이터 타입에 의미로 다른이름(별칭)을 부여, 기본 타입 이름과 추가한 별칭 모두 사용 가능
```swift
//각각 다른이름으로 Int 별칭 부여
typealias MyInt = Int
typealias YourInt = Int

//Double 별칭 부여
typealias MyDouble = Double

let age:  MyInt = 100 //MyInt는 Int의 또 다른 이름
var year: YourInt = 2080 //YourInt = Int
year = age //MyInt, YourInt = Int 이기에 같은 타입으로 취급
let month: Int = 7 //기존의 Int도 사용 가능
let percentage: MyDouble = 99.9
```

튜플
---
튜플은 타입의 이름이 따로 지정되어 있지 않은 ‘지정된 데이터의 묶음’, 파이썬 튜플과 유사, 타입 이름이 따로 없고 일정 타입의 나열만으로 튜플 타입 생성
```swift
// String, Int, Double 타입을 갖는 튜플
var man: (String, Int, Double) = ("jisung", 34, 170.2)
//인덱스를 통해 값을 빼 올 수 있음
print("이름: \(man.0), 나이: \(man.1), 신장: \(man.2)")
//인덱스를 통해 값을 할당
person.1 = 99
person.2 = 178.5
```

### 튜플의 요소마다 이름을 지정
```swift
//String, Int, Double 타입을 갖는 튜플
var person: (name: String, age: Int, height: Double) = ("jisung", 34, 170.2)

//요소 이름을 통해서 값을 빼오기
print("이름: \(person.name), 나이: \(person.age), 신장: \(person.height)")

//요소 이름을 통해 값을 할당
person.age = 99

//인덱스를 통해 값을 할당
person.2 = 179.5
```

### 튜플 별칭 지정
같은 모양의 튜플을 사용할때 긴 튜플 타입을 모두 안써줘도됨
```swift
typealias PersonTuple = (name: String, age: Int, height: Double)
let jisung: PersonTuple = ("jisung", 100, 178.5)
print("이름: \(jisung.name), 나이: \(jisung.age), 신장: \(jisung.height)")
```


컬렉션형 데이터 타입
===
튜플 외에도 많은 수의 데이터를 묶어서 저장하고 관리하는 타입 : 배열(Array), 딕셔너리(Dictionary), 세트(Set)

배열
---
- 같은 타입의 데이터를 일렬로 나열한 후 순서대로 저장하는 형태의 컬렉션 타입
- 배열은 각 요소에 인덱스를 통해 접근 가능, 0부터 시작, 
- 처음과 마지막 요소는 fisrt와 last 프로퍼티를 통해 가져올 수 있음

```swift
//대괄호를 사용하여 배열 표현
var names: Array<String>  = ["jisung","chulsoo","younghee","jisung"]

//위 선언과 같은 표현
var names2: [String] = ["jisung","chulsoo","younghee","jisung"]

//Any 데이터를 요소로 갖는 빈 배열 생성
var emptyArray: [Any] = [Any]()

//위 선언과 같은 표현
var emptyArray2: [Any] = Array<Any> ()

//[]만으로 빈 배열 생성
var emptyArray3: [Any] = []

```

배열 활용
```swift
print(names[2]) //younghee
names.append("elsa") // 마지막에 elsa추가
names.append(contentsOf: ["john",  "max"]) //맨 마지막에 john과 max가 추가
names.insert("happy", at:2) //인덱스 2에 삽입
names.insert(contentsOf: ["jinhee",  "minsoo"], at: 5) //인덱스5 위치에 jinhee와 minsoo가 삽입
print(names.firstIndex(of:"jisung")) //0 : 해당요소의 인덱스를 확인하기
print(names.first) //jisung
```

딕셔너리
---
- 순서 없이 키와 값의 쌍으로 구성되는 컬렉션 타입
- 값은 항상 키와 쌍을 이루게됨, 키가 하나이거나 여러 개일 수 있음
- 하나의 딕셔너리 안의 키는 같은 이름을 중복해서 사용 안됨, 키는 값을 대변하는 유일한 식별자
- Dictionary라는 키워드와 키의 타입과 값의 타입 이름의 조합으로 씀
- 대괄호로 키와 값의 타입 이름의 쌍을 묶어 딕셔너리 타입임을 표현
- 빈 딕셔너리는 이니셜라이저 또는 리터럴 문법을 통해 생성

```swift
// typealias를 통해 조금 더 단순하게 표현
typealias StringIntDictionary = [String: Int]

//키는 String, 값은 Int 타입인 빈 딕셔너리 생성
var numberForName: Dictionary<String, Int>  = Dictionary<String, Int> ()

//위 선언과 같은 표현(축약 표현)
var numberForName2: [String: Int] = [String: Int]()

//위 코드와 같은 동작
var numberForName3: StringIntDictionary = StringIntDictionary()

//[:] 만으로 빈 딕셔너리 생성
var numberForName4: [String: Int] = [:]

//초깃값을 주어 생성
var numberForName5: [String: Int] = ["jason": 100,  "chulsoo": 200,  "jenny": 300]
print(numberForName.isEmpty) //false
print(numberForName.count) //3
```
딕셔너리의 활용
```swift
print(numberForName["chulsoo"]) //200
print(numberForName["minji"]) //nil
numberForName["chulsoo"] = 150
print(numberForName["chulsoo"]) // 150
numberForName["max"] = 999 // max라는 키로 999라는 값을 추가
print(numberForName.removeValue(forKey: "jason")) //100
// jason 키에 해당하는 값이 없으면 기본으로 0이 반환
print(numberForName["yagom", default: 0]) //0
```

세트
---
- 세트는 같은 타입의 데이터를 순서 없이 하나의 묶음으로 저장하는 형태
- 세트 내의 값은 모두 유인한 값, 즉 중복된 값이 존재하지 않음
- 순서가 중요하지 않거나 각 요소가 유일한 값이어야 하는 경우 사용
- 세트의 요소로는 해시 가능한 값이 들어와야함(스위프트 기본 데이터 타입은 모두 해시 가능한 값)
- Set 키워드와 타입 이름의 조합, 배열과 같이 대괄호로 값들을 묶어 세트 타입임을 표현
- 배열과 달리 줄여서 표현할 수 있는 축약형(Array<Int  → [Int]) 가 없음

```swift
var firstnames: Set<String>  = Set<String>() // 빈 세트 생성
var firstnames2: Set<String>  = [] // 빈 세트 생성

// Array와 마찬가지로 대괄호 사용
var firstnames3: Set<String>  = ["jason",  "chulsoo",  "younghee",  "yagom"]

// 타입 추론을 사용하면 컴파일러는 Set이 아닌 Array로 타입을 지정
var numbers = [100, 200, 300]
print(type(of: numbers)) // Array<Int>
print(firstnames3.isEmpty) // false
print(firstnames3.count) //3 - 중복된 값은 허용하지 않아 jason 1개만 남음
```

세트 활용
```swift
print(firstnames3.count) // 3
firstnames3.insert("jenny") // 2
print(firstnames3.count) // 4
print(firstnames3.remove("chulsoon"))
```

### 집합 연산
```swift
let englishClassStudents: Set<String>  = ["john",  "chulsoo",  "jason"]
let koreanClassStudents: Set<String>  = ["jenny",  "jason",  "chulsoo", "hana",  "minsoo"]

// 교집합 {"jason",  "chulsoo"}
let intersectSet: Set<String>  = englishClassStudents.intersection(koreanClassStudents)

// 여집합의 합(배타적 논리합) {"john",  "jenny",  "hana",  "minsoo"}
let symmetricDiffSet: Set<String>  = englishClassStudents.symmetricDifference(koreanClassStudents)

//합집합
let unionSet: Set<String>  = englishClassStudents.union(koreanClassStudents)

//차집합 {"john"}
let subtractSet: Set<String>  = englishClassStudents.subtracting(koreanClassStudents)

//sorted()
print(unionSet.sorted()) //["chulsoo",  "haha",  "jenny",  "john",  "minsoo",  "jason"]
```

### 포함관계 연산
```swift
let 새: Set<String>  = ["비둘기",  "닭",  "기러기"]
let 포유류: Set<String>  = ["사자",  "호랑이",  "곰"]
let 동물: Set<String>  = 새.union(포유류) // 새와 포유류의 합집합

print(새.isDisjoint(with: 포유류)) //서로 배타적인지 - true
print(새.isSubset(of: 동물)) //새가 동물의 부분집합인가요? - true
print(동물.isSuperset(of: 포유류)) // 동물은 포유류의 전체집합인가요? - true
print(동물.isSuperset(of: 새)) //동물은 새의 전체집합인가요? - true
```

컬렉션에서 임의의 요소 추출과 뒤섞기
```swift
array.randomElement() // 임의의 요소
array.shuffled() // 뒤죽박죽된 배열(원본은 그대로)
array.shuffle() // array 자체를 뒤죽박죽 뒤섞기
set.shuffled() // 세트를 뒤섞으면 배열로 반환
set.shuffle() // 오류
dictionary.shuffled() // 딕셔너리를 뒤섞으면 (키, 값)이 쌍을 이룬 튜플의 배열로 반환
string.shuffled() // string 도 컬렉션임
```
