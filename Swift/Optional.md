# Optional
옵셔널은 값이 있을 수도 없을 수도 있는 타입
주로 타입 뒤에 ?를 붙여서 Optional을 표시한다.
## Optional Unwrapping
![](https://i.imgur.com/1ZsvqWg.png) ![](https://i.imgur.com/gBgnzt5.png)

nil은 그대로 nil로 출력이 되지만 1은 Optional에 Wrapping되어 출력되는 것을 볼 수 있다.
Wrapping 되어 있는 값으로 연산을 하게되면 에러가 발생한다.
```Swift
num1 + 2 // error
```
그래서 Wrapping된 값을 사용하기 위해서는 Unwrapping 하여 값을 꺼내야 한다.
### 강제 언래핑
!를 붙여 말 그대로 강제로 언래핑을 하는 것이다.
강제로 하는 것이다 보니 값이 nil일때도 언래핑을 하게되어 오류가 발생하고 앱이 멈추게 된다.
### Nil-Coalescing Operator
기본 값을 설정해주어 값이 nil일 때 사용할 수 있게 해주는 operator 이다.

![](https://i.imgur.com/GgN0NUh.png)![](https://i.imgur.com/aDPh9fz.png)
?? 를 붙여 nil일 때 대신 넣어줄 기본값을 설정한다.
num2는 nil이기 때문에 기본값 2가 들어가서 3으로 출력되는 것을 볼 수 있다.
### Optional Binding
옵셔널에 할당된 값을 임시 변수 또는 상수에 할당을 해주는 방식이다.
if 문 또는 gurad문을 사용하여 옵셔널의 값이 존재하는지 검사한 뒤, 존재하면 임시 변수나 상수에 값을 대입시켜준다.

if 문을 사용한 Optional Binding
```swift
var num1: Int? = 1

if let number = num1 {
	print("값이 존재합니다.")
} else {
	print("값이 존재하지 않습니다.")
}
```

guard 문을 사용한 Optional Binding
```swift
func processValue(_ optionalValue: Int?) { 
	guard let number = optionalValue else { print("값이 없습니다.") return }
	print("값이 있습니다: \(number)") 	
} 
processValue(42) // 값이 있습니다: 42
processValue(nil) // 값이 없습니다.
```
#### if let vs guard let
- if 문 내에서만 옵셔널 값을 할당한 임시 변수나 상수를 사용할 수 있다.
- guard문은 반대로 guard문 다음에 오는 코드에서 계속 사용 가능하다.

- if 문은 옵셔널 값이 존재 하는 경우에만 어떤 동작을 수행시키고 싶을 때 사용한다.
- guard 문은 필수 값이 있는지 확인을 하고 다음 코드를 수행시킬 때 사용합니다. 그래서 주로 함수 내에서 사용하여 nil일 때 함수를 빠져나오는 식으로 사용된다.

## Optional Chaining
chaining의 뜻은 "연쇄"로 말 그대로 옵셔널을 연쇄적으로 사용하는 것이다.
```swift
let saram = person.contacts?.address
let heesang = person?.contacts?.address
```
.을 통해 내부 프로퍼티나 메서드에 연속적으로 접근할 때 옵셔널 값이 하나라도 껴 있으면 옵셔널 체이닝이다.
만약 person에는 값이 있고 contacts에는 nil 값이 들어 있다면 saram은 nil이 된다.

옵셔널 체이닝은 값이 없을 수 있는 여러 단계의 연산을 간결하게 표현할 수 있게 해주고, 
중간에 값이 없으면 연산이 중단되어 안전하게 처리된다. // 강제 언래핑은 런타임 오류를 발생시켜 동작을 멈추게 한다.

#### 옵셔널 체이닝 vs 강제 언래핑
옵셔널 체이닝은 연속적으로 옵셔널을 확인하는 방식
강제 언래핑은 옵셔널을 완전히 벗겨내는 느낌