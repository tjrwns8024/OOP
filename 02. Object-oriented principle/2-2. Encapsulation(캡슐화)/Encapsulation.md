# **캡슐화(Encapsulation)**

- `캡슐화(encapsulation)`란 필요하 속성(Attribute)과 행위(Method)를 하나로 묶고 그 중 일부를 외부에서 사용하지 못하도록 은닉하는 작업을 의미합니다. 

- 캡슐화는 정보은닉을 통해 높은 응집도와 **낮은 결합도**를 갖도록 합니다. 

- 여기서 `정보은닉`이란, 알 필요가 없는 정보는 외부에서 접근하지 못하도록 제한하는 것입니다. 

그렇다면 정보은닉은 왜 필요할까?
 
 ### why?

 - 소프트웨어는 결합이 많을수록 문제가 많이 발생합니다. 

 - 한 클래스가 **변경이 발생**하면 변경된 클래스에 **의존**하는 다른 클래스들도 **변경해야 할 가능성**이 커지기 때문입니다. 

 ```java
public class ArrayStack{
    public int top;
    public int[] itemArray;
    public int stackSize;

    public ArrayStack(int stackSize){
        itemArray = new int[stackSize];
        top = -1;
        this.stackSize = stackSize;
    }

    public void push(int item){ //스택에 아이템 추가
        if(isFull()){
            System.out.println("Inserting fail! Array Stack is full!!");
        }
        else{
            itemArray[++top] = item;
            System.out.println("Inserted Item : " + item);
        }
    }

    publi int pop(){ //스택의 톱에 있는 아이템 반환
        if(isEmpty()){
            System.out.println("Deleting fail! Array Stack is empty");
            return -1;
        }
        else{
            return itemArray[top--];
        }
    }

    >> 실행 코드
    public class StackClient{
        public static void main(String[] args){
            ArrayStack st = new ArrayStack(10);
            st.itemArray(++st.top) = 20;
            System.out.println(st.itemArray[st.top]);
        }
    }
}
 ```

위 코드는 캡슐화를 사용하지 않고 배열을 사용하여 스택의 일부를 구현하였습니다. 

여기서 봐야 할 점은 필드, 메소드 들이 모두 `public` 을 붙여 외부에 공개 되었다는 점입니다. 

- 즉, StackClient 클래스 처럼 push메소드 , pop 메소드를 사용하지 않고 직접 배열에 값을 저장할 수 있습니다. 

- 이런 경우, StackClient와 ArrayStack에는 강력한 결합이 발생하게 됩니다. 


```java
public class StackClient{
    public static void main(String[] args){
        ArrayListStack st = new ArrayListStack(10);
        st.items.add(new Integer(20)); 
        System.out.println(st.items.get(st.items.size()-1))
    }
}
```

이렇게 만약 Array가 아닌 ArrayList 클래스를 사용해 스택 구현이 변경된다면 위와 같이 구현 할 수 있습니다. 

- 하지만 이렇게 변경했더라도 자료구조는 필요에 따라 계속 변경될 수 있습니다. 

이 문제를 해결하기 위해서 변경되는 곳을 파악하여 이를 **은닉**해야합니다. 

![정보은닉의 장점](https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcRtEdVfkdibMGuDzHxMVpOWh2D5UxGzthaPBA&usqp=CAU)

앞서 언급한 스택에서는 자료구조의 형태와 관련이 있는 top, itemArray, stackSize 를 외부에서 접근하지 못하도록 private 키워드를 붙여 은닉합니다. 

```java
private int top;
private int[] itemArray;
private int stackSize;
```

- 이렇게 private 키워드를 붙여 은닉을 시키면 push, pop, peek 메서드를 통해 스택의 연산을 수행할 수 있게 됩니다.

**즉, 스택과 이를 사용하는 코드의 결합이 낮아집니다.**

```java
public class StackClient{
    public void main(String[] args){
        ArrayListStack st = new ArrayListStack(10);
        st.push(20);        
        System.out.println(st.peek());
    }
}
```