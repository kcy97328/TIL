## μμΈ(Exception)



### π μμΈμ λ°μ

```java
package exception;

public class ExceptionApp {

	public static void main(String[] args) {
		System.out.println(1);
		System.out.println(2/0);	// μμΈ λ°μ
		System.out.println(3);
		
	}

}	
```

> π’ 1	

<hr> 



### π μμΈμ μ²λ¦¬

```java
package exception;

public class ExceptionApp {

	public static void main(String[] args) {
		System.out.println(1);
		try {
			System.out.println(2/0);	// μμΈ λ°μ
		} catch(ArithmeticException e) {
			System.out.println("μλͺ»λ κ³μ°μ΄λ€μ.");
		}
		System.out.println(3);
		
	}

}
```

> π’	
>
> 1
> μλͺ»λ κ³μ°μ΄λ€μ.						// μμΈκ° λ°μν λΆλΆμ tryλ‘ μ²΄ν¬ν catch μΆλ ₯
> 3

```java
package exception;

public class ExceptionApp {

	public static void main(String[] args) {
		System.out.println(1);
		int[] scores = {10,20,30};
		try {
			System.out.println(2);
			System.out.println(scores[3]);			//μμΈ λ°μ
			System.out.println(3);
			System.out.println(2/0);				//μμΈ λ°μ
			System.out.println(4);
		} catch(ArithmeticException e) {			//μ°μ μμΈμ²λ¦¬
			System.out.println("μλͺ»λ κ³μ°μ΄λ€μ.");
		} catch(ArrayIndexOutOfBoundsException e) {	//λ°°μ΄ μμΈμ²λ¦¬
			System.out.println("μλ κ°μ μ°Ύκ³  κ³μλ€μ ^^");
		}
		System.out.println(5);
	}

}
```

> π’
>
> 1											 
> 2											
> μλ κ°μ μ°Ύκ³  κ³μλ€μ ^^ 			   β
> 5

β μ‘΄μ¬ νμ§ μλ scores[3] λ°°μ΄μ ArrayIndexOutOfBoundsException(λ°°μ΄ μμΈμ²λ¦¬)μ μ¬μ©νμ¬ catchμΆλ ₯

* μμΈ λ°μν λΆλΆ μ΄ν μΆλ ₯x 
* μ΄λ° κ²½μ° λ€λ₯Έ μμΈ λν try/catch μ¬μ©ν΄μΌν¨

<hr>



### π μμΈμ μ°μ μμ

β λΆλͺ¨ Exception

1. Exception 	

βμμ Exception 	 

1. ArithmeticException (μ°μ μμΈμ²λ¦¬)

2. ArrayIndexOutOfBoundsException (λ°°μ΄ μμΈμ²λ¦¬)

3. ....λ±

   

* λΆλͺ¨ Exceptionμ μμ Exceptionλͺ¨λλ₯Ό ν¬κ΄ν¨

* λΆλͺ¨ Exceptionμ¬μ©μ μμ Exception μ μ¬μ© λͺ»ν¨
* catchλ¬Έ μμμ λ°λΌ μ¬μ©λ¨(λ¨Όμ μ΄ μμλλ‘)

<hr>



### π e μ λΉλ°

* μ μ½λμ€ **try/catch** μ λ³΄λ©΄ catch(Exception **`e`** ) μ΄ μλ€. 

* μ΄κ²μ€μ **`e`** λ **data type**μ΄ **exception**μΈ λ³μμ΄λ€.
* **`e`** λ₯Ό νμ©ν μμλ‘ **e.getMessage()** μ μ¬μ©νλ©΄ λ¬΄μ λλ¬Έμ μμΈκ° λ°μνλμ§ μλ €μ€λ€.
* **e.printStackTrace** κ·Όμμ§λ₯Ό μ°Ύμμ λ¨κ³λ³λ‘ μλ¬λ₯Ό μΆλ ₯
* **e.toString()** toString()μ νΈμΆν΄μ κ°λ¨ν μλ¬ λ©μμ§λ₯Ό νμΈ

<hr>



### π ( checked vs unchecked ) exception

* Exceptionμ checkedμ uncheckedκ° μλ€. 
* checkedλ μ²΄ν¬λ₯Ό νμ§ μμΌλ©΄ μ»΄νμΌ μ‘°μ°¨ λμ§ μμ§λ§  
* uncheckedλ μ»΄νμΌ μ€νμ΄ κ°λ₯νκ³  μ½μμμ μμΈ λ°μ μ νμλ₯Ό ν΄μ€λ€.

![checked_unchecked_exceptions](https://github.com/kcy97328/TIL/blob/main/JAVA/checked_unchecked_exceptions.png)

| κ΅¬λΆ          | Checked Exception                    | UnChecked Exception               |
| ------------- | ------------------------------------ | --------------------------------- |
| νμΈ μμ      | μ»΄νμΌ(Compile) μμ                  | λ°νμ(Runtime) μμ               |
| μ²λ¦¬ μ¬λΆ     | λ°λμ μμΈ μ²λ¦¬ν΄μΌ νλ€            | λͺμμ μΌλ‘ νμ§ μμλ λλ€.      |
| νΈλμ­μ μ²λ¦¬ | μμΈ λ°μμ λ‘€λ°±(rollback) νμ§ μμ | μμΈ λ°μμ λ‘€λ°±(rollback) ν΄μΌν¨ |

<hr>



### π finally

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
            // λ§μ½μ fκ° nullμ΄ μλλΌλ©΄
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

* μμΈμ¬λΆμ κ΄κ³μμ΄ μ€νμ΄ λλ€.

* μμΈμλ μκ΄ μμ΄ λ°λμ λλ΄μ€μΌ νλ μμμ΄ μμλ μ¬μ©
* μμΈλ₯Ό μ¬μ©νλ©΄ κ·Έ λ·λΆλΆμ΄ μλμ μνκΈ° λλ¬Έμ 

<hr>



### π try-with-resources

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

* μμΆλ ₯ μ²λ¦¬μ μμΈκ° λ°μνλ κ²½μ° μλμΌλ‘ close()λ₯Ό νΈμΆνμ¬ μμμ λ°λ©ν΄μ€
* try() μμ μμΆλ ₯ μ€νΈλ¦Όμ μμ±νλ λ‘μ§μ μμ±νλλ° μ΄λ ν΄λΉ κ°μ²΄λ **AutoCloseable** μΈν°νμ΄μ€λ₯Ό κ΅¬νν κ°μ²΄μ¬μΌ νλ€.
* λΆνμν μμΈμ²λ¦¬ κ΅¬λ¬Έλ€μ΄ μ¬λΌμ‘κΈ° λλ¬Έμ μμ€μ κ°λμ±μ΄ ν¨μ¬ μ¦κ°νλ€.

<hr>



### π Throw

![throw](https://github.com/kcy97328/TIL/blob/main/JAVA/throw.PNG)

* μ μ¬μ§μ²λΌ μμΈλ₯Ό μλ‘ λμ§κ³  λμ§κ³  λμ§λκ²
* λ§μ§λ§μ try-catchλ₯Ό μ¬μ©νμ¬ μμΈμ²λ¦¬νλ©΄λ¨















