# 공부하면서 궁금했던 점들

## 1. concurrent hashmap과 동시성


## 2. static이 아닌 이유
```java
public class AppConfig {
    public MemberService memberService() {
        return new MemberServiceImpl(memberRepository());
    }

    private MemberRepository memberRepository() {
        return new MemoryMemberRepository();
    }

    public OrderService orderService() {
        return new OrderServiceImpl(memberRepository(), discountPolicy());
    }

    public DiscountPolicy discountPolicy() {
        return new FixDiscountPolicy();
    }

}
```
이 코드에서 Repository 인스턴스를 계속 찍어내면 같은 repository가 아니게 되는거 아닐까...? 저장소는 공유되어야하는거 아니야?

-> 의도치 않았지만 내가 생각한것이 이후 수업내용으로 나왔다. 대규모 서비스에서 접근할 때마다 인스턴스를 생성하면 매우 비효율적이다. 이를 해결하기 위해서 static final로 관리하고 private으로 생성자를 막는방법이 있다. 
하지만 이런 싱글톤 패턴은 장점을 갖고 있지만 단점도 가지고 있다.
- DIP위반, OCP위반
- 테스트하기 어려움
- 유연성이 떨어짐 등

이를 위해서 스프링에서는 싱글톤 프레임워크를 제공한다.
### 단, 공유필드를 항상 조심하고, 스프링 빈은 항상 stateless 상태로 설계한다.