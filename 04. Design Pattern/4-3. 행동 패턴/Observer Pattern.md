# **Observer Pattern(옵저버 패턴)**

## 1-1. 옵저버 패턴이란?

- `Observer Pattern`이란 어떤 객체에 이벤트가 발생하였을 때, 이 객체와 관련된 객체들(옵저버들)에게 통지하도록 하는 디자인 패턴입니다.
 
- 즉, 객체의 **상태가 변경**되었을 때, **특정 객체에 의존하지 않으면서 상태의 변경을 관련된 객체들에게 통지**하는 것이 가능해집니다. 

![ㅇ](https://miro.medium.com/max/3304/1*W0B2TW5Ekh8-bULK5MIvdA.jpeg)

## 1-2. 사용 예제

우리는 지금 요리 주방에 들어와있습니다. 

- 쿠커들은 헤드셰프가 내린 명령을 모두 notify(알림)을 받아야 합니다. 

- 코치가 샐러드 주문들 받고 명령을 내렸다면 쿠커들은 모두 코치가 샐러드 주문 명령을 내렸다는 사실을 알아야합니다. 

- 즉, 헤드셰프는 모든 쿠커들에게 주문 정보를 알려야 합니다. 

위의 설명대로 인터페이스를 만들어 아래의 코드를 통해 알아보도록 합시다. 

```kotlin
interface Chef{
    fun subscribe(cook:Cook)
    fun unsubscribe(cook:Cook)
    fun notifyCook(msg:String )
}

interface Cook{ //cook은 요리사를 뜻합니다. (n : 명사)
    fun orderUpdate(msg: String)
}
```
이제 셰프를 구현하는 헤드셰프를 만들어보겠습니다. 

```kotlin
class HeadChef : Chef{
    private var cooks  = ArrayList<Cook>()

    fun orderSalad(){
        println("샐러드 주문 들어옴")
        notifyCook("샐러드 만들어")
    }
    fun orderSteak(){
        println("스테이크 주문 들어옴")
        notifyCook("스테이크 만들어")
    }
    fun orderSoup(){
        println("수프 주문들어옴")
        notifyCook("수프 만들어")
    }

    override fun subscribe(cook: Cook) {
        cooks.add(cook)
    }

    override fun unsubscribe(cook: Cook) {
        cooks.remove(cook)
    }

    override fun notifyCook(msg: String) {
        cooks.forEach { cook -> cook.orderUpdate(msg) }
    }

}
```

위와 같이 헤드 셰프는 Cook들의 리스트를 가지고 있습니다. 

- 헤드 셰프는 세가지 기능이 있습니다. 

- 스테이크 주문 명령, 샐러드 주문 명령, 수프 주문 명령

- 여기서 `notifyCook()` 이라는 메서드를 각 기능에서 호출합니다. 

이제 쿠커들은 명령을 받기를 원하므로 헤드셰프를 **구독**합니다. 


```kotlin
class Cook1:Cook{
    override fun orderUpdate(msg: String) {
        println("1번 요리사 수신 : $msg")
    }
}
class Cook2:Cook{
    override fun orderUpdate(msg: String) {
        println("2번 요리사 수신 : $msg")
    }
}
class Cook3:Cook{
    override fun orderUpdate(msg: String) {
        println("3번 요리사 수신 : $msg")
    }
}
```

이제 메인함수입니다 .

```kotlin
fun main(){
    val cook1 = Cook1()
    val cook2 = Cook2()
    val cook3 = Cook3()
    val headChef = HeadChef()
    
    headChef.subscribe(cook1)
    headChef.subscribe(cook2)
    headChef.subscribe(cook3)
    
    headChef.orderSalad()
}

>>실행 결과

샐러드 주문 들어옴
1번 요리사 수신 : 샐러드 만들어
2번 요리사 수신 : 샐러드 만들어
3번 요리사 수신 : 샐러드 만들어

```

이렇게 쿠커들은 헤드 셰프의 명령을 받을 수 있게 되었습니다. 

이제 1번 쿠커가 퇴근 할 시간이 되었습니다. 
1번 쿠커는 퇴근 후에도 헤드 셰프의 명령을 들을 필요가 없기 때문에 구독을 해지 합니다. 

```kotlin
headChef.unsubscribe(cook1)
```

남은 두 쿠커들은 야근을 하기 때문에 다음 스테이크 주문을 처리합니다. 

```kotlin
headChef.orderSteak()

>>실행 결과
스테이크 주문 들어옴
2번 요리사 수신 : 스테이크 만들어
3번 요리사 수신 : 스테이크 만들어
```

- 즉, `Cook 인터페이스`는 `Observer 인터페이스`가 될 것입니다. 

-  `Chef 인터페이스`는 `Observable 인터페이스`가 됩니다. 

