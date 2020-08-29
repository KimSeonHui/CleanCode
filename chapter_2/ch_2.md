## 2장 의미있는 이름

## 의도를 분명히 밝혀라
>"의도가 분명하게 이름을 지으라"고 말하기는 쉽다. **좋은 이름을 지으려면 시간이 걸리지만 좋은 이름으로 절약하는 시간이 훨씬 많다.**

변수, 함수, 클래스 이름은 존재 이유, 수행 기능, 사용 방법 등에 모두 답할 수 있는 이름이어야 한다. 따로 주석이 필요하다면 의도를 분명히 드러내지 못했다는 말이다.

**아무 의미도 드러나지 않은 예시**
```
int d; // 경과 시간(단위 : 날짜)
```

**의도가 드러나는 이름 예시**
```
int elapsedTimeInDays; // 측정하려는 값, 단위 표현
```


#### 의도가 드러나는 이름을 사용하면 코드 이해와 변경이 쉬워진다.
코드를 읽을 때 이해가 어려운 것은 코드의 **함축성** 때문이다.
코드의 맥락이 코드 자체에 명시적으로 드러나지 않는다.

```
public List<int[]> getThem() {
 List<int[]> list1 = new ArrayList<int[]>();
 
 for(int[] x : theList)
    if(x[0] == 4;
      list1.add(x);
      
 return list1;
 }
```

**이름 수정**
```
public List<int[]> getFlaggedCells() {
 List<int[]> flaggedCells = new ArrayList<int[]>();
 
 for(int[] cell : gameBoard)
   if(cell[STAUS_VALUE] == FLAGGED)
     flaggedCells.add(cell);
 
 return flaggedCells;
 }
```
코드에서 사용하는 이름을 바꾸는 것만으로 함수가 하는 일을 이해하기 쉬워진다.

## 그릇된 정보를 피하라
> "프로그래머는 코드에 그릇된 단서를 남겨서는 안 된다. 그릇된 단서는 코드 의미를 흘린다. 나름대로 널리 쓰이는 의미가 있는 단어를 다른 의미로 사용해도 안된다."

- 프로그래머에게 특수한 의미를 가진 단어를 다른 의미로 사용하지 않아야 함.
  + ex) hp, aix, sco
  + ex) 실제 List 형식이 아닌데 accountList로 이름만 붙이는 것

- 서로 흡사한 이름을 사용하지 않도록 해야함.
- 유사한 개념일 경우 유사한 표기법을 사용함.

## 의미 있게 구분하라
>"컴파일러나 인터프리터만 통과하려는 생각으로 코드를 구현하는 프로그래머는 스스로 문제를 일으킨다. ... 이름이 달라야 한다면 의미도 달라져야 한다."

```
getActiveAccount();
getActiveAccounts();
getActiveAccountInfo();
```
이 코드에서 어느 함수를 호출해야 고객 급여 이력을 찾을 수 있을까?.

**"읽는 사람이 차이를 알도록 이름을 지어라."**

## 발음하기 쉬운 이름을 사용하라
"단어는 발음이 가능하다. ... 그러므로 발음하기 쉬운 이름을 선택한다. 발음하기 어려운 단어는 토론하기도 어렵다."

```
class DtaRcrd102 {
  private Date genymdhms;
  private Date modymdhms;
  private final String pszqint = "102";
  /*...*/
  };
```

```
class Customer {
  private Date generateionTimestamp;
  private Date modificationTimestamp;
  private final String recordId = "102";
  /*...*/;
  };
```

## 검색하기 쉬운 이름을 사용하라
> **"이름 길이는 범위 크기에 비례해야 한다."

변수나 상수를 코드 여러 곳에서 사용한다면 검색하기 쉬운 이름이 바람직함.

- 문자 하나, 상수 사용하지 않고 의미 있는 긴 이름 사용

## 인코딩을 피하라
유형이나 범위 정보까지 인코등에 넣으면 그만큼 이름을 해독하기 어려워진다.

### 헝가리식 표기법
과거에는 컴파일러가 타입을 점검하지 않았기 때문에 프로그래머가 변수 타입을 기억할 단서가 필요했음.

지금은 이러한 방식이 변수, 함수, 클래스 이름이나 타입을 바꾸기 어려워지며 읽기도 어려워진다.

```
PhoneNumber phoneString; //타입이 바뀌어도 이름은 바뀌지 않음.

```

### 멤버 변수 접두어
 - 멤버 변수에 m_접두어 사용 x
 - 눈에 띄게 보여주는 IDE 사용
 
 
 ```
 public class Part {
    private String m_dsc; // 설명 문자열
    void setName(String name) {
       m_dsc = name;
   }
}  



```
public class Part {
   String description;
   void setDescription(String description) {
     this.description = description;
       }
   }
   
```


### 인터페이스 클래스와 구현 클래스
때로는 인코딩이 필요한 경우도 있음
 - 인터페이스, 구현 클래스의 이름을 지어야 할 때
   + 구현 클래스의 이름을 인코딩 함
   
## 자신의 기억력을 자랑하지 마라
>"독자가 코드를 읽으면서 변수 이름을 자신이 아는 이름으로 반환해야 한다면 그 변수 이름은 바람직하지 못하다. 이는 일반적으로 문제 영역이나 해법 영역에서 사용하지 않는 이름을 선택했기 때문에 생기는 문제다."

**남들이 이해하는 코드를 짜야한다.**

## 클래스 이름
 - 클래스 이름, 객체 이름 : 명사, 명사구 
 - 동사는 사용 하지 않음
   + 좋은 예시) Customer, Account, WikiPage...
   + 피해야 할 예시) Manager, Data, Info

## 메서드 이름
- 메서드 이름 : 동사, 동사구
  + 좋은 예시) postPayment, DeletePage, save ...
  

- 생성자를 중복정의 할 때는 정적 팩토리 메서드 사용

## 기발한 이름은 피하라
>"재미난 이름 보다는 명료한 이름을 선택하라. 의도를 솔직하고 분명하게 표현하라."

## 한 개념에 한 단어를 사용하라
>"추상적인 개념 하나에 단어 하나를 선택해 이를 고수한다. ... 메서드 이름은 독자적이고 일관적이어야 한다. ... 이름이 다르면 독자는 당연히 클래스도 다르고 타입도 다르리라 생각한다."

ex) 똑같은 메서드를 클래스마다 fetch, retrieve, get으로 부르면 혼란이 생김

## 말장난을 하지 마라
>"한 단어를 두 가지 목적으로 사용하지 마라. ... 프로그래머는 코드를 최대한 이해하기 쉽게 짜야 한다. 집중적인 탐구가 필요한 코드가 아니라 대충 훓터봐도 이해할 코드 작성이 목표다."

같은 개념은 같은 단어, 다른 개념에는 다른 단어를 사용한다.

## 해법 영역에서 가져온 이름을 사용하라
"코드를 읽을 사람도 프로그래머라는 사실을 명심한다. 그러므로 전산 용어, 알고리즘 이름, 패턴 이름, 수학 용어 등을 사용해도 괜찮다. ... 기술 개념에는 기술 이름이 가장 적합한 선택이다.

## 문제 영역에서 가져온 이름을 사용하라
"적절한 ' 프로그래머 용어'가 없다면 문제 영역에서 이름을 가져온다. ... 문제 영역 개념과 관련이 깊은 코드라면 문제 영역에서 이름을 가져와야 한다."

## 의미 있는 맥락을 추가하라
대다수 이름은 스스로 의미가 분명하지 않음으로 클래스, 함수, 이름 공간에 넣어 맥락을 부여한다. 이 때 의미가 분명할 수 있게 하는 맥락을 추가한다.

변수 number, verb, pluralModifier의 의미가 분명하지 않음
```
private void printGuessStatistics(char candidate, int count) {
  String number;
  String verb;
  String pluralModifier;
  
  if(count == 0) {
    number ="no";
    verb = "are";
    pluralModifier = "s";
    }
    else if(count == 1) {
    number = "1";
    verb = "is";
    pluralModifier = "";
    }
    else {
    number = Integer.toString(count);
    verb = "are";
    pluralModifier = "s";
    }
   
  String guessMessage = String.format("There %s %s %s%s", 
     verb, number,candiate, pluraModifier);
     
  print(guessMessage);
 
 }
```

의미가 분명해짐
```
public class GuessStatisticsMessage {
  private String number;
  private String verb;
  private String pluralModifier;
  
  public String make(char candidate, int count)  {
     cratePluralDependentMessageParts(count);
     return String.format("There %s %s %SS%S", verb, number,
       candidate, pluralModifier);
   }
   
   
   private void cratePluralDependentMesageParts(int count) {
   if(count == 0) {
     therAreNoLetters();
   } else if(count == 1) {
     thereIsOneLetter();
   } else {
     thereAreManyLetters(count);
   }
 } 
 
 private void thereAreManyLetters(int count) {
   number = Integer.toString(count);
   verb = "are";
   pluralModifier = "s";
 }
 
 private void thereIsOneLetter() {
   number = "1";
   verb = "is";
   pluralModifier = "";
 }
 
 private void thereAreNoLetters() {
   number = "no";
   verb = "are";
   pluralModifier = "s";
  }
} 
   
```
## 불필요한 맥락을 없애라
"일반적으로는 짧은 이름이 긴 이름보다 좋다. 단, 의미가 분명한 경우에 한해서다. 이름에 불필요한 맥락을 추가하지 않도록 주의한다."

## 느낀점
1장과 2장을 읽으면서 가장 크게 느꼈던 것은 코드를 짤 때는 **코드를 읽는 사람**을 생각 하면서 짜야 한다는 것이다. 최근에 졸업작품을 준비하면서 본격적인 개발에 들어가기 전에 같이 간단한 예제를 작업을 하게 되었다. 다른 사람이 만들어 놓은 코드에 내 분량을 덧붙이고 하다보니 제일 먼저 해야 할 일은 **코드를 읽는 일** 이었다. 일단 코드를 알아야 하니까!. 그래서 막상 첫번째 간단한 팀 프로젝트를 끝내고 보니까 내가 맡은 부분의 로직을 짜는 것보다 코드를 읽고 이해하는 데에 시간을 쏟았던 시간이 더 길었던 것 같다. 

이번 장은 의미있는 이름에 관한 내용이었는데 이 장을 읽으면서 내가 했던 프로젝트가 생각났다. 코드를 만들면서 '**전지적 개발자(나)**시점에서 코드를 짰구나' 하는 생각이 많이 들었다. 과연 이 코드를 봤을 때, 변수 이름만 보고도 무슨 일을 하는 건지 바로바로 알 수 있을가? 하는 생각이 들었다. 

