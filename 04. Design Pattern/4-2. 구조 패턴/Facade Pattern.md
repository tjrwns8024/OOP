# **Facade Pattern(퍼사드 패턴)**

## 1-1. 퍼사트 패턴이란?

- `facade pattern` 이란 어떤 서브 시스템의 일련의 인터페이스에 대한 통합된 인터페이스를 제공합니다. 

- `facade pattern`에서는 고수준의 인터페이스를 정의하기 떄문에 서브 시스템을 더 쉽게 사용할 수 있습니다. 

![퍼사트 사진](https://t1.daumcdn.net/cfile/tistory/99B6F54A5C68D4A91D)

### 퍼사드(Facade)

- **퍼사드**란 프랑스어로, 건물의 외관이라는 뜻을 가지고 있습니다. 

- **퍼사드 패턴**이라는 이름을 갖게 된 이유는 건물의 외벽에서 보면 안의 구조가 안보이는 것 처럼 서브 시스템을 거대한 클래스로 만들어 편리한 인터페이스를 제공해주기 떄문입니다. 



## 1-2. 사용 예제

한가지 예시 상황을 들어보겠습니다.  

우리는 전자레인지를 돌려야 합니다. 여기서 우리가 알아야 할 정보는 몇분을 돌릴지와  on off 스위치 만 알아도 작동이 가능합니다.  

여기서 우리가 on, off만 눌러도 작동이 되게끔 하는 것이 `facade pattern`입니다.  
다시 말해 우리는 on,off만 알아도 전자레인지 동작이 가능합니다. 하지만 전자레인지 안에서는 on 스위치가 눌리면 많은 동작이 동시에 일어나게 됩니다. 

마이크로웨이브 발생 시작, 턴 테이블 동작 시작, 시간 타이머 시작, 등등 여러가지 동작들이 on스위치 한번에 실행이 되게 됩니다. 이를 `facade pattern`이라고 하는 것입니다. 

만약   `facade pattern`이 없다면 우리는 전자레인지 on(), microwaveStart(), turnTable(), startTimer()등 많은 메소드들을 일일이 수행을 시켜줘야 할 것입니다. 

간단한 코드를 통해 퍼사드 활용 예시를 알아보겠습니다. 


우선 마이크로 웨이브 발생, 턴 테이블 동작, 타이머 시작 등과 같이 `SubClass`를 선언해주도록 하겠습니다.

```kotlin
class SubSample1{
    fun doSomething(name : String){
        println("subSample1  $name")
    }
}

class SubSample2{
    fun doSomething(name : String){
        println("subSample2  $name")
    }
}

class SubSample3{
    fun doSomething(name : String){
        println("subSample3  $name")
    }
}
```

다음은 이를 사용하게 쉽게 만들어 주는 `facade pattern`을 만들겠습니다. 

```kotlin
class Facade {
    private var subSample1:SubSample1? = null
    private var subSample2:SubSample2? = null
    private var subSample3:SubSample3? = null

    init {
        subSample1 = SubSample1()
        subSample2 = SubSample2()
        subSample3 = SubSample3()
    }

    fun excute(name:String){
        subSample1?.doSomething(name)
        subSample2?.doSomething(name)
        subSample3?.doSomething(name)
    }
}
```

마지막으로 main() 함수를 작성합시다. 

```kotlin
fun main(){
    val facadeService = Facade()

    facadeService.excute("tjrwns")
}


>>실행 결과
subSample1  tjrwns
subSample2  tjrwns
subSample3  tjrwns
```