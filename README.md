# JRPrintPreview

[![Build Status](https://travis-ci.com/prsolucoes/jrprintpreview.svg?branch=master)](https://travis-ci.com/prsolucoes/jrprintpreview)  

JasperReports print preview stage class written in JavaFX 12.  

This project is based on this project from **Vitomir Spasojević** but fitted for our needs:
https://github.com/vitomirs/JRPrintPreview

## Usage example

Whole functionality is contained in a `JRPrintPreview.java` file. This file should be copied to your project. The rest of the files represent an example project which demonstrates print preview functionality for one simple JasperReports report.

Basic usage is shown in the next example.

```
String reportFileName = "SomeReport.jasper";
Map<String, Object> paramMap = new HashMap<>();
JRBeanCollectionDataSource dataSource = new JRBeanCollectionDataSource(...);

JasperReport jasperReport = (JasperReport) JRLoader.loadObject(
	JRLoader.getResourceInputStream(reportFileName)
);

JasperPrint jasperPrint = JasperFillManager.fillReport(
	jasperReport, paramMap, dataSource
);

JRPrintPreview printPreview = new JRPrintPreview(jasperPrint);
printPreview.show();
```

## Commands

Some maven commands are available and you can execute it without IDE, including run the sample application:  

```
mvn clean
mvn compile
mvn javafx:run
```

To **package** use:

```
mvn package
```

To check only **dependencies** use:

```
mvn dependency:resolve
```

To **sign** jar file use:

```
mvn jarsigner:sign
```

## Generate a key to sign

```
keytool -genkey -keyalg RSA -alias demo -keystore keystore.jks -storepass 123456 -validity 365 -keysize 2048
```

## Requirements

You need Java 12 to run it.  

Obs: If you use Java 8, Java 9 or other you need change file **pom.xml** to 1.8, 1.9 or other version in elements **source**, **target** and **release** of configuration tag.  

## Screenshots

![](extras/screenshots/ss01.png)  


## Known bugs

**Problem 1:**

On macOS Mojave i receive this error when click on **"Print"** menu item:

```
2019-08-08 19:52:13.813 java[58472:3733930] 	Cocoa AWT: Running on AppKit thread 0 when not expected. (
	0   libawt_lwawt.dylib                  0x000000012d871fac nsPrintInfoToJavaPageFormat + 49
	1   libawt_lwawt.dylib                  0x000000012d871dfa Java_sun_lwawt_macosx_CPrinterJob_getDefaultPage + 49
	2   ???                                 0x000000010dcd8990 0x0 + 4526541200
)
2019-08-08 19:52:13.813 java[58472:3733930] 	Please file a bug report at http://bugreport.java.com/bugreport with this message and a reproducible test case.
```

I tested it with JDK 1.8.221 and JDK 12.

**Problem 2:**  

Something not working when run the generated JAR file:  

```
java -jar target/JRPrintPreview-1.0-SNAPSHOT.jar 
Error: A JNI error has occurred, please check your installation and try again
Exception in thread "main" java.lang.SecurityException: Invalid signature file digest for Manifest main attributes
	at java.base/sun.security.util.SignatureFileVerifier.processImpl(SignatureFileVerifier.java:336)
	at java.base/sun.security.util.SignatureFileVerifier.process(SignatureFileVerifier.java:269)
	at java.base/java.util.jar.JarVerifier.processEntry(JarVerifier.java:316)
	at java.base/java.util.jar.JarVerifier.update(JarVerifier.java:230)
	at java.base/java.util.jar.JarFile.initializeVerifier(JarFile.java:758)
	at java.base/java.util.jar.JarFile.ensureInitialization(JarFile.java:1035)
	at java.base/java.util.jar.JavaUtilJarAccessImpl.ensureInitialization(JavaUtilJarAccessImpl.java:69)
	at java.base/jdk.internal.loader.URLClassPath$JarLoader$2.getManifest(URLClassPath.java:870)
	at java.base/jdk.internal.loader.BuiltinClassLoader.defineClass(BuiltinClassLoader.java:788)
	at java.base/jdk.internal.loader.BuiltinClassLoader.findClassOnClassPathOrNull(BuiltinClassLoader.java:700)
	at java.base/jdk.internal.loader.BuiltinClassLoader.loadClassOrNull(BuiltinClassLoader.java:623)
	at java.base/jdk.internal.loader.BuiltinClassLoader.loadClass(BuiltinClassLoader.java:581)
	at java.base/jdk.internal.loader.ClassLoaders$AppClassLoader.loadClass(ClassLoaders.java:178)
	at java.base/java.lang.ClassLoader.loadClass(ClassLoader.java:521)
	at java.base/java.lang.Class.forName0(Native Method)
	at java.base/java.lang.Class.forName(Class.java:415)
	at java.base/sun.launcher.LauncherHelper.loadMainClass(LauncherHelper.java:760)
	at java.base/sun.launcher.LauncherHelper.checkAndLoadMain(LauncherHelper.java:655)
``` 

I tried sign the JAR using:

```
mvn jarsigner:sign
```

But don't work, same error. 

I tried remove the RSA, DS etc from web-inf, but when do it no dependencies are found more, even with dependencies inside the JAR.
