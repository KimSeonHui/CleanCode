# 5장 형식 맞추기
>프로그래머라면 형식을 깔끔하게 맞춰 코드를 짜야 한다.

----

## 형식을 맞추는 목적💡
- 코드 형식은 의사소통의 일환
- 의사소통은 전문 개발자의 일차적인 의무

코드의 스타일과 가독성 수준은 유지보수 용이성과 확장성에 계속 영향을 미치기 때문에 코드 형식을 맞춰 가독성을 높이는 것이 중요!

## 적절한 행 길이를 유지하라📏
일반적으로 큰 파일보다 작은 파일이 이해하기 쉽다.

큰 프로젝트들도 200줄 정도의 파일로 이루어진 것들도 있다.

### 신문 기사처럼 작성하라
- 이름은 간단하면서도 설명이 가능하게 짓는다
- 이름만 보고도 올바른 모듈을 살펴보고 있는지 아닌지를 판단 할 정도로 신경써서 짓는다
- 소스 파일 첫 부분은 고차원 개념과 알고리즘을 설명한다
- 아래로 내려갈수록 의도를 세세하게 묘사한다.
- 마지막에는 가장 저차원 함수와 세부 내역이 나온다.

### 개념은 빈 행으로 분리하라
빈 행(줄 바꿈)

- 새로운 개념을 시작한다는 단서
- 개념을 분리해주는 역할

```
pakage fitnesse.wikitext.widgets;

import java.util.regex.*;

public class BlodWidget extends ParentWidget {
  public static final String REGEXP = "'''.+?'''";
  private static final Pattern pattern = Pattern.compile("'''
  (.+?)'''", Pattern.MULTILNIE + Pattern.DOTALL
  );
  
public BoldWidget(ParentWidget parent, String text) throws
                                                  Execption
  super(parent);
  Matcher match = pattern.matcher(text);
  match.find();
  addChildWidgets(match.group(1));
  }
  ```
  
이 코드에서 사이사이 빈 행을 빼버리면 가독성이 훨씬 떨어진다.
```
pakage fitnesse.wikitext.widgets;
import java.util.regex.*;
public class BlodWidget extends ParentWidget {
  public static final String REGEXP = "'''.+?'''";
  private static final Pattern pattern = Pattern.compile("'''
  (.+?)'''", Pattern.MULTILNIE + Pattern.DOTALL
  );  
public BoldWidget(ParentWidget parent, String text) throws
                                                  Execption
  super(parent);
  Matcher match = pattern.matcher(text);
  match.find();
  addChildWidgets(match.group(1));
  }
```

### 세로 밀집도

- 연관성을 의미 
- 서로 밀집한 코드 행은 세로로 가까이 놓여야 한다.

### 수직 거리
서로 밀접한 개념은 세로로 가까위 둬야 한다.
 밀접한 두 개념은 세로 거리로 연관성을 표현한다.
 
 연관성은 한 개념을 이해하는 데 다른 개념이 중요한 정도, 연관성이 깊은 두 개념이 멀리 떨어져 있으면 코드를 읽는 사람이 소스 파일과 클래스를 여기저기 뒤지는 일이 일어나게 됨
 
- **변수 선언** : 변수는 사용하는 위치에 최대한 가까이 선언한다.
  + 루프를 제어하는 변수는 흔히 루프 문 내부에 선언
  

- **인스턴스 변수** : 클래스 맨 처음에 선언, 변수 간에 서로로 거리르 두지 않음
  + C++ : 클래스 마지막에 선언, 자바 : 클래스 맨 처음에 선언
  + 어느 쪽에 선언하느냐 보다 잘 알려진 위치에 인스턴스 변수를 모아서 변수 선언을 어디서 찾을지를 모두가 알고 있는 것이 중요하다
  

- **종속 함수** : 한 함수가 다른 함수를 호출한다면 두 함수는 세로 가까이 배치
   + 호출하는 함수를 호출되는 함수보다 먼저 배치
  

- **개념적 유사성** : 친화도가 높을수록 코드를 가까이 배치
  + 한 함수가 다른 함수를 호출할 때
  + 변수와 그 변수를 사용하는 함수
  + 비슷한 동작을 수행하는 일군의 함수
  
### 세로 순서
- 호출되는 함수를 호출하는 함수보다 나중에 배치
- 가장 중요한 개념을 가장 먼저 표현
- 가장 중요한 개념을 표현할 때 세세한 사항을 최대한 배제
- 세세한 사항은 가장 마지막에 표현

## 가로 형식 맞추기💁‍♂️💁‍♀️
한 행은 가로로 얼마나 길어야 적당할까? 
>"프로그래머는 명백하게 짧은 행을 선호한다. 그러므로 짧은 행이 바람직하다"

### 가로 공백과 밀집도
가로 공백
- 밀접한 개념, 느슨한 개념 표현
- ex)
```
private void measuerLine(String line) {
  lineCount++;
  int lineSize = line.length();
  totalChars += lineSize;
  lineWidthHistogram.addLine(lineSize, lineCount);
  recordWidestLine(lineSize);
}
```
할당문은 왼쪽 요소와 오른쪽 요소가 분명히 나뉘기 때문에 공백을 넣으면 두 가지 요소가 확실히 나뉜다는 사실이 분명해진다.

함수와 인수는 서로 밀접하기 때문에 함수 이름과 이어지는 괄호 사이에는 공백을 넣지 않는다.

### 가로 정렬
```
public class FitNesseExpediter implements RsponseSender {
  private  Soket          soket;
  private  InputStream    input;
  private  OutputStream   output;
  ...
```
코드가 엉뚱한 부분을 강조에 진짜 의도가 가려지기 때문에 위와 같은 정렬이 별로 유용하지 않음 정렬이 필요할 정도로 목록이 길다면 문제는 목록 길이지 정렬 부족이 아니다. 

### 들여쓰기
 범위로 이뤄진 계층을 표현
 프로그래머는 들여쓰기 체계에 크게 의존함
 왼쪽으로 코드를 맞춰 코드가 속하는 범위를 시각적으로 표현
 들여쓰기 한 파일은 구조가 한 눈에 들어옴
 
 - **들여쓰기 무시하기**
 간단한 if문, 짧은 while문, 짧은 함수에서 들여쓰기 규칙을 무시하고 싶을 때도 꼭 들여쓰기를 넣어주는 것이 좋음
 

 ```
 public CommentWidget(ParentWidget parent, String text){super(parent, text)};
 public String render() throws Exception {return "";}
 ```
 보다 다음과 같이 표현 해주는 것이 좋다
 ```
 public CommentWidget(ParentWidget parent, String text) {
   super(parent, text);
 }
 
 public String render() throws Exception {
   return "";
}
```

### 가짜 범위
때로 빈 while문이나 for문을 접할 때 

- 가능한 피하려 한다
-  피하지 못할 때는 빈 블록을 올바로 들여쓰고 괄호로 감싼다
- while문 끝에 ;이 있으면 눈에 띄지 않기 때문에 새 행에다가 들여써준다
```
while (dis.read(buf, 0, readBufferSize) != -1)
;
```

## 팀 규칙👨‍👨‍👧
프로그래머라면 각자 선호하는 규칙이 있다. 하지만 **팀에 속한다면 자신이 선호해야 할 규칙은 바로 팀 규칙이다.**

팀은 한 가지 규칙에 합의해야 하며 모든 팀원은 그 규칙을 따라야 한다. 그래야 소프트웨어가 일관적인 스타일을 보인다.

>"좋은 소프트웨어 시스템은 읽기 쉬운 문서로 이뤄진다는 사실을 기억하기 바란다"

----

## 느낀점🙊
코드를 어떻게 짜야 하는지에 대한 형식적인 부분을 이야기 한다. 사실 처음에 제목을 봤을 때 이 부분이 힘들지 않을까 하는 생각을 했다... 나는 형식적인 틀에 맞춰서 뭔가를 하는 걸 되게 되게 힘들어 하는 스타일이라서...

막상 읽어가다 보니 프로그램에서 말하는 형식이란 **"어떻게 더 읽기 쉽게, 다른 사람이 보기 쉽게 짜는가?"**에 대한 이야기였다. 지금 5장까지 읽어오고 있는데 계속해서 느껴지는 건 '나 혼자 코드를 짜는 게 아니다.'라는 것을 계속 말하고 있는 것 같다.

팀 규칙에서도 말했듯이 "팀에 속한다면 자신이 선호해야 할 규칙은 바로 팀 규칙이다." 같이 글을 쓰고 글을 읽는 사람들이 있기 때문에 팀은 어떻게 글을 쓸 지를 규칙을 정한다. 그래야 다른 사람이 글을 읽을 때 이해하기가 쉽기 때문에. 규칙을 어긴 사람이 있다면 그 사람이 쓴 글은 이해하기 어려워질테니까.

그래서 팀으로 일 할 때 함께 하는 사람이 읽기 쉽게 코드를 짜야겠다는 생각이 들었다. '졸작 팀플에서 다른 개발자가 좀 더 쉽게 읽을 수 있게 짜는 건 어떻게 짜는 걸까? 이거 괜찮나?'를 고민하기 시작했다. 

지금은 졸작도 시작단계라서 크게 개발이 진행된게 많지는 않지만 점점 완성되어 갈수록 코드 양도 늘어나고 작업량도 많아질텐데 나중을 생각해서 하나하나 신경써서 짜야겠다는 생각이든다

>코드는 읽기 쉽게! 나만이 아니라 다른 사람도!