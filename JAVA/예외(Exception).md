## 예외(Exception)



### 👉 예외의 발생

```java
package exception;

public class ExceptionApp {

	public static void main(String[] args) {
		System.out.println(1);
		System.out.println(2/0);	// 예외 발생
		System.out.println(3);
		
	}

}	
```

> 📢 1	

<hr> 



### 👉 예외의 처리

```java
package exception;

public class ExceptionApp {

	public static void main(String[] args) {
		System.out.println(1);
		try {
			System.out.println(2/0);	// 예외 발생
		} catch(ArithmeticException e) {
			System.out.println("잘못된 계산이네요.");
		}
		System.out.println(3);
		
	}

}
```

> 📢	
>
> 1
> 잘못된 계산이네요.						// 예외가 발생한 부분을 try로 체크후 catch 출력
> 3

```java
package exception;

public class ExceptionApp {

	public static void main(String[] args) {
		System.out.println(1);
		int[] scores = {10,20,30};
		try {
			System.out.println(2);
			System.out.println(scores[3]);			//예외 발생
			System.out.println(3);
			System.out.println(2/0);				//예외 발생
			System.out.println(4);
		} catch(ArithmeticException e) {			//산수 예외처리
			System.out.println("잘못된 계산이네요.");
		} catch(ArrayIndexOutOfBoundsException e) {	//배열 예외처리
			System.out.println("없는 값을 찾고 계시네요 ^^");
		}
		System.out.println(5);
	}

}
```

> 📢
>
> 1											 
> 2											
> 없는 값을 찾고 계시네요 ^^ 			   ✔
> 5

✔ 존재 하지 않는 scores[3] 배열을 ArrayIndexOutOfBoundsException(배열 예외처리)을 사용하여 catch출력

* 예외 발생한 부분 이후 출력x 
* 이런 경우 다른 예외 또한 try/catch 사용해야함

<hr>



### 👉 예외의 우선순위

✔ 부모 Exception

1. Exception 	

✔자식 Exception 	 

1. ArithmeticException (산수 예외처리)

2. ArrayIndexOutOfBoundsException (배열 예외처리)

3. ....등

   

* 부모 Exception은 자식 Exception모두를 포괄함

* 부모 Exception사용시 자식 Exception 은 사용 못함
* catch문 순서에 따라 사용됨(먼저쓴 순서대로)

<hr>



### 👉 e 의 비밀

* 위 코드중 **try/catch** 을 보면 catch(Exception **`e`** ) 이 있다. 

* 이것중에 **`e`** 는 **data type**이 **exception**인 변수이다.
* **`e`** 를 활용한 예시로 **e.getMessage()** 을 사용하면 무엇 때문에 예외가 발생했는지 알려준다.
* **e.printStackTrace** 근원지를 찾아서 단계별로 에러를 출력
* **e.toString()** toString()을 호출해서 간단한 에러 메시지를 확인

<hr>



### 👉 ( checked vs unchecked ) exception

* Exception은 checked와 unchecked가 있다. 
* checked는 체크를 하지 않으면 컴파일 조차 되지 않지만  
* unchecked는 컴파일 실행이 가능하고 콘솔에서 예외 발생 시 표시를 해준다.

![checked_unchecked_exceptions](C:\Users\young\Desktop\삼성멀티캠퍼스\잡것\정리\JAVA\checked_unchecked_exceptions.png)

| 구분          | Checked Exception                    | UnChecked Exception               |
| ------------- | ------------------------------------ | --------------------------------- |
| 확인 시점     | 컴파일(Compile) 시점                 | 런타임(Runtime) 시점              |
| 처리 여부     | 반드시 예외 처리해야 한다            | 명시적으로 하지 않아도 된다.      |
| 트랜잭션 처리 | 예외 발생시 롤백(rollback) 하지 않음 | 예외 발생시 롤백(rollback) 해야함 |

<hr>



### 👉 finally

```java
import java.io.FileWriter;
import java.io.IOException;

public class CheckedExceptionApp {
    public static void main(String[] args) {
        FileWriter f = null;
        try {
            f = new FileWriter("data.txt");
            f.write("Hello");
        } catch(IOException e){
            e.printStackTrace();
        } finally {
            // 만약에 f가 null이 아니라면
            if(f != null) {
                try {
                    f.close();
                } catch(IOException e){
                    e.printStackTrace();
                }
            }
        }
    }
}
```

* 예외여부와 관계없이 실행이 된다.

* 예외와는 상관 없이 반드시 끝내줘야 하는 작업이 있을때 사용
* 예외를 사용하면 그 뒷부분이 작동을 안하기 때문에 

<hr>



### 👉 try-with-resources

```java
import java.io.FileWriter;
import java.io.IOException;
 
public class TryWithResource {
    public static void main(String[] args) {
        // try with resource statements
        try (FileWriter f = new FileWriter("data.txt")) {
            f.write("Hello");
        } catch(IOException e){
            e.printStackTrace();
        }
    }
}
```

* 입출력 처리시 예외가 발생하는 경우 자동으로 close()를 호출하여 자원을 반납해줌
* try() 안에 입출력 스트림을 생성하는 로직을 작성하는데 이때 해당 객체는 **AutoCloseable** 인터페이스를 구현한 객체여야 한다.
* 불필요한 예외처리 구문들이 사라졌기 떄문에 소스의 가독성이 훨씬 증가한다.

<hr>



### 👉 Throw

![throw](C:\Users\young\Desktop\삼성멀티캠퍼스\잡것\정리\TIL\JAVA\throw.PNG)

* 위 사진처럼 예외를 위로 던지고 던지고 던지는것
* 마지막에 try-catch를 사용하여 예외처리하면됨















