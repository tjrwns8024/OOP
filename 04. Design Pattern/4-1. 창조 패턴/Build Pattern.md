# **Build Pattern(빌더 패턴)**


## 1-1. 빌더 패턴이란 ⛏?

- 우리는 인스턴스를 생성할 때, 생정자(Constructor)만을 통해 생성하는 데는 어려움이 있습니다. 

- `Build Pattern`은 이 문제를 기반으로 고안된 패턴 중 하나입니다. 

- 예를 들자면, 생성자 인자로 너무 많은 인자가 넘겨지는 경우 어떠한 인자가 어떠한 값을 나타내는지 확인하기 힘듭니다. 

- 또한 어떠한 인스턴스의 경우에는 특정 인자만으로 생성해야 하는 경우가 있습니다. 

이럴경우, 특정 인자에 해당하는 값을 null로 전달해줘야 하는데, 가독성 측면에서 매우 좋지 않습니다. 

## 1-2. 사용 예제


- 인스턴스를 생성할 때 생성자로 파라미터를 넘겨줍니다. 
```java
public class Sample(String name, Int age, int weight, int height){
    this.name = name;
    this.age = age;
    this.weight = weight;
    this.height = height;
}
```
위와 같이 클래스를 만들고 객체를 생성해보겠습니다. 

```java
//모든 파라미터들이 다 전달되는 경우
Sample sample = new Sample("tjrwns", 1, 12, 123);

//파라미터들이 일부 전달되는 겅우
Sample sample = new Sample("tjrwns",null,null,123);
```

- 이렇게 일부를 전달하는 경우 나머지 값들을 null로 채워서 보내주면 특정 파라미터가 어떠한 값을 나타내는지 확인하기 힘듭니다. 

### 점층적 생성자 패턴 

- 다른 방법 중 하나는 **점층적 생성자 패턴(telescoping constructor pattern)**입니다. 

- **점층적 생성자 패턴**이란 클래스내에 `Overloading`을 통해서 생성자를 여러개 작성하는 것을 말합니다. 

- 하지만 이 패턴을 사용하면 해당 클래스의 코드가 지저분해지고 한 인스턴스를 생성할 때 사용하지 않는 코드들도 같이 생성되는 문제가 발생합니다. 

```java
public class Sample{
    private final int age;
    private final int weight;
    private final int height;
    private final int birth;

    public Sample(int age, int weight){
        this(age,weight,0);
    }

    public Sample(int age, int weight, int height){
        this(age,weight,height,0);
    }

    public Sample(int age, int weight, int height, int birth){
        this.age = age;
        this.weight = weight;
        this.height = height;
        this.birth = birth;
    }
}
```

그렇다면 setter 메서드를 사용한 `Java Bean pattern`은 어떨까요?

```java
Sample sample = new Sample();
sample.setName("tjrwns");
sample.setAge(1);
sample.setWeight(12);
sample.setHeight(123);
```

**그래서 나온 것이 점층적 생성자 패턴과 자바 빈 패턴의 장점을 결합한 빌더 패턴입니다.**

### Build Pattern

- 인스턴스를 생성하는데 있어 필수적 인자와 선택적 인자를 구별할 수 있습니다. 

- 선택적인 인자의 경우, 가독성이 좋은 코드로 인스턴스를 생성할 수 있습니다. 

우선 빌더라는 정적 멤버 클래스를 하나 만듭니다. 
 
아래는 사용 예제입니다. 
```java
Sample sample = new Sample.Builder("tjrwns",1)
    .weight(12)
    .height(123)
    .build()
```

## Kotlin에서는?

kotlin에서는 `init` 키워드를 사용하여 생성자에서 초기값을 설정할 수 있기 때문에 반드시 필요한 변수 값만 입력 받아 사용할 수 있습니다. 

- 그래도 코틀린에서도 빌더 패턴을 적용할 수는 있습니다. 

```kotlin
class Sample private constructor(
        private val name: String,
        private val age: Int?,
        private val weight: Int?,
        private val height: Int?
) {
    class Builder(val name: String) {
        private var age: Int? = null
        private var weight: Int? = null
        private var height: Int? = null

        fun age(age: Int?): Builder {
            this.age = age
            return this
        }

        fun weight(weight: Int?): Builder {
            this.weight = weight
            return this
        }

        fun height(height: Int?): Builder{
            this.height = height
            return this
        }

        fun build() = Sample(name, age, weight, height)
    }
}
```
내부에 builder라는 클래스로 필드를 초기화합니다. 

```kotlin
Sample.Builder("tjrwns")
        .age(1)
        .weight(12)
        .height(123)
        .build()
```

