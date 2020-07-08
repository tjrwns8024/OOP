# **SingleTon(싱글톤 패턴)**

## 1-1. 싱글턴 패턴이란?

- `SingleTon Pattern`이란 인스턴스를 하나만 만들어 사용하기 위한 패턴입니다. 

- 하나의 인스턴스만을 유지하기 위해 인스턴스 생성에 특별한 제약을 걸어야 합니다.

- `new`를 실행할 수 없도록 생성자에 private 접근 제어자를 지정하고, 유일한 단일 객체를 반환할 수 있도록 **정적 메소드**를 지원해야합니다. (자바)

## 1-2. 왜 싱글턴 패턴을 사용하는가? 

- 인스턴스를 여러 개 만들게 되면 자원을 낭비하게 되거나 버그를 발생시킬 수 있습니다. 

- 따라서 오직 하나의 인스턴스만 생성하고 그 인스턴스를 사용하도록 하는 것입니다. 

## 1-3. 사용예제

사용 예제는 코틀린으로 작성을 하겠습니다. 

- 코틀린에서는 `object`키워드를 사용하여 싱글톤 패턴을 구현합니다. 

- `companion object`를 이용한 **팩토리 메서드**구현을 합니다. 

```kotlin
object Payroll {
    val allEmplyoees = arrayListOf()
    fun calculateSalary() {
        for (person in allEmplyoees) {
              ....
        }
    }
}
```

- 객체이름을 통해  property나 메서드에 직접 접근을 할 수 있습니다.

```kotlin
Payroll.allEmplyoees.add(Sample("예제1","예제2"))
Payroll.calculateSalary()
```

### Companion Object

- 코틀린에서는 static을 지원하지 않습니다. 

- 그 대신 class 내부에 선언된 private property에는 접근할 수 없는 제한을 받습니다. 

- 이를 해결하기 위해 `companion object`키워드가 존재합니다. 

```kotlin
class Sample{
    companion object{
        fun foo(){
            println("예제1")
        }
    }
}

fnu main(){
    A.bar()
}
```

- 위와 같이 클래스 내부에 선언된 `companion objcet`는 호출할 때 클래스 이름으로 바로 호출할 수 있습니다. 

- `companion object`는 외부 클래스의 private property에도 접근이 가능하기에, 팩토리 메서드를 만들기 적합합니다. 

```kotlin
class User private constructor(val nickname: String){
    companion object{
        fun newSubscribingUser(email: String) = 
            User(email.substringBefore('@'))

        fun newFacebookuser(accountId: Int) = 
            User(getFacebookName(accoutId))
    }
}

fun main(){
    val subscribingUser = User.newSubscribingUser("bob@gmail.com") 
    val facebookUser = User.newFacebookUser(4) 
    println(subscribingUser.nickname)
}
```

- companion object에 이름 명명이 가능합니다. 

- companion object 내부에 확장함수나 property 정의가 가능합니다. 