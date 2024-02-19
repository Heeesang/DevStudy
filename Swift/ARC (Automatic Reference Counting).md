Swift는 참조 타입을 자동으로 힙 영역에 할당하게 된다.
```swift
class Human { 
		var name: String?
		var age: Int?
		init(name: String?, age: Int?) {
	        self.name = name
	        self.age = age
	    }
}
let heesang = Human(name: "heesang", age: 20)
let heesang2 = heesang
```
![](https://i.imgur.com/B1MFJ4w.png)
코드를 작성하면
그림과 같이 메모리 구조가 형성이 된다.

그런데, 스택 영역에 있는 heesang, heesang2 변수가 Human을 참조를 해지한다면?

![](https://i.imgur.com/VTqhhxo.png)
다른 class를 참조하게 되거나 변수가 스택 영역에서 없어진다면   
힙 영역에 있는 Human은 사용하지 않지만 메모리만 차지하는 메모리 누수(memory leak)의 범인이 된다.

그래서 바로 저 범인을 잡아주고 주로 힙 영역을 관리해주는 것이 ARC 이다.
## 메모리 관리 방법
ARC 이름 그대로 RC(Reference Counting)을 하는 것이다.  

Reference Count는 이 인스턴스를 현재 얼마나 참조하고 있는지를 숫자로 나타낸것이다.
RC가 5이면 5곳에서 참조를 하고 있다는 뜻
위 사진을 보면 Human은 RC가 0, Animal은 RC가 2인것을 알 수 있다.

RC +1
- 인스턴스를 새로 할당할때
- 기존 인스턴스를 다른 변수에 대입할 때 (위 heesang2의 경우)

RC -1
- 인스턴스를 가리키던 변수가 메모리에서 해지됐을 때
- nil로 지정되었을 때
- 변수에 다른 값을 대입했을 때

RC가 계속 -1이 되어 0이 됐을 경우 이 인스턴스는 아무도 참조 하지 않는 것을 알고 힙 영역에서 해제 되는것

![](https://i.imgur.com/te5m3lO.png)