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

```java
public int MySquareRoot(int x)
{
    if (x<0)
    {
    throw new ArgumentOutOfBoundsException("Must be a non-negative integer");
    }

    //our implementation here

}
```
