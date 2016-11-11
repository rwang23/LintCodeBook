####Questions
what is exception?
Unchecked exception vs checked exception
final vs finally vs finalize
throws vs throw

##Exception
```java
        int caseNum = 0;
        try {
            caseNum = scan.nextInt();
        }
        catch(InputMismatchException exception) {
            System.out.println("This is not an integer");
        }
```
##自己做题的时候,写边界条件
- 有时候返回-1并不合理,所以throw new exception
- 一般会用这种ArgumentOutOfBoundsException是越界
- 或者IllegalArgumentException
- NullPointerException
- ArithmeticException
- NUmberformatExpection

###try
- 在try中声明的变量,是local variable

####Throwable
- Errors // errors is non-recoverable exceptions : outofmemoryerror, virtualmachineerror, assertionerrors
- Exception
- throw can only throw throwable exception not errors

###四种Exception
- IOException
- InterruptedException //multithread
- SqlException
- RuntimeException //包括上楼那些

####two types of exceptions:
- Checked Exception //expection gererated at compilation time
- Unchecked Exception //runtime exception, like arimetic exception

```java
public int MySquareRoot(int x) {
    if (x < 0) {
        throw new ArgumentOutOfBoundsException("Must be a non-negative integer");
    }

    //our implementation here

}
```

###Errors
- In Any Programming Language ,when ever we write a program , we get two types of errors, they are

####1)CompileTimeErrors
        SyntaxErrors and Imporper environment result is called CompileTime Errors

    SyntaxErrors Occur whenever a statement writen by the programmer cannot be compile by the compiler
    Whenever a source code is compiled ,first compiler checks whether a proper environment is available for the jvm or not to execute the byte code which it has generated for the source code.
####2)RunTimeErrors/LogicalErrors
    a)simplelogicalErrors
    b)SeriousLogicalErrors

    RuntimeErrors are generated while runing an application
     We can classfied two types of errors
     1)SimpleLogicalErrors
     ================
        Logical errors which can be neglected by the jvm .such errors are known as SimpleLogicalErrors.
    eg: int x=100/0;
     2)SeriousLogicalErrors
     ======================
     We cannot handle these exceptions jvm will be handled


####In General RunTimeErrors we can called as Exceptions

####e.gerMessage()
- 直接Print e的话,会写出他的class name
- 用getMessage() 只会打印出想要的信息

####pritStackTrace()
- 打印该exception发生的line

```java
try {

}
catch(Exception e) {
    e.printStackTrace();
}
```

####exit优先级高于finally,finally高于return
