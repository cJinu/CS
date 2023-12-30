## 싱글톤 패턴

하나의 인스턴스를 만들고 각각의 모듈들이 하나의 인스턴스를 공유해서 인스턴스를 생성하는 비용을 절약하지만 의존성이 높아진다.

주로 DB를 연결할때 많이 쓰이며 SpringBoot에서 만들어주는 Connection Pool과 같은 결인거 같음

### 단점

테스트 주도 개발할 때 방해가 됌

단위 테스트를 주로 하는데, 각각의 테스트가 독립적이지 못하기 때문에 테스트가 어려움

### 의존성 주입
하나의 인스턴스만 만들기 때문에 모듈간의 결합도가 너무 높아지기 때문에 의존성 주입이라는 

중간 매개체를 통해서 결합도는 느슨하게 만들수있음

![image](https://github.com/cJinu/CS/assets/94429120/bcd08862-4221-4200-be4c-cccc4f349013)


의존성이란 A가 변경되었을때 B도 변경된다는 것을 의미하는데 의존성 주입자를 통해서 의존성이 떨어지게 된다

### 장점
모듈을 쉽게 교체할 수 있는 구조가 되어 테스트와 마이그레이션이 수월해진다

구현 시 추상화 layer를 넣고 이를 기반으로 구현체를 넣기 때문에 의존성 방향이 일관되고, 쉽게 추론가능하며 모듈 간 관계들이 명확해진다.

### 단점

모듈들이 더욱 분리되어 클래스가 늘어나서 복잡성 또한 늘어난다. 

약간의 런타임 패널티가 생기기도 한다.

### 의존성 주입 원칙

```
상위 모듈은 하위 모듈에서 어떠한 것도 가져오지 않아야하며, 또한 둘 다 추상화에 의존해야 한다.
이때 추상화는 세부 사항에 의존하면 안된다.
```

### 의존성주입
```java
public class Dependency {
    public void doSomething() {
        System.out.println("Dependency doing something");
    }
}

// 의존성 주입을 사용하는 싱글톤 클래스
public class SingletonWithDependency {

    private static SingletonWithDependency instance;
    private Dependency dependency;

    // private 생성자
    private SingletonWithDependency() {
        // 외부에서 의존성을 주입받음
        this.dependency = new Dependency();
    }

    // 인스턴스 얻기
    public static synchronized SingletonWithDependency getInstance() {
        if (instance == null) {
            instance = new SingletonWithDependency();
        }
        return instance;
    }

    public void doSomething() {
        dependency.doSomething();
        System.out.println("SingletonWithDependency doing something");
        // 다른 로직 수행
    }
}
```
## 팩토리 패턴

객체를 사용하는 코드에서 객체 생성 부분을 떼어내 추상화한 패턴이자 상위 클래스가 중요한 뼈대를 결정하고 하위 클래스에서 객체 생성에 관한 구체적인 내용을 결정

상위와 하위로 나누어지기 때문에 결합도가 낮고 상위 클래스는 하위 클래스에 관여하지 않으므로 유연성이 높음

### 장점

클래스를 기반으로 객체를 만들지 않고 호출이 가능하며, 해당 메소드에 대한 메모리 할당을 한번만 할 수 있다는 장점이 있음

1. **객체 생성의 캡슐화:**
    
    팩토리 패턴은 객체 생성을 캡슐화하므로 클라이언트는 객체를 직접 생성하는 것이 아니라 팩토리를 통해 객체를 얻을 수 있습니다. 이로써 객체 생성에 대한 세부사항이 클라이언트 코드로부터 분리되어 캡슐화됩니다.
    
2. **중복된 코드 제거:**
    
    객체 생성 코드가 여러 곳에서 중복되는 것을 방지할 수 있습니다. 객체 생성 로직을 팩토리에 중앙 집중시켜 중복을 최소화할 수 있습니다.
    

### 단점

1. **복잡성 증가:**
    
    팩토리 패턴을 도입하면서 코드가 더 복잡해질 수 있습니다. 객체 생성을 추상화하고 캡슐화하는 추가적인 인터페이스 및 클래스가 필요하며, 이로 인해 코드의 양이 늘어날 수 있습니다.
    
2. **유연성 부족:**
    
    일부 상황에서는 팩토리 패턴이 유연성을 제한할 수 있습니다. 팩토리가 객체 생성에 대한 제어를 가져가기 때문에, 클라이언트가 직접 객체를 생성하는 것에 비해 유연성이 감소할 수 있습니다
    

### 팩토리 패턴 코드

```java
enum CoffeeType {
    LATTE,
    ESPRESSO
}

abstract class Coffee {
    protected String name;
    protected int price;

    public String getName() {
        return name;
    }

    @Override
    public String toString() {
        return "Coffee{" +
                "name='" + name + '\'' +
                ", price=" + price +
                '}';
    }
}

class Latte extends Coffee {
    public Latte(int price) {
        name = "latte";
        this.price = price;
    }
}

class Espresso extends Coffee {
    public Espresso(int price) {
        name = "Espresso";
        this.price = price;

    }
}

class CoffeeFactory {
    public static Coffee createCoffee(CoffeeType type, int price) {
        switch (type) {
            case LATTE:
                return new Latte(price);
            case ESPRESSO:
                return new Espresso(price);
            default:
                throw new IllegalArgumentException("Invalid coffee type: " + type);
        }
    }
}

public class Factory {
    public static void main(String[] args) {
        Coffee coffee = CoffeeFactory.createCoffee(CoffeeType.ESPRESSO, 1000);
        System.out.println(coffee); // latte
    }
}

// Coffee{name='Espresso', price=1000}
```
## 전략패턴

객체의 행위를 바꾸는 것이 아닌, 전략이라고 부르는 캡슐화된 알고리즘을 바꿔주면서 상호 교체가 가능하게 만드는 패턴

![image](https://github.com/cJinu/CS/assets/94429120/d92f4079-c538-49f7-a9e2-8c8e9bff18c1)

결제라는 행위는 같지만 그 안에서 어떤 식으로 결제할지 상호 교체가 가능하도록 하는 디자인 패턴

```java
import java.text.DecimalFormat;
import java.util.ArrayList;
import java.util.List;
interface PaymentStrategy {
    public void pay(int amount);
}

class KAKAOCardStrategy implements PaymentStrategy {
    private String name;
    private String cardNumber;
    private String cvv;
    private String dateOfExpiry;

    public KAKAOCardStrategy(String nm, String ccNum, String cvv, String expiryDate){
        this.name=nm;
        this.cardNumber=ccNum;
        this.cvv=cvv;
        this.dateOfExpiry=expiryDate;
    }

    @Override
    public void pay(int amount) {
        System.out.println(amount +" paid using KAKAOCard.");
    }
}

class LUNACardStrategy implements PaymentStrategy {
    private String emailId;
    private String password;

    public LUNACardStrategy(String email, String pwd){
        this.emailId=email;
        this.password=pwd;
    }

    @Override
    public void pay(int amount) {
        System.out.println(amount + " paid using LUNACard.");
    }
}

class Item {
    private String name;
    private int price;
    public Item(String name, int cost){
        this.name=name;
        this.price=cost;
    }

    public String getName() {
        return name;
    }

    public int getPrice() {
        return price;
    }
}

class ShoppingCart {
    List<Item> items;

    public ShoppingCart(){
        this.items=new ArrayList<Item>();
    }

    public void addItem(Item item){
        this.items.add(item);
    }

    public void removeItem(Item item){
        this.items.remove(item);
    }

    public int calculateTotal(){
        int sum = 0;
        for(Item item : items){
            sum += item.getPrice();
        }
        return sum;
    }

    public void pay(PaymentStrategy paymentMethod){
        int amount = calculateTotal();
        paymentMethod.pay(amount);
    }
}
public class Strategy{
    public static void main(String []args){
        ShoppingCart cart = new ShoppingCart();

        Item A = new Item("kundolA",100);
        Item B = new Item("kundolB",300);

        cart.addItem(A);
        cart.addItem(B);

        // pay by LUNACard
        cart.pay(new LUNACardStrategy("kundol@example.com", "pukubababo"));
        // pay by KAKAOBank
        cart.pay(new KAKAOCardStrategy("Ju hongchul", "123456789", "123", "12/01"));
    }
}
/*
400 paid using LUNACard.
400 paid using KAKAOCard.
*/
```
