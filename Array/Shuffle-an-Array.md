##Shuffle an Array

####Approach 1: Shuffle elements in an array

```java
public static int[] RandomizeArray(int[] array){
		Random rgen = new Random();  // Random number generator

		for (int i=0; i<array.length; i++) {
		    int randomPosition = rgen.nextInt(array.length);
		    int temp = array[i];
		    array[i] = array[randomPosition];
		    array[randomPosition] = temp;
		}

		return array;
	}
```

You can also define a method whose input is a range of the array like below:

Input: range of an int array

Output: randomly shuffled array

For example, given a=1 and b=10, the method returns a shuffled array such as {2 5 6 7 9 8 3 1 10 4}.

```java
public static int[] RandomizeArray(int a, int b){
		Random rgen = new Random();  // Random number generator
		int size = b-a+1;
		int[] array = new int[size];

		for(int i=0; i< size; i++){
			array[i] = a+i;
		}

		for (int i=0; i<array.length; i++) {
		    int randomPosition = rgen.nextInt(array.length);
		    int temp = array[i];
		    array[i] = array[randomPosition];
		    array[randomPosition] = temp;
		}

		for(int s: array)
			System.out.println(s);

		return array;
	}
```

####Approach 2: Java Collection.shuffle() method

```java
// Create an array
Integer[] array = new Integer[]{1, 2, 3, 4};

//int[] array = new int[]{1, 2, 3, 4}; //does not work

// Shuffle the elements in the array
Collections.shuffle(Arrays.asList(array));
```
