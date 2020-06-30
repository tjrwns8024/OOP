# **class diagram(클래스 다이어그램)**

- **클래스 다이어그램**은 시스템을 구성하는 클래스와 그들 사이의 관계를 보여줍니다. 

- 주요 구성 요소는 클래스와 관계입니다.

## 1.1 클래스 

- 클래스란 동일한 속성과 행위를 수행하는 **객체의 집합**입니다.  

![클래스와 객체](https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcT3m7sPCCVdgfDBWzCnDwsQlz9_2Zt5FcPKDw&usqp=CAU)

- 또한 우리는 흔히 클래스를 설계도라고 많이 얘기하곤 합니다. 

- 이러한 얘기는 코드를 보면 이해가 쉬울 것입니다. 

```java
public class Sample{
    private String name;

    public void play(){
        System.out.println(ex + "논다");
    }

    public Sample(String name){
        this.name = name;
    }
}
```

- 위의 Sample클래스를 사람을 만들어내는 설계도라고 생각을 합시다.   
 
- 우리는 위와 같이 설계도를 만들었습니다.   

- 아직 실제 사람을 만들지는 않았기 때문에 만들기 위해 new연산자를 사용합니다. 

```java
Sample person1 = new Sample("tjrwns");
Sample person2 = new Sample("cnldjq");
```

- 위의 두줄로 두 사람이 만들어졌습니다. 

- 다음은 이 두 사람을 놀도록 만들겠습니다. 

```java
person1.play();
person2.play();
```

UML에서는 아래와 같이 표현합니다. 

![UML클래스 예](https://lh3.googleusercontent.com/proxy/bOoXVUhOyfcqk3G-dTHKD2m3eDF8W1sg1mlL4Rxvp2zZG203o98bhvhCkqF6q7gOemPHSCAgszaP3cj-rP6CMqRLCSpqh_efqgylH-nbVcFJM_aBjcCWCaBzJRQhtISEYkDLuFzrJXP1ix8XABRs56_cmBRYjklQIISiiqCqE4xVOzegKsyQT822Df6iBEn_XV1WWau8SW52UvvCY8obC1Tw0wuzbHmlP-831k5e9psfNl-r-mMhKLCwfoKan-fPDT_RLhSvN_zdZlK2wJbB5w5TRFmo7DR_afRK9HffIGsSus3dEXRoNw)

- 가장 윗부분은 클래스 이름

- 중간 부분은 클래스의 특징을 나타내는 속성

- 마지막 부분은 클래스가 수행하는 책임(연산)

또한 클래스의 속성, 연산을 쓸 때 '+','-'같은 부호를 사용합니다. 이는 속성과 연산의 `가시화`를 정의한 것입니다. 

- 가시화란, 우리가 흔히 사용하는  접근 제어자라고 생각하면 쉬울 것 같습니다. 

![가시화 접근 제어자](https://gmlwjd9405.github.io/images/class-diagram/access-controller.png)

- 그러나 속성과 연산에 가시화 정보를 항상 표시해야하는 것은 아닙니다. 

- 클래스 다이어 그램은 개념 분석 단계 ~ 구현까지 광범위 하게 사용됩니다. 

- 따라서 가시화 정보는 설계 단계에서 표시하는 것이 일반적입니다.


## 1.2 관계

- 클래스 하나로만 이루어지는 시스템은 존재하지 않습니다. 

- 다수 클래스가 모인 시스템이 훨씬 효율적입니다. 

![관계](https://lh3.googleusercontent.com/proxy/7Y3OAg28Oslo7i5TnKTvPbefXtZ6PzjcTnKIhwlETmfwmJp2Llfz0909vqEPOqmAT-rmyrgdgZUTUHF3_ncAC8LQG48insQtFfwwSHAF6CjSS5bXbIDC_oJQK7ZH81Pa1oN_6vwhoWkVKRJb1pzkDFo-4hhNy3NZohw4KzCoCDCwkDdywZ0_NT-syjzOVS9RMDD5-byFERXoUAlDzvae4lmTQmSX9oc3c7qzv-9dr4hVx-L9kPz1dS_WpZFLsvL3bkWrunfhuWcxejgdJY-D_3JrfubC5yfypJCw5g)

### 연관 관계 

- 클래스들이 개념상 서로 연결되었음을 나타냅니다. 

- 실선이나 화살표로 표시하며 **보통 한 클래스가 다른 클래스에서 제공하는 기능을 사용하는 상황일때 표시합니다**. 


![역할](https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99FB793359F37A8713)

위와 같이 연관관계를 나타내는 선에 아무런 숫자가 없으면 연관 관계가 **일대일 관계**임을 나타냅니다. 

하지만 실제로 교수님은 여러 학생을 상대해야 하기 때문에 이와 연관된 객체(student 객체)수를 선 부근에 명시하는데 이를 `다중성`이라고 합니다.  

![다중성](https://gmlwjd9405.github.io/images/class-diagram/bi-directional.png)

위의 그림을 보면 한 교수에 1이상의 학생이 연관되어 있다는 점을 알 수 있습니다. 


### 일반화 관계

- 객체지향 개념에서는 상속관계라고 합니다. 

- 한 클래스가 다른 클래스를 포함하는 상위 개념일 때 이를 `IS-A 관계`라고 합니다. 

- 속이 빈 화살표로 표시합니다. 

![일반화 관계](https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99900A3359F440D709)



### 집합 관계

- 전체와 부분의 관계를 명확하게 명시하고자 할 때 사용합니다. 

- 이는 집약과 합성 관계가 존재합니다. 

코드를 통해 집약과 합성관계를 설명하도록 하겠습니다. 


### 합성

```java
public class Person{
    private Head head;
    private Body body;
    private Leg leg;

    public Person(){
        this.head = new Head();
        this.body = new Body();
        this.leg = new Leg();
    }
}
```
)
- 위의 코드는 생성자가 Person의 구성 요소가 되는 Person 객체들을 생성해 적절한 속성에 연결시켜줍니다. 

- 이러한 구성요소 객체들은 Person 클래스의 객체가 사라지면 모두 같이 사라집니다. 

- 즉, 구성요소 객체들이 Person객체의 라이프타입에 의존하는 관계가 형성되는 것입니다. 


### 집약

```java
public class Person{
    private Head head;
    private Body body;
    private Leg leg;

    public Person(Head head, Body body, Leg leg){
        this.head = head;
        this.body = body;
        this.leg = leg;
    }
}
```

- 위의 코드에서 Person객체가 사라져도 구성요소 객체들은 사라지지 않습니다. 

- 그 이유는 외부에서 이들 객체에 대한 참조만 받아 사용했기 때문입니다. 

- 따라서 집약 관계를 사용하여 모델링 하는 것이 적당합니다. 



### 의존 관계

일반적으로 한 클래스가 다른 클래스를 사용하는 경우는 다음과 같이 3가지가 있습니다. 

- 클래스의 속성에서 참조할 때
- 연산의 인자로 사용될 때 
- 메서드 내부의 지역 객체로 참조될 때 

예를 들자면, 자동차(Car 클래스)를 소유한 사람(Person 클래스)이 자동차를 이용해 출근을 한다고 할 경우 한번 출근한 후 다음날 출근 할 때도 어제와 같은 자동차를 타고 출근 할 것입니다. 

즉, 출근 할 때 마다 다른 자동차를 타는 일은 없다는 얘기입니다. 

이런경우 사람과 자동차의 관계는 연관관계이며, Person 클래스의 속성으로 Car객체를 참조합니다. 


```java
public class Car{
    ...
    public void fillGas(GasPump p){
        p.getGas(amount);
    }
}
```

위의 코드는 자동차와 주유기의 관계를 나타는 코드입니다. 

자동차는 주유를 할 때 특정 주유소에서 특정 주유기만 고집할 수는 없습니다. 

이런 경우 주유를 할 때 마다 주유기가 달라지는 것을 의미합니다. 

![의존 관계](https://lh3.googleusercontent.com/proxy/pwfGToSTzoHHcLKpaICCv_Ud8rM3odh5qS7LxXtVy5eADwXqZHT1qqLMRrEyjoY_rJ2Hl2Yy9OWynwn2iElgKyTsxGayuLQMJVPWKABppclRxlrV2DDO24vIc59TzRjuaeasgBL05Y2dIrWhpUTJo2sdDz6E5sJixGEhen9eYkQ4Y0VWu15KrZfBgHDsR3S2kfYGbfxxFqzgQF7JJwbQZUsxOFeE0-TQ4Tk4QvKJkwrrWfB2RW1KzbMDgwhdOpxU_EY5mm6tr5OF4uo6KAbPKYMrsRILjzAHZFJaw468gAWt)

<br/>



### 인터페이스와 실체화 관계

인터페이스란 책임이라 할 수 있습니다. 어떤 객체의 책임이란 객체가 해야 하는 일로서 해석할 수 있고 어떤 경우에는 객체가 할 수 있는 일로도 해석할 수 있습니다. 

예를 들어, 리모컨은 TV를 켜거나 크는 책임을 수행해야합니다.  
글너데 TV만 이런 책임을 수행하는 것일까요? 형광등 스위치도 이와 같은 책임을 수행해야합니다. 

```java
turn_off : 끄다
turn_on  : 켜다
```

- 인터페이스를 어떤 공통되는 능력이 있는 것들을 **대표하는 관점**으로도 볼 수 있습니다.

- 인터페이스는 실제로 책임을 수행하는 객체가 아닙니다. 

- 실제로 책임을 수행하는 객체는 TV 리모컨, 스위치 와 같은 객체들입니다. 

※ 일반화 관계는 **is a kind of** 관계이지만 실체화 관계는 **can do this**관계입니다. 