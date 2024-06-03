---
layout: post
title: Spring Transaction Scope
date: 2024-05-28
image: /assets/images/blog/2024-05-28/1.png
author: ultrakeypoint
tags: [dev, srping, transaction]
---

Transaction은 데이터베이스 관리 시스템 또는 유사한 시스템에서 상호작용의 단위 또는 업무 처리 단위, 로직 단위이다. 여기서 유사한 시스템이란 트랜잭션이 성공과 실패가 분명하고 상호 독립적이며, 일관되고 믿을 수 있는 시스템을 의미한다. 데이터의 정합성을 보장하기 위해 고안된 방법이다.

`트랜잭션 시작` → `비즈니스 로직 실행` → `트랜잭션 커밋`(로직 실패 시 롤백)

Transaction은 이런 순서로 실행하면서 오류로부터 복구를 허용하고 데이터베이스를 일관성 있게 유지하는 안정적인 작업 단위를 제공한다. 그리고 동시에 접근하는 여러 프로그램 간 격리를 제공하고, 데이터베이스 시스템은 각각의 트랜잭션에 대해 원자성(Atomicity), 일관성(Consistency), 독립성(Isolation), 영구성(Durability)을 보장한다. 이 성질을 첫 글자를 모아서 ACID라 부른다.

`원자성`(Atomicity) : 트랜잭션이 완전히 성공하거나 완전히 실패하는 단일 단위로 처리되도록 보장하는 능력이다. 중간 단계까지 실행되고 실패하는 일이 없도록 하는 것이다.  
`일관성`(Consistency) : 각 데이터 트랜잭션이 데이터베이스를 일관성 있는 상태에서 일관성 있는 상태로 이동해야 함을 의미한다. 즉 트랜잭션이 성공적으로 완료하면 언제나 동일한 데이터베이스 상태로 유지하는 것을 의미한다.  
`독립성`(Isolation) : 트랜잭션을 수행할 때 다른 트랜잭션의 연산 작업이 끼어들지 못하도록 보장하는 것을 의미한다. 이것은 트랜잭션 밖에 있는 어떤 연산도 중간 단계의 데이터를 볼 수 없음을 의미한다. 여러 트랜잭션이 동시에 발생하는 경우 최종 상태는 트랜잭션이 개별적으로 발생한 것과 같아야 한다. 즉, 데이터베이스는 스트레스 테스트를 통과해야 한다. 즉, 과부하로 인해 잘못된 데이터베이스 트랜잭션이 발생하지 않아야 한다.  
`지속성`(Durability) : 성공적으로 수행된 트랜잭션은 영원히 반영(기록)되어야 함을 의미한다. 트랜잭션은 로그에 모든 것이 저장된 후에만 commit 상태로 간주할 수 있다. 데이터베이스 내의 데이터는 트랜잭션의 결과로만 변경되어야 하며 외부 영향에 의해 변경될 수 없어야 한다. 예를 들어 소프트웨어 업데이트로 인해 데이터가 실수로 변경되거나 삭제되지 않아야 한다.

아래 예제는 데이터를 전송하고 사용자에게 메시지를 전송하는 예제이다. 만약, 아래 예제에서 Trasaction이 commit 전 구간인 Service에서 처리하게 될 경우 send 되기 전에 메시지를 받을 수도 있다.

예제 :

```Java

public class UserController {

   UserService userService;

   @PostMapping(value = "/send")
   public void send(@RequestBody @Valid Req<UserVO> userVo) {

    boolean isSend = userService.send(userVo) <= 0;
    if(isSend) {
      Date date3 = new Date();
      SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
      String str3 = format.format(date3);
      log.info("transaction commit after : " + str3);
    }
   }
}

public class UserServiceImpl implements UserService {

  UserDao userDao;

  @Transactional(rollbackFor = Exception.class)
  public int send(UserVO userVO) {

    Date date1 = new Date();
    SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
    String str1 = format.format(date1);
    log.info("transaction begin start : " + str1);

    int count = userDao.send(userVO);

    // send된 데이터를 보장하려면 commit 완료된 service를 호출한 컨트롤러에서 처리해야 된다.
    // log.info("전송 되었습니다. : " + str1); // 아직 데이터 관점에서 전송되기 전이다.

    Date date2 = new Date();
    String str2 = format.format(date2);
    log.info("transaction commit before : " + str2);
    return count;
  }
}
```

결과 :

```javascript
transaction begin start : 2024-05-28 11:06:51
transaction commit before : 2024-05-28 11:06:51

// Send Data update time : 2024-05-28 11:06:52

transaction commit after : 2024-05-28 11:06:53
```
