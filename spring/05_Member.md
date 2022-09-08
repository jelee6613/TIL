# Spring_05_Member

## 순서
1. src/main/java/hello.hellospring에 domain(hello.hellospring.domain) 패키지 생성
2. domain 패키지 안에 Member 클래스 생성
```java
package hello.hellospiring.domain;

public class Member {

    private Long id;
    private String name;

}
```
3. getter and setter 생성 (Alt + Insert)
```java
package hello.hellospiring.domain;

public class Member {

    private Long id;
    private String name;

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

4. src/main/java/hello.hellospring에 repository(hello.hellospiring.repository) 패키지 생성
- 회원 객체를 저장하기 위한 저장소

5. repository 패키지 안에 MemberRepository 인터페이스 생성 및 작성
```java
package hello.hellospiring.repository;

import hello.hellospiring.domain.Member;

import java.util.List;
import java.util.Optional;

public interface MemberRepository {
    // 회원이 저장된다.
    Member save(Member member);

    Optional<Member> findById(Long id);
    Optional<Member> findByName(String name);

    // findAll() 지금까지 저장된 모든 회원 정보를 반환한다.
    List<Member> findAll();
}
```

6. 구현체 생성 repository 패키지 안에 MemoryMemberRepository 클래스 생성
```java
package hello.hellospiring.repository;

// Alt + Enter 누르고 implement Methods 하면 아래와 같이 import
public class MemoryMemberRepository implements MemberRepository {
}

```

```java
package hello.hellospiring.repository;

import hello.hellospiring.domain.Member;

import java.util.List;
import java.util.Optional;

public class MemoryMemberRepository implements MemberRepository {
    @Override
    public Member save(Member member) {
        return null;
    }

    @Override
    public Optional<Member> findById(Long id) {
        return Optional.empty();
    }

    @Override
    public Optional<Member> findByName(String name) {
        return Optional.empty();
    }

    @Override
    public List<Member> findAll() {
        return null;
    }
}
```

```java
package hello.hellospiring.repository;

import hello.hellospiring.domain.Member;

import java.util.*;

public class MemoryMemberRepository implements MemberRepository {

    private static Map<Long, Member> store = new HashMap<>();
    private static long sequence = 0L;

    @Override
    public Member save(Member member) {
        member.setId(++sequence);
        store.put(member.getId(), member);
        return member;
    }

    @Override
    public Optional<Member> findById(Long id) {
        return Optional.ofNullable(store.get(id));
    }

    @Override
    public Optional<Member> findByName(String name) {
        return store.values().stream()
                .filter(member -> member.getName().equals(name))
                .findAny();
    }

    @Override
    public List<Member> findAll() {
        return new ArrayList<>(store.values());
    }

    public void clearStore() {
        store.clear();
    }
}
```

7. src/test/java/hello.hellospiring 안에 repository 패키지 생성

8. repository 패키지 안에 MemoryMemberRepositoryTest 클래스 생성 및 작성

```java
package hello.hellospiring.repository;

import hello.hellospiring.domain.Member;
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.Test;

import java.util.List;

import static org.assertj.core.api.Assertions.*;

public class MemoryMemberRepositoryTest {

    MemoryMemberRepository repository = new MemoryMemberRepository();
    
    // 하나의 테스트가 끝날때마다 초기화
    @AfterEach
    public void afterEach() {
        repository.clearStore();
    }
    
    @Test
    public void save() {
        Member member = new Member();
        member.setName("spring");

        repository.save(member);

        Member result = repository.findById(member.getId()).get();
        assertThat(member).isEqualTo(result);
    }

    @Test
    public void findByName() {
        Member member1 = new Member();
        member1.setName("spring1");
        repository.save(member1);

        Member member2 = new Member();
        member2.setName("spring2");
        repository.save(member2);

        Member result = repository.findByName("spring1").get();

        assertThat(result).isEqualTo(member1);
    }

    @Test
    public void findAll() {
        Member member1 = new Member();
        member1.setName("spring1");
        repository.save(member1);

        Member member2 = new Member();
        member2.setName("spring2");
        repository.save(member2);

        List<Member> result = repository.findAll();

        assertThat(result.size()).isEqualTo(2);
    }
}

```

9. src/main/java/hello.hellospring에 service 패키지 생성

10. service 패키지 안에 MemberService
```java
package hello.hellospiring.service;

import hello.hellospiring.domain.Member;
import hello.hellospiring.repository.MemberRepository;
import hello.hellospiring.repository.MemoryMemberRepository;

import java.util.List;
import java.util.Optional;

public class MemberService {

    private final MemberRepository memberRepository;

    public MemberService(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }
    // 회원가입
    public Long join(Member member) {

        validateDuplicateMember(member);  // 중복 회원 검증
        memberRepository.save(member);
        return member.getId();
    }

    // Ctrl + Alt + M (Extract Method) 메소드로 만들어준다.
    private void validateDuplicateMember(Member member) {
        memberRepository.findByName(member.getName())
                .ifPresent(m -> {
                    throw new IllegalStateException("이미 존재하는 회원이다!!");
                });
    }

    // 전체 회원 조회
    public List<Member> findMembers() {
        return memberRepository.findAll();
    }

    public Optional<Member> findOne(Long memberId) {
        return memberRepository.findById(memberId);
    }

}
```

10. MemberService Test 생성 및 작성
- Ctrl + Alt + T 누르고, 체크하고 생성

```java
package hello.hellospiring.service;

import hello.hellospiring.domain.Member;
import hello.hellospiring.repository.MemoryMemberRepository;
import org.assertj.core.api.Assertions;
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

import java.util.Optional;

import static org.junit.jupiter.api.Assertions.*;

class MemberServiceTest {

    MemberService memberService;
    MemoryMemberRepository memberRepository;

    @BeforeEach
    public void beforeEach() {
        memberRepository = new MemoryMemberRepository();
        memberService = new MemberService(memberRepository);
    }

    @AfterEach
    public void afterEach() {
        memberRepository.clearStore();
    }

    @Test
    void join() {
        // given
        Member member = new Member();
        member.setName("hello");

        // when
        Long saveId = memberService.join(member);

        // then
        Member findMember = memberService.findOne(saveId).get();
        Assertions.assertThat(member.getName()).isEqualTo(findMember.getName());
    }

    @Test
    public void 중복_회원_예외() {
        Member member1 = new Member();
        member1.setName("spring");
        memberService.join(member1);

        Member member2 = new Member();
        member2.setName("boot");
        memberService.join(member2);
    }

    @Test
    void findMembers() {
    }

    @Test
    void findOne() {
    }
}
```

