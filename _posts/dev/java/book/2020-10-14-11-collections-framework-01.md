---
layout: post
date: 2020-10-14 12:02:00
title: "컬렉션 프레임웍 1편"
description: "자바의 정석"
subject: java의 정석
category: [ java ]
tags: [ java, List, Stack, Queue ]
comments: true
---

# 컬렉션 프레임웍

> 이 글은 남궁성님의 [자바의 정석 3/e](http://www.kyobobook.co.kr/product/detailViewKor.laf?mallGb=KOR&ejkGb=KOR&barcode=9788994492032)을 기반으로 공부한 내용을 정리한 글입니다.

+ [컬렉션 프레임웍](#컬렉션-프레임웍-Collections-Framework)

## 컬렉션 프레임웍 Collections Framework

컬렉션 프레임웍이란, '데이터 군을 저장하는 클래스들을 표준화한 설계'를 뜻한다. 컬렉션은 데이터 그룹, 프레임웍은 표준화된 프로그래밍 방식을 의미한다.

### 1.1 컬렉션 프레임웍의 핵심 인터페이스

컬렉션 프레임웍에서는 컬렉션데이터 그룹을 크게 3가지 타입이 존재한다고 인식하고 각 컬렉션을 다루는데 필요한 기능을 가진 3개의 인터페이스를 정의하였다. 그리고 인터페이스 `List`와 `Set`의 공통된 부분을 다시 뽑아서 새로운 인터페이스 `Collection`을 추가로 정의하였다.

<table>
  <tr>
    <td><center> 인터페이스 </center></td>
    <td><center> 특 징 </center></td>
  </tr>
  <tr>
    <td rowspan=2><center> List </center></td>
    <td> 순서가 있는 데이터의 집합. 데이터의 중복을 허용한다.<br/>
    예) 대기자 명단 </td>
  </tr>
  <tr>
    <td> 구현클래스 : ArrayList, LinkedList, Stack, Vector 등 </td>
  </tr>
  <tr>
    <td rowspan=2><center> Set </center></td>
    <td> 순서를 유지하지 않는 데이터의 집합. 데이터의 중복을 허용하지 않는다.<br/>
    예) 양의 정수집합, 소수의 집합 </td>
  </tr>
  <tr>
    <td> 구현클래스 : HashSet, TreeSet 등 </td>
  </tr>
  <tr>
    <td rowspan=2><center> Map </center></td>
    <td> 키(key)와 값(value)의 쌍(pair)으로 이루어진 데이터의 집합<br/>
     순서는 유지되지 않으며, 키는 중복을 허용하지 않고, 값은 중복을 허용한다.<br/>
     예) 우편번호, 지역번호(전화번호) </td>
  </tr>
  <tr>
    <td> 구현클래스 : HashMap, TreeMap, Hashtable, Properties 등 </td>
  </tr>
</table>

<br/>
<span style="font-size:13px;">
<b>| 참고 | 키(key)란, 데이터 집합 중에서 어떤 값(value)을 찾는데 열쇠(key)가 된다는 의미에서 붙여진 이름이다. 그래서 중복을 허용하지 않는다.</b><br/>
</span>  

컬렉션 프레임웍의 모든 컬렉션 리스트들은 `List`, `Set`, `Map` 중의 하나를 구현하고 있으며, 구현한 인터페이스의 이름이 클래스의 이름에 포함되어 있어서 이름만으로도 클래스의 특징을 쉽게 알 수 있도록 되어있다.

`Vector`, `Stack`, `Hashtable`, `Properties`와 같은 클래스들은 컬렉션 프레임웍이 만들어지기 이전부터 존재하던 것이기 때문에 컬렉션 프레임웍의 명명법을 따르지 않는다. 새로 추가된 `ArrayList`나 `HashMap`을 사용하는 것이 좋다.

<p style="color:#a0adec"><b>Collection 인터페이스</b></p>

`List`와 `Set`의 조상인 `Collection`인터페이스는 컬렉션 클래스에 저장된 데이터를 읽고, 추가하고 삭제하는 등 컬렉션을 다루는데 가장 기본적인 메서드들을 정의하고 있다.

반환 타입이 boolean인 메서드들은 작업을 성공하거나 사실이면 true, 그렇지 않으면 false를 반환한다.

<p style="color:#a0adec"><b>List 인터페이스</b></p>

`List`인터페이스는 중복을 허용하면서 저장순서가 유지되는 컬렉션을 구현하는데 사용된다.

<p style="color:#a0adec"><b>Set 인터페이스</b></p>

`Set`인터페이스는 중복을 허용하지 않고 저장순서가 유지되지 않는 컬렉션 클래스를 구현하는데 사용된다. `Set`인터페이스를 구현한 클래스로는 `HashSet`, `TreeSet` 등이 있다.

<p style="color:#a0adec"><b>Map 인터페이스</b></p>

`Map`인터페이스는 키(key)와 값(value)을 하나의 쌍으로 묶어서 저장하는 컬렉션 클래스를 구현하는데 사용된다. 키는 중복될 수 없지만 값은 중복을 허용한다. 기존에 저장된 데이터와 중복된 키와 값을 저장하면 기존의 값은 없어지고 마지막에 저장된 값이 남게된다. `Map`인터페이스를 구현한 클래스로는 `Hashtable`, `HashMap`, `LinkedHashMap`, `SortedMap`, `TreeMap` 등이 있다.

<span style="font-size:13px;">
<b>| 참고 | Map이란 개념은 어떤 두 값을 연결한다는 의미에서 붙여진 이름이다.</b><br/>
</span>

`Map`인터페이스의 메서드 중 `values()`에서는 반환타입이 Collection이고, `keySet()`에서는 반환타입이 Set이다. 값은 중복을 허용하기 때문에 Collection타입으로 반환하고, 키는 중복을 허용하지 않기 때문에 Set타입으로 반환한다.

<p style="color:#a0adec"><b>Map.Entry 인터페이스</b></p>

`Map.Entry`인터페이스는 `Map`인터페이스의 내부 인터페이스이다. 인터페이스도 내부 클래스와 같이 인터페이스 안에 인터페이스를 정의하는 내부 인터페이스(inner interface)를 정의할 수 있다.

<span style="font-size:13px;">
<b>| 참고 | 각 인터페이스의 메서드는 Java API 공식문서를 참고.</b><br/>
</span>

### 1.2 ArrayList

`ArrayList`는 List인터페이스를 구현하기 때문에 데이터의 저장순서가 유지되고 중복을 허용한다는 특징을 갖는다. 기존의 `Vector`를 개선한 것으로 구현원리와 기능적인 측면에서 동일하다고 할 수 있다.

`ArrayList`는 `Object`배열을 이용해서 데이터를 순차적으로 저장한다. 배열에 순서대로 저장되며, 배열에 더 이상 저장할 공간이 없으면 더 큰 배열을 생성해서 기존 배열의 내용을 복사한 다음 저장한다.

```java
  import java.util.*;

  class ArrayListEx {
    public static void main(String[] args) {
      ArrayList list1 = new ArrayList(10);
      list1.add(new Integer(5));
      list1.add(new Integer(4));
      list1.add(new Integer(2));
      list1.add(new Integer(0));
      list1.add(new Integer(1));
      list1.add(new Integer(3));

      ArrayList list2 = new ArrayList(list1.subList(1, 4));
      print(list1, list2);

      Collection.sort(list1);
      Collection.sort(list2);
      print(list1, list2);

      System.out.println("list1.containsAll(list2) : " + list1.containsAll(list2));

      list2.add("B");
      list2.add("C");
      list2.add(3, "A");
      print(list1, list2);

      list2.set(3, "AA");
      print(list1, list2);

      System.out.println("list1.retainAll(list2) : " + list1.retainAll(list2));

      print(list1, list2);

      for(int i = list2.size() - 1; i >= 0; i--) {
        if(list1.contains(list2.get(i)))
          list2.remove(i);
      }
      print(list1, list2);
    }

    static void print(ArrayList list1, ArrayList list2) {
      System.out.println("list1 : " + list1);
      System.out.println("list2 : " + list2);
      System.out.println();
    }
  }
```

&#9660; 실행결과

```
  list1 : [5, 4, 2, 0, 1, 3]
  list2 : [4, 2, 0]

  list1 : [0, 1, 2, 3, 4, 5] // Collections.sort()로 정렬됨
  list2 : [0, 2, 4]

  list1.containsAll(list2) : true // list1이 list2의 모든 요소를 포함하고 있을 때 true
  list1 : [0, 1, 2, 3, 4, 5]
  list2 : [0, 2, 4, A, B, C] // add(Object obj)로 새로운 객체가 저장됨

  list1 : [0, 1, 2, 3, 4, 5]
  list2 : [0, 2, 4, AA, B, C] // set(int idx, Object obj)를 이용해서 객체 변경

  list1.retainAll(list2) : true // retainAll에 의해 list1에 변화가 있었으므로 true
  list1 : [0, 2, 4] // list2와 공통요소만 남기고 나머지는 삭제됨
  list2 : [0, 2, 4, AA, B, C]

  list1 : [0, 2, 4]
  list2 : [AA, B, C]
```

`ArrayList`의 기본적인 메서드를 이용해 객체를 다루는 예제로 저장된 순서를 유지한다는 것을 알 수 있다.

`ArrayList`를 생성할 때, 저장할 요소의 개수를 고려해서 실제 저장할 개수보다 약간 여유있는 크기로 하는 것이 좋다. 지정한 크기보다 더 많은 객체를 저장하면 자동적으로 크기가 늘어나기는 하지만 이 과정에서 처리시간이 많이 소요되기 때문이다.

### 1.3 LinkedList

배열은 구조가 간단하고 데이터를 읽는 시간이 가장 빠르다는 장점이 있지만 다음과 같은 단점도 가지고 있다.

<table style="width:100%; background-color:#3a3c42; border:0; margin-bottom:16px;">
  <tr style="border:0">
    <td style="border:0; padding:14px; padding-left:32px; padding-right:32px; font-size:14px; color:white">
      <b>1. 크기를 변경할 수 없다. </b><br/>
      &nbsp;&nbsp;&nbsp;&nbsp; - 크기를 변경할 수 없으므로 새로운 배열을 생성해 데이터를 복사해야 한다.<br/>
      &nbsp;&nbsp;&nbsp;&nbsp; - 실행속도 향상을 위해서는 충분히 큰 크기의 배열을 생성해야 하므로 메모리가 낭비된다.<br/>
      <b>2. 비순차적인 데이터의 추가 또는 삭제에 시간이 많이 걸린다. </b><br/>
      &nbsp;&nbsp;&nbsp;&nbsp; - 차례대로 데이터를 추가하고 마지막에서부터 삭제하는 것은 빠르지만,<br/>
      &nbsp;&nbsp;&nbsp;&nbsp; - 배열의 중간에 데이터를 추가하려면, 빈자리를 만들기 위해 다른 데이터들을 복사해서 이동해야 한다.
    </td>
  </tr>   
</table>

이러한 배열의 단점을 보완하기 위해서 링크드 리스트(linked list)라는 자료구조가 고안되었다. 배열은 모든 데이터가 연속적으로 존재하지만 링크드 리스트는 불연속적으로 존재하는 데이터를 서로 연결(link)한 형태로 구성되어 있다.

링크드 리스트의 각 요소(node)들은 자신과 연결된 다음 요소에 대한 참조(주소값)와 데이터로 구성되어 있다.

```JAVA
  class Node {
    Node next; // 다음 요소의 주소를 저장
    Object obj; // 데이터를 저장
  }
```

링크드 리스트에서의 데이터 삭제는 삭제하고자 하는 요소의 이전요소가 삭제하고자 하는 요소의 다음(next) 요소를 참조하도록 변경하면 된다. 하나의 참조만 변경하면 삭제가 이루어지는 것이다.

새로운 데이터를 추가할 때는 새로운 요소를 생성한 다음 추가하고자 하는 위치의 이전 요소의 참조를 새로운 요소에 대한 참조로 변경하고, 새로운 요소가 다음 요소를 참조하도록 변경하면 된다.

링크드 리스트는 이동방향이 단방향이기 때문에 다음 요소에 대한 접근은 쉽지만 이전요소에 대한 접근은 어렵다. 이를 보완한 것이 더블 링크드 리스트(이중 연결 리스트, doubly linked list)이다.

더블 링크드 리스트는 참조변수 하나를 추가하여 이전 요소에 대한 참조가 가능하도록 했을 뿐, 그 외에는 링크드 리스트와 같다.

```JAVA
  class Node {
    Node next;
    Node previous;
    Object obj;
  }
```

실제로 `LinkedList`클래스는 '링크드 리스트'가 아닌 '더블 링크드 리스트'로 구현되어 있는데, 이는 링크드 리스트의 단점인 낮은 접근성(accessability)을 높이기 위한 것이다.

`LinkedList` 역시 `List`인터페이스를 구현했기 때문에 `ArrayList`와 내부구현방법만 다를뿐 제공하는 메서드의 종류와 기능은 거의 같다. 둘을 비교했을 때 장단점은 다음과 같다.

<table style="width:100%; background-color:#3a3c42; border:0; margin-bottom:16px;">
  <tr style="border:0">
    <td style="border:0; padding:14px; padding-left:32px; padding-right:32px; font-size:14px; color:white">
      <b>1. 순차적으로 추가/삭제하는 경우에는 ArrayList가 LinkedList보다 빠르다.</b><br/>
      &nbsp;&nbsp;&nbsp;&nbsp; ArrayList의 초기용량을 충분히 확보한 상태에서, 단순히 저장하는 시간만 비교했을 때의 결과이다.<br/>
      &nbsp;&nbsp;&nbsp;&nbsp; 만일 충분한 크기가 아니라면, 새로운 크기의 ArrayList를 생성하고 데이터를 복사하는 일이 발생하므로 LinkedList가 더 빠를 수 있다.<br/>
      &nbsp;&nbsp;&nbsp;&nbsp; 순차적인 삭제는 마지막 데이터부터 역순으로 삭제해나간다는 것을 의미하므로, 마지막 요소의 값을 null로 바꾸는 ArrayList가 빠르다.<br/>
      <b>2. 중간 데이터를 추가/삭제하는 경우에는 LinkedList가 ArrayList보다 빠르다.</b><br/>
      &nbsp;&nbsp;&nbsp;&nbsp; 요소간의 연결만 변경해주면 되는 LinkedList가 빠르다.
    </td>
  </tr>   
</table>

배열은 각 요소들이 연속적으로 메모리상에 존재하기 때문에 간단한 계산만으로 원하는 요소의 주소를 얻어서 저장된 데이터를 곧바로 읽어올 수 있지만, LinkedList는 불연속적으로 위치한 각 요소들이 서로 연결된 것이라 처음부터 차례대로 따라가야만 원하는 값을 얻을 수 있다.

그래서 LinkedList는 저장해야하는 데이터의 개수가 많아질수록 데이터를 읽어 오는 시간, 접근시간(access time)이 길어진다는 단점이 있다.

|<center> 컬렉션|<center> 읽기(접근시간)|<center> 추가/삭제|<center> 장/단점|
|:---|:---:|:---:|:---|
|ArrayList|빠르다|느리다|순차적인 추가삭제는 더 빠름.<br/> 비효율적인 메모리사용.|
|LinkedList|느리다|빠르다|데이터가 많을수록 접근성이 떨어짐.|

<br/>
두 클래스의 장점을 이용해 조합해서 사용하는 방법도 있다. 컬렉션 프레임웍에 속한 대부분의 컬렉션 클래스들은 서로 변환이 가능한 생성자를 제공하므로 이를 이용해 간단히 데이터를 옮길 수 있다.

### 1.4 Stack과 Queue

스택(Stack)은 LIFO(후입선출, Last In First Out)구조로 마지막에 들어간 데이터가 가장 먼저 나온다. 쉽게 말해 한 쪽이 막힌 원통을 생각하면 된다.

큐(Queue)는 FIFO(선입선출, First In First Out)구조로 처음 들어간 데이터가 먼저 나오는데, 막히지 않은 원통을 생각하면 된다.

순차적으로 데이터를 추가하고 삭제하는 `Stack`에는 `ArrayList`와 같은 배열기반의 컬렉션 클래스가 적합하지만, `Queue`의 경우 데이터를 꺼내면 항상 첫번째 데이터가 삭제되므로 배열기반의 컬렉션 클래스를 사용할 경우 빈 공간을 채우기 위해 데이터의 복사가 발생하므로 비효율적이다. 따라서 `LinkedList`로 구현하는 편이 더 적합하다.

자바에서는 스택을 `Stack`클래스로 구현하여 제공하지만 큐는 `Queue`인터페이스로만 정의해 놓고 별도의 클래스는 제공하지 않는다. 대신 `Queue`인터페이스를 구현한 클래스들이 있어서 이 들 중의 하나를 선택해서 사용하면 된다.

<p style="color:#a0adec"><b>Stack 직접 구현하기</b></p>

`Vector`를 상속받아 구현된 `Stack` 코드이다.

```java
  import java.util.*;

  class Stack extends Vector {
    public Object push(Object item) {
      addElement(item);
      return item;
    }

    public Object pop() {
      Object obj = peek(); // 스택에 저장된 마지막 요소를 읽어온다.
      // 스택이 비어 있으면 peek() 메서드가 EmptyStackException을 발생시킨다.

      // 마지막 요소를 삭제한다.
      removeElementAt(size() - 1);
      return obj;
    }

    public Object peek() {
      int len = size();

      if(len == 0)
        throw new EmptyStackException();

      // 마지막 요소를 반환한다.
      return elementAt(len - 1);
    }

    public boolean empty() {
      return size() == 0;
    }

    public int search(Object o) {
      int i = lastIndexOf(o); // 끝에서부터 객체를 찾는다. 반환값은 저장된 위치(배열의 index)이다.

      if(i >= 0) { // 객체를 찾은 경우
        return size() - i;
      }

      return -1; // 객체를 찾지 못한 경우
    }
  }
```

<p style="color:#a0adec"><b>스택과 큐의 활용</b></p>

<table style="width:100%; background-color:#3a3c42; border:0; margin-bottom:16px;">
  <tr style="border:0">
    <td style="border:0; padding:14px; padding-left:32px; padding-right:32px; font-size:14px; color:white">
      <b>스택 활용 예</b><br/>
      &nbsp;&nbsp;&nbsp;&nbsp; - 수식계산, 수식괄호검사, 워드프로세서의 undo/redo, 웹브라우저의 뒤로/앞으로<br/>
      <b>큐 활용 예</b><br/>
      &nbsp;&nbsp;&nbsp;&nbsp; - 최근사용문서, 인쇄작업 대기목록, 버퍼(buffer)
    </td>
  </tr>   
</table>

스택을 활용해 웹브라우저의 페이지 이동 버튼(뒤로, 앞으로)을 구현한 코드이다.

```java
  import java.util.*;

  public class StackEx {
    public static Stack back = new Stack();
    public static Stack forward = new Stack();

    public static void main(String[] args) {
      goURL("1. 네이버")
      goURL("2. 다음")
      goURL("3. 구글")
      goURL("4. 네이트")

      printStatus();

      goBack();
      System.out.println("= 뒤로가기 버튼을 누른 후 =");
      printStatus();

      goBack();
      System.out.println("= '뒤로' 버튼을 누른 후 =");
      printStatus();

      goForward();
      System.out.println("= '앞으로' 버튼을 누른 후 =");
      printStatus();

      goURL("javatutorial.com");
      System.out.println("= 새로운 주소로 이동 후 =");
      printStatus();
    }

    public static void printStatus() {
      System.out.println("back : " + back);
      System.out.println("forward : " + forward);
      System.out.println("현재 화면은 '" + back.peek() + "' 입니다.");
      System.out.println();
    }

    public static void goURL(String url) {
      back.push(url);

      if(!forward.empty())
        forward.clear();
    }

    public static void goForward() {
      if(!forward.empty())
        back.push(forward.pop());
    }

    public static void goBack() {
      if(!back.empty())
        forward.push(back.pop());
    }
  }
```

유닉스의 명령어 중 입력한 명령어를 순서대로 보여주는 `history`명령어를 `Queue`를 이용해 구현한 코드이다.

```java
  import java.util.*;

  class QueueEx {
    static Queue que = new LinkedList();
    static final int MAX_SIZE = 5; // 최대 5개까지 저장되도록 한다.

    public static void main(String[] args) {
      System.out.println("help를 입력하면 도움말을 볼 수 있습니다.");

      while(true) {
        System.out.print(">>");
        try {
          // 화면으로부터 라인단위로 입력받는다.
          Scanner sc = new Scanner(System.in);
          String input = sc.nextLine().trim();

          if("".equals(input)) continue;

          if(input.equalsIgnoreCase("q")) {
            System.exit(0);
          } else if(input.equalsIgnoreCase("help")) {
            System.out.println(" help - 도움말을 보여줍니다. ");
            System.out.println(" q 또는 Q - 프로그램을 종료합니다. ");
            System.out.println(" history - 최근에 입력한 명령어를 " + MAX_SIZE + "개 보여줍니다.");
          } else if(input.equalsIgnoreCase("history")) {
            int i = 0;

            save(input); // 입력받은 명령어 저장

            // LinkedList의 내용을 보여준다.
            LinkedList tmp = (LinkedList)q;
            ListIterator it = tmp.listIterator();

            while(it.hasNext())
              System.out.println(++i + "." + it.next());
          } else {
            save(input);
            System.out.println(input);
          }
        } catch(Exception e) {
          System.out.println("입력오류입니다.");
        }
      }
    }

    public static void save(String input) {
      // queue에 저장한다.
      if(!"".equals(input))
        q.offer(input);

      // queue의 최대크기를 넘으면 제일 처음 입력된 것을 삭제한다.
      if(q.size() > MAX_SIZE) // size()는 Collection 인터페이스에 정의
        q.remove();
    }
  }
```

<p style="color:#a0adec"><b>PriorityQueue</b></p>

`Queue`인터페이스의 구현체 중의 하나로, 저장한 순에 관계없이 우선순위(priority)가 높은 것부터 꺼내게 되는 특징을 가지고 있다. 그리고 null을 저장할 수 없는데 null을 저장하면 NullPointerException이 발생한다.

`PriorityQueue`는 저장공간으로 배열을 사용하며, 각 요소를 `힙(heap)`이라는 자료구조의 형태로 저장한다.

```java
  import java.util.*;

  class PriorityQueueEx {
    public static void main(String[] args) {
      Queue pq = new PriorityQueue();
      pq.offer(3); // pq.offer(new Integer(3)); 오토박싱
      pq.offer(1);
      pq.offer(5);
      pq.offer(2);
      pq.offer(4);
      System.out.println(pq); // pq 내부 배열 출력

      Object obj = null;

      //PriorityQueue에 저장된 요소를 하나씩 꺼낸다.
      while((obj = pq.poll()) != null)
        System.out.println(obj);
    }
  }
```

저장순서는 3, 1, 5, 2, 4인데 출력결과는 1, 2, 3, 4, 5로 나온다. 숫자일 경우 우선순위가 오름차순을 기본으로 하기때문이다. 객체를 저장했을 때는 객체의 크기를 비교할 수 있는 방법을 제공해야 한다. Number의 자손들은 자체적으로 숫자를 비교하는 방법을 정의하고 있기 때문에 비교 방법을 지정해 주지 않아도 된다.

<p style="color:#a0adec"><b>Deque(Double-Ended Queue)</b></p>

`Queue`의 변형으로, 한 쪽 끝으로만 추가/삭제할 수 있는 큐와 달리, `Deque`(덱 또는 디큐)은 양쪽 끝에 추가/삭제가 가능하다. 덱의 조상은 큐이며, 구현체로는 `ArrayDeque`과 `LinkedList` 등이 있다.

덱은 스택과 큐를 하나로 합쳐놓은 것과 같으며 스택으로도 큐로도 사용할 수 있다.

[다음 편](/2020/java/11-collections-framework-02)

[위로](#컬렉션-프레임웍)
