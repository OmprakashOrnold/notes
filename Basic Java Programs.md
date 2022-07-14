
# Basic Java Programs

## 1) CountDigits

```java
public class CountDigits {

	public static void main(String[] args) {
		Integer number = 12345;

		Integer countNoOfNumberDigits = getCountNoOfDigits(number);
		System.out.println(countNoOfNumberDigits);

	}

	private static Integer getCountNoOfDigits(Integer number) {
		int count = 0;

		while (number != 0) {
			number = number / 10;
			count++;
		}
		return count;
	}

}

```
**output**

```
5
```


## 2) SumOfNumbers


```java
public class SumOfNumbers {

	public static void main(String[] args) {
		Integer number=12345;
		
		Integer sumOfGivenNmber=getSumOfGivenNumber(number);
		System.out.println(sumOfGivenNmber);

	}

	private static Integer getSumOfGivenNumber(Integer number) {
		int sum=0;
		int rem;
		//% get last one digit
		// divide reomves last one digit retun remaining part
		while(number!=0){
			rem=number%10;
			sum=sum+rem;
			number=number/10;
		}
		return sum;
	}

}

```
**output**

```
15
```

## 3) ReverseNumber


```java
public class ReverseNumber {

	public static void main(String[] args) {
		Integer number=12345;
		Integer revNumber=getReverseNumber(number);
		System.out.println(revNumber); 
		

	}

	private static Integer getReverseNumber(Integer number) {
		int rem,rev=0;
		while(number!=0){
			rem=number%10;
			rev=(rev*10)+rem;
			number=number/10;
		}
		return rev;
	}

}

```
**output**

```
54321
```
## 4) NumericPalindrome


```java
public class NumericPalindrome {

	public static void main(String[] args) {
		Integer number=1441;
		Boolean isPalindromeNumber=checkPalindromeOrNot(number);
		if(isPalindromeNumber){
			System.out.println("palindrome number");
		}else{
			System.out.println("not palindrome number");
		}
	}

	private static Boolean checkPalindromeOrNot(Integer number) {
		int rev=0;
		int rem;
		int temp=number;
		while(number!=0){
			rem=number%10;
			rev=(rev*10)+rem;
			number=number/10;
		}
		if(rev==temp){
			return true;
		}
		return false;
	}

}

```
**output**

```
palindrome number

```

## 5) ArmstrongNumber


```java
public class ArmstrongNumber {

	public static void main(String[] args) {
		// 1+64+125
		Integer number = 153;
		Boolean isArmstrongNumber = checkItIsaArmstrongNumber(number);
		if(isArmstrongNumber){
			System.out.println("It is armstrrong number");
		}else{
			System.out.println("It is not armstrrong number");
		}
	}

	private static Boolean checkItIsaArmstrongNumber(Integer number) {
		int rem, sum = 0;
		int temp = number;
		while (number != 0) {
			rem = number % 10;
			sum = sum + (rem * rem * rem);
			number = number / 10;
		}
		if(temp==sum){
			return true;
		}
		
		return false;
	}

}
```
**output**
```
It is armstrrong number

```

