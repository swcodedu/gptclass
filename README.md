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
