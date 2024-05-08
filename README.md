# Java File Handling
📁 In this file, contains all possible concepts of Java file handling in detail.

## Topics
- [x] 1. Introduction of Java File Handling
- [x] 2. How to create a file?
- [x] 3. How to read the content of a file and print it over the console?
- [x] 4. How to take input from the console and write it into a file?
- [x] 5. How to add new data in existing file {Append data}?
- [x] 6. How to count the number of characters, lines, and words in a file?
- [x] 7. How to read and write a file using Streams (Stream Classes)?
- [x] 8. Object Serialization and Deserialization in Java
- [x] 9. What will happen if we directly use FileWriter.write(s1) instead of BufferedWriter.write(s1) method?


## 1. Introduction of Java File Handling

**1.1 What is file handling and what is the need for using File Handling Techniques?**

> [!NOTE]
> In Java, file handling is a fundamental aspect of many applications, allowing them to read from and write to files on the file system.
> File handling in Java is a crucial functionality for developers, especially when dealing with large files. In this article, we'll explore the concept of Java File Handling in a simplified manner.
> In the subsequent sections, we'll delve into creating a file in Java, editing a file, and performing read and write operations on a file.

> [!IMPORTANT]
> We need to learn file handling as we sometimes need to.
  * Read data from the console and store it in a file
  * Read data from a file perform some logic on it and then save the result into some other file
> Different classes/Objects to access a file (Read, Write, and Append into a file).
  * Read class: Just to read, can not write into this file
  * Write class: we can write into this file but after every write old data will be lost?
  * Append class: we can write into this file but this time old data will not be lost.

## 2. How to create a file?

**Source Code**
```java
public class SampleClass {

	public static void main(String[] args) throws IOException {

		String path = "file1.txt";
		File file = new File(path);
		
		FileWriter fw = new FileWriter(file);
		BufferedWriter bw = new BufferedWriter(fw);

		String s1 = "Java";
		bw.write(s1);

		bw.close();
		fw.close();

	}

}
```

## 3. How to read the content of a file and print it over the console?
![1](https://github.com/AkashChauhanSoftEngi/Java_Programming_Practice/assets/23252844/594ed1cd-87b3-4ac6-bb23-596fe19b075b)

**Source Code**
```java
public class SampleClass {

	public static void main(String[] args) throws IOException {

		String path = "file1.txt";
		File file = new File(path);
		FileReader fr = new FileReader(file);
		BufferedReader bf = new BufferedReader(fr);

		int c;
		while ((c = bf.read()) != -1) {
			System.out.print((char) c);
		}

		fr.close();
		bf.close();

	}

}
```

## 4. How to take input from the console and write it into a file?
![2](https://github.com/AkashChauhanSoftEngi/Java_Programming_Practice/assets/23252844/a29e88ee-243e-49d8-a3cb-5e26b86edd53)

**Source Code**
```java
public class SampleClass {

	public static void main(String[] args) throws IOException {

		String path = "file1.txt";
		File file = new File(path);

		System.out.println("Enter s1 string");
		Scanner sc = new Scanner(System.in);
		String s1 = sc.nextLine();
		System.out.println(s1);

		FileWriter fw = new FileWriter(file);
		BufferedWriter bw = new BufferedWriter(fw);

		try {
			bw.write(s1);
		} catch (IOException e) {
			e.printStackTrace();
		}

		bw.close();
		fw.close();
		sc.close();
	}
}
```

## 5. How to add new data in existing file {Append data}?
![3](https://github.com/AkashChauhanSoftEngi/Java_Programming_Practice/assets/23252844/458768ac-c903-4ff5-8589-38419574f4a7)

**Source Code**
```java
public class SampleClass {

	public static void main(String[] args) throws IOException {

		String path = "file1.txt";
		File file = new File(path);

		System.out.println("Enter s1 string");
		Scanner sc = new Scanner(System.in);
		String s1 = sc.nextLine();
		System.out.println(s1);

		FileWriter fw = new FileWriter(file, true);
		BufferedWriter bw = new BufferedWriter(fw);

		try {
			bw.write(s1);
		} catch (IOException e) {
			e.printStackTrace();
		}

		bw.close();
		fw.close();
		sc.close();
	}
}

```

## 6. How to count the number of characters, lines, and words in a file?
![file](https://github.com/AkashChauhanSoftEngi/Java_Programming_Practice/assets/23252844/505566dc-6034-4120-a28c-b37067992f39)

**Source Code**
```java
public class SampleClass {

	public static void main(String[] args) throws IOException {

		int words = 0;
		int chars = 0;
		int lines = 0;

		String path = "file1.txt";
		File file = new File(path);

		FileReader fr = new FileReader(file);
		BufferedReader bf = new BufferedReader(fr);

		int c;
		while ((c = bf.read()) != -1) {
//			System.out.print((char)c);
			chars++;

			if ((char) c == ' ' || (char) c == '\n') {
				words++;
			}

			if ((char) c == '\n') {
				lines++;
			}

		}

		fr.close();
		bf.close();

		System.out.println("Words: " + words);
		System.out.println("Chars: " + chars);
		System.out.println("Lines: " + lines);

	}
}
```
![Screenshot 2024-05-08 at 7 59 57 PM](https://github.com/AkashChauhanSoftEngi/JavaFileHandling2024/assets/23252844/787ec1b9-84f8-4212-8f25-12e509aaa500)

## 7. How to read and write a file using Streams (Stream Classes)?

**1. FileInputStream Class {Read content from a file}.** <br/>
**2. FileOutputStream Class {Write content into a file}.**

> [!IMPORTANT]
> We can also cover this question, **First read the content of file1.txt, then write this content over the console, and then it into a file2.txt**

![4](https://github.com/AkashChauhanSoftEngi/Java_Programming_Practice/assets/23252844/b7052cc8-3344-442a-b6c9-6cce4d6010ff)

**Source Code**
```java
public class SampleClass {

	public static void main(String[] args) throws IOException {

		try {
			File inputFile = new File("file1.txt");
			File outputFile = new File("file2.txt");

			FileInputStream fis = new FileInputStream(inputFile);
			FileOutputStream fos = new FileOutputStream(outputFile);
			int c;

			while ((c = fis.read()) != -1) {
				System.out.print((char)c);
				fos.write(c);
			}

			fis.close();
			fos.close();
		} catch (FileNotFoundException e) {
			System.err.println("FileStreamsTest: " + e);
		} catch (IOException e) {
			System.err.println("FileStreamsTest: " + e);
		}

	}
}
```

## 8. Object Serialization and Deserialization in Java

Serialization is the process of transforming an object's state into a byte stream, while deserialization is its counterpart, where the byte stream is utilized to reconstruct the original Java object in memory. This mechanism serves to persist the object's state.

Put another way, serialization involves transforming a Java object into a fixed sequence of bytes, which can then be stored in a database or transmitted across a network.

![5](https://github.com/AkashChauhanSoftEngi/Java_Programming_Practice/assets/23252844/7a8bf9a6-cd40-47df-a0e9-843ff99ae211)

**Source Code**
```java
class MyClass implements Serializable {
    private static final long serialVersionUID = 1L;
    private String name;
    private int age;

    public MyClass(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String toString() {
        return "Name: " + name + ", Age: " + age;
    }
}

public class SampleClass {
    public static void main(String[] args) {
        // Serialization
        try {
            MyClass obj = new MyClass("John", 30);
            FileOutputStream fileOut = new FileOutputStream("object.ser");
            ObjectOutputStream out = new ObjectOutputStream(fileOut);
            out.writeObject(obj);
            out.close();
            fileOut.close();
            System.out.println("Object serialized successfully.");
        } catch (IOException e) {
            e.printStackTrace();
        }

        // Deserialization
        try {
            FileInputStream fileIn = new FileInputStream("object.ser");
            ObjectInputStream in = new ObjectInputStream(fileIn);
            MyClass newObj = (MyClass) in.readObject();
            in.close();
            fileIn.close();
            System.out.println("\nObject deserialized successfully.");
            System.out.println("\nDeserialized Object: " + newObj.toString());
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}

```

> [!Note]
> 1. MyClass is a simple class that implements the Serializable interface.
> 2. SerializationExample class demonstrates serialization and deserialization of the MyClass object.
> 3. In the main method, an instance of MyClass is serialized to a file named "object.ser".
> 4. Then, the object is deserialized from the same file, and the deserialized object is printed.

## 9. What will happen if we directly use FileWriter.write(s1) instead of BufferedWriter.write(s1) method?

**Code-1**
```java
FileWriter fw = new FileWriter("out.txt");
fw.write("simple method");
fw.close();
```

**Code-2**
```java
FileWriter fw = new FileWriter("out.txt");
BufferedWriter bw = new BufferedWriter(fw);
bw.write("too much code");
bw.close();
```

**Code-3**
```java
public class SampleClass {

	public static void main(String[] args) throws IOException {

		String path = "file1.txt";
		File file = new File(path);
		
		FileWriter fw = new FileWriter(file);
		BufferedWriter bw = new BufferedWriter(fw);

		String s1 = "Java";
		
		fw.write(s1);
		fw.write(s1);
		fw.write(s1);
		fw.write(s1);
		fw.write(s1);
		fw.write(s1);
	
		bw.write(s1);
		bw.write(s1);
		bw.write(s1);
		bw.write(s1);
		bw.write(s1);

		bw.close();
		fw.close();

	}

}

```

> [!NOTE]
> If we are going to write small statements many number of times (especially many short writes), then using the BufferedWriter will be more efficient.
> The BufferedWriter will save up many of the little writes and send only large chunks of data to the FileWriter.
> Writing one large chunk to a file is more efficient than many small ones because each call to FileWriter.write() involves a call to the operating system, and those are slow.
> It happens as BufferedWriter uses a buffer space to store data temporarily.
