1. [배열의 특징1 - 배열과 인덱스](#배열의-특징1---배열과-인덱스)
2. [빅오(O) 표기법](#빅오o-표기법)
3. [배열의 특징2 - 데이터 추가](#배열의-특징2---데이터-추가)
4. [직접 구현하는 배열 리스트1 - 시작](#직접-구현하는-배열-리스트1---시작)
5. [직접 구현하는 배열 리스트2 - 동적 배열](#직접-구현하는-배열-리스트2---동적-배열)
6. [직접 구현하는 배열 리스트3 - 기능 추가](#직접-구현하는-배열-리스트3---기능-추가)
7. [직접 구현하는 배열 리스트4 - 제네릭1](#직접-구현하는-배열-리스트4---제네릭1)
8. [직접 구현하는 배열 리스트5 - 제네릭2](#직접-구현하는-배열-리스트5---제네릭2)
9. [정리](#정리)

## 배열의 특징1 - 배열과 인덱스
배열과 같이 여러 데이터(자료)를 구조화해서 다루는 것을 자료구조라고 한다.  
자바는 배열 뿐만 아니라, `컬렉션 프레임워크`라는 이름으로 다양한 자료 구조를 제공한다.  
컬렉션 프레임워크와 자료구조를 설명하기 전에 먼저 자료 구조의 가장 기본이 되는 배열의 특징을 알아보자.

### [ArrayMain1.java](..%2Fsrc%2Fcollection%2Farray%2FArrayMain1.java)
```java
public class ArrayMain1 {
    public static void main(String[] args) {
        int[] arr = new int[5];

        // index 입력: 0(1)
        System.out.println("==index 입력: 0(1)==");
        arr[0] = 1;
        arr[1] = 2;
        arr[2] = 3;
        System.out.println(Arrays.toString(arr));

        // index 변경: 0(1)
        System.out.println("==index 변경: 0(1)==");
        arr[2] = 10;
        System.out.println(Arrays.toString(arr));

        // index 조회: 0(1)
        System.out.println("==index 조회: 0(1)==");
        System.out.println("arr[2] = " + arr[2]);

        // 검색: O(n)
        System.out.println("==배열 검색: 0(n)==");
        System.out.println(Arrays.toString(arr));
        int value = 10;
        for (int i = 0; i < arr.length; i++) {
            System.out.println("arr[" + i + "]: " + arr[i]);
            if (arr[i] == value) {
                System.out.println(value + " 찾음");
                break;
            }
        }
    }
}
```

#### 실행 결과
```text
==index 입력: 0(1)==
[1, 2, 3, 0, 0]
==index 변경: 0(1)==
[1, 2, 10, 0, 0]
==index 조회: 0(1)==
arr[2] = 10
==배열 검색: 0(n)==
[1, 2, 10, 0, 0]
arr[0]: 1
arr[1]: 2
arr[2]: 10
10 찾음
```

### 배열의 특징
![arraylist1.png](imgs%2Farraylist1.png)  
- 배열에서 자료를 찾을 때 인덱스 (index)를 사용하면 매우 빠르게 자료를 찾을 수 있다.
- 인덱스를 통한 입력, 변경, 조회의 경우 한 번의 계산으로 자료의 위치를 찾을 수 있다.
### 배열 index 사용 예시
![arraylist2.png](imgs%2Farraylist2.png)  
- `arr[2]`에 위치한 자료를 찾는다고 가정해보자.
- 배열은 메모리상에 순서대로 붙어서 존재한다.
- `int`는 `4byte`를 차지한다.
- 따라서 배열의 시작위치인 x100 부터 시작해서 자료의 크기(4byte)와 인덱스 번호를 곱하면 원하는 메모리위치를 찾을 수 있다.
- 배열의 시작 참조(x100) + (자료의 크기(4byte) * 인덱스 위치(2)) = x108이 나온다. 여기에는 숫자 10이 들어있다.

배열의 경우 인덱스를 사용하면 한 번의 계산으로 매우 효율적으로 자료의 위치를 찾을 수 있다.
인덱스를 통한 입력, 변경, 조회 모두 한 번의 계산으로 필요한 위치를 찾아서 처리할 수 있다.
정리하면, 배열에서 인덱스를 사용하는 경우 데이터가 아무리 많아도 **한 번의 연산으로 필요한 위치를 찾을 수 있다.**


### 배열의 검색
배열에 들어있는 데이터를 찾는 것을 검색이라고 한다.  
배열에 있는 데이터를 검색할 때는 배열에 들어있는 데이터를 하나하나 비교해야 한다.
이 때는 이전과 같이 인덱스를 사용해서 한 번에 찾을 수 없다.
대신에 배열안에 들어있는 데이터를 하나하나 확인해야 한다.
따라서 평균적으로 볼 때 배열의 크기가 클 수록 오랜시간이 걸린다.

배열의 순차 검색은 배열에 들어있는 데이터의 크기 만큼 연산이 필요하다. **배열의 크기가 n이면 연산도 n만큼 필요하다.**

## 빅오(O) 표기법
빅오 (Big O) 표기법은 알고리즘의 성능을 분석할 때 사용하는 수학적 표현 방식이다. 이는 특히 알고리즘이 처리해야 할
데이터의 양이 증가할 때, 그 알고리즘이 얼마나 빠르게 실행되는지 나타낸다. 여기서 중요한 것은
알고리즘의 정확한 실행 시간을 계산하는 것이 아니라, 데이터의 양의 증가에 따른 성능의 변화 추세를 이해하는 것이다.

![arraylist3.png](imgs%2Farraylist3.png)

### 빅오 표기법의 예시
| 표기법        | 설명                                             | 예시                          |
|------------|------------------------------------------------|-----------------------------|
| O(1)       | 상수 시간: 입력 데이터의 크기에 관계없이 알고리즘의 실행 시간이 일정하다.     | 배열에서 인덱스를 사용하는 경우           |
| O(n)       | 선형 시간: 알고리즘의 실행 시간이 입력 데이터의 크기에 비례하여 증가한다.     | 배열의 검색, 배열의 모든 요소를 순회하는 경우  |
| O(n^2)     | 제곱 시간: 알고리즘의 실행 시간이 입력 데이터의 크기의 제곱에 비례하여 증가한다. | 보통 이중 루프를 사용하는 알고리즘에서 나타난다. |
| O(log n    | 로그 시간: 알고리즘의 실행 시간이 데이터의 크기의 로그에 비례하여 증가한다.    | 이진 검색                       |
| O(n log n) | 선형 로그 시간                                       | 많은 효율적인 정렬 알고리즘들            |

빅오 표기벚은 매우 큰 데이터를 입력한다고 가정하고, 데이터 양 증가에 따른 성능의 변화 추세를 비교하는데 사용한다.
쉽게 이야기해서 정확한 성능을 측정하는 것이 목표가 아니라 매우 큰 데이터가 들어왔을 때의 대략적인 추세를 비교하는 것이 목적이다.
따라서 데이터가 매우 많이 들어오면 추세를 보는데 상수는 크게 의미가 없어진다.
이런 이유로 빅오 표기법에서는 상수를 제거한다. 예를 들어 O(n + 2), O(n/2)도 모두 O(n)으로 표시한다.

빅오 표기법은 별도의 이야기가 없으면 보통 최악의 상황을 가정해서 표기한다. 
물론 최적, 평균, 최악의 경우로 표기하는 경우도 있다. 예를 들어서 앞서 살펴본 배열의 순차 검색의 경우를 나누어 살펴보자.
- 최적의 경우: 배열의 첫번 째 항복에서 바로 값을 찾으면 O(1)이 된다.
- 최악의 경우: 마지막 항목에 있거나 항목이 없는 경우 전체 요소를 순회한다. 이 경우 O(n)이 된다.
- 평균의 경우: 평균적으로 보면 보통 중간쯤 데이터를 발견하게 된다. 이 경우 O(n/2)가 되지만, 상수를 제외해서 O(n)으로 표기한다. 최악과 비교를 위해 O(n/2)로 표기하는 경우도 있다.

배열의 인덱스를 사용하면 데이터의 양과 관계없이 원하는 결과를 한 번에 찾기 때문에 항상 O(1)이 된다.

### 배열 정리
- 배열의 인덱스 사용: O(1)
- 배열의 순차 검색: O(n)

배열의 데이터가 100,000건이 있다면 인덱스를 사용하면 1번의 연산으로 결과를 찾을 수 있지만,
순차 검색을 사용한다면 최악의 경우 100,000번의 연산이 필요하다. 배열에 들어있는 데이터의 크기가 증가할 수록 그 차이는 매우 커진다.

따라서 인덱스를 사용할 수 있다면 최대한 활용하는 것이 좋다.

## 배열의 특징2 - 데이터 추가
이번에는 배열의 특정 위치에 데이터를 추가해보자.  
추가는 기존 데이터를 유지하면서 새로운 데이터를 입력하는 것을 뜻한다.
참고로 데이터를 중간에 추가하면 기존 데이터가 오른쪽으로 한 칸씩 이동해야 한다. 이 말을 좀 더 쉽게 
풀어보자면 데이터를 추가하려면 새로운 데이터를 입력할 공간을 확보해야 한다. 따라서 기존 데이터를
오른쪽으로 한 칸씩 밀어야 한다. (기존 데이터의 인덱스를 하나씩 증가시켜야 한다.)

### 배열의 데이터 추가 예시
배열에 데이터를 추가하는 위치에 따라 크게 3가지로 나눌 수 있다.
- [배열의 첫 번째 위치에 추가](#배열의-첫-번째-위치에-추가)
- [배열의 중간 위치에 추가](#배열의-중간-위치에-추가)
- [배열의 마지막 위치에 추가](#배열의-마지막-위치에-추가)

#### 배열의 첫 번째 위치에 추가
![arraylist4.png](imgs%2Farraylist4.png)  
- 배열에는 1, 2 데이터가 순서대로 입력되어 있다.
- 배열의 첫 번째 위치에 숫자 3을 추가해보자.

![arraylist5.png](imgs%2Farraylist5.png)  
- 기존 데이터들을 모두 오른쪽으로 한 칸씩 밀어서 추가할 위치를 확보애햐 한다.
- 이때 배열의 마지막 부분 부터 오른쪽으로 밀어야 데이터를 유지할 수 있다.
- 왼쪽의 데이터를 오른쪽에 대입하는 과정을 반복한다.
- 그림의 순서를 참고하자.
- 이 과정이 끝나면 1, 1, 2 데이터가 순서대로 저장되어 있다.

![arraylist6.png](imgs%2Farraylist6.png)  
- 첫 번째 공간이 확보되었다. 여기에 새로운 값인 숫자 3을 추가하면 된다.

#### 배열의 중간 위치에 추가
![arraylist7.png](imgs%2Farraylist7.png)   
- 배열의 중간이나 특정 index 위치에 추가하는 경우를 보자.
- 여기서는 인덱스 2의 공간을 확보해야 한다.

![arraylist8.png](imgs%2Farraylist8.png)  
- 지정한 index에 데이터를 추가할 위치를 확보해야 한다. 따라서 index부터 시작해서 데이터들을 오른쪽으로 한 칸씩 밀어야 한다.
- 이 경우 index 왼쪽의 데이터는 이동하지 않아도 된다.
- 순서를 참고하자.

![arraylist9.png](imgs%2Farraylist9.png)
- 인덱스 2의 공간이 확보되었다. 여기에 새로운 값인 숫자 4를 추가하면 된다.

#### 배열의 마지막 위치에 추가
![arraylist10.png](imgs%2Farraylist10.png)  
- 배열의 마지막 위치에 데이터를 추가하는 경우 여기가 배열의 마지막이다. 이 경우 기존 데이터를 이동하지 않아도 된다.
- 따라서 단순하게 값만 입력하면 된다.

### 배열에 데이터를 추가할 때 위치에 따른 성능 변화
- 배열의 첫 번째 위치에 추가
  - 배열의 첫 번째 위치를 찾는데는 인덱스를 사용하므로 O(1)이 걸린다.
  - 모든 데이터를 배열의 크기만큼 한 칸씩 이동해야 한다. 따라서 O(n) 만큼의 연산이 걸린다.
  - O(1 + n) ➡️ O(n)이 된다.
- 배열의 중간 위치에 추가
  - 배열의 위치를 찾는데는 O(1)이 걸린다.
  - index의 오른쪽에 있는 데이터를 모두 한 칸씩 이동해야 한다. 
  - 따라서 평균 연산은 O(n/2)이 된다.
  - O(1 + n/2) ➡️ O(n)이 된다.
- 배열의 마지막 위치에 추가
  - 이 경우 배열이 이동하지 않고, 배열의 길이를 사용하면 마지막 인덱스에 바로 접근할 수 있으므로 한 번의 계산으로 위치를 찾을 수 있고, 기존 배열을 이동하지 않는다.
  - 즉, O(1)이 된다.

### [ArrayMain2.java](..%2Fsrc%2Fcollection%2Farray%2FArrayMain2.java)
```java
public class ArrayMain2 {

    public static void main(String[] args) {

        int[] arr = new int[5];
        arr[0] = 1;
        arr[1] = 2;
        System.out.println(Arrays.toString(arr));

        // 배열의 첫 번째 위치에 추가
        // 기본 배열의 데이터를 한 칸씩 뒤로 밀고 배열의 첫 번째 위치에 추가
        System.out.println("배열의 첫 번째 위치에 3 추가 O(n)");
        int newValue = 3;
        addFirst(arr, newValue);
        System.out.println(Arrays.toString(arr));

        // index 위치에 추가
        // 기본 배열의 데이터를 한 칸씩 뒤로 밀고 배열의 index 위치에 추가
        System.out.println("배열의 index(2) 위치에 4 추가 O(n)");
        int index = 2;
        int value = 4;
        addAtIndex(arr, index, value);
        System.out.println(Arrays.toString(arr));

        System.out.println("배열의 마지막 위치에 5 추가 O(1)");
        addLast(arr, 5);
        System.out.println(Arrays.toString(arr));
    }

    private static void addLast(int[] arr, int newValue) {
        arr[arr.length - 1] = newValue;
    }

    private static void addFirst(int[] arr, int newValue) {
        for (int i = arr.length - 1; i > 0; i--) {
            arr[i] = arr[i - 1];
        }

        arr[0] = newValue;
    }

    private static void addAtIndex(int[] arr, int index, int newValue) {
        for (int i = arr.length - 1; i > index; i--) {
            arr[i] = arr[i - 1];
        }

        arr[index] = newValue;
    }
}
```

#### 실행 결과
```text
[1, 2, 0, 0, 0]
배열의 첫 번째 위치에 3 추가 O(n)
[3, 1, 2, 0, 0]
배열의 index(2) 위치에 4 추가 O(n)
[3, 1, 4, 2, 0]
배열의 마지막 위치에 5 추가 O(1)
[3, 1, 4, 2, 5]
```

### 배열의 한계
배열은 가장 기본적인 자료 구조이고, 특히 인덱스를 사용할 때 최고의 효율이 나온다.
하지만 이런 배열에는 큰 단점이 있다. 바로 배열의 크기를 배열을 생성하는 시점에 미리 정해야 한다는 것이다.  
예를 들어서 이벤트를 하는데, 누구나 이벤트에 참여할 수 있고, 이벤트가 끝나면 추첨을 통해서 당첨자를 정한다고 가정해보자.
이때 이벤트에 참여하는 사용자를 배열에 보관한다고 가정하자. 사용자들을 실시간으로 계속 추가된다.
이때 넉넉하게 길이가 1000인 배열을 사용했는데, 예상보다 이벤트 참여자가 많아서 1000명을 넘게된다면 더 많은 사용자가
이벤트에 참여하지 못하는 문제가 발생한다. 그렇다고 처음부터 너무 많은 배열을 확보하면 메모리가 많이 낭비된다.

배열처럼 처음부터 정적으로 길이가 정해져있는 것이 아니라, 동적으로 언제든지 길이를 늘리고 줄일 수 있는 자료구조가 있다면 편리할 것이다.

## 직접 구현하는 배열 리스트1 - 시작
배열의 경우 다음 2가지 불편함이 있다.
- 배열의 길이를 동적으로 변경할 수 없다.
- 데이터를 추가하기 불편하다.
  - 데이터를 추가하는 경우 직접 오른쪽으로 한 칸씩 데이터를 밀어야 한다. (이런 코드를 직접 작성해야 한다.)

배열의 이런 불편함을 해소하고 동적으로 데이터를 추가할 수 있는 자료구조를 List(리스트)라고 한다.

### List 자료 구조
순서가 있고, 중복을 허용하는 자료 구조를 리스트라고 한다.

일반적으로 배열과 리스트는 구분해서 이야기한다. 리스트는 배열보다 유연한 자료구조로, 크기가 동적으로 변할 수 있다.

|     | 설명                                 |
|-----|------------------------------------|
| 배열  | 순서가 있고 중복을 허용하지만 크기가 정적으로 고정된다.    |
| 리스트 | 순서가 있고 중복을 허용하지만 크기가 동적으로 변할 수 있다. |

여기서 중복을 허용한다는 뜻은 같은 데이터를 입력할 수 있다는 것이다.
예를 들어서 `arr[0] = 1`, `arr[1] = 1`은 하나의 배열에 같은 숫자 `1`이 입력되었다.
이것이 중복을 허용한다는 뜻이다. 자료 구조 중에는 중복을 허용하지 않는 자료구조도 존재한다.

### [MyArrayListV1.java](..%2Fsrc%2Fcollection%2Farray%2FMyArrayListV1.java)
```java
public class MyArrayListV1 {

    private static final int DEFAULT_CAPACITY = 5;

    private Object[] elementData;

    private int size = 0;

    public MyArrayListV1() {
        elementData = new Object[DEFAULT_CAPACITY];
    }

    public MyArrayListV1(int initialCapacity) {
        elementData = new Object[initialCapacity];
    }

    public int size() {
        return size;
    }

    public void add(Object e) {
        elementData[size] = e;
        size++;
    }

    public Object get(int index) {
        return elementData[index];
    }

    public Object set(int index, Object element) {
        Object oldValue = get(index);
        elementData[index] = element;
        return oldValue;
    }

    public int indexOf(Object o) {
        for (int i = 0; i < size; i++) {
            if (o.equals(elementData[i])) {
                return i;
            }
        }

        return -1;
    }

    @Override
    public String toString() {
        return Arrays.toString(Arrays.copyOf(elementData, size)) + " size=" +
                size + ", capacity=" + elementData.length;
    }
}
```

| 멤버 변수 또는 메서드                       | 설명                                                                                                                                                    |
|------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Object[] elementData`             | 다양한 타입의 데이터를 보관하기 위해 `Object` 배열을 사용한다.                                                                                                               |
| `DEFAULT_CAPACITY`                 | 리스트(`MyArrayListV1`)를 생성할 때 사용하는 기본 배열의 크기                                                                                                            |
| `size`                             | 리스트의 크기는 `size`를 사용한다. 리스트를 표현하기 위해 내부에서 배열을 사용할 뿐이다. 배열의 크기를 뜻하는 `capacity`와 다르다는 점에 주의하자. 예를 들어서 배열의 크기가 `5` 인데, 입력된 데이터가 하나도 없으면 `size`는 `0` 이 된다. |
| `add(Object e)`                    | 리스트에 데이터를 추가한다. 데이터를 추가하면 `size`가 하나 증가한다.                                                                                                            |
| `get(index)`                       | 인덱스에 있는 항목을 조회한다.                                                                                                                                     |
| `set(index, element)`              | 인덱스에 있는 항목을 변경한다.                                                                                                                                     |
| `indexOf(Object o)`                | 검색 기능이다. 리스트를 순차 탐색해서 인수와 같은 데이터가 있는 인덱스의 위치를 반환한다. 데이터가 없으면 `-1`을 반환한다.                                                                              |
| `Arrays.copyOf(elementData, size)` | `size` 크기의 배열을 새로 만든다. 여기서는 `toString()` 출력시 `size` 이후의 의미 없는 값을 출력하지 않기 위해 사용한다.                                                                     |
### [MyArrayListV1Main.java](..%2Fsrc%2Fcollection%2Farray%2FMyArrayListV1Main.java)
```java
public class MyArrayListV1Main {

    public static void main(String[] args) {
        MyArrayListV1 list = new MyArrayListV1();
        System.out.println("==데이터 추가==");
        System.out.println(list);
        list.add("a");
        System.out.println(list);
        list.add("b");
        System.out.println(list);
        list.add("c");
        System.out.println(list);

        System.out.println("==기능 사용==");
        System.out.println("list.size() = " + list.size());
        System.out.println("list.get(1) = " + list.get(1));
        System.out.println("list.indexOf(c) = " + list.indexOf("c"));
        System.out.println("list.set(2, z) = " + list.set(2, "z"));
        System.out.println(list);

        System.out.println("==범위 초과==");
        list.add("d");
        System.out.println(list);
        list.add("e");
        System.out.println(list);

        // 범위 초과, capacity가 늘어나지 않으면 예외 발생
        list.add("f");
        System.out.println(list);

    }
}
```

#### 실행 결과
```text
==데이터 추가==
[] size=0, capacity=5
[a] size=1, capacity=5
[a, b] size=2, capacity=5
[a, b, c] size=3, capacity=5
==기능 사용==
list.size() = 3
list.get(1) = b
list.indexOf(c) = 2
list.set(2, z) = c
[a, b, z] size=3, capacity=5
==범위 초과==
[a, b, z, d] size=4, capacity=5
[a, b, z, d, e] size=5, capacity=5
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: Index 5 out of bounds for length 5
	at collection.array.MyArrayListV1.add(MyArrayListV1.java:26)
	at collection.array.MyArrayListV1Main.main(MyArrayListV1Main.java:30)
```



## 직접 구현하는 배열 리스트2 - 동적 배열
## 직접 구현하는 배열 리스트3 - 기능 추가
## 직접 구현하는 배열 리스트4 - 제네릭1
## 직접 구현하는 배열 리스트5 - 제네릭2
## 정리