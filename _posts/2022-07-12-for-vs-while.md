---
title: "언제 for를 사용하고 언제 while을 사용할까?"
date: 2022-07-12 22:40:00 +0900
categories: blog
tags: programming
---

흔히 사용되는 반복문에는 C++와 자바의 for, while, do-while이 있다. 언제 for를 사용하고 언제 while을 사용할까?

먼저 "반복문"이란 순환적인 제어 구조의 모든 형태, 즉 프로그램이 특정한 코드 블록을 반복 실행하게 만드는 모든 구조를 가리키는 비공식적인 용어다. 

**Code Complete**에서 가이드하는 반복문 선택의 지침은 아래와 같다.

1. 반복문을 몇 번 반복하고 싶은지 미리 정확하게 알지 못한다면 while 반복문을 사용한다.
2. for 반복문은 지정된 횟수만큼 실행하는 반복문이 필요할 때 사용한다.
3. 반복문 내부에서 제어가 필요 없는 간단한 작업에는 for 반복문을 사용한다.
4. 어떤 작업을 실행하다가 반복문을 빠져나가야 하는 상황이라면 while 반복문을 사용한다.
5. 배열이나 다른 컨테이너의 각 멤버에 대해서 연산을 수행하는 경우에는 foreach 반복문을 사용한다.

각 지침을 코드로 확인해보자.

1. 반복문을 몇 번 반복하고 싶은지 미리 정확하게 알지 못한다면 while 반복문을 사용한다.
2. for 반복문은 지정된 횟수만큼 실행하는 반복문이 필요할 때 사용한다.

```c
N = 10;

// bad
i = 0;
while (i < N) {
    printf("%d\n", i);
    i++;
}

// good
for (i = 0; i < N; i++) {
    printf("%d\n", i);
}
```

3. 반복문 내부에서 제어가 필요 없는 간단한 작업에는 for 반복문을 사용한다.
4. 어떤 작업을 실행하다가 반복문을 빠져나가야 하는 상황이라면 while 반복문을 사용한다.

```java
// bad
for (int i = 0; i < 100; i++>) {
    // code
    ...

    if (!(expression)) {
        i = 100;
    }
    
    // code
    ...
}

// good
while (true) {
    // code
    ...

    if (!(expression)):
        break;
    
    // code
    ...
}
```

5. 배열이나 다른 컨테이너의 각 멤버에 대해서 연산을 수행하는 경우에는 foreach 반복문을 사용한다.

```java
// array
int[] items = new int[]{1, 2, 3, 4, 5};

// bad
for (int i = 1; i < items.length; i++) {
    int item = items[i];
    System.out.println(item);
}

// good
for (int item: items) {
    System.out.println(item);
}
```

### Reference
- 스티브 맥코넬, <<코드 컴플리트 2>>, 16장 반복문 제어
- 니시오 히로카즈, <<코딩을 지탱하는 기술>>, 4장 처리 흐름 제어