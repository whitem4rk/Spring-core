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