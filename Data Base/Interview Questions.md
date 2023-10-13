# 데이터 베이스 개론

<a href = 'https://www.google.co.kr/books/edition/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4_%EA%B0%9C%EB%A1%A0_3%ED%8C%90/jTJaEAAAQBAJ?hl=ko&gbpv=0'>**데이터베이스 개론 (3판)**</a>

## Key

### Super Key란 ?
Super Key 는 **Table 내의 특정한 튜플을 식별할 수 있도록하는 Attribute의 집합**이다. 어떤 Attribute의 집합으로 특정한 Tuple을 식별하도록 하는 속성이 유일성이고 Super Key는 항상 이 유일성을 만족시켜야한다.
    
### Candiate Key란 ?
Candiate Key는 Super Key가 만족해야하는 유일성 뿐만 아니라 최소성도 만족시켜야 한다. 최소성이란 Super Key에 속하는 **Attribute의 집합 내에 Tuple을 식별하기 위한 Attribute만 존재하는 Key**를 의미한다. 예를 들어 주민등록번호와 이름은 Super Key가 될 수 있지만 Candiate Key는 될 수 없다. 동명이인이 있을 수 있기 때문이다.
    
### Primary Key란 ?
**Primary Key는 Candiate Key 중 하나를 선택하여 해당 Table에서 Tuple을 구분하는 기준으로 삼는 Key**를 의미한다. Primary Key는 NULL 값을 가질 수 없다는 엄격한 규칙이 있다.
  
### Alternate Key란 ?
**여러 Candiate Key들 중 Primary Key로 선택되지 않은 나머지 후보Key들은 모두 Alternate Key가 된다.**
   
### Foreign Key란 ?
**Foreign Key는 다른 Table의 Primary Key를 참조하는 Key**이다. Foreign Key의 Field 값은 Foregin Key가 참조하는 Primary Key의 Field값과 동일하거나 NULL 이어야 한다는 규칙이 있다.

## Join

### Natural Join이란 ?
**Natural Join은 두 Table에서 공통된 속성을 찾아 Field 값이 같은 Tuple을 합쳐서 하나의 Table로 만들어준다.** Natural Join은 동일한 자동으로 공통되는 속성을 찾기 때문에 두 Table의 도메인, 속성값, Field 값이 같아야 한다는 조건이 있다.
    
### Inner Join이란 ?
**Inner Join 은 두 Table 사이에 공통된 속성을 찾아 Field 값이 같은 Tuple을 합쳐서 하나의 Table로 만든다.** 이때 Join에 대한 조건을 직접 지정해주어서 지정된 속성과 속성값을 기준으로 Table을 합치게 된다.
   
### Natural Join과 Inner Join의 차이점
**Inner Join은 동일한 속성을 두 Table의 각각 속한 별개의 속성으로 표시하는 반면에 Natural Join은 하나의 속성으로 처리한다.**
  
```sql
# Inner Join
| table1.name | table2.name |

# Natural Join
| name |
```

### Outer Join이란 ?
**Outer Join은 두 Table을 동일한 속성과 속성값을 기준으로 합치지만 양 Table에 동일한 값이 없는 Tuple도 함께 합쳐준다**. 이때 값이 없는 Field는 NULL로 표시한다.
   
### Outer Join의 종류
**Left Join, Right Join, Full Join**이 있다.
**Left Join**은 왼쪽 Table에 있는 Data를 모두 읽은 뒤 좌측 Table을 읽으며 공통된 속성과 속성값을 가진 Tuple을 찾는다. 따라서 왼쪽 Table에는 존재하지 않지만 오른쪽 Table에 존재하는 Tuple은 제외된다.
**Right Join**은 반대로 오른쪽 Table을 먼저 읽기 때문에 오른쪽 Table에 존재하지 않는 속성값을 가진 Tuple은 왼쪽 Table에서 합칠 때 제외된다. 
**Full Join**은 두 Table의 모든 Tuple을 합쳐준다. 따라서 서로 겹치지 않는 Tuple도 제외되지 않고 모두 포함된다.
  
### MySQL에서 Full Join을 구현하는 방법
**MySQL 에서는 Full Join을 지원하지 않기 때문에 두 테이블을 각각 Left Join, Right Join하고 UNION으로 합쳐주어야 한다.**

## Normalization 

### 데이터 베이스 이상 현상이란 ?
**데이터 이상현상은 데이터베이스 내부에서 발생되는 불일치 현상**을 말한다. 데이터 이상현상에는 3종류가 있다.
**갱신 이상**은 어떤 데이터를 업데이트할 때 데이터베이스 내부에 중복된 데이터 중 일부만 갱신하여 데이터가 불일치 되는 문제입니다.
**삽입 이상**은 테이블에 새로운 튜플을 삽입할 때, 특정 속성에 대한 필드 값이 존재하지 않아 불필요한 NULL 값을 삽입하게 되는 문제입니다.
**삭제 이상**은 테이블에서 어떤 속성값을 삭제하고 싶을 때, 튜플 전체를 삭제하면서 발생하는 문제입니다.

### 데이터 베이스 정규화 방법
**데이터 베이스 이상현상을 방지하기 위해 데이터의 중복을 없애는 목적으로 정규화를 사용**한다. 정규화는 1NF부터 6NF, 그리고 BCNF가 있다.
**1NF**는 테이블의 모든 속성이 원자적인 값을 지니게 한다.
**2NF**는 1NF를 만족하며 Table의 모든 속성이 Primary Key에 대해 완전 함수적 종속을 만족해야한다. 완전 함수적 종속이란 Primary Key를 구성하는 모든 속성을 사용해야 Tuple을 특정할 수 있는 것을 말한다. Primary Key의 일부 속성만 사용해서 Tuple을 특정할 수 있다면, 2NF에 위배된다.
**3NF**는 2NF를 만족하며 Primary Key에 속하지 않는 속성이 이행적 함수 종속을 가지지 않아야한다. 이행적 함수종속은 어떤 속성 X로 속성 Y를 특정할 수 있을 때 Y로 Z 속성을 특정할 수 있어 X가 Z를 특정할 수 있는 상황을 말한다. 이때는 X, Y 로 구성된 Table과 Y, Z 로 구성된 Table로 분리하여 3NF를 만족킨다.
**BCNF**는 Table에 존재하는 모든 결정자가 Candiate Key가 되게 만들어야합니다. 만약 Candiate Key가 될 수 없다면 해당 결정자와 그 결정자와 종속관계에 있는 속성을 따로 분리해주는 것으로 BCNF 정규화를 만족시킬 수 있다.

### 정규화는 반드시 필요한가 ?
정규화는 데이터 이상현상을 방지하지만 Table을 여러개로 나누게 되므로 이후에 JOIN 연산을 많이 발생기켜 성능저하의 원인이 될 수 있다. 따라서 Table 사용시에 성능저하가 예상되는 Table은 의도적으로 정규화를 적용하지 않는 반정규화를 사용하기도 한다.

## Transaction 

### Transaction이란 ?
**Transaction은 데이터 베이스의 상태를 변화시키는 작업의 단위**를 말한다. 

### Transaction 보호가 필요한 이유
**Transaction은 다수의 사용자가 데이터 베이스의 데이터에 접근할 때 데이터의 무결성을 보장하기 위해서 사용**한다. 

### Transaction의 성질
Transaction은 4가지 성질을 가져야 한다. **(ACID)**
**원자성**이란 Transaction에 관련된 작업은 모두 다 실행되거나 실행되지 않도록 하는 것을 의미한다. 
**일관성**이란 Transaction이 완료되었을 때, 데이터 베이스의 데이터가 일관적인 상태를 유지하도록 해야하는 것을 의미한다. 
**격리성**이란 어떤 Transaction이 수행될 때 다른 Transaction이 간섭할 수 없게 해야하는 것을 의미한다. 
**지속성**이란 한번 성공한 Transaction은 데이터 베이스에 영구적으로 반영되어야 한다는 것을 의미한다. 

### 원자성을 보장하는 방법
Transaction의 원자성을 보장하기 위해서 **Commit**과 **Rollback**을 사용한다. 
**Commit**은 Transaction 작업이 정상적으로 종료되었고 데이터 베이스에 적용되었음을 확정한다. 
**Rollback**은 현재까지 진행중이던 Transaction 작업을 취소하고 Transaction이 시작되기 전 상태로 데이터 베이스를 되돌린다. 

### 일관성을 보장하는 방법
**일관성은 Trigger를 통해 어떤 작업이 수행될 때 연쇄적으로 다른 작업을 수행할 수 있도록 할 수 있다.** 
예를 들어 한 Table의 Tuple을 삭제한다고 했을 때, Foreign Key에 의해 연결된 Table이 있다면 해당 Table의 Tuple도 함께 삭제해주는 작업을 Trigger로 지정할 수 있다. 

### 격리성이 보장되지 않아 발생하는 이슈
**Phantom Read, Non-Repeatable Read, Dirty Read** 문제가 있다. 
**Phantom Read**는 한 Transaction 안에서 두 번의 읽기 연산이 있을 때, 처음 데이터를 읽은 후 다른 Transaction이 새로운 Tuple을 데이터 베이스에 삽입시켜 한번 더 데이터를 읽을 때 이전에는 없었던 데이터가 새로 생기는 현상을 의미한다. 
**Non-Repeatable Read**는 어떤 Transaction이 데이터를 두 번 조회할 때 처음 조회한 직후에 다른 Transaction이 간섭하여 해당 데이터의 값을 갱신하게 되면, 다음 조회에는 처음과 다른 데이터값이 조회되는 현상을 의미한다. 
**Dirty Read**는 어떤 Transaction이 아직 Commit을 하지 않은 상황에서 데이터를 수정하고 다른 Transaction이 수정된 데이터를 읽었을 때, 앞선 Transaction이 Rollback 된다면 데이터 베이스에 더이상 존재하지 않은 데이터를 조회하게 되는 현상을 의미한다. 

### Transaction 격리 수준
**Level 0-3까지 Transaction 격리 수준**이 있다. 
**Level 0**은 Read Uncommited로 모든 Transaction이 제한없이 데이터에 접근할 수 있는 격리 수준이다. 
**Level 1**은 Read Commited로 Commit이 완료된 데이터만 읽도록 한다. 
**Level 2**는 Repeatable Read로 한 Transaction 안에서 여러 번 Table을 조회해도 같은 Table을 얻을 수 있게 한다. 이를 위해 해당 Transaction이 시작되기 전에 완료된 Commit을 기준으로 데이터를 조회한다. 
**Level 3**은 Serializable로 여러 Transaction이 병렬적으로 수행되는 것을 허용하지 않는다. 

### 공유 Lock과 Beta Lock에 대한 설명
**공유 Lock 은 데이터를 읽을 때 사용하는 Lock**이고 B**eta Lock은 데이터를 변경할 때 사용하는 Lock**이다. 
**공유 Lock**으로 인해 읽기 연산은 여러 Transaction이 한번에 사용할 수 있다. 
그리고 **Beta Lock**으로 인해 해당 Lock이 해제될 때까지 다른 Transaction이 데이터를 변경하지 못하게 할 수 있다. 

### Lock 사용의 단점
**Locking이 과도하게 사용되면 동시성 문제는 해결**되지만 **처리 시간이 길어지는 단점**이 있다.

## Index

### Index의 장점과 단점
Index를 사용하면 Table을 조회하는 속도가 빨라진다. 하지만 조회가 아니라 데이터를 변경해야하는 속성에 Index를 걸면 오히려 성능이 저하될 수 있다. 

### 데이터를 변경하는 속성에 적용하면 성능이 저하되는 이유 
삭제, 갱신, 삽입으로 기존 데이터를 변경하거나 새로운 데이터를 추가하게 되면 **해당 데이터에 걸려있는 Index를 함께 변경하거나 추가해주어야 한다.** 따라서 추가적인 연산이 발생하므로 성능이 저하된다. 

### Index를 사용하기 적절한 상황이란 ?
**데이터의 양이 많지만 조회를 주로하고 중복 데이터가 많지 않은 속성에 적용했을 때 좋은 성능을 보장받을 수 있다.** 

### Index는 내부적으로 어떻게 구현되는가 ?
**데이터 베이스에서는 B+Tree 자료구조를 사용하여 Index를 관리**한다. 데이터를 나타내는 각 Leaf Node들이 Index를 가지고 있고 각 Leaf Node들이 서로 Double Linked-List로 연결되어 있어 순차적인 탐색을 빠르게 할 수 있다. 

### Clustered Index와 Non-Clustered Index의 차이점
**Clustered Index**는 데이터가 추가될 때마다 Index를 기준으로 데이터를 재배열한다. 따라서 데이터가 순차적으로 저장된다. 이 때문에 조회의 속도는 빠르지만 갱신, 삽입, 삭제 시 전체 Table을 다시 재배열 해주어야하는 Overhead를 가지고 있다. 
**Non-Clustered Index**는 데이터와 Index를 따로 분리하여 관리한다. 따라서 데이터는 물리적으로 정렬하지 않고 정렬된 Index가 가리키는 Pointer로 데이터를 찾는다. 따라서 조회에는 Clustered Index보다 많은 시간이 걸리지만 갱신, 삭제, 삽입에는 Clustered Index보다 빠른 성능을 보인다. 

### Index를 지정하는 기준
**Cardinality가 높은 Column을 Index로 결정하는 것이 유리**하다. 

### Cardinality란 ?
**Cardinality는 Column 내 중복되는 데이터의 비율에 따라서 결정**된다. 어떤 Column에 중복되는 데이터가 많다면 Cardinality가 낮다고 할 수 있다. Cardinality를 수치화하면 해당 Column에 있는 고유한 데이터의 갯수이다. 

### Selectivity란 ?
**Selectivity는 Cardinality를 해당 Column의 전체 데이터 갯수로 나눈 값**이다. 즉, 하나의 Column 내 고유한 데이터의 비율을 나타낸다. 

### Index를 설정할 때 Cardinality가 성능에 미치는 영향 
**Cardinality가 높은 Index를 설정하면 한 Index로 많은 데이터를 Filtering 할 수 있기 때문에 Index가 더 좋은 성능을 내도록 할 수 있다.** 

### 결합 Index란 ?
**결합 Index는 두 개 이상의 Column을 합쳐 Index를 생성하는 Index**이다. 예를 들어 특정 성별이면서 특정 연령 이상인 사람들의 목록을 얻는 연산이 자주 수행되는 Table이라면 성별과 연령을 결합 Index로 합쳐 관리할 수 있다.

## NoSQL

### NoSQL과 RDBMS의 차이점
RDBMS는 Schema를 사용하여 데이터를 저장한다. 또한 SQL 명령을 통해 구조화된 데이터 베이스를 구축할 수 있어 안전하고 Transaction을 통해 데이터의 무결성을 보장한다. 하지만 구조화된만큼 시스템이 복잡해지고 엄격하다. 
반면 NoSQL은 Schema가 없기 때문에 데이터를 추가하는 것이 자유롭고 확장에 열려있다. 하지만 중복 데이터에 대한 관리가 RDMS에 비해 복잡하다는 단점이 있다. 

### NoSQL이 확장에 열려있는 이유 
**NoSQL은 데이터를 분산된 Server에 저장하는 분산 처리 방식으로 운영**된다. 따라서 대용량 데이터를 더 쉽게 다룰 수 있다.