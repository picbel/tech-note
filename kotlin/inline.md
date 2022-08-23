
## kotlin의 inline 함수와 reified키워드 메모 입니다

inline
---
먼저 코틀린에서 메서드의 인자에 함수를 넣은 메서드의 경우 컴파일해보면 해당 인자 함수를 호출하기 위한 객체가 생성됩니다.
내부적으로 객체 생성과 함수 호출을 하도록 구현되어있습니다.
즉 불필요한 객체가 생성되는 만큼 성능이 하락합니다.

이러한 경우를 해결하는것이 inline입니다
함수앞 inline 키워드가 붙으면 컴파일이 될때 컴파일러가 함수 내부의 코드를 해당 함수를 호출하는 부분에 복붙합니다.
그러나 inline함수도 만능은 아닙니다 제약사항이 있습니다.
먼저 inline 함수는 private 함수를 호출 할 수 없습니다.

추가로 이러한 형태의 코드에서도 문제가 발생합니다

```kotlin
  inline fun newMethod(a: Int, func: () -> Unit, func2: () -> Unit) {
    func()
    someMethod(10, func2)
}

fun someMethod(a: Int, func: () -> Unit):Int {
    func()
    return 2*a
}

fun main(args: Array<String>) {
    newMethod(2, {println("Just some dummy function")},
         {println("can't pass function in inline functions")})
}
```
이경우 컴파일을 하여보면 에러가 발생합니다.
이유는 inline함수에서는 전달 받은 함수를 참조할수 없습니다. 따라서 다른 함수로 전달이 불가능합니다.
해당 경우는 noinline키워드로 해결이 가능합니다.
다른 함수로 참조시킬 함수에 noinline키워드를 붙혀 해결 할 수 있습니다

```kotlin
inline fun newMethod(a: Int, func: () -> Unit, noinline func2: () -> Unit) {
    func()
    someMethod(10, func2)
}
```

Reified
---

Reified키워드는 제네릭 관련 키워드로 inline 함수에서만 사용 가능합니다.

```kotlin
fun <T> function(argument: T)
```

컴파일러가 컴파일하기전에는 T에 대한 타입 정보를 추론할수있습니다.
하지만 컴파일 이후 runtime에는 type Eraser때문에 타입정보를 알수 없습니다.
Reified키워드를 이용하면 타입 정보에 접근이 가능해집니다.

### 응용
reified를 사용하면 리턴 타입에 따른 when이 가능합니다.

```kotlin
inline fun<reified T> doSomething(number: Int): T {
    return when (T::class) {
        String::class -> "The number is : $number" as T
        Int::class -> number as T
        else -> "Not string, Not Integer" as T
    }
}

val thisIsInt : Int = doSomething(10) // 10이 리턴
val thisIsStr : String = doSomething(10) // "The number is : 10" 이 리턴

```
