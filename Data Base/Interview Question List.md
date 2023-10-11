# 데이터 베이스 개론

<a href = 'https://www.google.co.kr/books/edition/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4_%EA%B0%9C%EB%A1%A0_3%ED%8C%90/jTJaEAAAQBAJ?hl=ko&gbpv=0'>**데이터베이스 개론 (3판)**</a>

## Key
### Super Key란 ?
 Super Key 는 **Table 내의 특정한 튜플을 식별할 수 있도록하는 Attribute의 집합**이다. 어떤 Attribute의 집합으로 특정한 Tuple을 식별하도록 하는 속성이 유일성이고 Super Key는 항상 이 유일성을 만족시켜야한다. 
    
### Candiate Key란 ?
Candiate Key는 Super Key가 만족해야하는 유일성 뿐만 아니라 최소성도 만족시켜야 한다. 최소성이란 슈퍼키에 속하는 **Attribute의 집합 내에 Tuple을 식별하기 위한 Attribute만 존재하는 Key**를 의미한다. 예를 들어 주민등록번호와 이름은 Super Key가 될 수 있지만 Candiate Key는 될 수 없다. 동명이인이 있을 수 있기 때문이다.
    
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
**Inner Join 은 두 Table 사이에 공통된 속성을 찾아 Field 값이 같은 Tuple을 합쳐서 하나의 Table로 만든다.** 이때 Join에 대한 조건을 직접 지정해주어서 지정된 속성과 속성값을 기준으로 테이블을 합치게 된다. 
   
### Natural Join과 Inner Join의 차이점
**Inner Join은 동일한 속성을 두 Table의 각각 속한 별개의 속성으로 표시하는 반면에 Natural Join은 하나의 속성으로 처리한다.**
  
```sql
# Inner Join
| table1.name | table2.name |

# Natural Join
| name |
```

### Outer Join이란 ?
**Outer Join은 두 Table을 동일한 속성과 속성값을 기준으로 합치지만 양 Table에 동일한 값이 없는 Tuple도 함께 합쳐준다**. 이때 값이 없는 필드는 NULL로 표시한다.
   
### Outer Join의 종류
**Left Join, Right Join, Full Join**이 있다.
**Left Join**은 왼쪽 Table에 있는 Data를 모두 읽은 뒤 좌측 Table을 읽으며 공통된 속성과 속성값을 가진 Tuple을 찾는다. 따라서 왼쪽 Table에는 존재하지 않지만 오른쪽 Table에 존재하는 Tuple은 제외된다.
**Right Join**은 반대로 오른쪽 Table을 먼저 읽기 때문에 오른쪽 Table에 존재하지 않는 속성값을 가진 Tuple은 왼쪽 Table에서 합칠 때 제외된다. 
**Full Join**은 두 Table의 모든 Tuple을 합쳐준다. 따라서 서로 겹치지 않는 Tuple도 제외되지 않고 모두 포함된다.
  
### MySQL에서 Full Join을 구현하는 방법
**MySQL 에서는 Full Join을 지원하지 않기 때문에 두 테이블을 각각 Left Join, Right Join하고 UNION으로 합쳐주어야 한다.**