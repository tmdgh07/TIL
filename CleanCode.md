# CleanCode

<br>

# 클린 코드 ( Clean Code ) 란?

클린 코드란 말 그대로 "코드를 깨끗하게 짜는 것"을 말합니다.

즉, 코드를 처음 보는 사람도 알아볼 수 있도록 코드의 가독성을 높여서 짜는것이라고 할 수 있겠습니다.

클린 코드라는 용어는 로버트 C. 마틴( Robert C. Martin ) 이 저술한 동명의 책에서 처음 등장했습니다.

![위 책이 로버트 C. 마틴이 저술한 책, Clean Code 이다.](CleanCode%20fa61090c1e1a4629aa049fe046a5ce37/Untitled.png)

위 책이 로버트 C. 마틴이 저술한 책, Clean Code 이다.

이 책에서는 개발자가 코드의 가독성과 유지보수성을 높이기 위한 다양한 방법을 알려줍니다.

## 클린 코드는 왜쓸까?

한 개발자가 혼자서 모든 코드와 서비스의 내용을 기억하고 있다면 굳이 클린 코드를 사용할 필요는 없을 것입니다.

그러나 사람의 기억력에는 한계가 있기마련이죠. 서비스를 운영하다 1년뒤에 수정하려고 봤는데 코드를 이해하지 못하면 결국에 코드를 다시 짜야하는 등의 문제가 생길 것 입니다.

그리고 다른 개발자와 협업을 해야하는 상황이라면 클린 코드의 역할이 더 중요해집니다.

자기자신만 알아볼 수 있는 코드를 작성했다면 협업에 지장이 생길테니까요.

## 클린 코드를 적용해서 코드를 작성하는 방법!

클린 코드에는 주요 원칙이 몇가지 있습니다.

### 1. 의미있는 변수와 함수 사용하기

변수와 함수는 사용되는 문맥에 맞게 명확하게 이름이 지어져야 합니다.

이를 통해 코드의 이해가 쉬워지고, 버그 발생의 가능성도 줄어들게 됩니다.

### 2. 가독성 좋은 코드 만들기

코드는 다른 사람이나 추후의 자신이 읽기 쉽게 작성되어야 합니다.

의미 있는 변수/함수/클래스명등을 사용하여 코드의 의도를 정확하게 전달해야 합니다.

```java
public class Main
    public static void main(String[] args) {
    	int a = 3, b = 8;
        int result = add(a, b);
        System.out.println("합 : " + result);
    }

    public static int add(int num1, int num2) {
    	return num1 + num2;
    }
}
```

위 코드에서는 변수명을 의미있는 이름으로 더 명확하게 변경할 필요가 있습니다.

예를 들면 a와 b를 operand1, operand2 (operand; 수식에서 연산이 수행되는 값 또는 피연산자를 나타내는 일반적인 용어 ) 로 변경하여 변수의 역할을 명확히 할 수 있습니다.

메서드명도 마찬가지로, add 대신 addNumbers를 사용하여 메서드가 무슨 역할을 하고있는지 명확히 해줄 수 있습니다.

```java
public class Main
    public static void main(String[] args) {
    	int operand1 = 3, operand2 = 8;
        int result = add(operand1, operand2);
        System.out.println("합 : " + result);
    }

    public static int addNumbers(int num1, int num2) {
    	return num1 + num2;
    }
}
```

### 3. 주석은 필요할 때만 사용하기

주석은 개발자가 코드를 이해하는데 도움을 주지만, 주석을 추가하는 것보다 코드 자체로 의도를 명확하게 드러내는 것이 좋습니다.

### 4. 간결한 코드 유지하기

불필요한 코드는 작성하지 않고, 간결한 코드를 유지해야 합니다. 코드를 간결하게 유지하면, 버그가 줄고 유지보수가 용이해집니다.

```java
import java.util.Scanner;

public class Main
    public static void main(String[] args) {
    	Scanner scanner = new Scanner(System.in);

        System.out.print("첫 번째 수를 입력해주세요: ");
        int operand1 = scanner.nextInt();

        System.out.print("두 번째 수를 입력해주세요: ");
        int operand2 = scanner.nextInt();

        int sum = operand1 + operand2;

        System.out.println("합 : " + sum);

        scanner.close();
    }

```

위 코드에서는 사용자 입력을 받는 부분에서 동일한 기능을 두 번 수행합니다. 이를 아래와 같이 InputNumber 메서드로 추출하여 중복을 제거할 수 있습니다

```java
import java.util.Scanner;

public class Main
    public static void main(String[] args) {
        int operand1 = InputNumber("첫 번째 수를 입력해주세요: ");
        int operand2 = InputNumber("두 번째 수를 입력해주세요: ");

        int sum = operand1 + operand2;

        System.out.println("합 : " + sum);
    }

    public static int InputNumber(String message) {
    	System.out.print(message);
        return new Scanner(System.in).nextInt();
    }
}
```

### 5. 모듈화 수행하기

코드를 크고 작은 모듈로 나누어, 각 모듈이 특정 기능이나 역할을 수행하게 해야합니다.

이로서 코드의 재사용성을 높이고 유지보수를 쉽게 만들 수 있습니다.

```java
import java.util.Scanner;

public class Main
    public static void main(String[] args) {
        int operand1 = InputNumber("첫 번째 수를 입력해주세요: ");
        int operand2 = InputNumber("두 번째 수를 입력해주세요: ");

        int sum = operand1 + operand2;
        int difference = operand1 - operand2;
        int product = operand1 * operand2;
        int quotient = operand1 / operand2;

        System.out.println("합 : " + sum);
        System.out.println("차 : " + difference);
        System.out.println("곱 : " + product);
        System.out.println("몫 : " + quotient);
    }

    public static int InputNumber(String message) {
    	System.out.print(message);
        return new Scanner(System.in).nextInt();
    }
}
```

위 코드에서 분리된 기능을 수행하는 add, subtract, multiply, devide를 만들어 각각 덧셈, 뺄셈, 곱셈, 나눗셈을 수행하게 만들 수 있습니다. 그리고 ResultOut 메서드를 만들어 코드의 가독성을 높이고 각각의 기능을 명확하게 구분해 재사용성을 높게 만들 수 있습니다.

```java
import java.util.Scanner;

public class Main
    public static void main(String[] args) {
        int operand1 = InputNumber("첫 번째 수를 입력해주세요: ");
        int operand2 = InputNumber("두 번째 수를 입력해주세요: ");

        int sum = addNumbers(operand1, operand2);
        int difference = subtractNumbers(operand1, operand2);
        int product = multiplyNumbers(operand, operand2);
        int quotient = devideNumbers(operand1, operand2);

        ResultOut("합 : ", sum);
        ResultOut("차 : ", difference);
        ResultOut("곱 : ", product);
        ResultOut("몫 : ", quotient);
    }

    public static int addNumbers(int num1, int num2) {
    	return num1 + num2;
    }

    public static int subtractNumbers(int num1, int num2) {
    	return num1 - num2;
    }

    public static int multiplyNumbers(int num1, int num2) {
    	return num1 * num2;
    }

    public static int devideNumbers(int num1, int num2) {
    	if (num2 != 0)
            return num1 / num2;
        else {
            System.out.println("0으로는 나눌 수 없습니다.");
            return -1;
        }
    }

    public static void ResultOut(String message, int result) {
    	System.out.println(message + result);
    }

    public static int InputNumber(String message) {
    	System.out.print(message);
        return new Scanner(System.in).nextInt();
    }
}
```

그러나 위와같이 지나친 모듈화는 코드의 길이가 증가하여 가독성과 간결성을 해칠 수 있습니다.

따라서 항상 적절한 수준에서 모듈화를 적용해야 합니다. 작은 규모의 프로그램이나 간단한 기능의 경우는 모듈화를 과도하게 적용하지 않고, 코드를 간결하게 유지하는 편이 좋습니다.

```java
import java.util.Scanner;

public class Main
    public static void main(String[] args) {
        int operand1 = InputNumber("첫 번째 수를 입력해주세요: ");
        int operand2 = InputNumber("두 번째 수를 입력해주세요: ");

        CalculateAndOut(operand1, operand2, "합", (a, b) -> a + b);
        CalculateAndOut(operand1, operand2, "차", (a, b) -> a - b);
        CalculateAndOut(operand1, operand2, "곱", (a, b) -> a * b);
        CalculateAndOut(operand1, operand2, "몫", (a, b) -> (b != 0) ? a / b : -1);
    }

    public static int InputNumber(String message) {
    	System.out.print(message);
        return new Scanner(System.in).nextInt();
    }

  	public static void CalculateAndOut(int num1, int num2, String operation, IntegerOperation op) {
    	int result = op.apply(num1, num2);
        System.out.println(operation + " : " + result);
    }

    @FunctionalInterface
    private interface IntegerOperation {
    	int apply(int a, int b);
    }
}
```

위 코드에서는 람다 표현식을 사용하여 간단한 연산을 처리하는 함수형 인터페이스 IntegerOperation을 만들었고, CalculateAndOut 메서드에서 각 연산을 처리하고 결과를 출력하게 됩니다.

결과적으로 하나의 메서드로 여러 연산을 처리하면서 코드를 간결하게 유지하여 불필요한 코드 라인을 줄이고 기능을 최적화 했다고 볼 수 있습니다.

### 6. 테스트가능한 코드 만들기

클린 코드는 테스트가 쉽게 가능한 구조여야 합니다. 테스트케이스를 작성하고 유지 보수할 때 테스트가 도움이 되도록 코드를 작성하는 것이 중요합니다. 테스트 가능성을 고려한 코드는 주로 모듈화, 의존성 주입, 인터페이스 활용등을 통해 적용할 수 있습니다.

위 소개한 6가지 원칙은 클린 코드를 수행하는 많은 방법들중 가장 대표적인 예제입니다. 더 자세한 내용은 위에서 소개한 책에 언급된 원칙을 참고하시면 될 것 같습니다.