# Java에서 + 연산으로 문자열 붙일 시 최적화

Java 1.5 이상의 version에서는 + 연산으로 문자열을 붙여도 StringBuilder를 사용하는 바이트 코드로 변경됨
한 줄에서 + 연산으로 string literal을 붙이면 모두 합쳐진 문자열로 컴파일러가 최적화함

```java
// 기존 코드
String s = "a" + "b" + "c";
// compile하면 아래처럼 모두 합쳐짐
String s = "abc";
```

### 기존 코드

```java
public class StringTest {
    public static void main(String[] args) {
        String str0 = "It's a string....";
        String str1 = "It's" + " a string" + "....";
        String str2 = "It's a string...." + str0 + "000";
        str2 = str0 + str1 + "1111";
        str2 = str2 + "1111";
        str2 += "1111";
        for (int i = 0; i < 10; ++i) {
            str2 = str2 + "1111";
            str2 += "1111";
        }
    }
}
```

### JDK 1.4로 complie

```java
public class StringTest {

    public StringTest() {
    }

    public static void main(String args[]) {
        String str0 = "It's a string....";
        String str1 = "It's a string....";
        String str2 = "It's a string...." + str0 + "000";
        str2 = str0 + str1 + "1111";
        str2 = str2 + "1111";
        str2 = str2 + "1111";
        for (int i = 0; i < 10; i++) {
            str2 = str2 + "1111";
            str2 = str2 + "1111";
        }

    }
    
}
```

### JDK 1.5로 complie

```java
public class StringTest {

    public StringTest() {
    }

    public static void main(String args[]) {
        String str0 = "It's a string....";
        String str1 = "It's a string....";
        String str2 = (new StringBuilder("It's a string....")).append(str0).append("000").toString();
        str2 = (new StringBuilder(String.valueOf(str0))).append(str1).append("1111").toString();
        str2 = (new StringBuilder(String.valueOf(str2))).append("1111").toString();
        str2 = (new StringBuilder(String.valueOf(str2))).append("1111").toString();
        for (int i = 0; i < 10; i++) {
            str2 = (new StringBuilder(String.valueOf(str2))).append("1111").toString();
            str2 = (new StringBuilder(String.valueOf(str2))).append("1111").toString();
        }
    }

}
```
