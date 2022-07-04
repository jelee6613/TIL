# Java_09_Collection



## Collection Framework

- 객체들을 한곳에 모아 놓고 편리하게 사용할 수 있는 환경을 제공



### 정적 자료구조 (Static structure)

- 고정된 크기의 자료구조
- 배열이 대표적인 정적 자료구조
- 선언 시 크기를 명시하면 바꿀 수 없음



### 동적 자료구조 (Dynamic structure)

- 요소의 개수에 따라 자료구조의 크기가 동적으로 증가하거나 감소
- 리스트, 스택, 큐 등



#### List

- 순서가 있고, 중복을 허용, 가변길이 특성을 제외하면 배열(고정길이)과 유사
- 구현 클래스
  - `ArrayList`
    - 장점 : 탐색에 유리
    - 단점 : 추가나 삭제에 불리
  - `LinkedList`
    - 장점 : 추가나 삭제에 유리
    - 단점 : 탐색에 불리

```java
List<String> lst = new ArrayList<>();
		lst.add("Kim");
		lst.add("Park");
		
		lst.add(1, "Lee");
		
		for (int i=0; i < lst.size(); i++) {
			if (lst.get(i).equals("Lee")) {
				System.out.println(lst.get(i));  // Lee		
			}
		}
```



#### Set

- 순서가 없고, 중복을 허용하지 않음
- 장점 : 빠른 속도, 효율적인 중복 데이터 제거 수단
- 단점 : 단순 집합의 개념으로 정렬하려면 별도의 처리가 필요하다.
- 구현 클래스
  - `HashSet`
  - `TreeSet`

```java
Set<String> set = new HashSet<>();
set.add("Kim");
set.add("Lee");
set.add("Park");

set.add("Lee");
System.out.println(set);  // [Lee, Kim, Park]
```



#### Map

- Key(키)와 Value(값)를 하나의 Entry로 묶어서 데이터 관리, 순서는 없으며, 키에 대한 중복은 없음
- 장점 : 빠른 속도
- 구현 클래스
  - `HashMap`
  - `TreeMap`

```java
Map<String, Integer> map = new HashMap<>();
map.put("Lee", 28);
map.put("Byul", 25);

System.out.println(map);  			// {Byul=25, Lee=28}
System.out.printIn(map.get("Lee"))  // 28
```