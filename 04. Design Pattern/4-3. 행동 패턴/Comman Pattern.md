# **Command Pattern (커맨드 패턴)**


## 커맨드 패턴이란? 
-  `Command pattern`은 실행될 기능을 **캡슐화**함으로써 주어진 여러 기능을 실행할 수 있는 재사용성이 높은 클래스를 설계하는 패턴입니다. 

- 이벤트가 발생했을 때 실행될 기능이 다양하면서도 변경이 필요한 경우에 이벤트를 발생시키는 클래스를 변경하지 않고 재사용하고자 할 때 유용합니다. 

![ㅇ](https://i1.daumcdn.net/thumb//R750x0/?fname=http%3A%2F%2Fcfile22.uf.tistory.com%2Fimage%2F99F1EE445B0AAF251BB69D)


## 사용 예제

예시 상황을 들어 설명을 해 보도록 하겠습니다. 

눌리면 특정 기능을 수행하는 버튼이 있다고 가정을 해보겠습니다. 위의 사진과 같이 버튼을 눌렀을 때 램프의 불이 켜지는 프로그램을 개발하려고 합니다. 

```kotlin
class Lamp{
    fun turnOn(){
        println("Lamp on")
    }
}

class Button(theLamp: Lamp) {
    private var theLamp:Lamp? = theLamp

    fun pressed(){
        theLamp?.turnOn()
    }
}

fun main(){
    val lamp = Lamp()
    val button = Button(lamp)

    button.pressed()
}
```

위의 코드에서 램프 대신 다른 기능을 실행하게끔 하려고 할 때 어떠한 변경을 해야 하는지 아래의 코드를 통해 알아보겠습니다. 

```kotlin
class Alarm{
    fun start(){
        println("Alarming")
    }
}

class Button (theAlarm: Alarm){
    private var theAlarm:Alarm? = theAlarm

    fun pressed(){
        theAlarm?.start()
    }
}

fun main(){
    val alarm = Alarm()
    val alarmButton = Button(alarm)

    alarmButton.pressed()
}
```

- 위의 코드는 버튼을 눌렀을 때, 지정된 특정기능(알람, 램프)만 고정적으로 수행하도록 설계되었습니다. 

- 알람 동작을 추가할 때 위 처럼 pressed() 메서드 전체를 변경해야 하므로 OCP를 위배하게 됩니다. 

그렇다면 버튼을 누르는 동작에 따라 다른 기능을 실행하는 경우의 코드를 작성해 보도록 합시다. 

```kotlin
//위의 Lamp class, Alarm class를 사용합니다. 

enum class Mode{ LAMP, ALARM}

class Button(theLamp: Lamp, theAlarm: Alarm) {
    private var theLamp:Lamp? = theLamp
    private var theAlarm:Alarm? = theAlarm
    private var theMode:Mode? = null

    fun setMode(mode:Mode){
        this.theMode = mode
    }
    
    fun pressed(){
        when(theMode){
            Mode.LAMP -> 
                theLamp?.turnOn()
            Mode.ALARM ->
                theAlarm?.start()
        }
    }
}

fun main(){
    val lamp = Lamp()
    val alarm = Alarm()
    val button = Button(lamp,alarm)
    
    button.setMode(Mode.LAMP)  // 램프 모드로 설정
    button.pressed()  // 램프 켜짐
    
    button.setMode(Mode.ALARM)  // 알람 모드로 설정
    button.pressed()  //알람 울림
}
```

- 이 경우 역시 기능을 추가시 버튼 클래스를 수정해야합니다. 

### 해결책

- 따라서, 새로운 기능을 추가하거나 변경하더라도 Button 클래스는 사용하려면 Button 클래스의 pressed() 메서드에서 구체적인 기능을 직접 구현하는 대신 버튼을 눌렀을 때 실행될 기능을 외부에서 제공받아 호출하는 방법을 사용해야 합니다.

![ㅇㅇ](https://gmlwjd9405.github.io/images/design-pattern-command/command-solution.png)

Command 인터페이스를 선언해줍니다. 

```kotlin
interface Command {
    fun execute()
}
```

여기서 사용하는 램프 클래스와 알람 클래스는 전에 사용한 것과 동일합니다. 

Button 클래스를 구현합니다. 
```kotlin
class Button(theCommand: Command) {
    private var theCommand: Command? = null

    init {
        setCommand(theCommand)
    }

    fun setCommand(newCommand: Command) {
        this.theCommand = newCommand
    }

    fun pressed() {
        theCommand?.execute()
    }

}
```
다음은 Command를 구현한 LampOnCommand, AlarmOnCommand 입니다. 

```kotlin
class LampOnCommand(theLamp: Lamp) : Command {
    private val theLamp: Lamp? = theLamp
    override fun execute() {
        theLamp?.turnOn()
    }
}

class AlarmOnCommand(theAlarm: Alarm) : Command {
    private val theAlarm: Alarm? = theAlarm

    override fun execute() {
        theAlarm?.start()
    }
}
```

이를 실행하는 부분입니다. 

```kotlin
fun main() {
    val lamp = Lamp()
    val lampOnCommand = LampOnCommand(lamp) 

    val button1 = Button(lampOnCommand) //램프 켜는 커맨드 설정
    button1.pressed()  // 램프 켜는 기능 실행

    val alarm = Alarm()
    val alarmOnCommand = AlarmOnCommand(alarm)

    val button2 = Button(alarmOnCommand)  // 알람 켜는 커맨드 설정
    button2.pressed()  // 알람 켜는 기능 실행
}
```