# Clean Code 7장 오류처리
>오류 처리 코드로 인해 프로그램 논리를 이해하기 어려워진다면 깨끗한 코드라 부르기 어렵다.

----

## 오류 코드보다 예외를 활용하라❗
오류 코드를 사용하면 함수를 호출하는 즉시 오류를 확인해야 하기 때문에 호출자 코드가 복잡해진다. 그렇기 때문에 프로그램 논리와 오류 처리 코드가 구분되도록 예외를 던지는 것이 좋다

```
public void sendShutDown(){
  try {
    tryToShutDown();
    } catch (DeviceShutDownError e) {
      logger.log(e);
      }
    } 
    
public void tryShutDown() thorows DeviceShutDownError {
....
}

```

프로그램 논리를 처리하는 부분과 오류를 처리하는 부분이 분리가 되어 코드가 깔끔해진다. 그리고 각 개념을 독립적으로 살펴보고 이해할 수 있다.

## Try-Catch-Finally 문부터 작성하라.✅
try 블록에서 무슨 일이 생기든 catch 블록은 프로그램 상태를 일관성 있게 유지해야 한다. 그렇기 때문에 예외가 발생하는 코드를 짤 때는 try-cath-finally 문으로 시작하는 편이 좋다.

먼저 강제로 예외를 일으키는 테스트 케이스를 작성한 후 테스트를 통과하게 코드를 작성하는 방법을 권장한다. 그러면 try 블록에서 무슨 일이 생기든지 호출자가 기대한느 상태를 정의하기 쉬워진다. 

## 미확인 예외를 사용하라💫
하위 단계의 메서드에서 확인된 예외를 던지게 되면 함수의 선언부에 throws 절을 추가해야한다. 그러면 변경한 함수를 호출하는 함수가 모두 catch 블록에서 새로운 예외를 처리하거나, 선언부에 throw 절을 추가해야 한다. 
즉, 하위단계에서 최상위 단계까지 연쇄 수정이 있어야 하고 이는 OCP 규칙을 위반한다. 확인된 예외는 처리되거나 선언되어야 하지만 미확인 예외에는 적용되지 않는다. 

###### 확인된 예외 : 일반적으로 응용 프로그램이 처리 할 수 있어야하는 예상 이벤트 ex) IOEXCEPTION
###### 미확인 예외 : 일반적으로 응용 프로그램이 처리할 수 없는 예기치 않은 이벤트

## 예외에 의미를 제공하라💡
예외를 던질 때 전후 상황을 충분히 덧붙이면 오류가 발생한 원인과 위치를 찾기가 쉬워진다. 오류 메세지에 정보를 담아 예외와 함께 던진다.
ex) 실패한 연산 이름, 실패 유형

## 호출자를 고려해 예외 클래스를 정의하라📟
애플리케이션에서 오류를 정의할 때 프로그래머에게 가장 중요한 관심사는 **오류를 잡아내는 방법**이 되어야 한다.

```
LocalPort port = new LocalPort(12);
try{
  port.open();
  } catch (PortDeviceFailure e) {
    reportError(e);
    logger.log(e.getMessage(),e);
  } finally {
  ...
  }
  
  
public class LocalPort {
  private ACMEPort innerPort;
  
  public LocalPort(int portNumber){
    innerPort = new ACMEPort(portNumber);
    }
    
  public void open() {
    try{
      innerPort.open();
      } catch(DeviceResponseException e) {
        throw new PortDeviceFailure(e);
        } catch(ATM1212UnlockedException e) {
          throw new portDeviceFailure(e);
        } catch (GMXError e) {
          throw new ProtDeviceFailure(e);
        }
       }
       ...
     }
```

LocalPort 클래스는 ACMEPort를 감싼다. 외부 API를 감싸서 사용하믕로써 외부 라이브러리와 프로그램 사이에서 의존성을 줄인다. 또한 그렇게 함으로써 예외 유형 하나를 반환한다.

 - 예외 클래스에 포함된 정보로 오류를 구분해도 괜찮은 경우
    +  예외 클래스 하나로 충분

- 한 예외를 잡아내고 다른 예외는 무시해도 괜찮은 경우
   + 여러 예외 클래스 사용


## 정상흐름을 정의하라🔗
클라이언트 코드가 특수 상황을 처리하지 않게 하는 것이 더 유용할 때가 있다. 
특수 사례 패턴을 활용하여 처리한다. 특수 사례 패턴은 클래스를 만들거나 객체를 조작해 특수 사례를 처리하는 방식이다.

```
try { 
  MealExpenses expenses = 
  expenseReportDAO.getMeals(employee.getID());
  m_total += expenses.getTotal();
 } catch(MealExpensesNotFound e) {
   m_total += getMealPerDiem();
  }  
```
직원이 식사비를 청구하지 않았을 경우를 기본 식비를 총계에 더하는 방식으로 처리를 한다. 직원이 식사비를 청구하지 않았을 경우의 특수 상황을 클라이언트가 처리하게 하는 것이 아니라 expeonseReportDAO 클래스를 수정해 청구된 식사비가 없다면 기본 식비를 반환하는 MealExpense 객체를 반환하게 한다.

```
MealExpenses expenses = 
  expenseReportDAO.getMeals(employee.getID());
  m_total += expenses.getTotal();
  

public class PerDiemMealExpenses implements MealExpenses {
  public int getTotal() {
    //기본값으로 일일 기본 식비를 반환
    }
  }
  ```
  이 경우 클래스나 객체가 예외적인 상황을 캡슐화해서 처리하게 된다.
  
  ## null을 반환하지 마라🔗
null을 반환하는 코드는 null 확인을 하나라도 놓치게 되면 애플리케이션에 문제가 생기게 된다. null 확인이 누락되는 문제를 발생하는 코드의 진짜 문제는 null 확인이 너무 많은 것이다. 
  
>메서드에서 null을 반환하고픈 유혹이 든다면 그 대신 예외를 던지거나 특수 사례 객체를 반환하는 것이 좋다.

## null을 전달하지 마라🔗
정상적인 인수로 null을 기대하는 것이 아니라면 메서드로 null을 전달하는 코드는 최대한 피한다.

대다수 프로그래밍 언어는 호출자가 실수로 넘기는 null을 적절히 처리하는 방법이 없다. 그렇기에 애초에 null을 넘기지 못하도록 금지하는 정책이 합리적이다. 

## 결론📝
오류 처리를 프로그램 논리와 분리해 독자적인 사안으로 고려하면 튼튼하고 깨끗한 코드를 작성할 수 있다. 오류 처리를 프로그램 논리와 분리하면 독립적인 추론이 가능해지며 코드 유지보수성도 크게 높아진다.

----
## 느낀점🙊
이번 장은 많이 어렵게 느껴졌다. 자바를 배울 때 예외를 던지고 try-catch-finally 문을 사용하고 하는 것을 다 배웠다. 근데 지금까지 코드를 쓰면서 사용해본 적은 진짜 드문것 같다. 오히려 제일 처음에 나왔던 소제목인 '오류 코드 대신 예외를 사용하라'에서 나온 예제처럼 오류 코드를 써왔던 것 같다. 그래서 코드를 딱 보면 한눈에 프로그램과 논리가 구분되어 들어오기 보다는 코드를 읽어가면서 이 부분은 오류를 처리하는 부분이고, 이 부분이 프로그램 부분이고- 하면서 읽어갔던 것 같다. 

이번 장은 오류를 처리하는 방법에 대해서 더 코드를 깔끔하고 안정성 있게 만들 수 있는 방법을 주로 설명을 한다. 하지만 나는 읽으면서 '왜 오류 코드가 아니라 예외를 던지는 게 더 좋은 방법인가'에 집중해서 읽었던 것 같다. 그리고 수업 때 왜 예외를 던지고, try-catch-finally 문을 쓰고 하는지 어떻게 활용되는 지를 배웠다기 보다는 문법적인 것에 집중했다는 것도 반성하게 됐다.ㅠㅠ
