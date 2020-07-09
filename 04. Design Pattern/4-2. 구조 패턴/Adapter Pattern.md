# **Adapter Pattern(어댑터 패턴)**  

## 어댑터 패턴이란?

- `adapter pattern`은 클래스의 인터페이스를 사용자가 기대하는 **인터페이스 형태로 변환시키는 패턴**이라고 정의합니다. 

- `adapter pattern`은 서로 일치하지 않는 인터페이스를 갖는 클래스들을 함께 동작 시킵니다. 

흔히 아래와 같은 그림으로 설명을 합니다. 

![adapter pattern](https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcTR5NLTskn4IsANTxqQpTd6uTK6OpZze8E7dg&usqp=CAU)

우리는 종종 일본 제품을 사용을 합니다.   
그 경우 플러그가 우리나라의 220V와 맞지 않는 경우를 마주하게 됩니다.   
이경우 우리는 보통 **돼지코**라고 불리는 제품을 사용을 합니다. 

맞습니다. 돼지코는 여기서 `adapter`역할을 합니다. 

## 사용 예제

위에서 설명한 플로그 예제를 사용하여 보겠습니다. 

```kotlin
interface Plugin{
    fun connect()
    fun disconnect()
}

class Plugin_220V : Plugin{
    override fun connect(){
        println("220V connect")
    }
    override fun disconnect(){
        println("220V disconnect")
    }
}
```

위는 Plugin 인터페이스를 구현한 Plugin_220V 클래스 입니다.   
하지만 여기서 만약 110V를 사용하고 싶다면 어떻게 해야할까요?

```kotlin
interface PluginAdapter{
    fun connect()
    fun disconnect()
}

class Adapter_110V(plugin: Plugin) : PluginAdapter{
    private var plugin:Plugin? = plugin

    override fun connect() {
        println("110V -> 220V convert")
        this.plugin?.connect()
    }

    override fun disconnect() {
        println("110V -> 220V convert")
        this.plugin?.disconnect()
    }
}

>> 실행코드
fun main(){
    val plugin : PluginAdapter = Adapter_110V(Plugin_220V())
    plugin.connect()
    plugin.disconnect()
}
```

위의 어댑터 패턴은 객체 어댑터 패턴을 구현한 것 입니다. 

![인스턴스 어댑터 패턴](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2Fzrxsz%2FbtqxyMwwMEC%2FoysvoygnP9rLsoehpj3pUk%2Fimg.png)

이렇게 된다면 클라이언트는 어댑터 인터페이스로만 의존하고 실제적인 어댑티는 알지 못하게 됩니다. 