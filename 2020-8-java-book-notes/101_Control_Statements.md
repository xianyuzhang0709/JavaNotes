## 1. if-else

- if statement
- if-else statement
- if-else-if ladder (阶梯式: if - else if - else if - else)
- nested if statement (嵌套式: if - if - ...)

```java
if(condition){  
	//code if condition is true  
}else{  
	//code if condition is false  
}  
```

#### Ternary Operator  ( ?  : ) 

```java
String output = (number%2 == 0)? "even number":"odd number";    
```

## 2. switch

It is like **if-else-if** ladder statement.

The switch statement works with byte, short, int, long, enum types, String and some wrapper types like Byte, Short, Int, and Long. Since Java 7, you can use [strings](https://www.javatpoint.com/java-string) in the switch statement.

In other words, the switch statement tests the equality of a variable against multiple values. (switch语句针对多个值测试变量的相等性。)

**A case label** can be :

* A constant expression of type **char**, **byte**, **short**, or **int** 
* An **enumerated constant**
* A **string literal** (starting with Java 7)

```java
String str = . . .; 
switch (str.toLowerCase()) {
    case "yes": // OK since Java 7 
    					...
    					break; 
    ...
}

enum Size {SMALL, MEDIUM, LARGE, EXTRA_LARGE};
Size sz = Suze.MEDIUM; //enumeric class
switch (sz)
{
    case SMALL: // no need to use Size.SMALL 
    					...
    					break;
    ...
}
```



```java
switch(expression){    
	case value1:    
 		//code to be executed;    
 		break;  
	case value2:    
 		//code to be executed;    
		break;  //optional  
	......    
    
	default:     
 		//code to be executed if all cases are not matched;    
}    
```

* Nested switch statement 

```java
 switch( collegeYear )  
        {  
            case 1:  
                System.out.println("English, Maths, Science");  
                break;  
            case 2:  
                switch( branch )   
                {  
                    case 'C':  
                        System.out.println("Operating System, Java, Data Structure");  
                        break;  
                    case 'E':  
                        System.out.println("Micro processors, Logic switching theory");  
                        break;  
                    case 'M':  
                        System.out.println("Drawing, Manufacturing Machines");  
                        break;  
                }  
                break;  
			 }
```

* Java allows us to use **enum** in switch statement.

```java
public class JavaSwitchEnumExample {      
       public enum Day {  Sun, Mon, Tue, Wed, Thu, Fri, Sat  }    
       public static void main(String args[])    
       {    
         Day[] DayNow = Day.values();    
           for (Day Now : DayNow)    
           {    
                switch (Now)    
                {    
                    case Sun:    
                        System.out.println("Sunday");    
                        break;    
                    case Mon:    
                        System.out.println("Monday");    
                        break;    
                    case Tue:    
                        System.out.println("Tuesday");    
                        break;         
                    ......   
                }    
             }    
        }    
}    
```

* Wrapper in Switch Statement: Java allows us to use four wrapper classes: **Byte, Short, Integer and Long** in switch statement.

```java
public class WrapperInSwitchCaseExample {       
       public static void main(String args[])  
       {         
            Integer age = 18;        
            switch (age)  
            {  
                case (16):            
                    System.out.println("You are under 18.");  
                    break;  
                case (18):                
                    System.out.println("You are eligible for vote.");  
                    break;  
                case (65):                
                    System.out.println("You are senior citizen.");  
                    break;  
                default:  
                    System.out.println("Please give the valid age.");  
                    break;  
            }             
        }  
}  
```

## 3. for loop

- for loop
- while loop
- do-while loop

| Comparison  | for loop                                    | while loop                              | do while loop                                                |
| :---------: | :------------------------------------------ | :-------------------------------------- | :----------------------------------------------------------- |
| When to use | If the number of iteration is fixed         | If the number of iteration is not fixed | If the number of iteration is not fixed and you must have to execute the loop at least once |
|   Syntax    | `for(init;condition;incr/decr){ //code  } ` | `while(condition){ //code  } `          | `do{ //code   }while(condition);  `                          |

* for-each loop:

```java
for(Type var:array){  
//code to be executed  
}  

//example:
public class ForEach {  
	public static void main(String[] args) {
      int arr[] = {12,23,44,56,78};  
      for(int i:arr){  
          System.out.println(i);  
      }  
	}  
}  
```

* **labeled for loop**: It is useful if we have nested for loop so that we can **break/continue** specific for loop.

```java
public class LabeledForExample {  
  public static void main(String[] args) {  
      aa:  
          for(int i=1;i<=3;i++){  
              bb:  
                  for(int j=1;j<=3;j++){  
                      if(i==2&&j==2){  
                          break aa;  
                      }  
                      System.out.println(i+" "+j);  
                  }  
          }  
  }  
}  
```

## 4. continue & switch

**continue**: jump to the next iteration of the loop immediately.

**break**: the loop is immediately terminated and the program control resumes at the next statement following the loop. (resume 继续)

## 5. Comments

* //   
* /* */
*  /**  */  Create Documentation API by **javadoc** tool: `javadoc Calculator.java`

