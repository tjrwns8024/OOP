# **Polymorphism(다형성)**

- 다형성은 전에 다뤘던 상속과 깊은 관계가 있습니다. 

- 다형성이란 **여러 가지 형태를 가질 수 있는 능력**이라고 흔히 얘기 합니다. 

- 하지만 자바에서는 **한 타입의 참조변수로 여러 타입의 객체를 참조할 수 있도록 함**이라고 정의합니다. 

-> 하나의 객체를 여러 가지 타입으로 선언할 수 있다는 뜻입니다. 

- 인터페이스와 `상속`은 둘 다 `다형성`이라는 객체지향 프록래밍의 특징을 구현하는 방식입니다.


![다형성 이미지 ](https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F246C0C3A5756894B14)


### Java에서 다형성은 상속과 인터페이스를 통해 이루어집니다. 

- 다형성의 의미는 말했다시피 하나의 객체를 다양한 타입으로 사용할 수 있게 한다는 의미입니다. 

- 중요한 것은 다양한 타입으로 객체를 바라보게 되면 호출할 수 있는 메소드 역시 타입에 따라 달라진다는 점입니다. 

- 상속의 오버라이딩을 설명하면서 오버라이딩을 하게 되면 컴파일러는 실제 객체의 메소드를 바라보는 것이 아니라, 변수 선언 타입의 메소드를 봅니다. 


위의 사진을 코드로 구현을 해보겠습니다. 

```java
public class Animal{
    
    void howl(){
    }
    void run(){
        System.out.println("달려");
    }
}

public class Dog extends Animal{
    @Override
    public void howl(){
        System.out.println("멍멍");
    }
}

public class Cat extends Animal{
    @Override
    public void howl(){
        System.out.println("야옹");
    }
}
;
>>실행 코드

public static void main(String[] args){
        Animal dog = new Dog();
        Animal cat = new Cat();
        
        dog.howl();
        dog.run();
        
        cat.howl();
        cat.run();
    }

>> 실행 결과
멍멍
달려
야옹
달려
```

위의 코드를 보면 이해가 쉬울 듯 합니다. 