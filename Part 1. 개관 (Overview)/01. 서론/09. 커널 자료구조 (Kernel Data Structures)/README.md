# 1.9 커널 자료구조 (Kernel Data Structures)
- 다음으로 운영체제 구현의 중심 주제인 시스템에서 데이터가 구조화되는 방법을 다룬다. 운영체제에서 광범위하게 사용되는 다수의 기본 데이터 구조를 알아보자.

## 1.9.1 리스트, 스택 및 큐 (Lists, Stacks, and Queues)
- 배열은 각 원소가 직접 접근할 수 있는 단순한 자료구조. 예를 들면 메인 메모리는 배열로 구성된다. 저장된 데이터가 한 바이트보다 크면 그 데이터에 여러 바이트를 할당할 수 있으며, 
그 데이터는 데이터 수 X 데이터 크기로 주소 지정된다. 그렇지만 크기가 변하는 데이터는 어떻게 저장할까? 또한 한 데이터를 제거하고 나머지 데이터들을 유지해야 할 경우에는 어떻게 할까?
이러한 상황에서는 배열 대신 다른 자료구조를 사용해야 한다.
- 배열 다음으로 리스트가 컴퓨터 과학의 가장 기본적인 자료구조일 것이다. 배열의 각 항은 직접 접근할 수 있지만 리스트의 각 항은 특정 순서로 접근해야 한다. 즉, 리스트는 데이터 값들의
모음을 하나의 시퀀스로 나타낸다. 이 구조를 구현하는 가장 일반적인 방법이 연결 리스트 (linked list) 이다. 연결 리스트는 각 항이 다른 하나에 연결되어 있다.
- 연결 리스트는 다음과 같은 유형이 있다.
  - 단일 연결 리스트에서는 각 항은 후속항을 가리킨다.
  - 이중 연결 리스트에서는 한 항은 자신의 앞 항이나 뒤 항을 가리킨다.
  - 원형 연결 리스트에서는 리스트의 마지막 항이 널(null)이 아니라 첫 항을 가리킨다.
- 연결 리스트는 가변 수의 항들을 수용하며 항의 삭제와 삽입이 쉽다. 리스트의 단점은 길이가 n인 리스트에서 특정 항을 검색하는 성능이 선형 즉, O(n)이라는 점이다. 왜냐하면 최악의 경우
전체 n개의 항을 전부 살펴보아야 할 수 있기 때문이다. 리스트는 때때로 커널 알고리즘에서 직접 사용된다. 그러나 스택이나 큐같은 보다 강력한 자료 구조를 구축하는 데 자주 사용된다.
- 스택은 순차적 순서를 가진 자료구조로 항을 넣거나 꺼내는 데 후입선출 (last in first out, LIFO)을 사용. 즉, 스캑에 마지막에 삽입된 항이 먼저 제거된다. 
- 스택에서 항을 삽입하거나 제거하는 작업을 각각 푸시(push), 팝(pop). 운영체제는 함수호출에서 스택을 사용. 
- 매개 변수, 지역 변수 및 반환 주소 등이 스택에 푸쉬. 함수 호출에서 반환하면 스택에서 해당 항을 팝.
- 반면, 큐는 순차 순서의 자료구조로 선입선출 (first in first out, FIFO)을 사용. 각 항은 삽입된 순서대로 큐로부터 제거됨. 
- 일상생활의 예로 상점의 계산대에서 기다리는 줄, 교통 신호를 기다리는 자동차들이 있다. 
- 운영체제에서도 흔히 사용되는데, 프린터에 보내진 작업은 전형적으로 제출된 순서대로 인쇄됨. CPU에서 수행을 기다리는 태스크들은 종종 큐로 구성.

## 1.9.2 트리 (Trees)
- 트리는 데이터의 서열을 표시하는 데 사용 가능한 자료구조.
- 트리 구조에서 데이터 값들은 부모-자식 관계로 연결됨
- 일반 트리 (general tree)에서 부모는 임의의 수의 자식을 가질 수 있다.
- 이진 트리에서 부모는 최대 두 개의 자식을 가질 수 있으며, 이들은 왼쪽 자식과 오른쪽 자식이라고 한다.
- 이진 탐색 트리는 추가로 부모의 두 자식 사이에 왼쪽 자식 <= 우측 자식의 순서를 요구한다.
- 이진 트람색 트리에서 한 항을 찾으려면 최악의 성능은 O(n)이다. 이러한 상황을 방지하기 위해 균형 이진 탐색 트리를 만드는 알고리즘 사용 가능.
- 그 경우 n개의 항을 갖는 트리는 최대 깊이가 log n 이며, 따라서 최악 경우 성능 O(log n)을 보장.
- Linux가 CPU 스케줄링 알고리즘의 일부로 (red-black tree로 알려진) 균형 이진 탐색 트리를 사용한다.

## 1.9.3 해시 함수와 맵 (Hash Functions and Maps)
- 해시 함수는 데이터를 입력으로 받아 이 데이터에 산술 연산을 수행하여 하나의 수를 반환한다. 이 수는 그 데이터를 인출하기 위해 테이블 (일반적으로 배열)의 인덱스로 사용 가능.
- 크기 n인 리스트에서 데이터를 찾는 데 최대 O(n)의 비교가 필요한 반면 테이블에서 해시 함수를 사용하여 데이터를 검색할 경우 O(1)만큼 좋을 수 있다. 이는 상세 구현에 좌우됨.
이러한 성능 떄문에 해시 함수는 운영체제에서 광범위하게 사용된다.
- 해시 함수의 한 어려운 점은 두 개의 서로 다른 입력이 하나의 출력 값을 가질 수 있다는 것이다. 즉, 이들이 테이블의 동일 위치로 색인될 수 있다. 이를 우리는 해시 충돌
  (hash collision)이라 하며 테이블의 각 항에 연결 리스트를 두어 동일한 해시 값을 갖는 모든 항을 수록하게 한다. 물론 충돌이 많을 수록 해시 함수의 효율이 떨어지게 된다.
- 해시 함수의 한 가지 용도는 해시 함수를 사용하여 [키:값] 쌍을 연결 (또는 매핑)하는 해시맵을 구현하는 것. 매핑이 설정되면 해시 함수를 키에 적용하여 해시 맵에서 값을 얻을 수 있다.
- 예를 들면, 한 사용자 이름이 한 패스워드로 매핑된다고 하자. 패스워드 인증은, 한 사용자가 자신의 사용자 이름과 패스워드를 입력하고 이어 사용자 이름에 해시 함수를 적용하여 그 결과
값으로 패스워드를 검색한다. 검색된 패스워드와 사용자가 인증을 위해 입력한 패스워드와 비교된다.

## 1.9.4 비트맵 (Bitmaps)
- 비트맵은 n개의 항의 상태를 나타내는 데 사용 가능한 n개의 이진 비트의 스트링이다. 예를 들어, 다수의 자원이 있고, 각 자원의 가용 여부를 이진 비트 값으로 표시한다. 0은 자원이
사용 가능함을 표시하고, 1은 사용 불가능함을 표시한다. (또는 그 반대). 비트맵에서 i번째 위치의 값은 i번째 자원과 연관되어 있다. 예로 다음 비트맵을 고려해 보자 :
001011101 : 자원 2,4,5,6,8은 사용 불가, 자원 0,1,3,7은 사용 가능하다.
- 비트맵의 힘은 공간 효율성을 고려할 때 분명해진다. 단일 비트 대신 8비트의 부울 값을 사용하는 경우 자료구조는 8배의 크기가 될 것이다. 따라서 비트맨은 대량의 자원의 가용성을 나타낼 때
일반적으로 사용된다. 디스크 드라이브는 좋은 예가 될 수 있다. 중간 크기의 디스크 드라이브는 디스크 블록이라 불리는 수천 개의 개별 단위로 나눌 수 있다. 비트맵을 사용하여 각 디스크
블록의 가용성을 나타낼 수 있다.
- 요약하면, 운영체제의 구현에는 자료구조가 널리 사용된다.

