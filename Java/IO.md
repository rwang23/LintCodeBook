##IO

```java
public static void main(String []argh)
   {
      ArrayList mylist=new ArrayList();
      Scanner sc=new Scanner(System.in);
      int t=sc.nextInt();
      for(int i=0;i<t;i++)
      {
         String s=sc.next();
         if(s.equals("Student"))mylist.add(new Student());
         if(s.equals("Rockstar"))mylist.add(new Rockstar());
         if(s.equals("Hacker"))mylist.add(new Hacker());
      }
      System.out.println(count(mylist));
   }
```

check if it is an integer

```java
Scanner sc=new Scanner(System.in);
try
{
  System.out.println("Please input an integer");
  //nextInt will throw InputMismatchException
  //if the next token does not match the Integer
  //regular expression, or is out of range
  int usrInput=sc.nextInt();
}
catch(InputMismatchException exception)
{
  //Print "This is not an integer"
  //when user put other than integer
  System.out.println("This is not an integer");
}
```
