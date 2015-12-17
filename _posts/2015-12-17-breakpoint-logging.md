---
layout: default
---

# 중단점(breakpoint)을 활용한 로그 출력

`WKWebView`를 사용하는 앱 개발중 자바스크립트 콘솔에 이런 메시지가 보인다.

```
ReferenceError: Can't find variable: Optional
```

`Optional`을 보면 Swift 코드에서 자바스크립트 실행하는 부분에서 발생하는 이슈인 것 같다.
문제는 자바스크립트를 실행하는 곳이 꽤 많다는 것. 일일히 찾아서 로그를 추가하기는 싫고 뭐 좋은 방법 없을까?

물론 좋은 방법이 있다. `WKWebView`가 자바스크립트 실행을 위해 제공하는 방법은 아래의 함수뿐이다.

```
public func evaluateJavaScript(javaScriptString: String, completionHandler: ((AnyObject?, NSError?) -> Void)?)
```

이 함수에 중단점을 설정하자. 내가 만든 함수가 아닌데 어떻게 중단점을 설정하냐고? Symbolic breakpoint 기능을 사용하면 된다.

1. Debug > Breakpoints > Create Symbolic Breakpoint... 메뉴를 선택하거나 옵션-커맨드-\ 키를 누른다.
1. Symbol 입력란에 해당 함수의 selector인 `evaluateJavaScript:completionHandler:`를 입력한다.

여기까지 하고 실행하면 해당 함수가 호출될 때마다 실행이 중단되어 디버깅을 할 수 있다.
로그 출력을 위해서는 몇 가지 더 해야할 것이 있다.
이미 중단점 속성 입력창을 닫았다면 Breakpoint Navigator에 해당 중단점을 우클릭하고 Edit Breakpoint...를 선택하여 다시 열자.

Action 옆에 Debugger Command가 선택되어 있을 것이다. (아니라면 선택하고)
아래 입력란에 `p (NSString*)$rdx`를 입력하면 해당 중단점을 만날 때마다 `rdx` 레지스터의 값을 `NSString*` 포맷으로 출력한다.
내가 만든 함수에 중단점을 설정했다면 원하는 변수를 출력하면 된다.
다른 함수의 경우 레지스터를 바꿔가며 시도해보면 원하는 것을 찾을 수 있다.

로그만 출력하고 실행이 멈추지 않도록 Automatically continue after evaluating actions 옆에 체크한다.

미션 성공!
