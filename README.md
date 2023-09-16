# gptclass

## Class Diagram
```mermaid
  class MembershipSystem {
    + signUp()
    + viewProfile()
    + withdraw()
    + approveMembership()
    + listMembersByGrade(grade)
    + listWithdrawnMembers()
    - upgradeMembership()
  }

  class User {
    + signUp()
    + viewProfile()
    + withdraw()
    + accumulatePoints()
  }

  class Admin {
    + approveMembership()
    + listMembersByGrade(grade)
    + listWithdrawnMembers()
  }

  class Membership {
    - points: int
    - grade: string
    + getPoints()
    + getGrade()
    + upgradeMembership()
  }

  MembershipSystem --|> User : includes
  MembershipSystem --|> Admin : includes
  MembershipSystem --|> Membership : includes
  MembershipSystem "1" --o "1" Membership : manages
  User --|> Membership : has
  Admin --|> Membership : has

```

## Sequence Diagram
```mermaid
  participant User as User
  participant MembershipSystem as System
  participant UserDB as User Database
  participant Admin as Admin

  User ->> System: 회원 가입 요청
  System ->> UserDB: 사용자 정보 저장
  User ->> System: 로그인
  System ->> User: 로그인 성공
  User ->> System: 개인정보 조회
  System ->> UserDB: 개인정보 검색
  User ->> System: 탈퇴 요청
  System ->> UserDB: 사용자 정보 삭제
  User ->> System: 포인트 조회
  System ->> UserDB: 포인트 정보 검색
  User ->> System: 로그아웃

  User ->> System: 포인트 적립
  System ->> UserDB: 포인트 정보 업데이트

  User ->> System: 현재 멤버십 등급 조회
  System ->> UserDB: 멤버십 정보 검색
  User ->> System: 멤버십 업그레이드 확인

  alt 업그레이드 가능
    System ->> User: 블루 멤버십으로 업그레이드
  else 업그레이드 불가
    System ->> User: 업그레이드 조건 충족 미달
  end

  User ->> System: 로그아웃

  Admin ->> System: 회원 가입 승인 요청
  System ->> UserDB: 사용자 정보 검색
  System ->> Admin: 사용자 정보 반환
  Admin ->> System: 회원 가입 승인

  Admin ->> System: 등급별 회원 목록 조회
  System ->> UserDB: 멤버십 정보에 따른 회원 목록 검색
  Admin ->> System: 조회 결과 반환

  Admin ->> System: 탈퇴회원 조회
  System ->> UserDB: 탈퇴한 회원 목록 검색
  Admin ->> System: 조회 결과 반환

```
