# 클래스

- 클래스 정의하는 방법

  ```java
  [접근제한자] [abstract] class 클래스명 [extends 부모클래스] [implements 인터페이스,...]{
    [접근제한자] [static] [변수타입] 변수명;
    [static]{}//초기화 블록
    클래스명(타입 parameter);//생성자
    [접근제한자] [static] [리턴타입] 메서드명(타입 parameter){}
  }
  ```

  > 멤버 변수의 초기화 시기 및 순서
  >
  > 클래스 변수의 초기화 시점 : 클래스가 로딩될 때 딱 한 번 초기화
  >
  > 클래스 변수의 초기화 순서 : 기본값 -> 명시적 초기화 -> 클래스 초기화 블럭
  >
  > 
  >
  > 인스턴스 변수의 초기화 시점 : 인스턴스가 생성될 때마다 각 인스턴스별로 초기화 진행
  >
  > 인스턴스 변수의 초기화 순서 : 기본값 -> 명시적 초기화 -> 인스턴스 초기화 블럭 -> 생성자
  >
  > 

- 객체 만드는 방법 (new 키워드 이해하기)

  new 키워드는 클래스 타입의 인스턴스를 생성해주는 역할을 담당합니다.

  new 연산자를 이용해서 메모리의 Heap 영역에 데이터를 저장할 공간을 할당하고 그 공간의 참조값을 객체에게 리턴해줍니다. 그 후 생성자를 호출합니다.

  new 연산자를 통해 참조값을 저장한 객체로만 인스턴스에 접근이 가능하기 때문에 new 연산자 이후에 어떤 생성자를 호출하는지에 따라서 사용할 수 있는 인스턴스가 달라집니다.

  

- 메소드 정의하는 방법

  메소드는 객체의 기능에 해당하는 부분을 정의합니다.

  ```java
  int add(int a,int b){//선언부
    //... 메서드 호출 시 수행될 코드 <- 함수 동작 구현 <- 구현부
  }
  ```

  

- 생성자 정의하는 방법

  생성자는 인스턴스가 생성될 때 호출되는 '인스턴스 초기화 메서드'입니다.

  생성자의 이름은 클래스의 이름과 같아야하고, 리턴값이 없습니다.

  ```java
  클래스이름(타입 변수명,...){
    //인스턴스 생성 시 수행될 코드
    //주로 인스턴스 변수의 초기화가 일어난다.
  }
  ```

  이 때 착각을 하기 쉬운게, 생성자가 인스턴스를 생성한다고 생각할 수 있는데, 생성자는 new를 통해 생성된 참조변수에 인스턴스 정보를 세팅하는 역할을 합니다.

  클래스를 정의할 때, 생성자를 만들지 않으면, 컴파일러에 의해서 기본 생성자(클래스이름( ))이 자동으로 추가됩니다.

- this 키워드 이해하기

  단어 뜻 그대로 this 지금 보고있는 이 객체를 의미합니다. this는 참조변수로 인스턴스 자신을 가리킵니다.

  1. this.

     클래스 내의 인스턴스 메서드와 생성자의 매개변수로 클래스의 인스턴스 변수와 이름이 같은 변수를 사용해야하는 경우(ex. 생성자의 매개변수로 인스턴스 변수들의 초기값을 제공받음)가 있습니다. 그 때, this를 이용해서 매개변수와 인스턴스 변수를 구분하면 코드의 가독성이 더 좋아집니다.

     ```java
     Person(String name, int age){
       this.name = name;
       this.age = age;
     }
     ```

     this를 사용할 때, 주의할 점은 this는 인스턴스 멤버만 사용가능하다는 것입니다. 

  2. this( ), this(타입 매개변수)

     생성자로, 같은 클래스의 다른 생성자를 호출할 때 사용합니다.

     ```java
     Person(String name){
       this.name = name;
     }
     Person(String name,int age){
       this(name);
       this.age = age;
     }
     ```

     이 때, this( )는 생성자 블록의 가장 첫 줄에 딱 하나만 호출할 수 있습니다.

# 인터페이스

- 인터페이스 정의하는 방법

  ```java
  interface 인터페이스 이름 [extends 인터페이스1, 인터페이스2,...]{
    [접근제한자][static][abstract][final] 타입 변수명;//final 일 경우 값 지정 필수
    [public][abstract] 메서드이름(매개변수목록);
  }
  //ex
  public interface Calculator { 
    public abstract int plus(int a, int b)
    static int multi(int a, int b){ 
      return a * b; 
    } 
  }
  ```

  

- 인터페이스 구현하는 방법

  ```java
  class 클래스 이름 implements 인터페이스 이름{
    //인터페이스에 정의된 추상메서드를 구현
  } 
  //ex
  public class CalculatorImpl interface Calculator {
    @override
    public abstract int plus(int a, int b){ 
      return a + b; 
    }
    @override
    static multi(int a, int b){ 
      return a * b; 
    }
  }
  ```

  이 때, 주의할 점은 구현하는 클래스에서 아직 구현하지않은 인터페이스의 abstract 메서드가 있다면 class는 반드시 abstract를 붙여 추상클래스임을 명시해야합니다.

  

- 인터페이스 레퍼런스를 통해 구현체를 사용하는 방법

  인터페이스 참조변수를 이용해서 해당 인터페이스를 구현한 클래스의 인스턴스에 접근할 수 있습니다.

  대표적인 예로, java.util에 있는 List가 있습니다.

  ```java
  List myList = new ArrayList();
  ```

  List 참조변수를 이용해서 List를 구현한 ArrayList에 접근할 수 있습니다.

  이처럼 인터페이스 레퍼런스를 통해서 구현체를 사용할 수 있음으로서 동적 바인딩의 효과를 더 잘 누릴 수 있습니다.

  

- 인터페이스 상속

  인터페이스는 인터페이스만 상속받을 수 있고, 여러개의 인터페이스를 상속받는 다중 상속이 가능합니다.

  

- 인터페이스의 기본 메소드 (Default Method), 자바 8

  ```java
  public interface Calculator { 
    default int defaultPlus(int a, int b){ 
      return a + b; 
    } 
    static int staticMulti(int a, int b){ 
      return a * b; 
    } 
  }
  ```

  이전의 버전까지는 모든 멤버변수는 public static final이고, 모든 메서드는 public abstract여야만 했습니다. 하지만 자바 8부터는 Default 메서드를 제공하기 때문에 그럴 필요가 없어졌으며, 인터페이스도 고유의 기능을 가질 수 있게되어, 인터페이스를 구현하는 객체들에게 공통된 속성을 부여해줄 수 있게 됐습니다. 이 메서드에 접근할 때는, 참조변수로 함수를 호출할 수 있습니다.

  또한, 인터페이스의 Default 메서드는 재정의가 가능합니다.

  요약하면, 인터페이스가 가지는 인스턴스 메서드가 바로 default 메서드 입니다.

- 인터페이스의 static 메소드, 자바 8

  Default 메서드와 함께 자바 8에서 추가된 인터페이스가 가질 수 있는 추상메서드가 아닌 메서드입니다.

  default 메서드와는 다르게 static 메서드를 호출할 때에는 반드시 클래스 명으로 메서드를 호출해줘야하고, 재정의가 불가능합니다.

  

- 인터페이스의 private 메소드, 자바 9

  ```java
  public interface Calculator { 
    default int defaultPlus(int a, int b){ 
      return a + b; 
    } 
    static int staticMulti(int a, int b){ 
      return a * b; 
    }
    private void turnOff(){
      System.out.println("Good Bye!!");
    }
  }
  ```

  인터페이스가 private 메서드를 가지면 인터페이스를 구현하는 클래스에게 인터페이스 구현에대한 세부 정보를 숨길 수 있습니다. 그 결과 캡슐화가 용이해집니다.

  또한 유사한 기능을 가진 메서드에대한 인터페이스에 중복이 적고 재사용 가능한 코드가 더 많이 추가될 수 있다는 장점이 있습니다.
