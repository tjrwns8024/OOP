# **Dependency Injection (의존성 주입)**

## 1-1. DI란?

- 외부에서 의존 객체를 생성하여 넘겨주는 것으로 **의존성 주입**을 말합니다. 

> DI는 프로그래밍에서 구성요소간의 의존 관계가 소스코드 내부가 아닌 외부의 설정 파일 등을 통해 정의되게 하는 디자인 패턴중의 하나이다.   
>      - 위키백과 -

![ㅇ](https://t1.daumcdn.net/cfile/tistory/99261E345B485FA11C)

위의 사진 처럼 B 객체를 A가 직접 생성하지 않고 외부에서 생성하여 넘겨주는 것을 의존성 주입이라고 합니다. 

왼쪽이 의존성 주입을 하기 전 일반적인 모습이고, 오른쪽이 의존성 주입을 하는 모습입니다. 



## 1-2. 사용 이유

- 보일러 플레이트 코드를 줄일 수 있습니다. 
( [보일러 플레이트 코드란? ](https://velog.io/@tjrwns8024/Boilerplate-code-%EB%B3%B4%EC%9D%BC%EB%9F%AC-%ED%94%8C%EB%A0%88%EC%9D%B4%ED%8A%B8-%EC%BD%94%EB%93%9C))

- interface에 구혀네를 쉽게 교체할 수 있게 됩니다. 

## 1-3. 사용 예제

아래의 예제는 Dagger에서 사용하고 있는 Coffee Maker 에제 입니다. 

Coffee를 내리는 데 필요한 열을 가하는 Heater, 압력을 가하는 Pump를 인터페이스로 구현합니다. 

```kotlin
interface Heater{
    fun on()
    fun off()
    fun isHot():Boolean
}
```

```kotlin
interface Pump{
    fun pump()
}
```
위의 인터페이스를 사용해 Coffeemaker 클래스를 구현합니다. 

```kotlin
class CoffeeMaker(heater: Heater, pump: Pump) {
    private final var heater: Heater? = heater
    private final var pump: Pump? = pump

    fun brew(){
        heater?.on()
        pump?.pump()
        println("----coffee----")
        heater?.off()
    }
}
```

Heater, Pump 인터페이스 구현체 입니다. 

```kotlin
class FirstHeater : Heater {
    private var heating: Boolean = true
    override fun on() {
        println("First heater heating")
    }

    override fun off() { this.heating = false }

    override fun isHot(): Boolean { return heating }

}

class FirstPump(private var heater: Heater) : Pump {
    override fun pump() {
        if (heater.isHot()) {
            println("FirstPump is pumping")
        }
    }
}
```

### **DI 사용 X**

```kotin
fun main(){
    val heater:Heater = FirstHeater()
    val pump:Pump = A_Pump(heater)
    val coffeeMaker = CoffeeMaker(heater,pump)
    coffeeMaker.brew()
}
```

### **DI 사용 O**

DI는 CoffeeMaker 사용자가 의존성을 모르는 상태(어떤 heater 와 pump 를 쓰는지 모르는 상태)에서도 커피를 내릴수 있도록 해줍니다. DI로 CoffeeMaker 사용자 대신에 의존성을 주입해주는 Injection 이라는 클래스를 생성합니다. 
```kotlin
class Injection{
    companion object{
        fun provideHeater(): Heater {
            return FirstHeater()
        }
        fun providePump(): Pump {
            return FirstPump(provideHeater())
        }
        fun provideCoffeeMaker():CoffeeMaker{
            return CoffeeMaker(provideHeater(), providePump())

        }
    }
}
```

이제 Injection 클래스에서 heater, pump를 제공받습니다. 

```kotlin
fun main() {
    val coffeeMaker = CoffeeMaker(Injection.provideHeater(), Injection.providePump())
    coffeeMaker.brew()
}
```

이를 좀더 간단히 구현을 하고싶다면 provideCoffeeMaker() 메서드를 통해 구현할 수 있습니다. 

```kotlin
fun main() {
    Injection.provideCoffeeMaker().brew()
}
```

```kotlin
>> 실행결과

First heater heating
FirstPump is pumping
----coffee----

```

---
**Reference**
-  https://faith-developer.tistory.com/147