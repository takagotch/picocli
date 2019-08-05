### picocli
---
https://picocli.info/

```java
import picocli.CommandLine;
import picocli.CommandLine.Option;
import picocli.CommandLine.Parameters;
import java.io.File;

@Command(name = "example", mixinStandardHelpOptions = true, version = "Picocli example 4.0")
public class Example implements Runnable {
  @Option(names = { "-v", "--verbose" }, description = "Verbose mode. Helpful for troubleshooting. " +
    "Multiple -v options increase the verbosity.")
  private boolean[] verbose = new boolean[0];
  
  @Parameters(arity = "1..*", paramLabel = "FILE", description = "File(s) to process.")
  private File[] inputFiles;
  
  public void run() {
    if (verbose.length > 0) {
      System.out.println(inputFiles.length + " files to process...");
    }
    if (verbose.length > 1) {
      for (File f : inputFiles) {
        System.out.println(f.getAbsolutePath());
      }
    }
  }
  
  public static void main(String[] args) {
    int exitCode = new CommandLine(new Example()).execute(args);
    System.exit(exitCode);
  }
}

libraryDependencies += "info.picocli" % "picocli" % "4.0.1"

@Grapes(
  @Grab(group='info.picocli', module='picocli', version='4.0.1')
)
```

```sh
java Example -v inputFile1 inputFile2
```

```
<dependency>
  <groupId>info.picocli</groupId>
  <artifactId>picocli</artifactId>
  <version>4.0.1</version>
</dependency>
```
