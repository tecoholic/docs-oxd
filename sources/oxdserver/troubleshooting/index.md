# Troubleshooting

## Java Path Setting
### Windows

* Java must be in your `PATH` for the oxD server to work. Please check the `java-version` to be sure. The oxD server can be run with the full path to the `java.exe` instead of using `java` in the command.

![image](http://ox.gluu.org/lib/exe/fetch.php?media=oxd:java_installed.png)

* The required JDK version is 1.6 or higher otherwise the following exception might be thrown
```
Exception in thread "main" java.lang.UnsupportedClassVersionError: Bad version number in .class file
        at java.lang.ClassLoader.defineClass1(Native Method)
```
