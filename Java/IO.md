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

####check if it is an integer

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
####get array fron scan
```java
public static void main (String[] args)
{
    Scanner input = new Scanner(System.in);
    double[] numbers = new double[5];

    for (int i = 0; i < numbers.length; i++)
    {
        System.out.println("Please enter number");
        numbers[i] = input.nextDouble();
    }
}
```

###IOStream
- byteOrientedClasses: InputStream OutputStream
- CharacterOrientedClasses: Reader Writer

###File
```java
File f = new File("abc.txt");
//File f = new File("dir", "abc.txt");
//dir is directory

System.out.println(f.extists());
if (!f.exists()) {
  f.mkdir();
  try {
    f.createNewFile();
  } catch (IOException e) {
    e.printStackTrace();
  }
}
System.out.println(f); // print abc.txt

```

###FileWriter
- We usually use BufferedWriter instead of FileWriter

FileWriter(String filename)
FileWriter(File f)

write(char character)
to write a single character to the file
write(char[] ch)
to write array of chars
write(String string)
flush()

###FileReader

```java
try {
  FileReader fr = new FileReader("abc.txt");
  inr i = fr.read();
  while (i != -1) {
    System.out.println((char) i);
    i = fr.read();
  }
} catch (FileNotFoundException e) {
  e.printStackTrace();
} catch (IOException e) {
  e.printStackTrace();
}
```

###BufferedWriter
- extending Writer
- should not use direction. should use with writer
- bw.writeLine()

```java
BufferedWriter bw = new BufferedWriter(new FileWriter(abc.txt), true);
```

###BufferdReader
```java
BufferredReader br = new BufferdReader(new FileReader("abc.txt"));
String line = br.readLine();
while (line != null) {
  System.out.println(line);
  line = br.readLine();
}
br.close();
```

###PrintWrter
- most enhanced writer to writer character data to file, we can write everything
- by using FileWriter and BufferdWriter we can only write character data

```
PrintWriter(String name)
PrintWriter(File f)
pw.println(string)
pw.close()
```
