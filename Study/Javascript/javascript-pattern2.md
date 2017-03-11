### 특권 (privileged) 메서드
* 특권 메서드라는 개념은 특정한 문법과 관련이 없다.
* 단지 비공개 멤버에 접근권한을 가진 공개 메서드를 가르키는 이름을 뿐이다.
* 특별한 접근권한을 가지고 있기 떄문에 특권 메서드라 한다.

### 비공개 맴버의 허점

* 비공개 멤버를 유지하는 게 관건이라면, 다음과 같은 경우에 대해서 신경을 써야한다.

* 이해가 안되 추후에 정리...

### 객체 리터널과 비공개 멤버

```javascript
var myobj; // 이 변수에 객체를 할당할 예정이다.

(function () {
	// 비공개 멤버
	var name = 'My, oh my',

	// 공개될 부분을 구현한다.
	// var를 사용하지 않다는 데 중의하라

	myobj = {
		//특권 메서드
		getName = function () {
			return name;
		}
	};

})();
myobj.getName(); // 'my, oh my'
```
* 비공개 데이터를 함수로 감싼다
* 객체리털럴 익명 즉시 실행함수를 추가하여 클로저를 만든다.
* 이 에제는 곧 살펴보게 될 모듈 패턴의 기초가 되는 부분이다.

### 프로토타입과 비공개 맴버

* 생성자를 사용하여 비공개 멤버를 만들 경우, 생성자를 호출하여 새로운 객체를 만들 때마다 비공개 멤버가 매번 재생성된다는 단점이있다.
* 사실상 생상저 내부에 this에 멤버를 추가하면 항상 이런 문제가 발생한다.
* 이러한 중복을 업애고 메모리를 절약하려면 공통 프로퍼티와 메서드를 생성자의 prototype 프로퍼티를 추가해야한다.
* 이렇게 하면 동일한 생성자로 생성한 모든 인스턴스가 공통된 부분을 공유하게된다.
* 감춰진 비공개 멤더들도 모든 인스턴스가 함께 슬 수있다.
* 이를 위해서는 두 가지 패턴, 즉 생성자 함수 내부에 비공개 맴버를 만든 패턴과 객체 리터널로 비공개 맴버를 만드는 패턴을 함께 써야한다.
* 왜냐하면 prototype 프로퍼티도 결국 객체라서, 객체 리터널로 생성할 수 있기 때문이다.

```javascript
function Gadget() {
	// 비공개 멤버
	var nmae = 'yun';
	// 공개함수
	this.getName = function () {
		return name
	};
}

Gadget.prototype = (function(){
	// 비공개 멤버
	var browser = 'Mobile Webkit';
	// 공개되 프로토타입
	return {
		getBrower : function(){
			return browser;
		}
	};
})();

var toy = new Gadget();
console.log(toy.getName); // 객체 인스턴스의 특권 메서드
console.log(toy.browser); // 프로토타입의 특권 메서드
```

### 비공개 함수를 공개 메서드로 노출 시키는 방법
* 추후 추가....


### 모둘패턴

* 모듈 패턴은 늘어나는 코드를 구조화하고 정리하는데 도움이 되기 떄문에 널리 쓰인다.
* 다른 언어와 달리 자바스크립트에서 패키지를 위한 별도의 문법이 없다.
* 하지만 모듈 패턴을 사용한다면 개벌적인 코드를 느슨하게 결합시킬 수 있다.
* 따라서 각 기능들은 블랙박스처럼 다루면서 소프트웨어 개발 중에 요구사항에 따라 기능을 추가하거나 교체하거나 삭제하는 것도 자유롭게 할 수있다.

#### 모듈 패턴은 다음 패턴들을 여러 개를 조합한 것이다.

* 네임스페이스 패턴
* 즉시 실행 함수
* 비공개 멤버와 특권 맴버
* 의존 관계 선언