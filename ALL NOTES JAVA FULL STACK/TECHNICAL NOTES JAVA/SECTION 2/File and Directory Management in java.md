# Overview  

Topic 1: File Class

What it is: File class = represents a path (file or folder). It's just metadata handler — doesn't read/write actual content. Think of it as "pointer to a location," not the content itself.

Key methods: exists(), createNewFile(), delete(), isDirectory(), canRead(), canWrite(), length(), getName(), getPath()

Gotcha: new File("x.txt") does NOT create the file on disk — it just creates a Java object representing that path. You need createNewFile() to actually create it.

## Practice Questions:

1. Write a program that checks if a file "data.txt" exists. If not, create it. If yes, print its size in bytes and last modified time.

```java
import java.io.File;

import java.io.IOException;

import java.util.Date;

public class Test {

    public static void main(String[] args) {

        File file = new File("data.txt");

        if (!file.exists()) {

            try {

                if (file.createNewFile()) {

                    System.out.println("File is created data.txt");

                    long sizeInBytes = file.length();

                    long lastModifiedMillis = file.lastModified();

                    Date lastModified = new Date(lastModifiedMillis);

                    System.out.println("Size : " + sizeInBytes + " Bytes");

                    System.out.println("Last Modified: " + lastModified);

                } else {

                    System.out.println("Failed to create the file");

                }

            } catch (IOException e) {

                System.err.println("An error occered while creating the file " + e.getMessage());

            }

        } else {

            System.out.println("file 'data.txt' exists");

            long sizeInBytes = file.length();

            long lastModifiedMillis = file.lastModified();

            Date lastModified = new Date(lastModifiedMillis);

            System.out.println("Size : " + sizeInBytes + " Bytes");

            System.out.println("Last Modified: " + lastModified);

        }

    }

}
```

1. Write a program that takes a folder path and prints whether it's a file, a directory, or doesn't exist at all.

```java
import java.io.File;

public class Test {

    public static void main(String[] args) {

        File file = new File(".");

        if (!file.exists()) {

            System.out.println("Path does not exist");

        } else if (file.isFile()) {

            System.out.println("This is a file");

        } else if (file.isDirectory()) {

            System.out.println("This is a Directory");

        }

    }

}
```

## 1. Write a program that lists all .txt files in a given directory (hint: listFiles() with a filter).

## Approach mine -

```java
import java.io.File;

public class Test {

    public static void main(String[] args) {

        File file = new File(".");

        File[] fileArray = file.listFiles();

        if (fileArray != null) {

            for (File name : fileArray) {

                if (name.getName().endsWith(".txt")) {

                    System.out.println(name.getName());

                }

            }

        } else {

            System.err.println("Not a Direcotry or Cant read");

        }

    }

}
```

## Apraoch Claude:

```java
import java.io.File;

public class Test {

    public static void main(String[] args) {

        File folder = new File(".");

        File[] txtFiles = folder.listFiles((dir, name) -> name.endsWith(".txt"));

        if (txtFiles == null) {

            System.out.println("Not a valid directory or an I/O error occurred");

        } else if (txtFiles.length == 0) {

            System.out.println("No .txt files found");

        } else {

            for (File f : txtFiles) {

                System.out.println(f.getName());

            }

        }

    }

}
```

Topic 2: Writing to Files (FileWriter + BufferedWriter)

## Quick concept recap:

- FileWriter → writes character data to a file. Creates the file if it doesn't exist. Overwrites existing content by default.
- BufferedWriter → wraps FileWriter to batch writes efficiently (fewer actual disk hits = faster).
- write() → writes a string. newLine() → adds a line break (platform-independent, better than hardcoding \n).
- Must close() at the end — otherwise buffered data may never actually get flushed to disk.
- Append mode: new FileWriter("file.txt", true) — that second boolean param means "append instead of overwrite."

Exception to expect: IOException — same reasoning as before (permission, disk, invalid path).

## Practice Q1:

Write a program using Scanner to take 5 strings from user input (one at a time), and write each one on its own line to notes.txt. Use FileWriter + BufferedWriter. Remember to close the writer at the end.

```java
import java.io.FileWriter;

import java.io.BufferedWriter;

import java.util.Scanner;

import java.io.IOException;

public class Test {

    public static void main(String[] args) {

        try (FileWriter fw = new FileWriter("Siddu.txt");

                BufferedWriter bw = new BufferedWriter(fw);

                Scanner sc = new Scanner(System.in);) {

            System.out.println("Enter the 5 Strings. Press enter after each line");

            for (int i = 1; i <= 5; i++) {

                System.out.println("Enter Line " + i + ": ");

                String line = sc.nextLine();

                bw.write(line);

                bw.newLine();

            }

            System.out.println("SuccessFully Saved to Siddu.txt");

        } catch (IOException e) {

            System.err.println("An error occured while writing to the file." +       e.getMessage());

        }

    }

}
```

Creating all the objects in try block, will automatically close it.

## Practice Q2:

Modify this concept slightly — write a program that appends a new line to Siddu.txt every time you run it (don't overwrite previous runs' data). Add a fixed string like "Log entry" plus today's date (you can hardcode a string for now, or if you want to combine modules — use LocalDate.now() from Date/Time module, your call).

```java
import java.io.FileWriter;

import java.io.BufferedWriter;

import java.time.LocalDate;

import java.io.IOException;

public class Test {

    public static void main(String[] args) {

        try (FileWriter fw = new FileWriter("Siddu.txt", true);

                BufferedWriter bw = new BufferedWriter(fw);) {

            LocalDate today = LocalDate.now();

            String logEntry = "Log Entry - " + today;

            bw.write(logEntry);

            bw.newLine();

            System.out.println("SuccessFully Appended: " + logEntry);

        } catch (IOException e) {

            System.err.println("An error occured while writing to the file." + e.getMessage());

        }

    }

}
```

Topic 3: Reading Files (FileReader + BufferedReader)

## Quick concept:

- FileReader → reads character data from a file.
- BufferedReader → wraps it, adds readLine() — reads one full line at a time (way better than reading char-by-char).
- Loop pattern: readLine() returns null when it hits end of file — that's your loop's exit condition.
- Exception: if the file doesn't exist, FileReader's constructor throws FileNotFoundException immediately (a subclass of IOException).

## Practice Q:

Write a program that reads Siddu.txt (the one you just built) line by line and prints each line to console, prefixed with a line number (e.g. 1: Enter Line 1). Use try-with-resources like before.

```java
import java.io.FileReader;

import java.io.BufferedReader;

import java.io.IOException;

public class Test {

    public static void main(String[] args) {

        try (BufferedReader br = new BufferedReader(new FileReader("Siddu.txt"));) {

            String line;

            int lineNumber = 1;

            while ((line = br.readLine()) != null) {

                System.out.println(lineNumber + ": " + line);

                lineNumber++;

            }

        } catch (IOException e) {

            System.err.println("An error occured while writing to the file." + e.getMessage());

        }

    }

}
```

Topic 4: Byte Streams (FileInputStream + FileOutputStream)

## Quick concept:

- Everything so far (FileReader/FileWriter) handled character data — text, with encoding.
- Byte streams handle raw bytes — works for any data type: text, images, videos, zip files, anything.
- Classes: InputStream/OutputStream are abstract base classes. You use FileInputStream (read bytes) and FileOutputStream (write bytes).
- read() reads one byte at a time, returns an int (0-255). Returns -1 when end of file is reached (this is your loop exit condition — same idea as readLine() returning null, just a different sentinel value).
- write(int b) writes one byte. There's also write(byte[] b) to write a whole array at once.

Classic interview gotcha: why does read() return int and not byte? Because a byte can only hold -128 to 127, but you need a way to signal "end of file" using a value that can't be a real byte — so Java uses int and reserves -1 specifically for EOF, since -1 isn't achievable from a byte read (0-255 range).

## Practice Q1:

Write a program that copies Siddu.txt into a new file called Siddu_copy.txt using FileInputStream and FileOutputStream — reading and writing one byte at a time in a loop. Use try-with-resources.

```java
import java.io.FileInputStream;

import java.io.FileOutputStream;

import java.io.IOException;

public class Test {

    public static void main(String[] args) {

        try (FileInputStream fis = new FileInputStream("Siddu.txt");

                FileOutputStream fos = new FileOutputStream("Siddu_copy.txt")) {

            int data;

            while ((data = fis.read()) != -1) {

                fos.write(data);

            }

            System.out.println("File SuccessFully copied using byte streams");

        } catch (IOException e) {

            System.err.println("An error occured during file copying" + e.getMessage());

        }

    }

}
```

## Approach 2 faster read 1024 bytes at a time

```java
import java.io.FileInputStream;

import java.io.FileOutputStream;

import java.io.IOException;

public class Test {

    public static void main(String[] args) {

        try (FileInputStream fis = new FileInputStream("Siddu.txt");

                FileOutputStream fos = new FileOutputStream("Siddu_copy2.txt")) {

            byte[] buffer = new byte[1024];

            int bytesRead;

            while ((bytesRead = fis.read(buffer)) != -1) {

                fos.write(buffer, 0, bytesRead);

            }

            System.out.println("File copied using buffered byte streams");

        } catch (IOException e) {

            System.err.println("An error occurred during file copying: " + e.getMessage());

        }

    }

}
```

## Another appraoch usingn bufferClasses easy! Just like bufferWrite

Topic 5: Directories (mkdir/mkdirs, list, delete)

## Quick concept:

Two APIs exist — java.io.File (older, simpler) and java.nio.file (newer, better exceptions). For now, stick with File since it matches what you've been using.

- Creating:

- mkdir() → creates one directory. Fails (false) if parent directories don't exist.
- mkdirs() → creates the directory and any missing parent folders along the way.
- Both return boolean — true if created, false if it failed or already exists.

- Listing:

- list() → returns String[] of names (files + subfolders) inside a directory.
- listFiles() → returns File[] instead (you used this already in Topic 1, Q3, with the filter).
- Gotcha: both return null if the path isn't a directory or doesn't exist — never skip the null check.

- Deleting:

- delete() → works on files always, but for directories, only if the directory is empty. Returns false otherwise (silently — no exception, no error message telling you why).

Interview gotcha to remember: mkdir() vs mkdirs() is asked a lot — "single vs single+parents" is the whole answer.

## Practice Q1:

## Write a program that:

1. Creates a folder called "Reports" (check if it already exists first, print appropriate message either way)
2. Inside that logic, also try creating a nested path "Reports/2026/January" using the other method (the one that handles missing parents) — this should work even though Reports/2026 doesn't exist yet.

```java
import java.io.File;

public class Test {

    public static void main(String[] args) {

        // Part 1: create "Reports" folder

        File reportsFolder = new File("Reports");

        if (reportsFolder.exists()) {

            System.out.println("Reports folder already exists");

        } else {

            if (reportsFolder.mkdir()) {

                System.out.println("Reports folder created successfully");

            } else {

                System.out.println("Failed to create Reports folder");

            }

        }

        // Part 2: create nested path Reports/2026/January

        File nestedFolder = new File("Reports/2026/January");

        if (nestedFolder.exists()) {

            System.out.println("Nested folder already exists");

        } else {

            if (nestedFolder.mkdirs()) {

                System.out.println("Nested folder structure created successfully");

            } else {

                System.out.println("Failed to create nested folders");

            }

        }

    }

}

// no try-catch needed, since mkdir()/mkdirs() don't throw exceptions, they just return false on failure.
```

## The java.nio version

```java
import java.nio.file.Files;

import java.nio.file.Path;

import java.nio.file.Paths;

import java.io.IOException;

public class Test {

    public static void main(String[] args) {

        Path nestedPath = Paths.get("ReportsNio/2026/January");

        if (Files.exists(nestedPath)) {

            System.out.println("Nested folder already exists");

        } else {

            try {

                Files.createDirectories(nestedPath);

                System.out.println("Nested folder structure created successfully");

            } catch (IOException e) {

                System.err.println("Failed to create directories: " + e.getMessage());

            }

        }

    }

}
```

What's different: Paths.get(String) builds a Path object (same idea as new File(...), just the newer type). Files.createDirectories() is the mkdirs() equivalent — creates missing parents too. Key difference: it throws IOException instead of silently returning false. That's the whole selling point of NIO — you actually find out why something failed.

Q2: Listing Directory Contents

```java
import java.io.File;

public class Test {

    public static void main(String[] args) {

        File folder = new File("."); // current directory

        String[] contents = folder.list();

        if (contents == null) {

            System.out.println("Not a valid directory");

        } else if (contents.length == 0) {

            System.out.println("Directory is empty");

        } else {

            System.out.println("Contents of " + folder.getAbsolutePath() + ":");

            for (String name : contents) {

                System.out.println(" - " + name);

            }

        }

    }

}
```

Why this works: list() gives you plain filenames as String[] — both files and subfolders mixed together, no distinction. If you needed to know which are folders vs files, you'd loop through and call new File(folder, name).isDirectory() on each — but for now, just listing names is enough. The null check matters here just like with listFiles() earlier.

## The java.nio version

```java
import java.nio.file.*;

import java.io.IOException;

public class Test {

    public static void main(String[] args) {

        Path folder = Paths.get(".");

        try (DirectoryStream<Path> stream = Files.newDirectoryStream(folder)) {

            System.out.println("Contents of " + folder.toAbsolutePath() + ":");

            for (Path entry : stream) {

                System.out.println(" - " + entry.getFileName());

            }

        } catch (IOException e) {

            System.err.println("Error reading directory: " + e.getMessage());

        }

    }

}
```

What's different: Files.newDirectoryStream() gives you an iterable DirectoryStream<Path> — notice it's used in try-with-resources (it holds a system resource that needs closing, unlike File.list() which just returns a plain array). You loop with a normal for-each. No null check needed — if the directory is invalid, it throws IOException directly instead of giving you a silent null.

Q3: Deleting an Empty Directory

```java
import java.io.File;

public class Test {

    public static void main(String[] args) {

        File folder = new File("Reports/2026/January");

        if (!folder.exists()) {

            System.out.println("Folder does not exist");

        } else if (folder.delete()) {

            System.out.println("Folder deleted successfully");

        } else {

            System.out.println("Failed to delete — folder may not be empty");

        }

    }

}
```

## The java.nio version

```java
import java.nio.file.*;

import java.io.IOException;

public class Test {

    public static void main(String[] args) {

        Path folder = Paths.get("ReportsNio/2026/January");

        try {

            Files.delete(folder);

            System.out.println("Folder deleted successfully");

        } catch (NoSuchFileException e) {

            System.err.println("Folder does not exist");

        } catch (DirectoryNotEmptyException e) {

            System.err.println("Cannot delete — folder is not empty");

        } catch (IOException e) {

            System.err.println("Delete failed: " + e.getMessage());

        }

    }

}
```

This is the big payoff. Remember how File.delete() just returned false with no explanation? Here, Files.delete() throws specific exceptions — NoSuchFileException if it's not there, DirectoryNotEmptyException if it has contents. You catch each one separately and know exactly what went wrong. This is the exact interview answer for "why is NIO better than File for error handling."

Key gotcha here (this is the one that trips people up): delete() returns false silently if the directory has anything inside it — no exception, no error message telling you why it failed. It just returns false, same as if the folder didn't exist or you lacked permission. Since January is empty (you just created it, nothing inside), this will succeed. But try running it a second time on Reports (not January) — since Reports still contains the 2026 subfolder, delete() will return false, and you won't know why unless you already know this rule.

This is exactly why java.nio.file.Files.delete() is considered better in modern Java — it throws a specific exception (DirectoryNotEmptyException) instead of silently returning false. Just good to know for interviews, not something you need to use yet.

Other useful Files methods of java.nio worth knowing (quick list, no need to practice all):

|   |   |
|---|---|
|Method|Purpose|
|Files.copy(source, target)|Copies a file (no manual byte-loop needed!)|
|Files.move(source, target)|Moves/renames a file|
|Files.readAllLines(path)|Reads entire file into a List<String> — one line, no BufferedReader loop|
|Files.write(path, byteArrayOrLines)|Writes to a file — one line, no BufferedWriter setup|
|Files.isDirectory(path) / Files.isRegularFile(path)|Same as File's isDirectory/isFile|
|Files.size(path)|File size in bytes|

Notice Files.readAllLines() and Files.write() basically replace everything you did manually with FileReader/FileWriter in one line each — that's why NIO is called "more efficient," it's less boilerplate too, not just better exceptions.
