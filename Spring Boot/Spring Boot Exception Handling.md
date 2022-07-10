# Spring Boot Exception Handling (REST & CRUD)

* GET     : Fetch data from application
* POST    : Create new data at application
* PUT     : Modify existed data at application
* DELETE  : Remove existed data at application

### Q) How can we create a Custom exception?
*  i. write a class that extends RuntimeException class
*  ii. Provide one defualt one param constrcutor
*  iii. Use this class where is it required


```java
public class BalInSuffException extends RuntimeException {

	private static final long serialVersionUID = 1L;

	public BalInSuffException() {
		super();
	}
	
	public BalInSuffException(String message) {
		super(message);
	}
}
```

```java
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data 
@NoArgsConstructor
@AllArgsConstructor
public class ErrorData {

	private String message;
	private String datetime;
	private String module;
}

```

```java

import java.util.Date;

import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestControllerAdvice;

import in.nareshit.raghu.exception.ProductNotFoundException;
import in.nareshit.raghu.model.ErrorData;

@RestControllerAdvice
public class CustomExceptionHandlerService {

	/*
	 * Below method is called by FC. When ProductNotFoundException
	 * is thrown by any Rest controller (after throwing exception)
	 */
	
	//--->Message comes in String format

	@ExceptionHandler(ProductNotFoundException.class)
	public ResponseEntity<String> handleProductNotFoundException(
			ProductNotFoundException pne
			)
	{
		return new ResponseEntity<String>(
				pne.getMessage(),HttpStatus.NOT_FOUND
				);
	}


	//--->Message comes in JSON format
	
	@ExceptionHandler(ProductNotFoundException.class)
	public ResponseEntity<ErrorData> handleProductNotFoundException(
			ProductNotFoundException pne
			)
	{
		return new ResponseEntity<ErrorData>(
				new ErrorData(
						pne.getMessage(), 
						new Date().toString(), 
						"Product"),
				HttpStatus.NOT_FOUND
				);
	}
}


```



