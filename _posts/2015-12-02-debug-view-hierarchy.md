---
layout: default
---

# `bringSubviewToFront()` 버그?

`bringSubviewToFront()`가 동작하지 않는다.

* 혹시 해당 코드가 실행되지 않는 걸까?
  브레이크포인트를 걸어 보니 분명히 실행된다.
* `UIPageViewController`의 버그?
  구글링해봐도 눈에 띄는 게 없다.

Xcode의 Debug View Hierarchy 버튼을 눌러본다.
![Debug View Hierarchy](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/debugging_with_xcode/Art/dbgah-debug_button_bar-vdbgr_2x.png)

마우스로 살짝 드래그해서 뷰 계층을 3차원으로 본다.
![Xcode](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/debugging_with_xcode/Art/dwx-sw-dvh-1_2x.png)

어라? 맨 앞으로 나와있네???
그런데 크기가 이상하다.
수퍼 뷰를 차례로 클릭해서 확인해보니 `autoresizesSubviews`가 `true`인 놈이 범인.
사건 해결!

오늘의 교훈: [Debug View Hierarchy](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/debugging_with_xcode/chapters/special_debugging_workflows.html#//apple_ref/doc/uid/TP40015022-CH9-SW2)를 잘 활용하자!
